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
            margin-bottom: 10px;
            text-align: center;
            position: relative;
            font-size: 24px;
            color: white;
            transition: transform 0.5s;
        }

        .podium-position:nth-child(1) {
            background-color: #FFD700; /* Gold */
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
            document.querySelector('.container h1').innerText = "Bewerten Sie die Lehrer";
            document.getElementById("students-btn").style.display = "none";
            document.getElementById("teachers-btn").style.display = "none";
            document.getElementById("rating-section").style.display = "block";
            renderTeachers();
        }

        function renderTeachers() {
            const teachersContainer = document.getElementById("teachers-container");
            teachersContainer.innerHTML = ""; // Clear previous content

            teachers.forEach((teacher, index) => {
                const teacherCard = document.createElement("div");
                teacherCard.className = "teacher-card";

                const teacherImage = document.createElement("img");
                teacherImage.src = teacher.image;
                teacherImage.alt = teacher.name;
                teacherImage.className = "teacher-image";

                const teacherName = document.createElement("h3");
                teacherName.innerText = teacher.name;

                const ratingContainer = document.createElement("div");
                ratingContainer.className = "rating-container";

                const ratingSpan = document.createElement("span");
                ratingSpan.innerText = "⭐️";
                ratingSpan.className = "rating";
                ratingSpan.dataset.rating = 1;
                ratingSpan.addEventListener("click", () => setRating(index, ratingSpan));
                ratingContainer.appendChild(ratingSpan);

                const adjectiveContainer = document.createElement("div");
                adjectiveContainer.className = "adjectives-container";

                adjectives.forEach(adjective => {
                    const label = document.createElement("label");
                    label.innerHTML = `<input type="checkbox" value="${adjective}"> ${adjective}`;
                    adjectiveContainer.appendChild(label);
                });

                teacherCard.appendChild(teacherImage);
                teacherCard.appendChild(teacherName);
                teacherCard.appendChild(ratingContainer);
                teacherCard.appendChild(adjectiveContainer);
                teachersContainer.appendChild(teacherCard);
            });
        }

        function setRating(index, ratingElement) {
            const ratingValue = ratingElement.dataset.rating;
            const selectedRating = document.querySelectorAll('.teacher-card')[index].querySelector('.rating');

            // Clear previous ratings
            const allStars = document.querySelectorAll('.rating');
            allStars.forEach(star => star.classList.remove('selected'));
            
            // Set selected rating
            for (let i = 0; i < ratingValue; i++) {
                allStars[i].classList.add('selected');
            }
        }

        document.getElementById("submit-button").addEventListener("click", submitFeedback);

        function submitFeedback() {
            feedbackArray = []; // Reset feedback array

            const teacherCards = document.querySelectorAll('.teacher-card');
            teacherCards.forEach((card, index) => {
                const selectedRating = card.querySelector('.rating.selected');
                const selectedAdjectives = Array.from(card.querySelectorAll('input[type="checkbox"]:checked')).map(checkbox => checkbox.value);
                const teacherName = teachers[index].name;

                if (selectedRating) {
                    const ratingValue = selectedRating.dataset.rating;
                    feedbackArray.push({ teacher: teacherName, rating: ratingValue, adjectives: selectedAdjectives });
                }
            });

            // Calculate top teachers
            const topTeachers = calculateTopTeachers();
            displayTopTeachers(topTeachers);
        }

        function calculateTopTeachers() {
            const teacherScores = {};

            feedbackArray.forEach(feedback => {
                const teacher = feedback.teacher;
                const rating = parseInt(feedback.rating);

                if (!teacherScores[teacher]) {
                    teacherScores[teacher] = { score: 0, count: 0 };
                }

                teacherScores[teacher].score += rating;
                teacherScores[teacher].count += 1;
            });

            const scoresArray = Object.entries(teacherScores).map(([name, { score, count }]) => ({
                name,
                average: (score / count).toFixed(2)
            }));

            scoresArray.sort((a, b) => b.average - a.average);
            return scoresArray.slice(0, 3); // Top 3 teachers
        }

        function displayTopTeachers(topTeachers) {
            document.getElementById("top-teachers").style.display = "block";

            document.getElementById("first").innerText = `${topTeachers[0].name} - ${topTeachers[0].average} Sterne`;
            document.getElementById("second").innerText = `${topTeachers[1].name} - ${topTeachers[1].average} Sterne`;
            document.getElementById("third").innerText = `${topTeachers[2].name} - ${topTeachers[2].average} Sterne`;

            startConfetti();
            startTimer();
        }

        function startConfetti() {
            const confetti = document.getElementById("confetti");
            confetti.classList.add("show");

            setTimeout(() => {
                confetti.classList.remove("show");
            }, 5000); // Show for 5 seconds
        }

        function startTimer() {
            let timeLeft = 10; // 10 seconds countdown
            const timerElement = document.getElementById("timer");
            timerElement.innerText = `Redirecting in ${timeLeft} seconds...`;

            const timerInterval = setInterval(() => {
                timeLeft -= 1;
                timerElement.innerText = `Redirecting in ${timeLeft} seconds...`;

                if (timeLeft <= 0) {
                    clearInterval(timerInterval);
                    alert("Vielen Dank für Ihre Rückmeldung!");
                    location.reload(); // Redirect or refresh page
                }
            }, 1000);
        }
    </script>
</body>
</html>