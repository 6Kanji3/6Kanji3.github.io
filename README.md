<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lehrerbewertung - Top 3 Lehrer der Q1</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #e0f7fa; /* Weiches, wolkenartiges Blau */
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            overflow-x: hidden;
            color: #333;
        }

        h1 {
            font-size: 40px;
            color: #555;
            margin-bottom: 30px;
            text-align: center;
        }

        .container {
            background-color: #ffffff;
            border-radius: 50px; /* Runde Ecken für das fluffige Design */
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            padding: 40px;
            width: 95%;
            max-width: 800px;
            text-align: center;
            animation: fadeIn 0.7s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .button {
            background-color: #009688;
            color: white;
            padding: 15px 30px;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            margin: 10px;
            font-size: 18px;
            transition: background-color 0.3s, transform 0.3s;
        }

        .button:hover {
            background-color: #00796b;
            transform: scale(1.05);
        }

        .rating-section {
            display: none;
        }

        .teacher-card {
            border: 2px solid #f0f0f0;
            border-radius: 30px;
            margin: 20px 0;
            padding: 20px;
            background-color: #f9f9f9;
            transition: transform 0.3s;
        }

        .teacher-card:hover {
            transform: scale(1.02);
        }

        .rating-container {
            display: flex;
            justify-content: center;
            margin: 10px 0;
        }

        .rating-container span {
            font-size: 28px;
            cursor: pointer;
            margin: 0 3px;
            color: #ccc;
        }

        .rating-container span.selected {
            color: gold;
        }

        .adjectives-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 15px;
        }

        .adjectives-container label {
            margin: 8px;
            font-size: 16px;
            background-color: #f0f0f0;
            padding: 8px 15px;
            border-radius: 20px;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .adjectives-container input[type="checkbox"] {
            display: none;
        }

        .adjectives-container input[type="checkbox"]:checked + label {
            background-color: #80deea;
        }

        #submit-button {
            display: none;
        }

        .top-teachers {
            display: none;
            margin-top: 30px;
        }

        .podium {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .podium-position {
            background-color: #FFD700;
            padding: 20px;
            border-radius: 20px;
            color: white;
            font-size: 24px;
            margin: 10px 0;
            width: 100%;
            max-width: 400px;
            text-align: center;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
        }

        .podium-position:nth-child(2) {
            background-color: #C0C0C0;
        }

        .podium-position:nth-child(3) {
            background-color: #cd7f32;
        }

        .confetti {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            pointer-events: none;
            display: none;
        }

        .confetti.show {
            display: block;
        }

        /* Responsive Anpassungen */
        @media (max-width: 768px) {
            h1 {
                font-size: 28px;
            }

            .teacher-card {
                padding: 15px;
            }

            .podium-position {
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Top 3 Lehrer der Q1 - Bewertung</h1>
        <button class="button" id="start-rating-btn">Bewertung Starten</button>

        <div class="rating-section" id="rating-section">
            <h2>Lehrer bewerten</h2>
            <div id="teachers-container"></div>
            <button class="button" id="submit-button">Bewertung abschicken</button>
        </div>

        <div class="top-teachers" id="top-teachers">
            <h2>Top 3 Lehrer</h2>
            <div class="podium" id="podium">
                <div class="podium-position" id="first"></div>
                <div class="podium-position" id="second"></div>
                <div class="podium-position" id="third"></div>
            </div>
            <div class="confetti" id="confetti"></div>
        </div>
    </div>

    <script>
        // Liste aller Lehrer
        const teachers = [
            { name: "Frau Milani" }, { name: "Frau Heuser" }, { name: "Herr Geßner" },
            { name: "Frau Kölker" }, { name: "Frau Luckey" }, { name: "Herr Leitner" },
            { name: "Herr Menzel" }, { name: "Frau Leistner" }, { name: "Herr Schmitt" },
            { name: "Frau Thomas" }, { name: "Herr Rosenfeld" }, { name: "Herr Müller" },
            { name: "Frau Becker" }, { name: "Herr Krüger" }, { name: "Frau Neumann" }
        ];

        // Liste der Adjektive
        const adjectives = [
            "freundlich", "hilfsbereit", "motiviert", "kompetent", "engagiert", 
            "inspirierend", "verständlich", "unterstützend", "fair", "teamfähig",
            "interessant", "unterhaltsam", "ansprechbar", "lebensnah", "respektvoll",
            "schwierig", "langweilig", "unorganisiert", "wenig verständlich", 
            "unmotiviert", "ungerecht", "verwirrend", "abweisend", "nicht hilfsbereit"
        ];

        let currentTeacherIndex = 0;
        let feedbackArray = [];

        document.getElementById("start-rating-btn").addEventListener("click", function() {
            document.getElementById("rating-section").style.display = 'block';
            this.style.display = 'none';
            showNextTeacher();
        });

        function showNextTeacher() {
            if (currentTeacherIndex < teachers.length) {
                const teacher = teachers[currentTeacherIndex];
                const teacherCard = `
                    <div class="teacher-card">
                        <h3>${teacher.name}</h3>
                        <div class="rating-container" id="rating-${currentTeacherIndex}">
                            ${[...Array(10)].map((_, i) => `<span class="star" data-value="${i+1}">★</span>`).join('')}
                        </div>
                        <div class="adjectives-container">
                            ${adjectives.map(adj => `
                                <input type="checkbox" id="adj-${adj}-${currentTeacherIndex}" value="${adj}">
                                <label for="adj-${adj}-${currentTeacherIndex}">${adj}</label>
                            `).join('')}
                        </div>
                    </div>
                `;
                document.getElementById("teachers-container").innerHTML += teacherCard;

                // Ereignis-Listener für die Sternebewertung
                const ratingContainer = document.getElementById(`rating-${currentTeacherIndex}`);
                const stars = ratingContainer.querySelectorAll('.star');

                stars.forEach(star => {
                    star.addEventListener('click', function() {
                        stars.forEach(s => s.classList.remove('selected'));
                        for (let i = 0; i < this.dataset.value; i++) {
                            stars[i].classList.add('selected');
                        }
                    });
                });

                currentTeacherIndex++;
            } else {
                document.getElementById("submit-button").style.display = 'block';
            }
        }

        document.getElementById("submit-button").addEventListener("click", submitFeedback);

        function submitFeedback() {
            const allTeachers = document.querySelectorAll('.teacher-card');
            allTeachers.forEach((teacherCard, index) => {
                const selectedStars = teacherCard.querySelectorAll('.star.selected');
                const selectedAdjectives = Array.from(teacherCard.querySelectorAll('input[type="checkbox"]:checked')).map(input => input.value);
                const rating = selectedStars.length;
                const name = teachers[index].name;
                feedbackArray.push({ name, rating, adjectives: selectedAdjectives });
            });

            document.getElementById("rating-section").style.display = 'none';
            showTopTeachers();
        }

        function showTopTeachers() {
            const teacherScores = {};
            feedbackArray.forEach(({ name, rating }) => {
                if (!teacherScores[name]) teacherScores[name] = 0;
                teacherScores[name] += rating;
            });

            const sortedTeachers = Object.keys(teacherScores).sort((a, b) => teacherScores[b] - teacherScores[a]).slice(0, 3);
            document.getElementById("first").innerText = sortedTeachers[0] || "N/A";
            document.getElementById("second").innerText = sortedTeachers[1] || "N/A";
            document.getElementById("third").innerText = sortedTeachers[2] || "N/A";

            document.getElementById("top-teachers").style.display = 'block';
            showConfetti();
        }

        function showConfetti() {
            const confetti = document.getElementById("confetti");
            confetti.classList.add("show");
            setTimeout(() => {
                confetti.classList.remove("show");
            }, 3000);
        }
    </script>
</body>
</html>