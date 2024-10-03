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

        <div class="teacher-card" data-teacher="herr-gessner">
            <img src="https://upload.wikimedia.org/wikipedia/commons/4/45/Ed_Sheeran_2018.png" alt="Herr Geßner" class="teacher-image">
            <h3>Herr Geßner</h3>
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

        <div class="teacher-card" data-teacher="frau-kolker">
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/46/LGBTQ_Flag.svg/1920px-LGBTQ_Flag.svg.png" alt="Frau Kölker" class="teacher-image">
            <h3>Frau Kölker</h3>
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

        <!-- Weitere Lehrer hinzufügen -->

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