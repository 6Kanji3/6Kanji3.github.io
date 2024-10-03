<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monthly Lehrer Rating GSS</title>
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
        }

        h1 {
            color: #333;
        }

        .container {
            text-align: center;
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
            font-size: 18px;
        }

        .button:hover {
            background-color: #3700b3;
        }

        #rating-section {
            display: none;
            background: white;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 500px;
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

        #timer {
            font-size: 20px;
            margin-top: 20px;
            color: red;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Monthly Lehrer Rating GSS</h1>
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
            <div id="first"></div>
            <div id="second"></div>
            <div id="third"></div>
        </div>
    </div>

    <script>
        const teachers = [
            { name: "Frau Milani", image: "https://example.com/milani.jpg" },
            { name: "Frau Heuser", image: "https://example.com/heuser.jpg" },
            { name: "Herr Geßner", image: "https://example.com/geschner.jpg" },
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

        const adjectives = [
            "freundlich", "streng", "geduldig", "zielorientiert",
            "kreativ", "hilfsbereit", "inspirierend", "strukturiert",
            "motiviert", "kompetent", "unorganisiert", "ungerecht",
            "langweilig", "unfreundlich", "nervig", "abgelenkt",
            "chaotisch", "arrogant", "faul", "respektlos"
        ];

        let timerInterval;
        let countdown;
        let currentTeacherIndex = 0;

        document.getElementById("students-btn").addEventListener("click", showRatingSection);
        document.getElementById("teachers-btn").addEventListener("click", () => alert("Sie wurden aus der Seite geworfen!"));

        function showRatingSection() {
            document.querySelector(".container h1").style.display = "none";
            document.getElementById("rating-section").style.display = "block";
            populateTeachers();
            startTimer();
        }

        function populateTeachers() {
            const teachersContainer = document.getElementById("teachers-container");
            teachersContainer.innerHTML = "";

            const teacher = teachers[currentTeacherIndex];
            const teacherCard = document.createElement("div");
            teacherCard.classList.add("teacher-card");
            teacherCard.innerHTML = `
                <img src="${teacher.image}" alt="${teacher.name}" class="teacher-image">
                <h3>${teacher.name}</h3>
                <div class="rating-container" data-teacher="${currentTeacherIndex}">
                    ${Array.from({ length: 10 }, (_, i) => `<span data-value="${i + 1}">★</span>`).join('')}
                </div>
                <div class="adjectives-container">
                    ${adjectives.map(adj => `<label><input type="checkbox" value="${adj}"> ${adj}</label>`).join('')}
                </div>
            `;
            teachersContainer.appendChild(teacherCard);
            addStarRatingListeners();
        }

        function addStarRatingListeners() {
            const ratingContainer = document.querySelector('.rating-container');
            ratingContainer.addEventListener('click', (e) => {
                if (e.target.dataset.value) {
                    const value = e.target.dataset.value;
                    ratingContainer.querySelectorAll('span').forEach(span => {
                        span.classList.remove('selected');
                    });
                    for (let i = 0; i < value; i++) {
                        ratingContainer.children[i].classList.add('selected');
                    }
                }
            });
        }

        function startTimer() {
            countdown = 30;
            updateTimer();
            clearInterval(timerInterval);
            timerInterval = setInterval(() => {
                countdown--;
                updateTimer();
                if (countdown <= 0) {
                    clearInterval(timerInterval);
                    alert("Zeit abgelaufen!");
                    displayTopTeachers([]);
                }
            }, 1000);
        }

        function updateTimer() {
            document.getElementById("timer").innerText = `Zeit verbleibend: ${countdown}s`;
        }

        document.getElementById("submit-button").addEventListener("click", () => {
            const name = teachers[currentTeacherIndex].name;
            const rating = document.querySelector('.rating-container .selected') ? 
                document.querySelector('.rating-container .selected').dataset.value : 'Keine Bewertung';
            const selectedAdjectives = Array.from(document.querySelectorAll('.adjectives-container input:checked'))
                .map(input => input.value);

            const feedback = {
                name: name,
                rating: rating,
                adjectives: selectedAdjectives
            };

            console.log("Feedback:", feedback);
            currentTeacherIndex++;

            if (currentTeacherIndex < teachers.length) {
                populateTeachers(); // Show next teacher
            } else {
                clearInterval(timerInterval);
                displayTopTeachers([feedback]);
            }
        });

        function displayTopTeachers(feedback) {
            document.getElementById("top-teachers").style.display = "block";
            document.getElementById("first").innerHTML = `
                <div class="top-teacher">
                    <h3>${feedback[0].name}</h3>
                    <p>Bewertung: ${feedback[0].rating}</p>
                    <p>Adjektive: ${feedback[0].adjectives.join(', ')}</p>
                </div>
            `;

            setTimeout(() => {
                alert("Sie werden jetzt von der Seite geworfen.");
                window.location.reload(); // Refresh the page after 30 seconds
            }, 30000);
        }
    </script>
</body>
</html>