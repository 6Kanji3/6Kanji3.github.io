# Monthly Lehrer Rating GSS

Eine einfache Website, auf der Schüler ihre Lehrer bewerten können. Die Lehrer der Q1-Stufe werden anhand von Sternen (1-10) und durch Auswahl von Attributen wie "freundlich", "streng" usw. bewertet. Der Lehrer mit der besten Bewertung wird monatlich gekrönt!

## Features
- Bewertungssystem für Lehrer (1-10 Sterne)
- Auswahl von Attributen, um den Lehrer sachlich zu beschreiben
- Speicherung der Bewertungen im LocalStorage des Browsers
- Automatische Berechnung der besten 3 Lehrer pro Monat
- Die Seite ist so konzipiert, dass jede IP-Adresse nur einmal abstimmen kann.

## Lehrer und zugewiesene Bilder
Die Bilder der Lehrer sind durch ihre Namen zugeordnet:

- **Frau Milani** - Rammstein Logo ![Rammstein Logo](https://upload.wikimedia.org/wikipedia/en/d/dc/Rammstein_logo.png)
- **Frau Heuser** - Isaac Newton Bild ![Isaac Newton](https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Isaac_Newton_by_William_Blake.jpg/480px-Isaac_Newton_by_William_Blake.jpg)
- **Herr Geßner** - Ed Sheeran Bild ![Ed Sheeran](https://upload.wikimedia.org/wikipedia/commons/4/45/Ed_Sheeran_2018.png)
- **Frau Kölker** - LGBTQ Flagge ![LGBTQ Flagge](https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/LGBTQ_Flag.svg/1920px-LGBTQ_Flag.svg.png)
- **Frau Luckey** - Frankreich Flagge
- **Herr Leitner** - Kroatische Flagge
- **Herr Menzel** - Fossil Uhr
- **Frau Leistikow** - Waden
- **Frau Selenkowitch** - Irgendwas mit Kunst
- **Frau Kosar** - Heiratsringe
- **Frau Dietsch** - Teebeutel
- **Herr Luetel** - Mark Forster Bild
- **Herr Claßen** - Sokrates Bild
- **Herr Hanke** - Irgendwas mit Religion
- **Frau Lips** - Dicke Lippen Bild

## Verwendung der Website

1. Forke dieses Repository oder klone es lokal.
2. Öffne die Datei `index.html`, um die Website lokal zu testen.
3. Um die Website live zu schalten, kannst du sie auf [GitHub Pages](https://pages.github.com/) bereitstellen.

### Bereitstellung auf GitHub Pages

1. Gehe zu den "Settings" deines GitHub-Repositories.
2. Scrolle zu "GitHub Pages".
3. Wähle unter "Source" die `main`-Branch und den Ordner `/root` aus.
4. Deine Website wird nach kurzer Zeit unter `https://<dein-github-benutzername>.github.io/<repository-name>/` verfügbar sein.

### QR-Code für die Website generieren

1. Nachdem die Website live ist, kopiere die URL von GitHub Pages.
2. Gehe auf eine QR-Code-Generator-Seite wie [qr-code-generator.com](https://www.qr-code-generator.com/).
3. Füge die URL der Website in den Generator ein und erhalte deinen QR-Code.
4. Drucke den QR-Code oder teile ihn, damit Schüler die Seite leicht erreichen können.

## HTML-Code der Website

```html
<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monthly Lehrer Rating GSS</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            background-color: #f0f0f0;
        }
        h1, h2 {
            text-align: center;
        }
        .teacher-card {
            background-color: #fff;
            border: 1px solid #ccc;
            border-radius: 10px;
            margin: 20px;
            padding: 20px;
            width: 300px;
            display: inline-block;
            vertical-align: top;
        }
        .teacher-image {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
        }
        .rating-container {
            margin: 10px 0;
        }
        .rating-container span {
            font-size: 24px;
            cursor: pointer;
        }
        .highlighted {
            color: gold;
        }
        .adjectives-container {
            margin: 10px 0;
        }
        .adjectives-container label {
            display: block;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 16px;
        }
        pre {
            background-color: #eee;
            padding: 10px;
            border-radius: 5px;
            margin: 20px auto;
            width: 80%;
        }
    </style>
</head>
<body>
    <h1>Bewerte deine Lehrer der Q1</h1>

    <div id="teacher-list">
        <div class="teacher-card" data-teacher="frau-milani">
            <img src="https://upload.wikimedia.org/wikipedia/en/d/dc/Rammstein_logo.png" alt="Frau Milani" class="teacher-image">
            <h3>Frau Milani</h3>
            <div class="rating-container">
                <span data-value="1">★</span><span data-value="2">★</span><span data-value="3">★</span>
                <span data-value="4">★</span><span data-value="5">★</span><span data-value="6">★</span>
                <span data-value="7">★</span><span data-value="8">★</span><span data-value="9">★</span>
                <span data-value="10">★</span>
            </div>
            <div class="adjectives-container">
                <label><input type="checkbox" value="freundlich"> Freundlich</label>
                <label><input type="checkbox" value="streng"> Streng</label>
                <label><input type="checkbox" value="geduldig"> Geduldig</label>
                <label><input type="checkbox" value="engagiert"> Engagiert</label>
                <label><input type="checkbox" value="zielorientiert"> Zielorientiert</label>
            </div>
        </div>

        <div class="teacher-card" data-teacher="frau-heuser">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/43/Isaac_Newton_by_William_Blake.jpg/480px-Isaac_Newton_by_William_Blake.jpg" alt="Frau Heuser" class="teacher-image">
            <h3>Frau Heuser</h3>
            <div class="rating-container">
                <span data-value="1">★</span><span data-value="2">★</span><span data-value="3">★</span>
                <span data-value="4">★</span><span data-value="5">★</span><span data-value="6">★</span>
                <span data-value="7">★</span><span data-value="8">★</span><span data-value="9">★</span>
                <span data-value="10">★</span>
            </div>
            <div class="adjectives-container">
                <label><input type="checkbox" value="freundlich"> Freundlich</label>
                <label><input type="checkbox" value="streng"> Streng</label>
                <label><input type="checkbox" value="geduldig"> Geduldig</label>
                <label><input type="checkbox" value="engagiert"> Engagiert</label>
                <label><input type="checkbox" value="zielorientiert"> Zielorientiert</label>
            </div>
        </div>

        <!-- Weitere Lehrer hier hinzufügen -->

    </div>

    <button id="submit-button">Bewertung abschicken</button>

    <h2>Deine Bewertung</h2>
    <pre id="results"></pre>

    <script>
        const ratings = {};
        const adjectives = {};

        document.querySelectorAll('.rating-container span').forEach(star => {
            star.addEventListener('click', function() {
                const rating = this.getAttribute('data-value');
                const teacher = this.closest('.teacher-card').getAttribute('data-teacher');
                ratings[teacher] = rating;

                this.parentElement.querySelectorAll('span').forEach(s => s.classList.remove('highlighted'));

                for (let i = 0; i < rating; i++) {
                    this.parentElement.children[i].classList.add('highlighted');
                }
            });
        });

        document.querySelectorAll('.adjectives-container input').forEach(checkbox => {
            checkbox.addEventListener('change', function() {
                const teacher = this.closest('.teacher-card').getAttribute('data-teacher');
                if (!adjectives[teacher]) adjectives[teacher] = [];
                if (this.checked) {
                    adjectives[teacher].push(this.value);
                } else {
                    const index = adjectives[teacher].indexOf(this.value);
                    if (index > -1) adjectives[teacher].splice(index, 1);
                }
            });
        });

        document.getElementById('submit-button').addEventListener('click', function() {
            saveRatings();
            displayResults();
        });

        function displayResults() {
            const resultElement = document.getElementById('results');
            resultElement.innerText = JSON.stringify({ ratings, adjectives }, null, 2);
        }

        function saveRatings() {
            localStorage.setItem('teacherRatings', JSON.stringify(ratings));
            localStorage.setItem('teacherAdjectives', JSON.stringify(adjectives));
        }

        function loadRatings() {
            const savedRatings = JSON.parse(localStorage.getItem('teacherRatings') || '{}');
            const savedAdjectives = JSON.parse(localStorage.getItem('teacherAdjectives') || '{}');
            Object.assign(ratings, savedRatings);
            Object.assign(adjectives, savedAdjectives);
        }

        loadRatings();
        displayResults();
    </script>
</body>
</html>