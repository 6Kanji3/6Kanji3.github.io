<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monatliche Lehrerbewertung GSS</title>
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
            height: 100vh;
            overflow: hidden;
            color: #333;
        }

        h1 {
            font-size: 36px;
            margin-bottom: 20px;
            text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.1);
        }

        .container {
            text-align: center;
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            padding: 30px;
            width: 90%;
            max-width: 600px;
            animation: fadeIn 0.5s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .button {
            background-color: #009688;
            color: white;
            padding: 15px 25px;
            border: none;
            border-radius: 30px;
            cursor: pointer;
            margin: 10px;
            transition: background-color 0.3s, transform 0.3s;
            font-size: 20px;
        }

        .button:hover {
            background-color: #00796b;
            transform: scale(1.05);
        }

        #rating-section {
            display: none;
        }

        .teacher-card {
            border: 1px solid #ddd;
            border-radius: 15px;
            margin: 10px 0;
            padding: 15px;
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
            font-size: 24px;
            cursor: pointer;
            margin: 0 2px;
            color: #ccc;
        }

        .rating-container span.selected {
            color: gold;
        }

        .adjectives-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin: 10px 0;
        }

        .adjectives-container label {
            margin: 5px;
            font-size: 14px;
        }

        #top-teachers {
            display: none;
            margin-top: 20px;
        }

        .top-teacher {
            background-color: #fff3cd;
            border: 1px solid #ffeeba;
            border-radius: 10px;
            padding: 10px;
            margin: 5px;
            font-size: 20px;
        }

        /* Podium Styles */
        #podium {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            margin-top: 20px;
        }

        .podium-position {
            width: 300px;
            padding: 20px;
            border-radius: 10px;
            background-color: #FFD700; /* Gold color for first */
            margin-bottom: 10px;
            text-align: center;
            position: relative;
            font-size: 24px;
            color: white;
            transition: transform 0.5s;
        }

        .podium-position:nth-child(2) {
            background-color: #C0C0C0; /* Silver */
        }

        .podium-position:nth-child(3) {
            background-color: #cd7f32; /* Bronze */
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

        /* Responsive Styles */
        @media (max-width: 600px) {
            h1 {
                font-size: 28px;
            }

            .button {
                font-size: 18px;
                padding: 12px 20px;
            }

            .teacher-card {
                padding: 15px;
            }

            .podium-position {
                width: 80%;
                font-size: 20px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Monatliche Lehrerbewertung GSS</h1>
        <button class="button" id="students-btn">Schüler</button>
        <button class="button" id="teachers-btn">Lehrer</button>

        <div id="rating-section">
            <h2>Lehrer bewerten</h2>
            <div id="teachers-container"></div>
            <button class="button" id="submit-button">Bewertung abschicken</button>
            <div id="timer"></div>
        </div>

        <div id="top-teachers">
            <h2>Top 3 Lehrer der Q1</h2>
            <div id="podium">
                <div class="podium-position" id="first"></div>
                <div class="podium-position" id="second"></div>
                <div class="podium-position" id="third"></div>
                <div class="confetti" id="confetti"></div>
            </div>
        </div>
    </div>

    <script>
        const teachers = [
            { name: "Frau Milani" },
            { name: "Frau Heuser" },
            { name: "Herr Geßner" },
            { name: "Frau Kölker" },
            { name: "Frau Luckey" },
            { name: "Herr Leitner" },
            { name: "Herr Menzel" },
            { name: "Frau Leistikow" },
            { name: "Frau Selenkowitch" },
            { name: "Frau Kosar" },
            { name: "Frau Dietsch" },
            { name: "Herr Luetel" },
            { name: "Herr Claßen" },
            { name: "Herr Hanke" },
            { name: "Frau Lips" }
        ];

        const goodAdjectives = [
            "freundlich", "geduldig", "hilfsbereit", "inspirierend", "kreativ",
            "kompetent", "motiviert", "strukturiert", "erfahren", "zielstrebig",
            "einfühlsam", "sympathisch", "dynamisch", "entspannt", "zuverlässig"
        ];

        const badAdjectives = [
            "streng", "langweilig", "unorganisiert", "faul", "nervig",
            "arrogant", "ungerecht", "chaotisch", "respektlos", "unfreundlich",
            "abgelenkt", "überheblich", "unmotiviert", "langatmig", "schüchtern"
        ];

        const adjectives = [...goodAdjectives, ...badAdjectives];

        let currentTeacherIndex = 0;
        let feedbackArray = [];

        document.getElementById("students-btn").addEventListener("click", showRatingSection);
        document.getElementById("teachers-btn").addEventListener("click", () => alert("Sie wurden aus der Seite geworfen."));

        function showRatingSection() {
            document.querySelector('.container h1').style.display = 'none';
            document.getElementById("students-btn").style.display = 'none';
            document.getElementById("teachers-btn").style.display = 'none';
            document.getElementById("rating-section").style.display = 'block';
            loadNextTeacher();
        }

        function loadNextTeacher() {
            if (currentTeacherIndex < teachers.length) {
                const teacher = teachers[currentTeacherIndex];
                const teacherCard = `
                    <div class="teacher-card">
                        <h3>${teacher.name}</h3>
                        <div class="rating-container" id="rating-${currentTeacherIndex}">
                            <span class="star" data-value="1">★</span>
                            <span class="star" data-value="2">★</span>
                            <span class="star" data-value="3">★</span>
                            <span class="star" data-value="4">★</span>
                            <span class="star" data-value="5">★</span>
                        </div>
                        <div class="adjectives-container">
                            ${adjectives.map(adj => `
                                <label>
                                    <input type="checkbox" value="${adj}"> ${adj}
                                </label>
                            `).join('')}
                        </div>
                    </div>
                `;
                document.getElementById("teachers-container").innerHTML += teacherCard;

                // Add event listeners for star rating
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
            const ratings = feedbackArray.map(f => f.rating);
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