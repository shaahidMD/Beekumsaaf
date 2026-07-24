<!DOCTYPE html>
<html lang="om">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beekkumsaaf | AI Note Generator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        :root {
            --primary: #2563eb;
            --primary-dark: #1d4ed8;
            --bg: #f8fafc;
            --card-bg: #ffffff;
            --text: #1e293b;
            --muted: #64748b;
            --border: #e2e8f0;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }

        header {
            background: var(--card-bg);
            border-bottom: 1px solid var(--border);
            padding: 1rem 2rem;
            text-align: center;
        }

        .logo {
            font-size: 1.8rem;
            font-weight: 700;
            color: var(--primary);
        }

        main {
            max-width: 900px;
            margin: 2rem auto;
            padding: 0 1rem;
        }

        .generator-card {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            border: 1px solid var(--border);
            margin-bottom: 2rem;
        }

        .form-group {
            margin-bottom: 1.2rem;
        }

        label {
            display: block;
            font-weight: 600;
            margin-bottom: 0.5rem;
        }

        select, input {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
        }

        button {
            width: 100%;
            background: var(--primary);
            color: white;
            border: none;
            padding: 0.85rem;
            font-size: 1rem;
            font-weight: 600;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.2s;
        }

        button:hover {
            background: var(--primary-dark);
        }

        .notes-display {
            background: var(--card-bg);
            padding: 2rem;
            border-radius: 12px;
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            border: 1px solid var(--border);
            display: none;
        }

        .notes-header {
            border-bottom: 2px solid var(--primary);
            padding-bottom: 0.5rem;
            margin-bottom: 1rem;
            color: var(--primary);
        }

        .note-section {
            margin-bottom: 1.5rem;
        }

        .note-section h4 {
            color: #334155;
            margin-bottom: 0.5rem;
        }

        .quiz-box {
            background: #eff6ff;
            padding: 1rem;
            border-left: 4px solid var(--primary);
            border-radius: 4px;
            margin-top: 1rem;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">📖 Beekkumsaaf - Note Generator</div>
        <p style="color: var(--muted);">Nootii fi cuunfaa barnootaa kutaalee 1-8 dafii uummadhu</p>
    </header>

    <main>
        <div class="generator-card">
            <h2>Nootii Uumuu (Generate Notes)</h2>
            <p style="color: var(--muted); margin-bottom: 1.5rem;">Kutaa fi gosa barnoota dhiheeffachuun nootii barbaaddan galchaa.</p>

            <div class="form-group">
                <label for="grade">Kutaa Filadhu:</label>
                <select id="grade">
                    <option value="Kutaa 7ffaa">Kutaa 7ffaa</option>
                    <option value="Kutaa 8ffaa">Kutaa 8ffaa</option>
                </select>
            </div>

            <div class="form-group">
                <label for="subject">Gosa Barnootaa:</label>
                <select id="subject">
                    <option value="Saayinsii Uumamaa">Saayinsii Uumamaa (General Science)</option>
                    <option value="Hisaaba">Hisaaba (Mathematics)</option>
                    <option value="Saayinsii Hawaasaa">Saayinsii Hawaasaa (Social Studies)</option>
                </select>
            </div>

            <button onclick="generateNotes()">Nootii Dhiheessi (Generate)</button>
        </div>

        <!-- Saanduqa Nootiin Itti Mula'atu -->
        <div id="outputCard" class="notes-display">
            <h2 id="noteTitle" class="notes-header"></h2>
            
            <div class="note-section">
                <h4>📌 Qabxiilee Ijoo (Key Summary)</h4>
                <p id="noteSummary"></p>
            </div>

            <div class="note-section">
                <h4>📚 Jechoota Ijoo (Key Terms)</h4>
                <ul id="noteTerms" style="margin-left: 1.5rem;"></ul>
            </div>

            <div class="quiz-box">
                <h4>❓ Gaaffii Shaakalaa (Practice Question)</h4>
                <p id="noteQuiz"></p>
            </div>
        </div>
    </main>

    <script>
        const database = {
            "Kutaa 8ffaa": {
                "Saayinsii Uumamaa": {
                    summary: "Barnootni kun waa'ee Sella (Cell), orgaanizimoota lubbu-qabeeyyii fi fiiziksii bu'uuraa irratti xiyyeeffata. Sellii jechuun qaama lubbu-qabeeyyii isa xiqqaa fi bu'uuraati.",
                    terms: ["Cell: Qaama bu'uuraa lubbu-qabeeyyii.", "Photosynthesis: Adeemsa biqiltoonni nyaata isaanii itti qopheessan.", "Atom: Yuunitii xiqqaa maatarxii."],
                    quiz: "Selliin simbirrootaa fi biqiltootaa garaagarrummaa maali qabu? (Deebii: Selliin biqiltuu Cell Wall qaba)."
                },
                "Hisaaba": {
                    summary: "Kutaa kana keessatti seera lakkoofsota 'Linear Equations' fi saayinsii ji'oomeetiriidhaa baranna. $x$ fi $y$ barbaaduun dandeettii bu'uuraati.",
                    terms: ["Variable: Lakkoofsa hin beekamne ($x$ ykn $y$).", "Equation: Hirmannaa garmalee fuula bitaa fi mirgaa wal-sima."],
                    quiz: "Yoo $2x + 4 = 10$ ta'e, gatiin $x$ meeqa ta'a? (Deebii: $x = 3$)."
                },
                "Saayinsii Hawaasaa": {
                    summary: "Seenaa addunyaa, ji'ogiraafii fi naannoo keenya ilaalchisee barnoota dhihaatudha.",
                    terms: ["Latitude: Sarara kiilolee diriiraa.", "History: Galmee darbiinsa hawaasaa."],
                    quiz: "Afaan Oromoo guddina seenaa keessatti gahee maalii qaba?"
                }
            },
            "Kutaa 7ffaa": {
                "Saayinsii Uumamaa": {
                    summary: "Qorannoo maatarxii, humnaa fi anniisaa ilaalchisee cuunfaa qophaa'e.",
                    terms: ["Energy: Dandeettii hojii hojjechuu.", "Matter: Wanta bakka fudhatu fi ulfaina qabu."],
                    quiz: "Gosa anniisaa keessaa lama caqasaa."
                },
                "Hisaaba": {
                    summary: "Kutaa 7ffatti waa'ee lakkoofsota gutuu (Integers) fi pirasentiijii (Percentage) baranna.",
                    terms: ["Integer: Lakkoofsota waltajjii (+, -).", "Fraction: Hirama lakkoofsa biroo."],
                    quiz: "$\frac{1}{2}$ gara dhibbeentaatti ($\%$) jijjiiri. (Deebii: $50\%$)"
                },
                "Saayinsii Hawaasaa": {
                    summary: "Waa'ee Qilleensaa fi haala teessuma lafaa qorachuu.",
                    terms: ["Climate: Haala qilleensaa yeroo dheeraa.", "Map: Fakkii teessuma lafaa."],
                    quiz: "Garaagarrummaa weather fi climate gidduu jiru maali?"
                }
            }
        };

        function generateNotes() {
            const grade = document.getElementById('grade').value;
            const subject = document.getElementById('subject').value;
            
            const selectedData = database[grade][subject];

            if (selectedData) {
                document.getElementById('noteTitle').innerText = grade + " - " + subject;
                document.getElementById('noteSummary').innerText = selectedData.summary;

                const termsList = document.getElementById('noteTerms');
                termsList.innerHTML = "";
                selectedData.terms.forEach(term => {
                    const li = document.createElement('li');
                    li.innerText = term;
                    termsList.appendChild(li);
                });

                document.getElementById('noteQuiz').innerText = selectedData.quiz;
                document.getElementById('outputCard').style.display = 'block';
            }
        }
    </script>
</body>
</html>
