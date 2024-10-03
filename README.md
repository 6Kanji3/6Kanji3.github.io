<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monthly Lehrer Rating GSS</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(to right, #83a4d4, #b6fbff);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        .container {
            background-color: #ffffff;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            text-align: center;
            max-width: 400px;
            width: 100%;
            animation: fadeIn 1s ease-in-out;
        }
        h1, h2 {
            font-weight: 700;
            margin-bottom: 20px;
        }
        .menu button {
            padding: 15px 30px;
            font-size: 18px;
            border: none;
            border-radius: 8px;
            background-color: #007BFF;
            color: #fff;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
            margin: 10px 0;
            width: 100%;
        }
        .menu button:hover {
            background-color: #0056b3;
            transform: scale(1.05);
        }
        .teacher-card {
            background-color: #f0f0f0;
            border: 1px solid #ccc;
            border-radius: 10px;
            padding: 20px;
            margin: 20px auto;
            width: 100%;
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        .teacher-card.active {
            display: block;
            opacity: 1;
        }
        .teacher-image {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            object-fit: cover;
            margin-bottom: 10px;
        }
        .rating-container {
            margin: 15px 0;
        }
        .rating-container span {
            font-size: 30px;
            cursor: pointer;
            transition: transform 0.2s;
        }
        .rating-container span:hover {
            transform: scale(1.2);
        }
        .highlighted {
            color: gold;
        }
        .adjectives-container {
            text-align: left;
            margin: 10px 0;
        }
        .adjectives-container label {
            display: block;
            font-size: 14px;
            margin-bottom: 5px;
        }
        button#next-button, button#submit-button {
            display: block;
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            border-radius: 8px;
            background-color: #28a745;
            color: #fff;
            cursor: pointer;
            transition: background-color 0.3s, transform 0.2s;
            margin: 20px 0;
            width: 100%;
        }
        button#next-button:hover, button#submit-button:hover {
            background-color: #218838;
            transform: scale(1.05);
        }
        .hidden {
            display: none;
        }
        .results-page {
            display: none;
        }
        #top-teachers {
            font-size: 18px;
            margin-top: 20px;
        }
        .medal {
            font-size: 24px;
            margin-right: 10px;
        }
        #timer {
            font-size: 16px;
            margin-top: 10px;
        }
        /* Animationen */
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        /* Mobile Responsive Design */
        @media (max-width: 768px) {
            .container {
                padding: 15px;
                max-width: 100%;
            }
            .teacher-card {
                width: 100%;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Menüauswahl Lehrer oder Schüler -->
        <div id="menu-screen">
            <h1>Lehrer Rating GSS</h1>
            <h2>Wähle deine Rolle:</h2>
            <div class="menu">
                <button id="lehrer-btn">Lehrer</button>
                <button id="schueler-btn">Schüler</button>
            </div>
        </div>

        <!-- Lehrerbewertung -->
        <div id="rating-screen" class="hidden">
            <h2>Bewerte deine Lehrer</h2>
            <div id="teacher-list">
                <!-- Lehrer-Karte für Frau Milani -->
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
                        <label><input type="checkbox" value="zielorientiert"> Zielorientiert</label>
                        <label><input type="checkbox" value="kreativ"> Kreativ</label>
                        <label><input type="checkbox" value="hilfsbereit"> Hilfsbereit</label>
                        <label><input type="checkbox" value="inspirierend"> Inspirierend</label>
                        <label><input type="checkbox" value="strukturiert"> Strukturiert</label>
                        <label><input type="checkbox" value="motiviert"> Motiviert</label>
                        <label><input type="checkbox" value="kompetent"> Kompetent</label>
                        <label><input type="checkbox" value="unorganisiert"> Unorganisiert</label>
                        <label><input type="checkbox" value="ungerecht"> Ungerecht</label>
                        <label><input type="checkbox" value="langweilig"> Langweilig</label>
                        <label><input type="checkbox" value="unfreundlich"> Unfreundlich</label>
                        <label><input type="checkbox" value="nervig"> Nervig</label>
                        <label><input type="checkbox" value="abgelenkt"> Abgelenkt</label>
                        <label><input type="checkbox" value="chaotisch"> Chaotisch</label>
                        <label><input type="checkbox" value="arrogant"> Arrogant</label>
                        <label><input type="checkbox" value="faul"> Faul</label>
                        <label><input type="checkbox" value="respektlos"> Respektlos</label>
                    </div>
                </div>

                <!-- Weitere Lehrer hinzufügen, ähnlich wie oben -->
                <!-- Beispiel: Frau Heuser -->
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
                        <!-- Gleiche Adjektive wie bei Milani -->
                    </div>
                </div>

                <!-- Lehrer durchblättern -->
                <button id="next-button">Nächster Lehrer</button>
                <button id="submit-button" class="hidden">Bewertung abschicken</button>
            </div>
        </div>

        <!-- Ergebnisseite -->
        <div id="results-page" class="hidden">
            <h2>Top 3 Lehrer</h2>
            <div id="top-teachers">
                <!-- Ergebnisse werden hier eingefügt -->
            </div>
            <div id="timer">Zeit bis zum Logout: <span id="time-left">30</span> Sekunden</div>
        </div>
    </div>

    <script>
        // Startseite Logik
        const lehrerBtn = document.getElementById("lehrer-btn");
        const schuelerBtn = document.getElementById("schueler-btn");
        const menuScreen = document.getElementById("menu-screen");
        const ratingScreen = document.getElementById("rating-screen");
        const teacherCards = document.querySelectorAll(".teacher-card");
        const nextButton = document.getElementById("next-button");
        const submitButton = document.getElementById("submit-button");
        const resultsPage = document.getElementById("results-page");
        const topTeachers = document.getElementById("top-teachers");
        const timeLeftSpan = document.getElementById("time-left");

        let currentTeacherIndex = 0;

        // Lehrer oder Schüler auswählen
        lehrerBtn.addEventListener("click", () => {
            alert("Lehrer-Funktion wird noch implementiert.");
        });

        schuelerBtn.addEventListener("click", () => {
            menuScreen.classList.add("hidden");
            ratingScreen.classList.remove("hidden");
            showTeacherCard(currentTeacherIndex);
        });

        // Nächster Lehrer anzeigen
        nextButton.addEventListener("click", () => {
            currentTeacherIndex++;
            if (currentTeacherIndex < teacherCards.length) {
                showTeacherCard(currentTeacherIndex);
            } else {
                nextButton.classList.add("hidden");
                submitButton.classList.remove("hidden");
            }
        });

        // Lehrerkarte anzeigen
        function showTeacherCard(index) {
            teacherCards.forEach(card => card.classList.remove("active"));
            teacherCards[index].classList.add("active");
        }

        // Bewertung abschicken und Top 3 Lehrer anzeigen
        submitButton.addEventListener("click", () => {
            ratingScreen.classList.add("hidden");
            resultsPage.classList.remove("hidden");
            showTopTeachers();
            startTimer();
        });

        // Beispiel-Logik zur Anzeige der Top 3 Lehrer (Dummy-Daten)
        function showTopTeachers() {
            topTeachers.innerHTML = `
                <p><span class="medal">🥇</span> Frau Milani</p>
                <p><span class="medal">🥈</span> Frau Heuser</p>
                <p><span class="medal">🥉</span> Herr Geßner</p>
            `;
        }

        // Timer-Funktion
        function startTimer() {
            let timeLeft = 30;
            const countdown = setInterval(() => {
                timeLeft--;
                timeLeftSpan.textContent = timeLeft;
                if (timeLeft <= 0) {
                    clearInterval(countdown);
                    alert("Zeit ist um! Du wirst jetzt weitergeleitet.");
                    window.location.reload();  // Seite neu laden
                }
            }, 1000);
        }
    </script>
</body>
</html>