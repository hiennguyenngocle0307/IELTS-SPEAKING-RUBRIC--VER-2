<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms Hien - IELTS Rating Explorer</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --primary-hover: #1e40af;
            --text-dark: #0f172a;
            --text-light: #64748b;
            --bg-page: #f1f5f9;
            --border: #cbd5e1;
            
            /* Theme Colors for Matrix */
            --theme-grey-bg: #f8fafc;
            --theme-grey-border: #94a3b8;
            --theme-yellow-bg: #fef9c3;
            --theme-yellow-border: #eab308;
            --theme-green-bg: #dcfce7;
            --theme-green-border: #22c55e;
            --theme-blue-bg: #dbeafe;
            --theme-blue-border: #3b82f6;
        }

        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { margin: 0; background-color: var(--bg-page); color: var(--text-dark); font-size: 14px; line-height: 1.5; }

        /* Top Sticky Navbar */
        .navbar {
            position: sticky; top: 0; background-color: white; padding: 12px 25px;
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05); z-index: 100; border-bottom: 2px solid var(--primary);
        }
        .header-left { display: flex; align-items: center; gap: 15px; }
        .logo { background: var(--primary); color: white; width: 35px; height: 35px; display: flex; align-items: center; justify-content: center; font-size: 1.2rem; font-weight: bold; border-radius: 6px; }
        .brand h1 { margin: 0; font-size: 1.1rem; color: var(--primary); }
        .brand p { margin: 0; font-size: 0.8rem; color: var(--text-light); }
        
        .controls button { padding: 8px 16px; font-weight: bold; border: none; border-radius: 6px; cursor: pointer; transition: 0.2s; }
        .btn-export { background: #10b981; color: white; margin-right: 10px; }
        .btn-export:hover { background: #059669; }
        .btn-reset { background: #ef4444; color: white; }
        .btn-reset:hover { background: #dc2626; }

        /* Dashboard Overview (VSTEP Style) */
        .dashboard-container { display: flex; gap: 20px; padding: 20px 25px; max-width: 1600px; margin: 0 auto; align-items: stretch; }
        .panel-card { background: white; border: 1px solid var(--border); border-radius: 8px; padding: 20px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        .panel-title { font-size: 0.95rem; font-weight: bold; margin-top: 0; margin-bottom: 15px; color: var(--text-dark); border-bottom: 1px solid var(--border); padding-bottom: 10px; }
        
        /* Left: Student & Scores */
        .panel-scores { flex: 1; display: flex; flex-direction: column; }
        .student-input { padding: 10px 12px; border: 1px solid var(--border); border-radius: 6px; width: 100%; font-size: 14px; margin-bottom: 15px; background: var(--bg-page);}
        .score-row { display: flex; justify-content: space-between; align-items: center; padding: 8px 0; border-bottom: 1px dashed var(--border); }
        .score-row:last-child { border-bottom: none; }
        .score-label { font-weight: 600; color: var(--text-light); }
        .score-val { font-weight: bold; color: var(--primary); font-size: 1.1rem; }

        /* Center: Final Band */
        .panel-final { flex: 0.8; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .final-title { font-size: 0.9rem; color: var(--text-light); font-weight: bold; text-transform: uppercase; letter-spacing: 1px; }
        .final-score { font-size: 4rem; font-weight: 900; color: var(--primary); line-height: 1.1; margin: 10px 0; }
        .cefr-badge { background: var(--theme-grey-border); color: white; padding: 4px 12px; border-radius: 20px; font-weight: bold; font-size: 0.85rem; }

        /* Right: General Comment Tab */
        .panel-comment { flex: 1.5; display: flex; flex-direction: column; }
        .comment-area { width: 100%; flex: 1; min-height: 120px; padding: 12px; border: 1px solid var(--border); border-radius: 6px; font-size: 14px; resize: none; background: var(--bg-page); color: var(--text-dark); }
        .comment-area:focus { outline: none; border-color: var(--primary); background: white; }

        /* Main Rubric Table */
        .table-wrapper { padding: 0 25px 20px 25px; max-width: 1600px; margin: 0 auto; overflow-x: auto; }
        table { width: 100%; border-collapse: collapse; background: white; box-shadow: 0 1px 3px rgba(0,0,0,0.1); min-width: 1000px; border-radius: 8px; overflow: hidden;}
        th { background: var(--primary); color: white; padding: 15px; text-align: left; position: sticky; top: 0; border: 1px solid #0f172a; font-size: 1rem; }
        th.band-col { width: 6%; text-align: center; }
        td { border: 1px solid var(--border); padding: 15px; vertical-align: top; width: 23.5%; }
        
        /* Vertical Band Coloring */
        td.band-cell { font-size: 1.5rem; font-weight: 900; text-align: center; vertical-align: middle; border-right: 3px solid; }
        tr.row-blue td.band-cell { background: var(--theme-blue-bg); color: var(--theme-blue-border); border-right-color: var(--theme-blue-border); }
        tr.row-green td.band-cell { background: var(--theme-green-bg); color: var(--theme-green-border); border-right-color: var(--theme-green-border); }
        tr.row-yellow td.band-cell { background: var(--theme-yellow-bg); color: var(--theme-yellow-border); border-right-color: var(--theme-yellow-border); }
        tr.row-grey td.band-cell { background: var(--theme-grey-bg); color: var(--theme-grey-border); border-right-color: var(--theme-grey-border); }

        /* Interactive Cells */
        td.clickable { cursor: pointer; transition: all 0.1s; }
        td.clickable:hover { background: #f8fafc; }
        td.clickable ul { margin: 0; padding-left: 15px; }
        td.clickable li { margin-bottom: 8px; }
        
        /* OUTSTANDING BOLD KEYWORDS (Basic Colors) */
        td.clickable b { 
            font-weight: 900; 
            text-transform: uppercase; 
            font-size: 0.9em; 
            letter-spacing: 0.5px; 
            padding: 0 2px;
        }
        /* Pure Blue for Band 9 */
        tr.row-blue td.clickable b { color: #0000FF; } 
        /* Solid Green for Bands 6-8 */
        tr.row-green td.clickable b { color: #008000; } 
        /* Deep Orange for Bands 4-5 */
        tr.row-yellow td.clickable b { color: #D2691E; } 
        /* Bright Red for Bands 1-3 */
        tr.row-grey td.clickable b { color: #FF0000; } 

        /* Selected States */
        td.clickable.selected { box-shadow: inset 0 0 0 3px; }
        tr.row-blue td.clickable.selected { background: var(--theme-blue-bg); border-color: var(--theme-blue-border); box-shadow: inset 0 0 0 3px var(--theme-blue-border); }
        tr.row-green td.clickable.selected { background: var(--theme-green-bg); border-color: var(--theme-green-border); box-shadow: inset 0 0 0 3px var(--theme-green-border); }
        tr.row-yellow td.clickable.selected { background: var(--theme-yellow-bg); border-color: var(--theme-yellow-border); box-shadow: inset 0 0 0 3px var(--theme-yellow-border); }
        tr.row-grey td.clickable.selected { background: var(--theme-grey-bg); border-color: var(--theme-grey-border); box-shadow: inset 0 0 0 3px var(--theme-grey-border); }
        td.clickable.selected b { color: #0f172a; background: rgba(255,255,255,0.5); border-radius: 3px;}

    </style>
</head>
<body>

    <!-- Top Navbar -->
    <div class="navbar">
        <div class="header-left">
            <div class="logo">H</div>
            <div class="brand">
                <h1>Ms Hien</h1>
                <p>IELTS Rating Scales Explorer</p>
            </div>
        </div>
        <div class="controls">
            <button class="btn-export" onclick="exportReport()">Export Report</button>
            <button class="btn-reset" onclick="clearWorkspace()">Clear All</button>
        </div>
    </div>

    <!-- Dashboard Overview -->
    <div class="dashboard-container">
        <!-- Mark & Level Details -->
        <div class="panel-card panel-scores">
            <h2 class="panel-title">Mark & Level Details</h2>
            <input type="text" id="studentName" class="student-input" placeholder="Enter Student Name..." oninput="saveDataLocally()">
            <div class="score-row">
                <span class="score-label">Fluency & Coherence</span>
                <span class="score-val" id="lbl-fc">-</span>
            </div>
            <div class="score-row">
                <span class="score-label">Lexical Resource</span>
                <span class="score-val" id="lbl-lr">-</span>
            </div>
            <div class="score-row">
                <span class="score-label">Grammar Range</span>
                <span class="score-val" id="lbl-gra">-</span>
            </div>
            <div class="score-row">
                <span class="score-label">Pronunciation</span>
                <span class="score-val" id="lbl-pr">-</span>
            </div>
        </div>

        <!-- Big Overall Score -->
        <div class="panel-card panel-final">
            <div class="final-title">Overall Band</div>
            <div class="final-score" id="finalScore">0.0</div>
            <div class="cefr-badge" id="cefrBadge" style="background: var(--theme-grey-border);">Pending</div>
        </div>

        <!-- General Comments Tab -->
        <div class="panel-card panel-comment">
            <h2 class="panel-title">General Feedback & Comments</h2>
            <textarea id="generalComment" class="comment-area" placeholder="Enter overall assessment, key strengths, and specific areas for improvement here..." oninput="saveDataLocally()"></textarea>
        </div>
    </div>

    <!-- Main Vertical Matrix -->
    <div class="table-wrapper">
        <table id="rubricTable">
            <thead>
                <tr>
                    <th class="band-col">Band</th>
                    <th>Fluency & Coherence (FC)</th>
                    <th>Lexical Resource (LR)</th>
                    <th>Grammatical Range & Accuracy (GRA)</th>
                    <th>Pronunciation (PR)</th>
                </tr>
            </thead>
            <tbody>
                <!-- Band 9 -->
                <tr class="row-blue">
                    <td class="band-cell">9</td>
                    <td class="clickable cell-fc" id="fc-9" onclick="setScore('fc', 9)">
                        <ul><li><b>Speaks fluently</b> with rare repetition.</li><li><b>Cohesion is fully natural</b>.</li><li><b>Develops topics fully</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-9" onclick="setScore('lr', 9)">
                        <ul><li>Uses vocabulary with <b>full flexibility</b> and <b>precision</b>.</li><li>Uses <b>idiomatic language</b> naturally.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-9" onclick="setScore('gra', 9)">
                        <ul><li>Uses a <b>full range</b> of structures naturally.</li><li>Consistently <b>accurate</b> apart from 'slips'.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-9" onclick="setScore('pr', 9)">
                        <ul><li>Uses a <b>full range</b> of pronunciation features.</li><li>Is <b>effortless to understand</b>.</li></ul>
                    </td>
                </tr>
                <!-- Band 8 -->
                <tr class="row-green">
                    <td class="band-cell">8</td>
                    <td class="clickable cell-fc" id="fc-8" onclick="setScore('fc', 8)">
                        <ul><li><b>Speaks fluently</b> with occasional repetition.</li><li>Develops topics <b>coherently</b> and <b>appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-8" onclick="setScore('lr', 8)">
                        <ul><li>Uses a <b>wide vocabulary</b> resource readily.</li><li>Uses <b>less common</b> and <b>idiomatic</b> vocabulary skillfully.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-8" onclick="setScore('gra', 8)">
                        <ul><li>Uses a <b>wide range</b> of structures flexibly.</li><li>Majority of <b>error-free</b> sentences.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-8" onclick="setScore('pr', 8)">
                        <ul><li>Uses a <b>wide range</b> of features flexibly.</li><li><b>Easy to understand</b>; L1 accent has minimal effect.</li></ul>
                    </td>
                </tr>
                <!-- Band 7 -->
                <tr class="row-green">
                    <td class="band-cell">7</td>
                    <td class="clickable cell-fc" id="fc-7" onclick="setScore('fc', 7)">
                        <ul><li>Speaks <b>at length</b> without noticeable effort.</li><li>Some <b>language-related hesitation</b>.</li><li>Uses a range of <b>connectives</b> flexibly.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-7" onclick="setScore('lr', 7)">
                        <ul><li>Uses vocabulary flexibly across a <b>variety of topics</b>.</li><li>Uses some <b>less common</b> vocabulary.</li><li>Can <b>paraphrase effectively</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-7" onclick="setScore('gra', 7)">
                        <ul><li>Uses a range of <b>complex structures</b> flexibly.</li><li><b>Frequently produces</b> error-free sentences.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-7" onclick="setScore('pr', 7)">
                        <ul><li>Shows <b>all positive features</b> of Band 6 and some, but not all, of Band 8.</li></ul>
                    </td>
                </tr>
                <!-- Band 6 -->
                <tr class="row-green">
                    <td class="band-cell">6</td>
                    <td class="clickable cell-fc" id="fc-6" onclick="setScore('fc', 6)">
                        <ul><li>Willing to speak <b>at length</b>, though may <b>lose coherence</b>.</li><li>Uses connectives but <b>not always appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-6" onclick="setScore('lr', 6)">
                        <ul><li><b>Wide enough vocabulary</b> to discuss topics at length.</li><li><b>Generally paraphrases successfully</b>.</li><li>Sometimes makes errors in word choice.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-6" onclick="setScore('gra', 6)">
                        <ul><li>Uses a <b>mix of simple and complex</b> structures.</li><li>May make <b>frequent mistakes</b> with complex structures.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-6" onclick="setScore('pr', 6)">
                        <ul><li>Uses a range of features with <b>mixed control</b>.</li><li>Can <b>generally be understood</b> throughout.</li></ul>
                    </td>
                </tr>
                <!-- Band 5 -->
                <tr class="row-yellow">
                    <td class="band-cell">5</td>
                    <td class="clickable cell-fc" id="fc-5" onclick="setScore('fc', 5)">
                        <ul><li>Maintains flow but uses <b>repetition</b>, <b>self-correction</b>, or <b>slow speech</b>.</li><li>May <b>over-use</b> certain connectives.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-5" onclick="setScore('lr', 5)">
                        <ul><li>Manages familiar topics but uses <b>limited vocabulary</b>.</li><li>Attempts paraphrase with <b>mixed success</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-5" onclick="setScore('gra', 5)">
                        <ul><li>Produces <b>basic sentence forms</b> with reasonable accuracy.</li><li>Complex structures <b>usually contain errors</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-5" onclick="setScore('pr', 5)">
                        <ul><li>Shows <b>all positive features</b> of Band 4 and some, but not all, of Band 6.</li></ul>
                    </td>
                </tr>
                <!-- Band 4 -->
                <tr class="row-yellow">
                    <td class="band-cell">4</td>
                    <td class="clickable cell-fc" id="fc-4" onclick="setScore('fc', 4)">
                        <ul><li>Cannot respond without <b>noticeable pauses</b>.</li><li>Links basic sentences with <b>repetitious</b> connectives.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-4" onclick="setScore('lr', 4)">
                        <ul><li>Talks about familiar topics but conveys <b>basic meaning</b> on unfamiliar ones.</li><li><b>Rarely attempts paraphrase</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-4" onclick="setScore('gra', 4)">
                        <ul><li>Produces basic sentence forms.</li><li><b>Frequent errors</b> may lead to misunderstanding.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-4" onclick="setScore('pr', 4)">
                        <ul><li>Uses a <b>limited range</b> of pronunciation features.</li><li><b>Frequent mispronunciations</b> cause difficulty.</li></ul>
                    </td>
                </tr>
                <!-- Band 3 -->
                <tr class="row-grey">
                    <td class="band-cell">3</td>
                    <td class="clickable cell-fc" id="fc-3" onclick="setScore('fc', 3)">
                        <ul><li>Speaks with <b>long pauses</b>.</li><li>Limited ability to <b>link simple sentences</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-3" onclick="setScore('lr', 3)">
                        <ul><li>Uses simple vocabulary to convey <b>personal information</b>.</li><li><b>Insufficient vocabulary</b> for unfamiliar topics.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-3" onclick="setScore('gra', 3)">
                        <ul><li>Attempts basic sentence forms but with <b>abundant errors</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-3" onclick="setScore('pr', 3)">
                        <ul><li>Shows some features of Band 2 and some, but not all, of Band 4.</li></ul>
                    </td>
                </tr>
                <!-- Band 2 -->
                <tr class="row-grey">
                    <td class="band-cell">2</td>
                    <td class="clickable cell-fc" id="fc-2" onclick="setScore('fc', 2)">
                        <ul><li>Pauses <b>lengthily</b> before most words.</li><li><b>Little communication</b> possible.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-2" onclick="setScore('lr', 2)">
                        <ul><li>Produces <b>isolated words</b> or <b>memorised utterances</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-2" onclick="setScore('gra', 2)">
                        <ul><li><b>Cannot produce</b> basic sentence forms.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-2" onclick="setScore('pr', 2)">
                        <ul><li>Speech is <b>often unintelligible</b>.</li></ul>
                    </td>
                </tr>
                <!-- Band 1 -->
                <tr class="row-grey">
                    <td class="band-cell">1</td>
                    <td class="clickable cell-fc" id="fc-1" onclick="setScore('fc', 1)">
                        <ul><li><b>No communication</b> possible.</li><li><b>No rate of speech</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-1" onclick="setScore('lr', 1)">
                        <ul><li>Only a few <b>isolated words</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-1" onclick="setScore('gra', 1)">
                        <ul><li><b>No communicable structures</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-1" onclick="setScore('pr', 1)">
                        <ul><li>Speech is <b>unintelligible</b>.</li></ul>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        let scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
        
        window.onload = function() {
            if(localStorage.getItem('ielts_final_name')) {
                document.getElementById('studentName').value = localStorage.getItem('ielts_final_name');
            }
            if(localStorage.getItem('ielts_final_comment')) {
                document.getElementById('generalComment').value = localStorage.getItem('ielts_final_comment');
            }
            if(localStorage.getItem('ielts_final_scores')) {
                scores = JSON.parse(localStorage.getItem('ielts_final_scores'));
                if(scores.fc > 0) applySelection('fc', scores.fc);
                if(scores.lr > 0) applySelection('lr', scores.lr);
                if(scores.gra > 0) applySelection('gra', scores.gra);
                if(scores.pr > 0) applySelection('pr', scores.pr);
                updateTotalScore();
            }
        };

        window.setScore = function(criterion, value) {
            scores[criterion] = value;
            applySelection(criterion, value);
            updateTotalScore();
            saveDataLocally();
        }

        function applySelection(criterion, value) {
            const cells = document.querySelectorAll(`.cell-${criterion}`);
            cells.forEach(cell => cell.classList.remove('selected'));
            const selectedCell = document.getElementById(`${criterion}-${value}`);
            if(selectedCell) selectedCell.classList.add('selected');
        }

        function updateTotalScore() {
            // Update Mini Labels
            document.getElementById('lbl-fc').innerText = scores.fc > 0 ? scores.fc.toFixed(1) : '-';
            document.getElementById('lbl-lr').innerText = scores.lr > 0 ? scores.lr.toFixed(1) : '-';
            document.getElementById('lbl-gra').innerText = scores.gra > 0 ? scores.gra.toFixed(1) : '-';
            document.getElementById('lbl-pr').innerText = scores.pr > 0 ? scores.pr.toFixed(1) : '-';
            
            const cefrBadge = document.getElementById('cefrBadge');

            if (scores.fc === 0 || scores.lr === 0 || scores.gra === 0 || scores.pr === 0) {
                document.getElementById('finalScore').innerText = "0.0";
                cefrBadge.innerText = "Pending";
                cefrBadge.style.background = "var(--theme-grey-border)";
            } else {
                const average = (scores.fc + scores.lr + scores.gra + scores.pr) / 4;
                const final = Math.round(average * 2) / 2;
                document.getElementById('finalScore').innerText = final.toFixed(1);

                // Update CEFR Badge logic
                if (final >= 9.0) { cefrBadge.innerText = "C2 - Expert User"; cefrBadge.style.background = "var(--theme-blue-border)"; }
                else if (final >= 7.0) { cefrBadge.innerText = "C1 - Advanced User"; cefrBadge.style.background = "var(--theme-green-border)"; }
                else if (final >= 5.5) { cefrBadge.innerText = "B2 - Independent User"; cefrBadge.style.background = "var(--theme-green-border)"; }
                else if (final >= 4.0) { cefrBadge.innerText = "B1 - Threshold User"; cefrBadge.style.background = "var(--theme-yellow-border)"; }
                else { cefrBadge.innerText = "Pre-A1/A2 - Basic User"; cefrBadge.style.background = "var(--theme-grey-border)"; }
            }
        }

        function saveDataLocally() {
            localStorage.setItem('ielts_final_name', document.getElementById('studentName').value);
            localStorage.setItem('ielts_final_comment', document.getElementById('generalComment').value);
            localStorage.setItem('ielts_final_scores', JSON.stringify(scores));
        }

        function clearWorkspace() {
            if(confirm("Clear student data, comments, and reset the rubric?")) {
                localStorage.removeItem('ielts_final_name');
                localStorage.removeItem('ielts_final_comment');
                localStorage.removeItem('ielts_final_scores');
                scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
                document.getElementById('studentName').value = '';
                document.getElementById('generalComment').value = '';
                document.querySelectorAll('.clickable').forEach(c => c.classList.remove('selected'));
                updateTotalScore();
            }
        }

        function stripHTML(html) {
            let tempDiv = document.createElement("div");
            tempDiv.innerHTML = html.replace(/<li>/g, "• ").replace(/<\/li>/g, "\n");
            return tempDiv.innerText || tempDiv.textContent || "";
        }

        function exportReport() {
            const finalScore = document.getElementById('finalScore').innerText;
            if(finalScore === "0.0" || finalScore === "-") {
                alert("Select a band score for all 4 criteria to export.");
                return;
            }

            const studentName = document.getElementById('studentName').value || "Unnamed Student";
            const cefr = document.getElementById('cefrBadge').innerText;
            const comment = document.getElementById('generalComment').value || "No general comments provided.";

            let report = "IELTS SPEAKING GRADING REPORT\n";
            report += "Teacher: Ms Hien\n";
            report += `Student: ${studentName}\n`;
            report += "========================================\n\n";
            report += `OVERALL BAND SCORE: ${finalScore} (${cefr})\n\n`;
            
            report += "--- GENERAL FEEDBACK ---\n";
            report += `${comment}\n\n`;

            report += "========================================\n";
            report += "DETAILED CRITERIA BREAKDOWN:\n\n";
            
            const fcText = stripHTML(document.getElementById(`fc-${scores.fc}`).innerHTML);
            const lrText = stripHTML(document.getElementById(`lr-${scores.lr}`).innerHTML);
            const graText = stripHTML(document.getElementById(`gra-${scores.gra}`).innerHTML);
            const prText = stripHTML(document.getElementById(`pr-${scores.pr}`).innerHTML);

            report += `1. Fluency and Coherence (Band ${scores.fc})\n${fcText}\n`;
            report += `2. Lexical Resource (Band ${scores.lr})\n${lrText}\n`;
            report += `3. Grammatical Range & Accuracy (Band ${scores.gra})\n${graText}\n`;
            report += `4. Pronunciation (Band ${scores.pr})\n${prText}\n`;

            const fileName = studentName === "Unnamed Student" ? "IELTS_Speaking_Report.txt" : `${studentName.replace(/ /g, "_")}_IELTS_Report.txt`;

            const blob = new Blob([report], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = fileName;
            a.click();
            URL.revokeObjectURL(url);
        }
    </script>
</body>
</html>
