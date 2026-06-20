<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ms Hien - Professional IELTS Scales</title>
    <style>
        :root {
            --primary: #2563eb;
            --primary-dark: #1e40af;
            --text-dark: #1e293b;
            --text-light: #64748b;
            --bg-page: #f8fafc;
            --border-color: #cbd5e1;
            
            /* Basic Colors for Highlights */
            --color-red: #ef4444;
            --color-orange: #f97316;
            --color-green: #22c55e;
            --color-blue: #3b82f6;
            
            /* Background Tints */
            --bg-red: #fef2f2;
            --bg-orange: #fff7ed;
            --bg-green: #f0fdf4;
            --bg-blue: #eff6ff;
        }

        * { box-sizing: border-box; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        body { margin: 0; background-color: var(--bg-page); color: var(--text-dark); font-size: 13px; line-height: 1.4; padding-bottom: 50px;}

        /* Header */
        .header { background: white; padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid var(--border-color); box-shadow: 0 2px 4px rgba(0,0,0,0.02); position: sticky; top: 0; z-index: 100;}
        .brand { display: flex; align-items: center; gap: 15px; }
        .logo-box { background: var(--primary); color: white; width: 32px; height: 32px; display: flex; align-items: center; justify-content: center; font-weight: bold; font-size: 1.2rem; border-radius: 4px;}
        .brand h1 { margin: 0; font-size: 1.1rem; color: var(--text-dark); }
        .brand span { color: var(--text-light); font-weight: normal; font-size: 0.9rem;}
        
        .controls button { padding: 8px 16px; font-weight: 600; border: none; border-radius: 4px; cursor: pointer; transition: 0.2s; font-size: 13px;}
        .btn-export { background: var(--primary); color: white; margin-right: 10px; }
        .btn-export:hover { background: var(--primary-dark); }
        .btn-reset { background: white; color: var(--text-dark); border: 1px solid var(--border-color); }
        .btn-reset:hover { background: #f1f5f9; }

        /* Dashboard Area - FULL WIDTH */
        .dashboard { width: 100%; margin: 20px 0; padding: 0 20px; display: flex; gap: 20px; }
        .panel { background: white; border: 1px solid var(--border-color); border-radius: 8px; padding: 20px; box-shadow: 0 1px 3px rgba(0,0,0,0.05); }
        
        /* Left: Student & Comments */
        .panel-left { flex: 1; display: flex; flex-direction: column; gap: 15px;}
        .panel-title { margin: 0 0 10px 0; font-size: 1rem; color: var(--text-dark); border-bottom: 1px solid var(--border-color); padding-bottom: 10px;}
        .input-box { width: 100%; padding: 10px; border: 1px solid var(--border-color); border-radius: 4px; font-size: 14px; }
        textarea.input-box { flex: 1; resize: none; min-height: 80px; }

        /* Center: Visual Scales */
        .panel-scales { flex: 1.5; }
        .scale-row { display: flex; align-items: center; gap: 15px; margin-bottom: 15px; }
        .scale-label { width: 160px; font-weight: 600; color: var(--text-dark); }
        .scale-track { flex: 1; height: 8px; background: #e2e8f0; border-radius: 4px; position: relative; overflow: hidden;}
        .scale-fill { height: 100%; background: var(--primary); width: 0%; transition: width 0.3s ease; border-radius: 4px;}
        .scale-val { width: 40px; text-align: right; font-weight: bold; color: var(--primary); font-size: 1.1rem;}

        /* Right: Final Score */
        .panel-score { flex: 0.8; display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center; }
        .score-circle { width: 120px; height: 120px; border-radius: 50%; border: 6px solid var(--primary); display: flex; align-items: center; justify-content: center; font-size: 3rem; font-weight: 900; color: var(--primary); margin-bottom: 10px;}
        .cefr-label { background: var(--text-dark); color: white; padding: 4px 12px; border-radius: 20px; font-size: 0.85rem; font-weight: bold;}

        /* Rubric Table Container - FULL WIDTH */
        .rubric-container { width: 100%; padding: 0 20px; overflow-x: auto; }
        .table-wrapper { border: 2px solid var(--border-color); border-radius: 8px; overflow: hidden; background: white; width: 100%;}
        
        table { width: 100%; border-collapse: collapse; min-width: 1400px; }
        th, td { border: 1px solid var(--border-color); padding: 12px 10px; vertical-align: top; }
        
        th { background: #f8fafc; color: var(--text-dark); text-align: left; font-size: 0.95rem; }
        th.col-criteria { width: 140px; position: sticky; left: 0; background: white; z-index: 10; box-shadow: 2px 0 4px rgba(0,0,0,0.05);}
        td.col-criteria { position: sticky; left: 0; background: #f8fafc; font-weight: bold; z-index: 10; box-shadow: 2px 0 4px rgba(0,0,0,0.05); color: var(--text-dark);}

        /* Column Headers Widths */
        th.band-hdr { text-align: center; width: 9%; }

        /* Interactive Cells */
        td.clickable { cursor: pointer; transition: all 0.1s; }
        td.clickable:hover { background: #f1f5f9; }
        td.clickable ul { margin: 0; padding-left: 15px; }
        td.clickable li { margin-bottom: 6px; }

        /* OUTSTANDING BOLD KEYWORDS (Basic Colors) */
        td.clickable b { font-weight: 800; }
        .band-red b { color: var(--color-red); }
        .band-orange b { color: var(--color-orange); }
        .band-green b { color: var(--color-green); }
        .band-blue b { color: var(--color-blue); }

        /* Selected States */
        td.clickable.selected { box-shadow: inset 0 0 0 3px; }
        td.clickable.selected.band-red { background: var(--bg-red); box-shadow: inset 0 0 0 3px var(--color-red); }
        td.clickable.selected.band-orange { background: var(--bg-orange); box-shadow: inset 0 0 0 3px var(--color-orange); }
        td.clickable.selected.band-green { background: var(--bg-green); box-shadow: inset 0 0 0 3px var(--color-green); }
        td.clickable.selected.band-blue { background: var(--bg-blue); box-shadow: inset 0 0 0 3px var(--color-blue); }
        
        td.clickable.selected b { color: var(--text-dark); background: rgba(255,255,255,0.7); padding: 0 2px; border-radius: 2px;}

    </style>
</head>
<body>

    <!-- Header -->
    <div class="header">
        <div class="brand">
            <div class="logo-box">V</div>
            <h1>Ms Hien <span>| Interactive Rating Scales Explorer</span></h1>
        </div>
        <div class="controls">
            <button class="btn-export" onclick="exportReport()">Mark & Level (Export)</button>
            <button class="btn-reset" onclick="clearWorkspace()">Clear Ink</button>
        </div>
    </div>

    <!-- Dashboard -->
    <div class="dashboard">
        <!-- Student & Comments -->
        <div class="panel panel-left">
            <h2 class="panel-title">Report Details</h2>
            <input type="text" id="studentName" class="input-box" placeholder="Student Name..." oninput="saveDataLocally()">
            <textarea id="generalComment" class="input-box" placeholder="Overall feedback and comments..." oninput="saveDataLocally()"></textarea>
        </div>

        <!-- Visual Scales -->
        <div class="panel panel-scales">
            <h2 class="panel-title">Productive Skill Band Calculator</h2>
            
            <div class="scale-row">
                <div class="scale-label">Fluency & Coherence</div>
                <div class="scale-track"><div class="scale-fill" id="bar-fc"></div></div>
                <div class="scale-val" id="val-fc">0.0</div>
            </div>
            
            <div class="scale-row">
                <div class="scale-label">Lexical Resource</div>
                <div class="scale-track"><div class="scale-fill" id="bar-lr"></div></div>
                <div class="scale-val" id="val-lr">0.0</div>
            </div>
            
            <div class="scale-row">
                <div class="scale-label">Grammar Range</div>
                <div class="scale-track"><div class="scale-fill" id="bar-gra"></div></div>
                <div class="scale-val" id="val-gra">0.0</div>
            </div>
            
            <div class="scale-row">
                <div class="scale-label">Pronunciation</div>
                <div class="scale-track"><div class="scale-fill" id="bar-pr"></div></div>
                <div class="scale-val" id="val-pr">0.0</div>
            </div>
        </div>

        <!-- Final Score -->
        <div class="panel panel-score">
            <h2 class="panel-title" style="width: 100%; text-align: left;">Overall Band</h2>
            <div class="score-circle" id="finalScore">0.0</div>
            <div class="cefr-label" id="cefrBadge">Unrated</div>
        </div>
    </div>

    <!-- Rubric Grid -->
    <div class="rubric-container">
        <div class="table-wrapper">
            <table id="rubricTable">
                <thead>
                    <tr>
                        <th class="col-criteria">CRITERIA</th>
                        <th class="band-hdr">Band 1</th>
                        <th class="band-hdr">Band 2</th>
                        <th class="band-hdr">Band 3</th>
                        <th class="band-hdr">Band 4</th>
                        <th class="band-hdr">Band 5</th>
                        <th class="band-hdr">Band 6</th>
                        <th class="band-hdr">Band 7</th>
                        <th class="band-hdr">Band 8</th>
                        <th class="band-hdr">Band 9</th>
                    </tr>
                </thead>
                <tbody>
                    <!-- Fluency Row -->
                    <tr>
                        <td class="col-criteria">Fluency & Coherence</td>
                        <!-- Bands 1-3 (Red) -->
                        <td class="clickable band-red cell-fc" id="fc-1" onclick="setScore('fc', 1)"><ul><li><b>No communication</b> possible.</li><li><b>No rate</b> of speech.</li></ul></td>
                        <td class="clickable band-red cell-fc" id="fc-2" onclick="setScore('fc', 2)"><ul><li>Pauses <b>lengthily</b> before most words.</li><li><b>Little communication</b> possible.</li></ul></td>
                        <td class="clickable band-red cell-fc" id="fc-3" onclick="setScore('fc', 3)"><ul><li>Speaks with <b>long pauses</b>.</li><li><b>Limited ability</b> to link simple sentences.</li><li>Gives only <b>simple responses</b> and is frequently unable to convey basic message.</li></ul></td>
                        <!-- Bands 4-5 (Orange) -->
                        <td class="clickable band-orange cell-fc" id="fc-4" onclick="setScore('fc', 4)"><ul><li>Cannot respond without <b>noticeable pauses</b> and may speak slowly.</li><li>Frequent <b>repetition and self-correction</b>.</li><li>Links basic sentences but with <b>repetitious use</b> of simple connectives.</li></ul></td>
                        <td class="clickable band-orange cell-fc" id="fc-5" onclick="setScore('fc', 5)"><ul><li>Usually <b>maintains flow</b> but uses repetition, self-correction and/or slow speech.</li><li>May <b>over-use</b> certain connectives and discourse markers.</li><li>Produces simple speech fluently, but complex communication causes <b>fluency problems</b>.</li></ul></td>
                        <!-- Bands 6-8 (Green) -->
                        <td class="clickable band-green cell-fc" id="fc-6" onclick="setScore('fc', 6)"><ul><li>Willing to speak <b>at length</b>, though may lose coherence at times due to occasional repetition, self-correction or hesitation.</li><li>Uses a range of connectives and discourse markers but <b>not always appropriately</b>.</li></ul></td>
                        <td class="clickable band-green cell-fc" id="fc-7" onclick="setScore('fc', 7)"><ul><li>Speaks <b>at length</b> without noticeable effort or loss of coherence.</li><li>May demonstrate <b>language-related hesitation</b> at times, or some repetition/self-correction.</li><li>Uses a range of connectives and discourse markers with <b>some flexibility</b>.</li></ul></td>
                        <td class="clickable band-green cell-fc" id="fc-8" onclick="setScore('fc', 8)"><ul><li>Speaks fluently with only <b>occasional repetition</b> or self-correction.</li><li>Hesitation is usually <b>content-related</b>.</li><li>Develops topics <b>coherently and appropriately</b>.</li></ul></td>
                        <!-- Band 9 (Blue) -->
                        <td class="clickable band-blue cell-fc" id="fc-9" onclick="setScore('fc', 9)"><ul><li>Speaks fluently with only <b>rare repetition</b> or self-correction.</li><li>Hesitation is <b>content-related</b> rather than to search for words/grammar.</li><li>Speaks coherently with <b>fully appropriate</b> cohesive features.</li><li><b>Develops topics fully</b> and appropriately.</li></ul></td>
                    </tr>

                    <!-- Vocabulary Row -->
                    <tr>
                        <td class="col-criteria">Lexical Resource</td>
                        <!-- Bands 1-3 (Red) -->
                        <td class="clickable band-red cell-lr" id="lr-1" onclick="setScore('lr', 1)"><ul><li><b>No communication</b> possible.</li><li><b>No rate</b> of speech.</li></ul></td>
                        <td class="clickable band-red cell-lr" id="lr-2" onclick="setScore('lr', 2)"><ul><li>Only produces <b>isolated words</b> or <b>memorised utterances</b>.</li></ul></td>
                        <td class="clickable band-red cell-lr" id="lr-3" onclick="setScore('lr', 3)"><ul><li>Uses simple vocabulary to convey <b>personal information</b>.</li><li><b>Insufficient vocabulary</b> for less familiar topics.</li></ul></td>
                        <!-- Bands 4-5 (Orange) -->
                        <td class="clickable band-orange cell-lr" id="lr-4" onclick="setScore('lr', 4)"><ul><li>Able to talk about familiar topics but can only convey <b>basic meaning</b> on unfamiliar topics.</li><li>Makes <b>frequent errors</b> in word choice.</li><li><b>Rarely attempts paraphrase</b>.</li></ul></td>
                        <td class="clickable band-orange cell-lr" id="lr-5" onclick="setScore('lr', 5)"><ul><li>Manages to talk about familiar and unfamiliar topics but uses vocabulary with <b>limited flexibility</b>.</li><li>Attempts to use paraphrase but with <b>mixed success</b>.</li></ul></td>
                        <!-- Bands 6-8 (Green) -->
                        <td class="clickable band-green cell-lr" id="lr-6" onclick="setScore('lr', 6)"><ul><li>Has a <b>wide enough vocabulary</b> to discuss topics at length and make meaning clear in spite of inappropriacies.</li><li><b>Generally paraphrases successfully</b>.</li></ul></td>
                        <td class="clickable band-green cell-lr" id="lr-7" onclick="setScore('lr', 7)"><ul><li>Uses vocabulary resource <b>flexibly</b> to discuss a variety of topics.</li><li>Uses some <b>less common and idiomatic</b> vocabulary and shows some awareness of style/collocation.</li><li>Uses <b>paraphrase effectively</b>.</li></ul></td>
                        <td class="clickable band-green cell-lr" id="lr-8" onclick="setScore('lr', 8)"><ul><li>Uses a <b>wide vocabulary resource</b> readily and flexibly to convey precise meaning.</li><li>Uses <b>less common and idiomatic</b> vocabulary skilfully, with occasional inaccuracies.</li><li>Uses <b>paraphrase effectively</b> as required.</li></ul></td>
                        <!-- Band 9 (Blue) -->
                        <td class="clickable band-blue cell-lr" id="lr-9" onclick="setScore('lr', 9)"><ul><li>Uses vocabulary with <b>full flexibility and precision</b> in all topics.</li><li>Uses <b>idiomatic language</b> naturally and accurately.</li></ul></td>
                    </tr>

                    <!-- Grammar Row -->
                    <tr>
                        <td class="col-criteria">Grammatical Range & Accuracy</td>
                        <!-- Bands 1-3 (Red) -->
                        <td class="clickable band-red cell-gra" id="gra-1" onclick="setScore('gra', 1)"><ul><li><b>No communication</b> possible.</li><li><b>No rate</b> of speech.</li></ul></td>
                        <td class="clickable band-red cell-gra" id="gra-2" onclick="setScore('gra', 2)"><ul><li><b>Cannot produce</b> basic sentence forms.</li></ul></td>
                        <td class="clickable band-red cell-gra" id="gra-3" onclick="setScore('gra', 3)"><ul><li>Attempts basic sentence forms but with <b>limited success</b>, or relies on memorised utterances.</li><li>Makes <b>numerous errors</b> except in memorised expressions.</li></ul></td>
                        <!-- Bands 4-5 (Orange) -->
                        <td class="clickable band-orange cell-gra" id="gra-4" onclick="setScore('gra', 4)"><ul><li>Produces basic sentence forms and some correct simple sentences but <b>subordinate structures are rare</b>.</li><li>Errors are frequent and may <b>lead to misunderstanding</b>.</li></ul></td>
                        <td class="clickable band-orange cell-gra" id="gra-5" onclick="setScore('gra', 5)"><ul><li>Produces basic sentence forms with <b>reasonable accuracy</b>.</li><li>Uses a limited range of more complex structures, but these <b>usually contain errors</b>.</li></ul></td>
                        <!-- Bands 6-8 (Green) -->
                        <td class="clickable band-green cell-gra" id="gra-6" onclick="setScore('gra', 6)"><ul><li>Uses a <b>mix of simple and complex structures</b>, but with limited flexibility.</li><li>May make <b>frequent mistakes</b> with complex structures though these rarely cause comprehension problems.</li></ul></td>
                        <td class="clickable band-green cell-gra" id="gra-7" onclick="setScore('gra', 7)"><ul><li>Uses a range of <b>complex structures with some flexibility</b>.</li><li>Frequently produces <b>error-free sentences</b>, though some grammatical mistakes persist.</li></ul></td>
                        <td class="clickable band-green cell-gra" id="gra-8" onclick="setScore('gra', 8)"><ul><li>Uses a <b>wide range of structures flexibly</b>.</li><li>Produces a <b>majority of error-free sentences</b> with only very occasional inappropriacies.</li></ul></td>
                        <!-- Band 9 (Blue) -->
                        <td class="clickable band-blue cell-gra" id="gra-9" onclick="setScore('gra', 9)"><ul><li>Uses a <b>full range of structures naturally</b> and appropriately.</li><li>Produces <b>consistently accurate</b> structures apart from 'slips' characteristic of native speaker speech.</li></ul></td>
                    </tr>

                    <!-- Pronunciation Row -->
                    <tr>
                        <td class="col-criteria">Pronunciation</td>
                        <!-- Bands 1-3 (Red) -->
                        <td class="clickable band-red cell-pr" id="pr-1" onclick="setScore('pr', 1)"><ul><li><b>No communication</b> possible.</li><li><b>No rate</b> of speech.</li></ul></td>
                        <td class="clickable band-red cell-pr" id="pr-2" onclick="setScore('pr', 2)"><ul><li>Speech is <b>often unintelligible</b>.</li></ul></td>
                        <td class="clickable band-red cell-pr" id="pr-3" onclick="setScore('pr', 3)"><ul><li>Shows some of the features of Band 2 and some, but not all, of the <b>positive features of Band 4</b>.</li></ul></td>
                        <!-- Bands 4-5 (Orange) -->
                        <td class="clickable band-orange cell-pr" id="pr-4" onclick="setScore('pr', 4)"><ul><li>Uses a <b>limited range</b> of pronunciation features.</li><li>Attempts to control features but <b>lapses are frequent</b>.</li><li>Mispronunciations are frequent and cause <b>some difficulty</b> for the listener.</li></ul></td>
                        <td class="clickable band-orange cell-pr" id="pr-5" onclick="setScore('pr', 5)"><ul><li>Shows all the positive features of Band 4 and some, but not all, of the <b>positive features of Band 6</b>.</li></ul></td>
                        <!-- Bands 6-8 (Green) -->
                        <td class="clickable band-green cell-pr" id="pr-6" onclick="setScore('pr', 6)"><ul><li>Uses a range of pronunciation features with <b>mixed control</b>.</li><li>Can <b>generally be understood</b> throughout, though mispronunciation of individual words reduces clarity at times.</li></ul></td>
                        <td class="clickable band-green cell-pr" id="pr-7" onclick="setScore('pr', 7)"><ul><li>Shows all the positive features of Band 6 and some, but not all, of the <b>positive features of Band 8</b>.</li></ul></td>
                        <td class="clickable band-green cell-pr" id="pr-8" onclick="setScore('pr', 8)"><ul><li>Uses a <b>wide range of pronunciation features</b>; sustains flexible use with only occasional lapses.</li><li>Is <b>easy to understand</b> throughout; L1 accent has minimal effect on intelligibility.</li></ul></td>
                        <!-- Band 9 (Blue) -->
                        <td class="clickable band-blue cell-pr" id="pr-9" onclick="setScore('pr', 9)"><ul><li>Uses a <b>full range of pronunciation features</b> with precision and subtlety.</li><li>Sustains <b>flexible use</b> of features throughout.</li><li>Is <b>effortless to understand</b>.</li></ul></td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        let scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
        
        window.onload = function() {
            if(localStorage.getItem('vstep_style_name')) {
                document.getElementById('studentName').value = localStorage.getItem('vstep_style_name');
            }
            if(localStorage.getItem('vstep_style_comment')) {
                document.getElementById('generalComment').value = localStorage.getItem('vstep_style_comment');
            }
            if(localStorage.getItem('vstep_style_scores')) {
                scores = JSON.parse(localStorage.getItem('vstep_style_scores'));
                if(scores.fc > 0) applySelection('fc', scores.fc);
                if(scores.lr > 0) applySelection('lr', scores.lr);
                if(scores.gra > 0) applySelection('gra', scores.gra);
                if(scores.pr > 0) applySelection('pr', scores.pr);
                updateVisuals();
            }
        };

        window.setScore = function(criterion, value) {
            scores[criterion] = value;
            applySelection(criterion, value);
            updateVisuals();
            saveDataLocally();
        }

        function applySelection(criterion, value) {
            const cells = document.querySelectorAll(`.cell-${criterion}`);
            cells.forEach(cell => cell.classList.remove('selected'));
            const selectedCell = document.getElementById(`${criterion}-${value}`);
            if(selectedCell) selectedCell.classList.add('selected');
        }

        function updateVisuals() {
            // Update Text Values
            document.getElementById('val-fc').innerText = scores.fc > 0 ? scores.fc.toFixed(1) : '0.0';
            document.getElementById('val-lr').innerText = scores.lr > 0 ? scores.lr.toFixed(1) : '0.0';
            document.getElementById('val-gra').innerText = scores.gra > 0 ? scores.gra.toFixed(1) : '0.0';
            document.getElementById('val-pr').innerText = scores.pr > 0 ? scores.pr.toFixed(1) : '0.0';

            // Animate Scale Bars (Percentage out of 9)
            document.getElementById('bar-fc').style.width = (scores.fc / 9 * 100) + '%';
            document.getElementById('bar-lr').style.width = (scores.lr / 9 * 100) + '%';
            document.getElementById('bar-gra').style.width = (scores.gra / 9 * 100) + '%';
            document.getElementById('bar-pr').style.width = (scores.pr / 9 * 100) + '%';
            
            const cefrBadge = document.getElementById('cefrBadge');

            if (scores.fc === 0 || scores.lr === 0 || scores.gra === 0 || scores.pr === 0) {
                document.getElementById('finalScore').innerText = "0.0";
                cefrBadge.innerText = "Unrated";
                cefrBadge.style.background = "var(--text-dark)";
            } else {
                const average = (scores.fc + scores.lr + scores.gra + scores.pr) / 4;
                const final = Math.round(average * 2) / 2;
                document.getElementById('finalScore').innerText = final.toFixed(1);

                // CEFR Logic
                if (final >= 9.0) { cefrBadge.innerText = "Level 6 / C2"; cefrBadge.style.background = "var(--color-blue)"; }
                else if (final >= 7.0) { cefrBadge.innerText = "Level 5 / C1"; cefrBadge.style.background = "var(--color-green)"; }
                else if (final >= 5.5) { cefrBadge.innerText = "Level 4 / B2"; cefrBadge.style.background = "var(--color-green)"; }
                else if (final >= 4.0) { cefrBadge.innerText = "Level 3 / B1"; cefrBadge.style.background = "var(--color-orange)"; }
                else { cefrBadge.innerText = "Below Level 3"; cefrBadge.style.background = "var(--color-red)"; }
            }
        }

        function saveDataLocally() {
            localStorage.setItem('vstep_style_name', document.getElementById('studentName').value);
            localStorage.setItem('vstep_style_comment', document.getElementById('generalComment').value);
            localStorage.setItem('vstep_style_scores', JSON.stringify(scores));
        }

        function clearWorkspace() {
            if(confirm("Clear student data and reset the rubric?")) {
                localStorage.removeItem('vstep_style_name');
                localStorage.removeItem('vstep_style_comment');
                localStorage.removeItem('vstep_style_scores');
                scores = { fc: 0, lr: 0, gra: 0, pr: 0 };
                document.getElementById('studentName').value = '';
                document.getElementById('generalComment').value = '';
                document.querySelectorAll('.clickable').forEach(c => c.classList.remove('selected'));
                updateVisuals();
            }
        }

        function stripHTML(html) {
            let tempDiv = document.createElement("div");
            tempDiv.innerHTML = html.replace(/<li>/g, "• ").replace(/<\/li>/g, "\n");
            return tempDiv.innerText || tempDiv.textContent || "";
        }

        function exportReport() {
            const finalScore = document.getElementById('finalScore').innerText;
            if(finalScore === "0.0") {
                alert("Please select a band score for all 4 criteria.");
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
