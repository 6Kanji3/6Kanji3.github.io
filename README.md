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
            background-color: #f0f0f0;
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
        }

        .container {
            text-align: center;
            background-color: white;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            padding: 30px;
            width: 90%;
            max-width: 600px;
        }

        .button {
            background-color: #6200ea;
            color: white;
            padding: 15px 25px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            margin: 10px;
            transition: background-color 0.3s;
            font-size: 20px;
        }

        .button:hover {
            background-color: #3700b3;
        }

        #rating-section {
            display: none;
        }

        .teacher-card {
            border: 1px solid #ddd;
            border-radius: 10px;
            margin: 10px 0;
            padding: 10px;
            background-color: #f9f9f9;
            transition: transform 0.3s;
        }

        .teacher-card:hover {
            transform: scale(1.02);
        }

        .teacher-image {
            width: 100%;
            height: auto;
            border-radius: 10px;
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
            <h2>Top 3 Lehrer</h2>
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
            { name: "Frau Milani", image: "https://example.com/milani.jpg" },
            { name: "Frau Heuser", image: "https://example.com/heuser.jpg" },
            { name: "Herr Geßner", image: "https://example.com/geßner.jpg" },
            { name: "Frau Kölker", image: "https://example.com/koelker.jpg" },
            { name: "Frau Luckey", image: "https://example.com/luckey.jpg" },
            { name: "Herr Leitner", image: "https://example.com/leitner.jpg" },
            { name: "Herr Menzel", image: "https://example.com/menzel.jpg" },
            { name: "Frau Leistikow", image: "https://example.com/leistikow.jpg" },
            { name: "Frau Selenkowitch", image: "https://example.com/selenkowitch.jpg" },
            { name: "Frau Kosar", image: "https://example.com/kosar.jpg" },
            { name: "Frau Dietsch", image: "https://example.com/dietsch.jpg" },
            { name: "Herr Luetel", image: "https://example.com/luetel.jpg" },
            { name: "Herr Claßen", image: "https://example.com/classen.jpg" },
            { name: "Herr Hanke", image: "https://example.com/hanke.jpg" },
            { name: "Frau Lips", image: "https://example.com/lips.jpg" }
        ];

        const goodAdjectives = [
            "freundlich", "geduldig", "hilfsbereit", "inspirierend", "kreativ",
            "kompetent", "motiviert", "strukturiert", "erfahren", "zielstrebig",
            "einfühlsam", "sympathisch", "dynamisch", "entspannt", "verlässlich",
            "lebensbejahend", "flexibel", "engagiert", "zuverlässig", "humorvoll",
            "positiv", "intelligent", "begeisternd", "herzlich", "tolerant"
        ];

        const badAdjectives = [
            "streng", "langweilig", "unorganisiert", "faul", "nervig",
            "arrogant", "ungerecht", "chaotisch", "respektlos", "unfreundlich",
            "abgelenkt", "überheblich", "unmotiviert", "langatmig", "schüchtern",
            "unentschlossen", "negativ", "desinteressiert", "giftig", "kritiklos",
            "unprofessionell", "verletzend", "einfältig", "verwirrend", "resigniert"
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
                        <img src="${teacher.image}" alt="${teacher.name}" class="teacher-image">
                        <h3>${teacher.name}</h3>
                        <div class="rating-container" id="rating-${currentTeacherIndex}">
                            <span class="star" data-value="1">★</span>
                            <span class="star" data-value="2">★</span>
                            <span class="star" data-value="3">★</span>
                            <span class="star" data-value="4">★</span>
                            <span class="star" data-value="5">★</span>
                        </div>
                        <div class="adjectives-container">
                            ${adjectives.map(adj => `<label><input type="checkbox" value="${adj}"> ${adj}</label>`).join('')}
                        </div>
                    </div>
                `;
                document.getElementById("teachers-container").innerHTML += teacherCard;
                addStarListeners(currentTeacherIndex);
                currentTeacherIndex++;
            } else {
                document.getElementById("submit-button").style.display = 'block';
            }
        }

        function addStarListeners(index) {
            const stars = document.querySelectorAll(`#rating-${index} .star`);
            stars.forEach(star => {
                star.addEventListener('click', () => {
                    stars.forEach(s => s.classList.remove('selected'));
                    star.classList.add('selected');
                    feedbackArray[index] = { rating: star.dataset.value, adjectives: [] };
                });
            });
        }

        document.getElementById("submit-button").addEventListener("click", handleSubmit);

        function handleSubmit() {
            document.querySelectorAll(".adjectives-container").forEach((container, index) => {
                const checkedAdjectives = Array.from(container.querySelectorAll("input:checked")).map(input => input.value);
                if (feedbackArray[index]) {
                    feedbackArray[index].adjectives = checkedAdjectives;
                }
            });
            showTopTeachers();
        }

        function showTopTeachers() {
            document.getElementById("rating-section").style.display = 'none';
            const results = calculateTopTeachers();
            displayTopTeachers(results);
            startTimer();
        }

        function calculateTopTeachers() {
            const ratings = feedbackArray.map(feedback => parseInt(feedback.rating) || 0);
            const adjectiveCounts = {};
            feedbackArray.forEach(feedback => {
                feedback.adjectives.forEach(adj => {
                    adjectiveCounts[adj] = (adjectiveCounts[adj] || 0) + 1;
                });
            });
            const sortedAdjectives = Object.entries(adjectiveCounts).sort((a, b) => b[1] - a[1]);
            const topAdjectives = sortedAdjectives.slice(0, 3).map(entry => entry[0]);

            const topTeachers = ratings
                .map((rating, index) => ({ name: teachers[index].name, rating, adjectives: feedbackArray[index].adjectives }))
                .sort((a, b) => b.rating - a.rating)
                .slice(0, 3);

            return { topTeachers, topAdjectives };
        }

        function displayTopTeachers({ topTeachers, topAdjectives }) {
            document.getElementById("top-teachers").style.display = 'block';
            document.getElementById("first").innerText = `1. ${topTeachers[0].name}`;
            document.getElementById("second").innerText = `2. ${topTeachers[1].name}`;
            document.getElementById("third").innerText = `3. ${topTeachers[2].name}`;
            if (topTeachers[0]) {
                animateConfetti();
            }
        }

        function startTimer() {
            let timeLeft = 30;
            const timerElement = document.getElementById("timer");
            timerElement.innerText = `Sie werden in ${timeLeft} Sekunden herausgeworfen.`;
            const countdown = setInterval(() => {
                timeLeft--;
                timerElement.innerText = `Sie werden in ${timeLeft} Sekunden herausgeworfen.`;
                if (timeLeft <= 0) {
                    clearInterval(countdown);
                    alert("Danke für Ihre Bewertungen! Sie werden jetzt zur Startseite weitergeleitet.");
                    window.location.reload();
                }
            }, 1000);
        }

        function animateConfetti() {
            const confetti = document.getElementById("confetti");
            confetti.classList.add("show");
            setTimeout(() => {
                confetti.classList.remove("show");
            }, 3000);
        }
    </script>
</body>
</html>