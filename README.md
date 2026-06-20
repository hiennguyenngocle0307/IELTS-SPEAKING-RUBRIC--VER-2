# IELTS-SPEAKING-RUBRIC--VER-2
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms Hien - IELTS Speaking Rubric</title>
    <style>
        :root {
            --primary: #1e3a8a; /* Deep professional blue */
            --primary-hover: #1e40af;
            --secondary: #eff6ff; /* Very light blue for selected cells */
            --border: #cbd5e1;
            --text-dark: #0f172a;
            --text-light: #475569;
            --highlight: #0284c7; /* Color for bold key terms */
        }
        
        * {
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            margin: 0;
            padding: 0;
            background-color: #f8fafc;
            color: var(--text-dark);
            line-height: 1.5;
        }

        /* Top Sticky Dashboard */
        .dashboard {
            position: sticky;
            top: 0;
            background-color: white;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            padding: 15px 30px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            z-index: 100;
            border-bottom: 3px solid var(--primary);
        }

        .brand h1 {
            margin: 0;
            font-size: 1.5rem;
            color: var(--primary);
        }
        .brand p {
            margin: 0;
            font-size: 0.9rem;
            color: var(--text-light);
        }

        .student-info {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .student-info input {
            padding: 8px 12px;
            font-size: 1rem;
            border: 1px solid var(--border);
            border-radius: 4px;
            width: 250px;
        }

        .score-board {
            display: flex;
            align-items: center;
            gap: 20px;
        }
        .criteria-summary {
            font-weight: 600;
            color: var(--text-light);
            font-size: 1.1rem;
            background: #f1f5f9;
            padding: 8px 15px;
            border-radius: 6px;
        }
        .final-score-box {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .final-score-box span {
            font-size: 1.2rem;
            font-weight: bold;
        }
        .score-number {
            font-size: 2.5rem;
            font-weight: 900;
            color: var(--primary);
            min-width: 60px;
            text-align: center;
        }

        .controls button {
            padding: 10px 20px;
            font-size: 1rem;
            font-weight: bold;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .btn-export {
            background-color: #10b981;
            color: white;
            margin-right: 10px;
        }
        .btn-export:hover { background-color: #059669; }
        .btn-reset {
            background-color: #ef4444;
            color: white;
        }
        .btn-reset:hover { background-color: #dc2626; }

        /* Full Screen Table Container */
        .table-container {
            padding: 30px;
            width: 100%;
            overflow-x: auto;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            box-shadow: 0 1px 3px rgba(0,0,0,0.1);
        }

        th {
            background-color: var(--primary);
            color: white;
            padding: 15px;
            font-size: 1.1rem;
            text-align: left;
            border: 1px solid #0f172a;
        }

        td {
            border: 1px solid var(--border);
            padding: 15px;
            vertical-align: top;
            font-size: 0.95rem;
            width: 23%; /* Distribute 4 columns evenly */
        }

        /* The "Column of Scores" */
        th.band-col-header {
            width: 8%;
            text-align: center;
        }
        td.band-col {
            font-size: 2rem;
            font-weight: bold;
            text-align: center;
            vertical-align: middle;
            background-color: #e2e8f0;
            color: var(--primary);
            width: 8%;
            border-right: 3px solid var(--primary);
        }

        /* Interactive Cells */
        td.clickable {
            cursor: pointer;
            transition: all 0.15s ease;
        }
        td.clickable:hover {
            background-color: #f1f5f9;
        }
        td.clickable b {
            color: var(--highlight);
            font-weight: 700;
        }
        
        /* Selected State */
        td.selected {
            background-color: var(--secondary);
            border: 3px solid var(--primary);
            box-shadow: inset 0 0 10px rgba(30, 58, 138, 0.1);
        }
        td.selected b {
            color: var(--primary);
        }
    </style>
</head>
<body>

    <!-- Sticky Top Dashboard -->
    <div class="dashboard">
        <div class="brand">
            <h1>Ms Hien</h1>
            <p>IELTS Speaking Marking Rubric</p>
        </div>
        
        <div class="student-info">
            <input type="text" id="studentName" placeholder="Enter Student Name..." oninput="saveDataLocally()">
        </div>

        <div class="score-board">
            <div class="criteria-summary" id="scoreSummary">
                FC: - &nbsp;|&nbsp; LR: - &nbsp;|&nbsp; GRA: - &nbsp;|&nbsp; PR: -
            </div>
            <div class="final-score-box">
                <span>Overall:</span>
                <div class="score-number" id="finalScore">0.0</div>
            </div>
        </div>

        <div class="controls">
            <button class="btn-export" onclick="exportReport()">Export Report</button>
            <button class="btn-reset" onclick="clearWorkspace()">Reset</button>
        </div>
    </div>

    <!-- Main Interactive Grid -->
    <div class="table-container">
        <table id="rubricTable">
            <thead>
                <tr>
                    <th class="band-col-header">Band</th>
                    <th>Fluency & Coherence (FC)</th>
                    <th>Lexical Resource (LR)</th>
                    <th>Grammatical Range & Accuracy (GRA)</th>
                    <th>Pronunciation (PR)</th>
                </tr>
            </thead>
            <tbody>
                <!-- Band 9 -->
                <tr>
                    <td class="band-col">9.0</td>
                    <td class="clickable cell-fc" id="fc-9" onclick="setScore('fc', 9)">
                        • <b>Speaks fluently</b> with only <b>rare repetition</b> or self-correction.<br>
                        • <b>Cohesion is fully natural</b> and appropriate.<br>
                        • <b>Develops topics fully</b> and appropriately.
                    </td>
                    <td class="clickable cell-lr" id="lr-9" onclick="setScore('lr', 9)">
                        • Uses vocabulary with <b>full flexibility and precision</b>.<br>
                        • Uses <b>idiomatic language naturally</b> and accurately.
                    </td>
                    <td class="clickable cell-gra" id="gra-9" onclick="setScore('gra', 9)">
                        • Uses a <b>full range of structures naturally</b> and appropriately.<br>
                        • Produces consistently <b>accurate</b> structures apart from <b>'slips'</b>.
                    </td>
                    <td class="clickable cell-pr" id="pr-9" onclick="setScore('pr', 9)">
                        • Uses a <b>full range of pronunciation features</b> with precision.<br>
                        • Is <b>effortless to understand</b> throughout.
                    </td>
                </tr>
                <!-- Band 8 -->
                <tr>
                    <td class="band-col">8.0</td>
                    <td class="clickable cell-fc" id="fc-8" onclick="setScore('fc', 8)">
                        • <b>Speaks fluently</b> with only <b>occasional repetition</b> or self-correction.<br>
                        • Develops topics <b>coherently and appropriately</b>.
                    </td>
                    <td class="clickable cell-lr" id="lr-8" onclick="setScore('lr', 8)">
                        • Uses a <b>wide vocabulary resource</b> readily and flexibly.<br>
                        • Uses <b>less common and idiomatic</b> vocabulary skillfully.
                    </td>
                    <td class="clickable cell-gra" id="gra-8" onclick="setScore('gra', 8)">
                        • Uses a <b>wide range of structures flexibly</b>.<br>
                        • Produces a <b>majority of error-free sentences</b> with only very occasional inaccuracies.
                    </td>
                    <td class="clickable cell-pr" id="pr-8" onclick="setScore('pr', 8)">
                        • Uses a <b>wide range</b> of pronunciation features flexibly.<br>
                        • Is <b>easy to understand</b> throughout; L1 accent has <b>minimal effect</b>.
                    </td>
                </tr>
                <!-- Band 7 -->
                <tr>
                    <td class="band-col">7.0</td>
                    <td class="clickable cell-fc" id="fc-7" onclick="setScore('fc', 7)">
                        • Speaks <b>at length</b> without noticeable effort.<br>
                        • May demonstrate some <b>language-related hesitation</b> or repetition.<br>
                        • Uses a range of <b>connectives and discourse markers</b> with some flexibility.
                    </td>
                    <td class="clickable cell-lr" id="lr-7" onclick="setScore('lr', 7)">
                        • Uses vocabulary flexibly to discuss a <b>variety of topics</b>.<br>
                        • Uses some <b>less common and idiomatic</b> vocabulary with style awareness.<br>
                        • Can <b>paraphrase effectively</b>.
                    </td>
                    <td class="clickable cell-gra" id="gra-7" onclick="setScore('gra', 7)">
                        • Uses a range of <b>complex structures</b> with some flexibility.<br>
                        • <b>Frequently produces error-free sentences</b>, though some grammatical mistakes persist.
                    </td>
                    <td class="clickable cell-pr" id="pr-7" onclick="setScore('pr', 7)">
                        • Shows <b>all the positive features of Band 6</b> and some, but not all, of the positive features of <b>Band 8</b>.
                    </td>
                </tr>
                <!-- Band 6 -->
                <tr>
                    <td class="band-col">6.0</td>
                    <td class="clickable cell-fc" id="fc-6" onclick="setScore('fc', 6)">
                        • Willing to speak <b>at length</b>, though may <b>lose coherence</b> at times.<br>
                        • Uses a range of connectives but <b>not always appropriately</b>.
                    </td>
                    <td class="clickable cell-lr" id="lr-6" onclick="setScore('lr', 6)">
                        • Has a <b>wide enough vocabulary</b> to discuss topics at length.<br>
                        • <b>Generally paraphrases successfully</b>.<br>
                        • Sometimes makes <b>errors in word choice</b>.
                    </td>
                    <td class="clickable cell-gra" id="gra-6" onclick="setScore('gra', 6)">
                        • Uses a <b>mix of simple and complex structures</b>, but with limited flexibility.<br>
                        • May make <b>frequent mistakes with complex structures</b> (though rarely cause comprehension problems).
                    </td>
                    <td class="clickable cell-pr" id="pr-6" onclick="setScore('pr', 6)">
                        • Uses a range of pronunciation features with <b>mixed control</b>.<br>
                        • Can <b>generally be understood</b> throughout, though mispronunciation of individual words may occur.
                    </td>
                </tr>
                <!-- Band 5 -->
                <tr>
                    <td class="band-col">5.0</td>
                    <td class="clickable cell-fc" id="fc-5" onclick="setScore('fc', 5)">
                        • Usually <b>maintains flow</b> but uses <b>repetition, self-correction, or slow speech</b>.<br>
                        • May <b>over-use</b> certain connectives.
                    </td>
                    <td class="clickable cell-lr" id="lr-5" onclick="setScore('lr', 5)">
                        • Manages to talk about familiar/unfamiliar topics but uses <b>limited vocabulary</b>.<br>
                        • Attempts to use paraphrase but with <b>mixed success</b>.
                    </td>
                    <td class="clickable cell-gra" id="gra-5" onclick="setScore('gra', 5)">
                        • Produces <b>basic sentence forms</b> with reasonable accuracy.<br>
                        • Uses a <b>limited range</b> of more complex structures, but these <b>usually contain errors</b>.
                    </td>
                    <td class="clickable cell-pr" id="pr-5" onclick="setScore('pr', 5)">
                        • Shows <b>all the positive features of Band 4</b> and some, but not all, of the positive features of <b>Band 6</b>.
                    </td>
                </tr>
                <!-- Band 4 -->
                <tr>
                    <td class="band-col">4.0</td>
                    <td class="clickable cell-fc" id="fc-4" onclick="setScore('fc', 4)">
                        • Cannot respond without <b>noticeable pauses</b> and may speak <b>slowly</b>.<br>
                        • Links basic sentences but with <b>repetitious</b> use of simple connectives.
                    </td>
                    <td class="clickable cell-lr" id="lr-4" onclick="setScore('lr', 4)">
                        • Able to talk about familiar topics but can only convey <b>basic meaning</b> on unfamiliar topics.<br>
                        • <b>Rarely attempts paraphrase</b>.
                    </td>
                    <td class="clickable cell-gra" id="gra-4" onclick="setScore('gra', 4)">
                        • Produces basic sentence forms; <b>errors are frequent</b> and may lead to misunderstanding.
                    </td>
                    <td class="clickable cell-pr" id="pr-4" onclick="setScore('pr', 4)">
                        • Uses a <b>limited range</b> of pronunciation features.<br>
                        • <b>Frequent mispronunciations</b> cause some difficulty for the listener.
                    </td>
                </tr>
            </tbody>
        </table>
    </div>

    <script>
        // State variables
        let scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
        
        // Load saved data on page load
        window.onload = function() {
            if(localStorage.getItem('ielts_student_name')) {
                document.getElementById('studentName').value = localStorage.getItem('ielts_student_name');
            }
            if(localStorage.getItem('ielts_pure_matrix')) {
                scores = JSON.parse(localStorage.getItem('ielts_pure_matrix'));
                // Visually restore selections
                if(scores.fc > 0) document.getElementById(`fc-${scores.fc}`).classList.add('selected');
                if(scores.lr > 0) document.getElementById(`lr-${scores.lr}`).classList.add('selected');
                if(scores.gra > 0) document.getElementById(`gra-${scores.gra}`).classList.add('selected');
                if(scores.pr > 0) document.getElementById(`pr-${scores.pr}`).classList.add('selected');
                updateTotalScore();
            }
        };

        // Handle Table Clicks
        window.setScore = function(criterion, value) {
            scores[criterion] = value;
            
            // Remove 'selected' class from all cells in this column
            const cells = document.querySelectorAll(`.cell-${criterion}`);
            cells.forEach(cell => cell.classList.remove('selected'));
            
            // Add 'selected' class to the clicked cell
            document.getElementById(`${criterion}-${value}`).classList.add('selected');
            
            updateTotalScore();
            saveDataLocally();
        }

        // Calculate and display average
        function updateTotalScore() {
            document.getElementById('scoreSummary').innerHTML = 
                `FC: ${scores.fc || '-'} &nbsp;|&nbsp; LR: ${scores.lr || '-'} &nbsp;|&nbsp; GRA: ${scores.gra || '-'} &nbsp;|&nbsp; PR: ${scores.pr || '-'}`;
            
            if (scores.fc === 0 || scores.lr === 0 || scores.gra === 0 || scores.pr === 0) {
                document.getElementById('finalScore').innerText = "0.0";
            } else {
                const average = (scores.fc + scores.lr + scores.gra + scores.pr) / 4;
                const final = Math.round(average * 2) / 2; // Round to nearest 0.5
                document.getElementById('finalScore').innerText = final.toFixed(1);
            }
        }

        // Save to browser memory
        function saveDataLocally() {
            localStorage.setItem('ielts_student_name', document.getElementById('studentName').value);
            localStorage.setItem('ielts_pure_matrix', JSON.stringify(scores));
        }

        // Reset App
        function clearWorkspace() {
            if(confirm("Clear student name and all selected scores?")) {
                localStorage.clear();
                scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
                document.getElementById('studentName').value = '';
                document.querySelectorAll('.clickable').forEach(c => c.classList.remove('selected'));
                updateTotalScore();
            }
        }

        // Clean up HTML tags for text file export
        function stripHTML(html) {
            let tempDiv = document.createElement("div");
            tempDiv.innerHTML = html.replace(/<br>/g, "\n");
            return tempDiv.innerText || tempDiv.textContent || "";
        }

        // Export Report
        function exportReport() {
            const finalScore = document.getElementById('finalScore').innerText;
            if(finalScore === "0.0" || finalScore === "-") {
                alert("Please select a band score for all 4 criteria in the table.");
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
            
            // Grab text directly from the selected table cells
            const fcText = stripHTML(document.getElementById(`fc-${scores.fc}`).innerHTML);
            const lrText = stripHTML(document.getElementById(`lr-${scores.lr}`).innerHTML);
            const graText = stripHTML(document.getElementById(`gra-${scores.gra}`).innerHTML);
            const prText = stripHTML(document.getElementById(`pr-${scores.pr}`).innerHTML);

            report += `1. Fluency and Coherence (Band ${scores.fc})\n${fcText}\n\n`;
            report += `2. Lexical Resource (Band ${scores.lr})\n${lrText}\n\n`;
            report += `3. Grammatical Range & Accuracy (Band ${scores.gra})\n${graText}\n\n`;
            report += `4. Pronunciation (Band ${scores.pr})\n${prText}\n\n`;

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
