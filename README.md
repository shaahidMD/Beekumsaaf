<!DOCTYPE html>
<html lang="om">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Beekkumsaaf | AI Note Generator & PDFs</title>
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
            --success: #16a34a;
        }

        body {
            background-color: var(--bg);
            color: var(--text);
            line-height: 1.6;
        }

        header {
            background: var(--card-bg);
            border-bottom: 1px solid var(--border);
            padding: 1.5rem 2rem;
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

        select {
            width: 100%;
            padding: 0.75rem;
            border: 1px solid #cbd5e1;
            border-radius: 8px;
            font-size: 1rem;
            outline: none;
            background: white;
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

        .btn-pdf {
            display: inline-block;
            margin-top: 1rem;
            padding: 0.75rem 1.5rem;
            background-color: var(--success);
            color: white;
            text-decoration: none;
            font-weight: 600;
            border-radius: 8px;
            transition: background 0.2s;
        }

        .btn-pdf:hover {
            background-color: #15803d;
        }
    </style>
</head>
<body>

    <header>
        <div class="logo">📖 Beekkumsaaf - Note & Book Center</div>
        <p style="color: var(--muted);">Nootii, cuunfaa fi kitaboota PDF kutaalee 1-8 argadhu</p>
    </header>

    <main>
        <div class="generator-card">
            <h2>Nootii fi PDF Filadhu</h2>
            <p style="color: var(--muted); margin-bottom: 1.5rem;">Kutaa, Gosa Barnootaa fi Yuunitii filachuun barnoota keessan hordofaa.</p>

            <div class="form-group">
                <label for="grade">Kutaa Filadhu:</label>
                <select id="grade">
                    <option value="Kutaa 8ffaa">Kutaa 8ffaa</option>
                </select>
            </div>

            <div class="form-group">
                <label for="subject">Gosa Barnootaa:</label>
                <select id="subject" onchange="updateUnits()">
                    <option value="Hisaaba">Hisaaba (Mathematics)</option>
                </select>
            </div>

            <div class="form-group">
                <label for="unit">Yuunitii Filadhu:</label>
                <select id="unit">
                    <option value="Unit 1">Unit 1 - Rational Numbers</option>
                    <option value="Unit 2">Unit 2 - Squares, Square Roots, Cubes and Cube Roots</option>
                    <option value="Unit 3">Unit 3 - Linear Equations and Inequalities</option>
                    <option value="Unit 4">Unit 4 - Similar Figures</option>
                    <option value="Unit 5">Unit 5 - Theorems on Similarity of Triangles</option>
                    <option value="Unit 6">Unit 6 - Lines and Angles in a Circle</option>
                    <option value="Unit 7">Unit 7 - Solid Figures</option>
                    <option value="Unit 8">Unit 8 - Introduction to Probability</option>
                </select>
            </div>

            <button onclick="generateNotes()">Nootii fi PDF Agarsiisi</button>
        </div>

        <!-- Saanduqa Nootiin Itti Mula'atu -->
        <div id="outputCard" class="notes-display">
            <h2 id="noteTitle" class="notes-header"></h2>
            
            <div class="note-section">
                <h4>📌 Qabxiilee Ijoo (Key Summary)</h4>
                <p id="noteSummary"></p>
            </div>

            <div class="note-section">
                <h4>📚 Jechoota / Seera Ijoo (Key Concepts)</h4>
                <ul id="noteTerms" style="margin-left: 1.5rem;"></ul>
            </div>

            <div class="quiz-box">
                <h4>❓ Gaaffii Shaakalaa (Practice Question)</h4>
                <p id="noteQuiz"></p>
            </div>

            <div style="margin-top: 1.5rem;">
                <h4>📄 Faayilii PDF Guutuu</h4>
                <a id="pdfLink" href="#" target="_blank" class="btn-pdf">📥 PDF Banadhu / Download Godhu</a>
            </div>
        </div>
    </main>

    <script>
        const mathUnits = {
            "Unit 1": {
                title: "Unit 1: Rational Numbers",
                summary: "Lakkoofsotni Rational Numbers kanneen bifa $\\frac{a}{b}$ tiin barreeffamuu danda'aniidha (bakka $b \\neq 0$ ta'etti).",
                terms: ["Rational Number: Lakkoofsa bifa $\\frac{a}{b}$ tiin kaa'amu.", "Terminating Decimal: Lakkoofsa desimaala dhiheessa xumura qabu.", "Repeating Decimal: Desimaala irra deebi'amu."],
                quiz: "Lakkoofsi $0.75$ jedhu bifa frākshiiniin ($\\frac{a}{b}$) yoo barreeffamu meeqa ta'a? (Deebii: $\\frac{3}{4}$).",
                pdf: "https://github.com/user-attachments/files/30328326/Unit.1.-.Rational.Numbers.pdf"
            },
            "Unit 2": {
                title: "Unit 2: Squares, Square Roots, Cubes and Cube Roots",
                summary: "Iskawerii ($x^2$) fi kiyyoowwan lakkoofsotaa ($x^3$), akkasumas iskaawer ruutii ($\\sqrt{x}$) fi kiyoob ruutii ($\\sqrt[3]{x}$) shallaguu baranna.",
                terms: ["Square: Lakkoofsa isumaan baay'isuu ($x \\times x$).", "Square Root: Lakkoofsa iskuweeriin isa erga kennamee booda hundee barbaaduu."],
                quiz: "Gatiin $\\sqrt{144}$ fi $\\sqrt[3]{27}$ meeqatami? (Deebii: $12$ fi $3$).",
                pdf: "https://github.com/user-attachments/files/30328203/Unit.2.-.Squares.Square.Roots.Cubes.and.Cube.Roots.pdf"
            },
            "Unit 3": {
                title: "Unit 3: Linear Equations and Inequalities",
                summary: "Sariitii sammanyaa sararaawaa fi Inequlaalitiiwwan ($<$, $>$, $\\leq$, $\\geq$) furuu.",
                terms: ["Linear Equation: Sararaawaa gatii sarara diriiraa kennu.", "Inequality: Wal-qixxummaa kan hin qabne ($>$ ykn $<$)."],
                quiz: "Yoo $3x - 5 = 10$ ta'e, gatiin $x$ meeqa ta'a? (Deebii: $x = 5$).",
                pdf: "https://github.com/user-attachments/files/30328201/Unit.3.-.Linear.Equations.and.Inequalities.pdf"
            },
            "Unit 4": {
                title: "Unit 4: Similar Figures",
                summary: "Muka fi bifa wal-fakkaatan (Similar Figures) kanneen fakkii walfakkaataa qaban garuu guddinaan garaagar ta'uu danda'an qorachuu.",
                terms: ["Similarity: Bifa wal-fakkaatu garuu hamma addaa.", "Ratio: Reeshoo cinaachota wal-gitiinsaa."],
                quiz: "Bifoonni wal-fakkaatan kantiilolee (angles) wal-gita ta'an qabu? (Deebii: Eeyyee).",
                pdf: "https://github.com/user-attachments/files/30328202/Unit.4.-.Similar.Figures.pdf"
            },
            "Unit 5": {
                title: "Unit 5: Theorems on Similarity of Triangles",
                summary: "Tiyooreemota wal-fakkii Sarseenaa (Triangles) kanneen akka AAA, SSS, fi SAS qorachuu.",
                terms: ["AAA Postulate: Angle-Angle-Angle", "SAS Postulate: Side-Angle-Side"],
                quiz: "Kantiiloonni 3n sarseenaa lamaanii wal-qixxeennaan, tiyooreema kam fayyadamna? (Deebii: AAA).",
                pdf: "https://github.com/user-attachments/files/30328206/Unit.5.-.Theorems.on.Similarity.of.Triangles.pdf"
            },
            "Unit 6": {
                title: "Unit 6: Lines and Angles in a Circle",
                summary: "Sararoota fi kantiilota geengoo (Circle) keessatti uumaman, kanneen akka Tangent, Secant, fi Radius qorachuu.",
                terms: ["Radius: Sarara wiirtuu irraa gara sarara geengoo.", "Tangent: Sarara geengoo tuqee darbu."],
                quiz: "Sararri geengoo qabxii tokko qofa irratti tuqu maal jedhama? (Deebii: Tangent).",
                pdf: "https://github.com/user-attachments/files/30328204/Unit.6.-.Lines.and.Angles.in.a.Circle.pdf"
            },
            "Unit 7": {
                title: "Unit 7: Solid Figures",
                summary: "Bifoota Jajjaboo (3D Figures) kanneen akka Prism, Cylinder, Cone, fi Sphere bal'ina dachee fi qabeenya (Volume) isaanii calculate gochuu.",
                terms: ["Volume: Qabeenya bifa 3D keessa jiru.", "Surface Area: Bal'ina alaa."],
                quiz: "Formulaan Volume silindarii maali? (Deebii: $V = \\pi r^2 h$).",
                pdf: "https://github.com/user-attachments/files/30328205/Unit.7.-.Solid.Figures.pdf"
            },
            "Unit 8": {
                title: "Unit 8: Introduction to Probability",
                summary: "Carraa (Probability) ta'iinsa tokkoo shallaguu: $P(E) = \\frac{\\text{Carraa Ta'iinsaa}}{\\text{Guutummaa Ta'iinsaa}}$.",
                terms: ["Sample Space: Iddoo guutuu ta'iinsaa.", "Event: Ta'iinsa murtaa'aa."],
                quiz: "Yoo Saantima ol darbannu, carraan fuulli 'Head' dhufuu meeqatami? (Deebii: $\\frac{1}{2}$ ykn $50\\%$).",
                pdf: "https://github.com/user-attachments/files/30328207/Unit.8.-.Introduction.to.Probability.pdf"
            }
        };

        function generateNotes() {
            const selectedUnit = document.getElementById('unit').value;
            const data = mathUnits[selectedUnit];

            if (data) {
                document.getElementById('noteTitle').innerText = data.title;
                document.getElementById('noteSummary').innerText = data.summary;

                const termsList = document.getElementById('noteTerms');
                termsList.innerHTML = "";
                data.terms.forEach(term => {
                    const li = document.createElement('li');
                    li.innerText = term;
                    termsList.appendChild(li);
                });

                document.getElementById('noteQuiz').innerText = data.quiz;
                document.getElementById('pdfLink').href = data.pdf;
                document.getElementById('outputCard').style.display = 'block';
            }
        }
    </script>
</body>
</html>
