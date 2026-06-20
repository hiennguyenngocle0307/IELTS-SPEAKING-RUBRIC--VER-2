<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms Hien - IELTS Rating Scales Explorer</title>
    <style>
        :root {
            --primary: #1e3a8a;
            --text-dark: #1e293b;
            --text-light: #475569;
            --border: #cbd5e1;
            --bg-page: #f8fafc;
            
            /* Theme Colors */
            --theme-grey-light: #f1f5f9;
            --theme-grey-border: #94a3b8;
            --theme-yellow-light: #fef9c3;
            --theme-yellow-border: #eab308;
            --theme-green-light: #dcfce7;
            --theme-green-border: #22c55e;
            --theme-blue-light: #dbeafe;
            --theme-blue-border: #3b82f6;
        }
        
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            margin: 0;
            background-color: var(--bg-page);
            color: var(--text-dark);
            font-size: 14px;
        }

        /* Top Dashboard */
        .dashboard {
            position: sticky;
            top: 0;
            background-color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
            z-index: 100;
            border-bottom: 2px solid var(--primary);
        }

        .header-left { display: flex; align-items: center; gap: 20px; }
        .logo-badge {
            background-color: var(--primary);
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
            width: 40px;
            height: 40px;
            display: flex;
            align-items: center;
            justify-content: center;
            border-radius: 6px;
        }
        .brand h1 { margin: 0; font-size: 1.2rem; color: var(--primary); }
        .brand p { margin: 0; font-size: 0.85rem; color: var(--text-light); }

        .student-input {
            padding: 8px 12px;
            border: 1px solid var(--border);
            border-radius: 6px;
            width: 250px;
            font-size: 14px;
        }

        .score-board {
            display: flex;
            align-items: center;
            gap: 20px;
            background: #f1f5f9;
            padding: 8px 20px;
            border-radius: 50px;
            border: 1px solid var(--border);
        }
        .criteria-summary { font-weight: 600; color: var(--text-light); font-size: 0.95rem; }
        .final-score { font-size: 1.5rem; font-weight: 900; color: var(--primary); }

        .controls button {
            padding: 8px 16px;
            font-weight: 600;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            transition: 0.2s;
        }
        .btn-export { background-color: var(--primary); color: white; margin-right: 10px; }
        .btn-export:hover { background-color: #1e40af; }
        .btn-reset { background-color: white; color: #ef4444; border: 1px solid #ef4444; }
        .btn-reset:hover { background-color: #fef2f2; }

        /* Full Screen Table container */
        .table-wrapper {
            width: 100%;
            overflow-x: auto;
            padding: 20px;
            height: calc(100vh - 80px);
        }

        table {
            border-collapse: collapse;
            width: 100%;
            min-width: 1800px; /* Forces horizontal scroll to maintain readability */
            background: white;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        th, td {
            border: 1px solid var(--border);
            padding: 12px;
            vertical-align: top;
            line-height: 1.4;
        }

        /* Criteria Column (Sticky Left) */
        th.criteria-col, td.criteria-col {
            position: sticky;
            left: 0;
            background-color: white;
            font-weight: bold;
            width: 150px;
            z-index: 10;
            box-shadow: 2px 0 5px rgba(0,0,0,0.05);
            color: var(--primary);
        }

        /* Column Headers & Color Coding */
        th { text-align: left; font-size: 1rem; }
        .th-grey { background-color: var(--theme-grey-light); border-bottom: 3px solid var(--theme-grey-border); }
        .th-yellow { background-color: var(--theme-yellow-light); border-bottom: 3px solid var(--theme-yellow-border); }
        .th-green { background-color: var(--theme-green-light); border-bottom: 3px solid var(--theme-green-border); }
        .th-blue { background-color: var(--theme-blue-light); border-bottom: 3px solid var(--theme-blue-border); }

        /* Interactive Cells */
        td.clickable {
            cursor: pointer;
            transition: all 0.1s ease;
            position: relative;
        }
        td.clickable:hover { background-color: #f8fafc; }
        td.clickable ul { margin: 0; padding-left: 15px; }
        td.clickable li { margin-bottom: 6px; }
        td.clickable b { font-weight: 600; color: #0284c7; } /* Blue highlight for key terms */

        /* Selected States Based on Theme Column */
        td.clickable.selected.col-grey {
            background-color: var(--theme-grey-light);
            box-shadow: inset 0 0 0 3px var(--theme-grey-border);
        }
        td.clickable.selected.col-yellow {
            background-color: var(--theme-yellow-light);
            box-shadow: inset 0 0 0 3px var(--theme-yellow-border);
        }
        td.clickable.selected.col-green {
            background-color: var(--theme-green-light);
            box-shadow: inset 0 0 0 3px var(--theme-green-border);
        }
        td.clickable.selected.col-blue {
            background-color: var(--theme-blue-light);
            box-shadow: inset 0 0 0 3px var(--theme-blue-border);
        }

        /* Give selected items darker text for contrast */
        td.clickable.selected b { color: #0f172a; }

    </style>
</head>
<body>

    <!-- Sticky Top Dashboard -->
    <div class="dashboard">
        <div class="header-left">
            <div class="logo-badge">H</div>
            <div class="brand">
                <h1>Ms Hien</h1>
                <p>Interactive IELTS Speaking Descriptors</p>
            </div>
            <input type="text" id="studentName" class="student-input" placeholder="Enter Student Name..." oninput="saveDataLocally()">
        </div>

        <div class="score-board">
            <div class="criteria-summary" id="scoreSummary">
                FC: - &nbsp;|&nbsp; LR: - &nbsp;|&nbsp; GRA: - &nbsp;|&nbsp; PR: -
            </div>
            <div class="final-score" id="finalScore">0.0</div>
        </div>

        <div class="controls">
            <button class="btn-export" onclick="exportReport()">Export Report</button>
            <button class="btn-reset" onclick="clearWorkspace()">Clear</button>
        </div>
    </div>

    <!-- Main Table -->
    <div class="table-wrapper">
        <table id="rubricTable">
            <thead>
                <tr>
                    <th class="criteria-col">CRITERION</th>
                    <th class="th-grey">Band 1</th>
                    <th class="th-grey">Band 2</th>
                    <th class="th-grey">Band 3</th>
                    <th class="th-yellow">Band 4</th>
                    <th class="th-yellow">Band 5</th>
                    <th class="th-green">Band 6</th>
                    <th class="th-green">Band 7</th>
                    <th class="th-green">Band 8</th>
                    <th class="th-blue">Band 9</th>
                </tr>
            </thead>
            <tbody>
                
                <!-- Fluency Row -->
                <tr>
                    <td class="criteria-col">Fluency and Coherence (FC)</td>
                    <td class="clickable col-grey cell-fc" id="fc-1" onclick="setScore('fc', 1, 'col-grey')">
                        <ul><li>No communication possible.</li><li>No rate of speech.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-fc" id="fc-2" onclick="setScore('fc', 2, 'col-grey')">
                        <ul><li>Pauses lengthily before most words.</li><li>Little communication possible.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-fc" id="fc-3" onclick="setScore('fc', 3, 'col-grey')">
                        <ul><li>Speaks with <b>long pauses</b>.</li><li>Limited ability to link simple sentences.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-fc" id="fc-4" onclick="setScore('fc', 4, 'col-yellow')">
                        <ul><li>Cannot respond without <b>noticeable pauses</b>.</li><li>Speaks slowly, frequent repetition.</li><li>Links basic sentences with <b>repetitious</b> connectives.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-fc" id="fc-5" onclick="setScore('fc', 5, 'col-yellow')">
                        <ul><li>Maintains flow but uses <b>repetition, self-correction, or slow speech</b>.</li><li>May <b>over-use</b> certain connectives.</li></ul>
                    </td>
                    <td class="clickable col-green cell-fc" id="fc-6" onclick="setScore('fc', 6, 'col-green')">
                        <ul><li>Willing to speak <b>at length</b>, though may <b>lose coherence</b>.</li><li>Uses a range of connectives but <b>not always appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable col-green cell-fc" id="fc-7" onclick="setScore('fc', 7, 'col-green')">
                        <ul><li>Speaks <b>at length</b> without noticeable effort.</li><li>Some <b>language-related hesitation</b>.</li><li>Uses a range of <b>connectives and discourse markers</b> flexibly.</li></ul>
                    </td>
                    <td class="clickable col-green cell-fc" id="fc-8" onclick="setScore('fc', 8, 'col-green')">
                        <ul><li><b>Speaks fluently</b> with only <b>occasional repetition</b>.</li><li>Develops topics <b>coherently and appropriately</b>.</li></ul>
                    </td>
                    <td class="clickable col-blue cell-fc" id="fc-9" onclick="setScore('fc', 9, 'col-blue')">
                        <ul><li><b>Speaks fluently</b> with only <b>rare repetition</b>.</li><li><b>Cohesion is fully natural</b>.</li><li>Develops topics fully.</li></ul>
                    </td>
                </tr>

                <!-- Lexical Resource Row -->
                <tr>
                    <td class="criteria-col">Lexical Resource (LR)</td>
                    <td class="clickable col-grey cell-lr" id="lr-1" onclick="setScore('lr', 1, 'col-grey')">
                        <ul><li>Only a few isolated words.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-lr" id="lr-2" onclick="setScore('lr', 2, 'col-grey')">
                        <ul><li>Produces isolated words or memorised utterances.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-lr" id="lr-3" onclick="setScore('lr', 3, 'col-grey')">
                        <ul><li>Uses simple vocabulary to convey <b>personal information</b>.</li><li>Insufficient vocabulary for less familiar topics.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-lr" id="lr-4" onclick="setScore('lr', 4, 'col-yellow')">
                        <ul><li>Talks about familiar topics but only conveys <b>basic meaning</b> on unfamiliar ones.</li><li><b>Rarely attempts paraphrase</b>.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-lr" id="lr-5" onclick="setScore('lr', 5, 'col-yellow')">
                        <ul><li>Manages familiar/unfamiliar topics but uses <b>limited vocabulary</b>.</li><li>Attempts paraphrase with <b>mixed success</b>.</li></ul>
                    </td>
                    <td class="clickable col-green cell-lr" id="lr-6" onclick="setScore('lr', 6, 'col-green')">
                        <ul><li>Has a <b>wide enough vocabulary</b> to discuss topics at length.</li><li><b>Generally paraphrases successfully</b>.</li><li>Sometimes makes errors in word choice.</li></ul>
                    </td>
                    <td class="clickable col-green cell-lr" id="lr-7" onclick="setScore('lr', 7, 'col-green')">
                        <ul><li>Uses vocabulary flexibly across a <b>variety of topics</b>.</li><li>Uses <b>less common and idiomatic</b> vocabulary.</li><li>Can <b>paraphrase effectively</b>.</li></ul>
                    </td>
                    <td class="clickable col-green cell-lr" id="lr-8" onclick="setScore('lr', 8, 'col-green')">
                        <ul><li>Uses a <b>wide vocabulary resource</b> readily and flexibly.</li><li>Uses <b>less common and idiomatic</b> vocabulary skillfully.</li></ul>
                    </td>
                    <td class="clickable col-blue cell-lr" id="lr-9" onclick="setScore('lr', 9, 'col-blue')">
                        <ul><li>Uses vocabulary with <b>full flexibility and precision</b>.</li><li>Uses <b>idiomatic language naturally</b> and accurately.</li></ul>
                    </td>
                </tr>

                <!-- Grammar Row -->
                <tr>
                    <td class="criteria-col">Grammatical Range & Accuracy (GRA)</td>
                    <td class="clickable col-grey cell-gra" id="gra-1" onclick="setScore('gra', 1, 'col-grey')">
                        <ul><li>No communicable structures.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-gra" id="gra-2" onclick="setScore('gra', 2, 'col-grey')">
                        <ul><li>Cannot produce basic sentence forms.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-gra" id="gra-3" onclick="setScore('gra', 3, 'col-grey')">
                        <ul><li>Attempts basic sentence forms but with <b>abundant errors</b>.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-gra" id="gra-4" onclick="setScore('gra', 4, 'col-yellow')">
                        <ul><li>Produces basic sentence forms.</li><li><b>Frequent errors</b> may lead to misunderstanding.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-gra" id="gra-5" onclick="setScore('gra', 5, 'col-yellow')">
                        <ul><li>Produces <b>basic sentence forms</b> with reasonable accuracy.</li><li>Limited range of complex structures, which <b>usually contain errors</b>.</li></ul>
                    </td>
                    <td class="clickable col-green cell-gra" id="gra-6" onclick="setScore('gra', 6, 'col-green')">
                        <ul><li>Uses a <b>mix of simple and complex structures</b>.</li><li>May make <b>frequent mistakes with complex structures</b> (rarely causing comprehension problems).</li></ul>
                    </td>
                    <td class="clickable col-green cell-gra" id="gra-7" onclick="setScore('gra', 7, 'col-green')">
                        <ul><li>Uses a range of <b>complex structures</b> with some flexibility.</li><li><b>Frequently produces error-free sentences</b>.</li></ul>
                    </td>
                    <td class="clickable col-green cell-gra" id="gra-8" onclick="setScore('gra', 8, 'col-green')">
                        <ul><li>Uses a <b>wide range of structures flexibly</b>.</li><li>Produces a <b>majority of error-free sentences</b>.</li></ul>
                    </td>
                    <td class="clickable col-blue cell-gra" id="gra-9" onclick="setScore('gra', 9, 'col-blue')">
                        <ul><li>Uses a <b>full range of structures naturally</b>.</li><li>Produces consistently <b>accurate</b> structures apart from <b>'slips'</b>.</li></ul>
                    </td>
                </tr>

                <!-- Pronunciation Row -->
                <tr>
                    <td class="criteria-col">Pronunciation (PR)</td>
                    <td class="clickable col-grey cell-pr" id="pr-1" onclick="setScore('pr', 1, 'col-grey')">
                        <ul><li>Speech is unintelligible.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-pr" id="pr-2" onclick="setScore('pr', 2, 'col-grey')">
                        <ul><li>Speech is often unintelligible.</li></ul>
                    </td>
                    <td class="clickable col-grey cell-pr" id="pr-3" onclick="setScore('pr', 3, 'col-grey')">
                        <ul><li>Shows some of the features of Band 2 and some, but not all, of the positive features of Band 4.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-pr" id="pr-4" onclick="setScore('pr', 4, 'col-yellow')">
                        <ul><li>Uses a <b>limited range</b> of pronunciation features.</li><li><b>Frequent mispronunciations</b> cause difficulty for the listener.</li></ul>
                    </td>
                    <td class="clickable col-yellow cell-pr" id="pr-5" onclick="setScore('pr', 5, 'col-yellow')">
                        <ul><li>Shows all positive features of Band 4 and some, but not all, of Band 6.</li></ul>
                    </td>
                    <td class="clickable col-green cell-pr" id="pr-6" onclick="setScore('pr', 6, 'col-green')">
                        <ul><li>Uses a range of features with <b>mixed control</b>.</li><li>Can <b>generally be understood</b> throughout.</li></ul>
                    </td>
                    <td class="clickable col-green cell-pr" id="pr-7" onclick="setScore('pr', 7, 'col-green')">
                        <ul><li>Shows all positive features of Band 6 and some, but not all, of Band 8.</li></ul>
                    </td>
                    <td class="clickable col-green cell-pr" id="pr-8" onclick="setScore('pr', 8, 'col-green')">
                        <ul><li>Uses a <b>wide range</b> of pronunciation features flexibly.</li><li>Is <b>easy to understand</b> throughout; L1 accent has <b>minimal effect</b>.</li></ul>
                    </td>
                    <td class="clickable col-blue cell-pr" id="pr-9" onclick="setScore('pr', 9, 'col-blue')">
                        <ul><li>Uses a <b>full range of pronunciation features</b> with precision.</li><li>Is <b>effortless to understand</b> throughout.</li></ul>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        let scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
        
        window.onload = function() {
            if(localStorage.getItem('ielts_horizontal_name')) {
                document.getElementById('studentName').value = localStorage.getItem('ielts_horizontal_name');
            }
            if(localStorage.getItem('ielts_horizontal_scores')) {
                scores = JSON.parse(localStorage.getItem('ielts_horizontal_scores'));
                if(scores.fc > 0) applySelection('fc', scores.fc);
                if(scores.lr > 0) applySelection('lr', scores.lr);
                if(scores.gra > 0) applySelection('gra', scores.gra);
                if(scores.pr > 0) applySelection('pr', scores.pr);
                updateTotalScore();
            }
        };

        window.setScore = function(criterion, value, colorClass) {
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
                `FC: <b style="color:var(--primary)">${scores.fc || '-'}</b> &nbsp;|&nbsp; 
                 LR: <b style="color:var(--primary)">${scores.lr || '-'}</b> &nbsp;|&nbsp; 
                 GRA: <b style="color:var(--primary)">${scores.gra || '-'}</b> &nbsp;|&nbsp; 
                 PR: <b style="color:var(--primary)">${scores.pr || '-'}</b>`;
            
            if (scores.fc === 0 || scores.lr === 0 || scores.gra === 0 || scores.pr === 0) {
                document.getElementById('finalScore').innerText = "0.0";
            } else {
                const average = (scores.fc + scores.lr + scores.gra + scores.pr) / 4;
                const final = Math.round(average * 2) / 2;
                document.getElementById('finalScore').innerText = final.toFixed(1);
            }
        }

        function saveDataLocally() {
            localStorage.setItem('ielts_horizontal_name', document.getElementById('studentName').value);
            localStorage.setItem('ielts_horizontal_scores', JSON.stringify(scores));
        }

        function clearWorkspace() {
            if(confirm("Clear student data and reset the rubric?")) {
                localStorage.removeItem('ielts_horizontal_name');
                localStorage.removeItem('ielts_horizontal_scores');
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
                alert("Please select a band score for all 4 criteria to generate a report.");
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
