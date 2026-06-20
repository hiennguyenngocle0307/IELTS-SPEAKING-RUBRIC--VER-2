<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms Hien - IELTS Rating Matrix</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --text-dark: #0f172a;
            --text-light: #475569;
            --bg-page: #f8fafc;
            --border: #cbd5e1;
            
            /* Theme Colors */
            --theme-grey-bg: #f1f5f9;
            --theme-grey-border: #94a3b8;
            --theme-yellow-bg: #fef9c3;
            --theme-yellow-border: #eab308;
            --theme-green-bg: #dcfce7;
            --theme-green-border: #22c55e;
            --theme-blue-bg: #dbeafe;
            --theme-blue-border: #3b82f6;
        }

        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { margin: 0; background-color: var(--bg-page); color: var(--text-dark); font-size: 14px; line-height: 1.4; }

        /* Sticky Top Dashboard */
        .dashboard {
            position: sticky; top: 0; background-color: white; padding: 15px 25px;
            display: flex; justify-content: space-between; align-items: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.05); z-index: 100; border-bottom: 3px solid var(--primary);
        }
        .header-left { display: flex; align-items: center; gap: 15px; }
        .logo { background: var(--primary); color: white; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; font-weight: bold; border-radius: 6px; }
        .brand h1 { margin: 0; font-size: 1.2rem; color: var(--primary); }
        .brand p { margin: 0; font-size: 0.85rem; color: var(--text-light); }
        .student-input { padding: 8px 12px; border: 1px solid var(--border); border-radius: 6px; width: 220px; font-size: 14px; }
        
        .score-board { display: flex; align-items: center; gap: 20px; background: #f1f5f9; padding: 5px 20px; border-radius: 50px; border: 1px solid var(--border); }
        .criteria-summary { font-weight: 600; color: var(--text-light); }
        .final-score { font-size: 1.8rem; font-weight: 900; color: var(--primary); min-width: 50px; text-align: center; }

        .controls button { padding: 8px 16px; font-weight: bold; border: none; border-radius: 6px; cursor: pointer; transition: 0.2s; }
        .btn-export { background: #10b981; color: white; margin-right: 10px; }
        .btn-export:hover { background: #059669; }
        .btn-reset { background: #ef4444; color: white; }
        .btn-reset:hover { background: #dc2626; }

        /* VSTEP Style Band Summary */
        .summary-container { padding: 20px 25px 0 25px; max-width: 1600px; margin: 0 auto; }
        .summary-title { font-size: 0.85rem; font-weight: 800; color: var(--text-light); letter-spacing: 1px; margin-bottom: 10px; text-transform: uppercase; }
        .summary-cards { display: flex; gap: 15px; }
        .card { flex: 1; padding: 12px 15px; border-radius: 8px; border: 1px solid; }
        .card-title { font-weight: bold; margin-bottom: 5px; font-size: 0.95rem; }
        .card-desc { font-size: 0.85rem; color: var(--text-light); }
        
        .card-grey { background: var(--theme-grey-bg); border-color: var(--theme-grey-border); }
        .card-yellow { background: var(--theme-yellow-bg); border-color: var(--theme-yellow-border); }
        .card-green { background: var(--theme-green-bg); border-color: var(--theme-green-border); }
        .card-blue { background: var(--theme-blue-bg); border-color: var(--theme-blue-border); }

        .badge { display: inline-block; padding: 2px 6px; border-radius: 4px; font-size: 0.75rem; font-weight: bold; color: white; margin-right: 5px; }
        .badge-grey { background: var(--theme-grey-border); }
        .badge-yellow { background: var(--theme-yellow-border); }
        .badge-green { background: var(--theme-green-border); }
        .badge-blue { background: var(--theme-blue-border); }

        /* Main Rubric Table */
        .table-wrapper { padding: 20px 25px; max-width: 1600px; margin: 0 auto; overflow-x: auto; }
        table { width: 100%; border-collapse: collapse; background: white; box-shadow: 0 1px 3px rgba(0,0,0,0.1); min-width: 1000px; }
        th { background: var(--primary); color: white; padding: 12px; text-align: left; position: sticky; top: 0; border: 1px solid #0f172a; font-size: 1rem; }
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
        td.clickable li { margin-bottom: 5px; }
        td.clickable b { color: #0284c7; }

        /* Selected States */
        td.clickable.selected { box-shadow: inset 0 0 0 3px; }
        tr.row-blue td.clickable.selected { background: var(--theme-blue-bg); border-color: var(--theme-blue-border); box-shadow: inset 0 0 0 3px var(--theme-blue-border); }
        tr.row-green td.clickable.selected { background: var(--theme-green-bg); border-color: var(--theme-green-border); box-shadow: inset 0 0 0 3px var(--theme-green-border); }
        tr.row-yellow td.clickable.selected { background: var(--theme-yellow-bg); border-color: var(--theme-yellow-border); box-shadow: inset 0 0 0 3px var(--theme-yellow-border); }
        tr.row-grey td.clickable.selected { background: var(--theme-grey-bg); border-color: var(--theme-grey-border); box-shadow: inset 0 0 0 3px var(--theme-grey-border); }
        td.clickable.selected b { color: #0f172a; }

    </style>
</head>
<body>

    <div class="dashboard">
        <div class="header-left">
            <div class="logo">H</div>
            <div class="brand">
                <h1>Ms Hien</h1>
                <p>IELTS Speaking Descriptors Matrix</p>
            </div>
            <input type="text" id="studentName" class="student-input" placeholder="Student Name..." oninput="saveDataLocally()">
        </div>

        <div class="score-board">
            <div class="criteria-summary" id="scoreSummary">
                FC: - &nbsp;|&nbsp; LR: - &nbsp;|&nbsp; GRA: - &nbsp;|&nbsp; PR: -
            </div>
            <div class="final-score" id="finalScore">0.0</div>
        </div>

        <div class="controls">
            <button class="btn-export" onclick="exportReport()">Export</button>
            <button class="btn-reset" onclick="clearWorkspace()">Reset</button>
        </div>
    </div>

    <div class="summary-container">
        <div class="summary-title">Overall Band Summary Profile</div>
        <div class="summary-cards">
            <div class="card card-grey">
                <div class="card-title">Extremely Limited (Pre-A1)</div>
                <div class="card-desc"><span class="badge badge-grey">Bands 1-3</span> Memorized phrases, heavy pauses, systematic basic mistakes, often unintelligible.</div>
            </div>
            <div class="card card-yellow">
                <div class="card-title">Modest / Limited (B1)</div>
                <div class="card-desc"><span class="badge badge-yellow">Bands 4-5</span> Maintains flow with repetition, relatively accurate simple structures, noticeable hesitations.</div>
            </div>
            <div class="card card-green">
                <div class="card-title">Competent / Good (B2 / C1)</div>
                <div class="card-desc"><span class="badge badge-green">Bands 6-8</span> Speaks at length, good control of complex structures, non-systematic errors, clear pronunciation.</div>
            </div>
            <div class="card card-blue">
                <div class="card-title">Expert (C2)</div>
                <div class="card-desc"><span class="badge badge-blue">Band 9</span> Flexibly and accurately uses a wide range, effortless to understand, natural cohesion.</div>
            </div>
        </div>
    </div>

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
                <tr class="row-blue">
                    <td class="band-cell">9</td>
                    <td class="clickable cell-fc" id="fc-9" onclick="setScore('fc', 9)">
                        <ul><li><b>Speaks fluently</b> with rare repetition.</li><li><b>Cohesion is fully natural</b>.</li><li>Develops topics fully.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-9" onclick="setScore('lr', 9)">
                        <ul><li>Uses vocabulary with <b>full flexibility and precision</b>.</li><li>Uses <b>idiomatic language naturally</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-9" onclick="setScore('gra', 9)">
                        <ul><li>Uses a <b>full range of structures naturally</b>.</li><li>Consistently <b>accurate</b> apart from 'slips'.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-9" onclick="setScore('pr', 9)">
                        <ul><li>Uses a <b>full range of pronunciation features</b>.</li><li>Is <b>effortless to understand</b>.</li></ul>
                    </td>
                </tr>
                <tr class="row-green">
                    <td class="band-cell">8</td>
                    <td class="clickable cell-fc" id="fc-8" onclick="setScore('fc', 8)">
                        <ul><li><b>Speaks fluently</b> with occasional repetition.</li><li>Develops topics <b>coherently and appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-8" onclick="setScore('lr', 8)">
                        <ul><li>Uses a <b>wide vocabulary resource</b> readily.</li><li>Uses <b>less common and idiomatic</b> vocabulary skillfully.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-8" onclick="setScore('gra', 8)">
                        <ul><li>Uses a <b>wide range of structures flexibly</b>.</li><li>Majority of <b>error-free sentences</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-8" onclick="setScore('pr', 8)">
                        <ul><li>Uses a <b>wide range</b> of features flexibly.</li><li><b>Easy to understand</b>; L1 accent has minimal effect.</li></ul>
                    </td>
                </tr>
                <tr class="row-green">
                    <td class="band-cell">7</td>
                    <td class="clickable cell-fc" id="fc-7" onclick="setScore('fc', 7)">
                        <ul><li>Speaks <b>at length</b> without noticeable effort.</li><li>Some <b>language-related hesitation</b>.</li><li>Uses a range of <b>connectives</b> flexibly.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-7" onclick="setScore('lr', 7)">
                        <ul><li>Uses vocabulary flexibly across a <b>variety of topics</b>.</li><li>Uses some <b>less common</b> vocabulary.</li><li>Can <b>paraphrase effectively</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-7" onclick="setScore('gra', 7)">
                        <ul><li>Uses a range of <b>complex structures</b> flexibly.</li><li><b>Frequently produces error-free sentences</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-7" onclick="setScore('pr', 7)">
                        <ul><li>Shows all positive features of Band 6 and some, but not all, of Band 8.</li></ul>
                    </td>
                </tr>
                <tr class="row-green">
                    <td class="band-cell">6</td>
                    <td class="clickable cell-fc" id="fc-6" onclick="setScore('fc', 6)">
                        <ul><li>Willing to speak <b>at length</b>, though may <b>lose coherence</b>.</li><li>Uses connectives but <b>not always appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-6" onclick="setScore('lr', 6)">
                        <ul><li><b>Wide enough vocabulary</b> to discuss topics at length.</li><li><b>Generally paraphrases successfully</b>.</li><li>Sometimes makes errors in word choice.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-6" onclick="setScore('gra', 6)">
                        <ul><li>Uses a <b>mix of simple and complex structures</b>.</li><li>May make <b>frequent mistakes with complex structures</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-6" onclick="setScore('pr', 6)">
                        <ul><li>Uses a range of features with <b>mixed control</b>.</li><li>Can <b>generally be understood</b> throughout.</li></ul>
                    </td>
                </tr>
                <tr class="row-yellow">
                    <td class="band-cell">5</td>
                    <td class="clickable cell-fc" id="fc-5" onclick="setScore('fc', 5)">
                        <ul><li>Maintains flow but uses <b>repetition, self-correction, or slow speech</b>.</li><li>May <b>over-use</b> certain connectives.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-5" onclick="setScore('lr', 5)">
                        <ul><li>Manages familiar topics but uses <b>limited vocabulary</b>.</li><li>Attempts paraphrase with <b>mixed success</b>.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-5" onclick="setScore('gra', 5)">
                        <ul><li>Produces <b>basic sentence forms</b> with reasonable accuracy.</li><li>Complex structures <b>usually contain errors</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-5" onclick="setScore('pr', 5)">
                        <ul><li>Shows all positive features of Band 4 and some, but not all, of Band 6.</li></ul>
                    </td>
                </tr>
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
                <tr class="row-grey">
                    <td class="band-cell">3</td>
                    <td class="clickable cell-fc" id="fc-3" onclick="setScore('fc', 3)">
                        <ul><li>Speaks with <b>long pauses</b>.</li><li>Limited ability to link simple sentences.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-3" onclick="setScore('lr', 3)">
                        <ul><li>Uses simple vocabulary to convey <b>personal information</b>.</li><li>Insufficient vocabulary for unfamiliar topics.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-3" onclick="setScore('gra', 3)">
                        <ul><li>Attempts basic sentence forms but with <b>abundant errors</b>.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-3" onclick="setScore('pr', 3)">
                        <ul><li>Shows some features of Band 2 and some, but not all, of Band 4.</li></ul>
                    </td>
                </tr>
                <tr class="row-grey">
                    <td class="band-cell">2</td>
                    <td class="clickable cell-fc" id="fc-2" onclick="setScore('fc', 2)">
                        <ul><li>Pauses lengthily before most words.</li><li>Little communication possible.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-2" onclick="setScore('lr', 2)">
                        <ul><li>Produces isolated words or memorised utterances.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-2" onclick="setScore('gra', 2)">
                        <ul><li>Cannot produce basic sentence forms.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-2" onclick="setScore('pr', 2)">
                        <ul><li>Speech is often unintelligible.</li></ul>
                    </td>
                </tr>
                <tr class="row-grey">
                    <td class="band-cell">1</td>
                    <td class="clickable cell-fc" id="fc-1" onclick="setScore('fc', 1)">
                        <ul><li>No communication possible.</li><li>No rate of speech.</li></ul>
                    </td>
                    <td class="clickable cell-lr" id="lr-1" onclick="setScore('lr', 1)">
                        <ul><li>Only a few isolated words.</li></ul>
                    </td>
                    <td class="clickable cell-gra" id="gra-1" onclick="setScore('gra', 1)">
                        <ul><li>No communicable structures.</li></ul>
                    </td>
                    <td class="clickable cell-pr" id="pr-1" onclick="setScore('pr', 1)">
                        <ul><li>Speech is unintelligible.</li></ul>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        let scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
        
        window.onload = function() {
            if(localStorage.getItem('ielts_matrix_name_v2')) {
                document.getElementById('studentName').value = localStorage.getItem('ielts_matrix_name_v2');
            }
            if(localStorage.getItem('ielts_matrix_scores_v2')) {
                scores = JSON.parse(localStorage.getItem('ielts_matrix_scores_v2'));
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
            document.getElementById('scoreSummary').innerHTML = 
                `FC: <span style="color:var(--primary)">${scores.fc || '-'}</span> &nbsp;|&nbsp; 
                 LR: <span style="color:var(--primary)">${scores.lr || '-'}</span> &nbsp;|&nbsp; 
                 GRA: <span style="color:var(--primary)">${scores.gra || '-'}</span> &nbsp;|&nbsp; 
                 PR: <span style="color:var(--primary)">${scores.pr || '-'}</span>`;
            
            if (scores.fc === 0 || scores.lr === 0 || scores.gra === 0 || scores.pr === 0) {
                document.getElementById('finalScore').innerText = "0.0";
            } else {
                const average = (scores.fc + scores.lr + scores.gra + scores.pr) / 4;
                const final = Math.round(average * 2) / 2;
                document.getElementById('finalScore').innerText = final.toFixed(1);
            }
        }

        function saveDataLocally() {
            localStorage.setItem('ielts_matrix_name_v2', document.getElementById('studentName').value);
            localStorage.setItem('ielts_matrix_scores_v2', JSON.stringify(scores));
        }

        function clearWorkspace() {
            if(confirm("Clear student data and reset the rubric?")) {
                localStorage.removeItem('ielts_matrix_name_v2');
                localStorage.removeItem('ielts_matrix_scores_v2');
                scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
                document.getElementById('studentName').value = '';
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

            let report = "IELTS SPEAKING GRADING REPORT\n";
            report += "Teacher: Ms Hien\n";
            report += `Student: ${studentName}\n`;
            report += "========================================\n\n";
            report += `OVERALL BAND SCORE: ${finalScore}\n\n`;
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
