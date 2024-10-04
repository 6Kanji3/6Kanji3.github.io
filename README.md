<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rate Your Teacher</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;500&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #e0f7fa;
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
            border-radius: 50px;
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

        .next-teacher-button {
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
        <h1>Rate Your Teacher</h1>
        <button class="button" id="start-student-rating-btn">Für Schüler bewerten</button>
        <button class="button" id="start-teacher-rating-btn">Für Lehrer bewerten</button>

        <div class="rating-section" id="rating-section">
            <h2>Lehrer bewerten</h2>
            <div id="teachers-container"></div>
            <button class="button next-teacher-button" id="next-teacher-btn">Nächsten Lehrer bewerten</button>
            <button class="button" id="submit-button">Bewertung abschicken</button>
        </div>

        <div class="top-teachers" id="top-teachers">
            <h2>Top 3 Lehrer der Q1</h2>
            <div class="podium" id="podium">
                <div class="podium-position" id="first"></div>
                <div class="podium-position" id="second"></div>
                <div class="podium-position" id="third"></div>
            </div>
            <div class="confetti" id="confetti"></div>
        </div>
    </div>

    <script>
        const teachers = [
            { name: "Frau Milani" }, { name: "Frau Heuser" }, { name: "Herr Geßner" },
            { name: "Frau Kölker" }, { name: "Frau Luckey" }, { name: "Herr Leitner" },
            { name: "Herr Menzel" }, { name: "Frau Leistikow" }, { name: "Frau Jenker" },
            { name: "Frau Selenkowitch" }, { name: "Frau Kosar" }, { name: "Frau Dietsch" },
            { name: "Herr Luetel" }, { name: "Herr Claßen" }, { name: "Herr Hanke" }, 
            { name: "Frau Lips" }
        ];

        const adjectives = [
            "freundlich", "hilfsbereit", "motiviert", "kompetent", "engagiert", 
            "inspirierend", "verständlich", "lustig", "geduldig", "interessant", 
            "organisiert", "verantwortungsbewusst", "sympathisch", "fair", "kreativ",
            "streng", "chaotisch", "unorganisiert", "kalt", "launisch", 
            "unfreundlich", "überfordernd", "langweilig", "desinteressiert", "unzuverlässig"
        ];

        let currentTeacherIndex = 0;
        let ratings = {};

        document.getElementById("start-student-rating-btn").addEventListener("click", startRating);
        document.getElementById("start-teacher-rating-btn").addEventListener("click", startRating);
        document.getElementById("next-teacher-btn").addEventListener("click", showNextTeacher);
        document.getElementById("submit-button").addEventListener("click", submitRatings);

        function startRating() {
            document.getElementById("rating-section").style.display = "block";
            document.getElementById("start-student-rating-btn").style.display = "none";
            document.getElementById("start-teacher-rating-btn").style.display = "none";
            showNextTeacher();
        }

        function showNextTeacher() {
            if (currentTeacherIndex >= teachers.length) {
                document.getElementById("submit-button").style.display = "block";
                document.getElementById("next-teacher-btn").style.display = "none";
                return;
            }

            const teacher = teachers[currentTeacherIndex];
            const teachersContainer = document.getElementById("teachers-container");

            teachersContainer.innerHTML = `
                <div class="teacher-card">
                    <h3>${teacher.name}</h3>
                    <div class="rating-container" id="rating-${teacher.name}">
                        ${Array.from({ length: 10 }, (_, i) => `<span data-rating="${i + 1}">&#9733;</span>`).join("")}
                    </div>
                    <div class="adjectives-container">
                        ${adjectives.map(adj => `
                            <input type="checkbox" id="${teacher.name}-${adj}" />
                            <label for="${teacher.name}-${adj}">${adj}</label>
                        `).join("")}
                    </div>
                </div>
            `;

            setupRatingSystem(teacher.name);
            currentTeacherIndex++;
        }

        function setupRatingSystem(teacherName) {
            const stars = document.querySelectorAll(`#rating-${teacherName} span`);
            stars.forEach(star => {
                star.addEventListener("click", function () {
                    stars.forEach(s => s.classList.remove("selected"));
                    this.classList.add("selected");
                    ratings[teacherName] = {
                        rating: this.dataset.rating,
                        adjectives: getSelectedAdjectives(teacherName)
                    };
                });
            });
        }

        function getSelectedAdjectives(teacherName) {
            return adjectives.filter(adj => document.getElementById(`${teacherName}-${adj}`).checked);
        }

        function submitRatings() {
            console.log("Bewertungen:", ratings);
            showTopTeachers();
        }

        function showTopTeachers() {
            const topTeachersDiv = document.getElementById("top-teachers");
            topTeachersDiv.style.display = "block";

            // Sortiere Lehrer nach Bewertung (für das Beispiel einfach Zufallsdaten)
            const sortedTeachers = Object.keys(ratings).sort((a, b) => ratings[b].rating - ratings[a].rating);
            
            document.getElementById("first").textContent = `1. Platz: ${sortedTeachers[0]}`;
            document.getElementById("second").textContent = `2. Platz: ${sortedTeachers[1]}`;
            document.getElementById("third").textContent = `3. Platz: ${sortedTeachers[2]}`;
        }
    </script>
</body>
</html>