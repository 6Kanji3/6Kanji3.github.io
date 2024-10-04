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
            background-color: #e0f7fa; /* Heller Hintergrund */
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            overflow: hidden;
            color: #333; /* Textfarbe */
        }

        h1 {
            font-size: 36px; /* Schriftgröße für den Haupttitel */
            margin-bottom: 20px; /* Abstand nach unten */
            text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.1); /* Leichte Schatten */
        }

        .container {
            text-align: center; /* Text zentrieren */
            background-color: white; /* Hintergrundfarbe des Containers */
            border-radius: 20px; /* Abgerundete Ecken */
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2); /* Schatten für Tiefe */
            padding: 30px; /* Innenabstand */
            width: 90%; /* Breite des Containers */
            max-width: 600px; /* Maximale Breite */
            animation: fadeIn 0.5s ease; /* Animation beim Laden */
        }

        @keyframes fadeIn {
            from { opacity: 0; } /* Von unsichtbar */
            to { opacity: 1; } /* Zu sichtbar */
        }

        .button {
            background-color: #009688; /* Hauptfarbe der Schaltflächen */
            color: white; /* Schriftfarbe */
            padding: 15px 25px; /* Innenabstand */
            border: none; /* Keine Rahmen */
            border-radius: 30px; /* Abgerundete Ecken */
            cursor: pointer; /* Zeiger für Hover-Effekt */
            margin: 10px; /* Abstand zwischen Schaltflächen */
            transition: background-color 0.3s, transform 0.3s; /* Animationseffekte */
            font-size: 20px; /* Schriftgröße */
        }

        .button:hover {
            background-color: #00796b; /* Dunklere Farbe beim Hover */
            transform: scale(1.05); /* Vergrößerungseffekt */
        }

        #rating-section {
            display: none; /* Anfangs unsichtbar */
        }

        .teacher-card {
            border: 1px solid #ddd; /* Rahmen für Lehrerkarte */
            border-radius: 15px; /* Abgerundete Ecken */
            margin: 10px 0; /* Abstand nach oben und unten */
            padding: 15px; /* Innenabstand */
            background-color: #f9f9f9; /* Hintergrundfarbe der Karte */
            transition: transform 0.3s; /* Animation für Hover */
        }

        .teacher-card:hover {
            transform: scale(1.02); /* Vergrößerung beim Hover */
        }

        .rating-container {
            display: flex; /* Flexbox für Sterne */
            justify-content: center; /* Zentrieren */
            margin: 10px 0; /* Abstand nach oben und unten */
        }

        .rating-container span {
            font-size: 24px; /* Schriftgröße für Sterne */
            cursor: pointer; /* Zeiger für Hover-Effekt */
            margin: 0 2px; /* Abstand zwischen Sternen */
            color: #ccc; /* Standardfarbe der Sterne */
        }

        .rating-container span.selected {
            color: gold; /* Farbe für ausgewählte Sterne */
        }

        .adjectives-container {
            display: flex; /* Flexbox für Adjektive */
            flex-wrap: wrap; /* Zeilenumbruch */
            justify-content: center; /* Zentrieren */
            margin: 10px 0; /* Abstand nach oben und unten */
        }

        .adjectives-container label {
            margin: 5px; /* Abstand für Adjektiv-Labels */
            font-size: 14px; /* Schriftgröße */
        }

        #top-teachers {
            display: none; /* Anfangs unsichtbar */
            margin-top: 20px; /* Abstand nach oben */
        }

        .top-teacher {
            background-color: #fff3cd; /* Hintergrundfarbe der besten Lehrer */
            border: 1px solid #ffeeba; /* Rahmen für beste Lehrer */
            border-radius: 10px; /* Abgerundete Ecken */
            padding: 10px; /* Innenabstand */
            margin: 5px; /* Abstand zwischen besten Lehrern */
            font-size: 20px; /* Schriftgröße */
        }

        /* Podium-Stile */
        #podium {
            display: flex; /* Flexbox für Podium */
            flex-direction: column; /* Vertikale Anordnung */
            align-items: center; /* Zentrieren */
            justify-content: center; /* Zentrieren */
            margin-top: 20px; /* Abstand nach oben */
        }

        .podium-position {
            width: 300px; /* Breite der Podiumsposition */
            padding: 20px; /* Innenabstand */
            border-radius: 10px; /* Abgerundete Ecken */
            background-color: #FFD700; /* Gold für erste Position */
            margin-bottom: 10px; /* Abstand nach unten */
            text-align: center; /* Text zentrieren */
            position: relative; /* Für Konfetti-Effekte */
            font-size: 24px; /* Schriftgröße */
            color: white; /* Schriftfarbe */
            transition: transform 0.5s; /* Animationseffekt */
        }

        .podium-position:nth-child(2) {
            background-color: #C0C0C0; /* Silber für zweite Position */
        }

        .podium-position:nth-child(3) {
            background-color: #cd7f32; /* Bronze für dritte Position */
        }

        .confetti {
            position: absolute; /* Absolute Positionierung für Konfetti */
            width: 100%; /* Volle Breite */
            height: 100%; /* Volle Höhe */
            top: 0; /* Oben */
            left: 0; /* Links */
            pointer-events: none; /* Keine Interaktion */
            display: none; /* Anfangs unsichtbar */
        }

        .confetti.show {
            display: block; /* Sichtbar, wenn aktiviert */
        }

        /* Responsive Styles */
        @media (max-width: 600px) {
            h1 {
                font-size: 28px; /* Kleinere Schriftgröße für Mobilgeräte */
            }

            .button {
                font-size: 18px; /* Kleinere Schriftgröße für Schaltflächen */
                padding: 12px 20px; /* Kleinerer Innenabstand */
            }

            .teacher-card {
                padding: 15px; /* Kleinerer Innenabstand */
            }

            .podium-position {
                width: 80%; /* Breitere Position für Mobilgeräte */
                font-size: 20px; /* Kleinere Schriftgröße */
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
            <div id="teachers-container"></div> <!-- Container für Lehrer -->
            <button class="button" id="submit-button">Bewertung abschicken</button> <!-- Button zum Absenden -->
            <div id="timer"></div> <!-- Timer, falls benötigt -->
        </div>

        <div id="top-teachers">
            <h2>Top 3 Lehrer der Q1</h2>
            <div id="podium">
                <div class="podium-position" id="first"></div> <!-- Platz 1 -->
                <div class="podium-position" id="second"></div> <!-- Platz 2 -->
                <div class="podium-position" id="third"></div> <!-- Platz 3 -->
                <div class="confetti" id="confetti"></div> <!-- Konfetti-Effekt -->
            </div>
        </div>
    </div>

    <script>
        // Lehrerarray mit Namen aller Lehrer
        const teachers = [
            { name: "Frau Milani" },
            { name: "Frau Heuser" },
            { name: "Herr Geßner" },
            { name: "Frau Kölker" },
            { name: "Frau Luckey" },
            { name: "Herr Leitner" },
            { name: "Herr Menzel" },
            { name: "Frau Leistner" },
            { name: "Herr Schmitt" },
            { name: "Frau Thomas" },
            { name: "Herr Rosenfeld" },
            { name: "Herr Müller" },
            { name: "Frau Becker" },
            { name: "Herr Krüger" },
            { name: "Frau Neumann" }
        ];

        // Array von Adjektiven für die Bewertung
        const adjectives = [
            "freundlich", "hilfsbereit", "motiviert", "kompetent", "engagiert",
            "inspirierend", "verständlich", "unterstützend", "fair", "teamfähig",
            "interessant", "unterhaltsam", "ansprechbar", "lebensnah", "aufrichtig", "respektvoll",
            "schwierig", "langweilig", "unorganisiert", "wenig verständlich", "unmotiviert",
            "ungerecht", "verwirrend", "abweisend", "nicht hilfsbereit", "nicht ansprechend",
            "uninteressant", "nicht engagiert", "unzuverlässig", "nicht verständlich", "nicht kompetent"
        ];

        let currentTeacherIndex = 0; // Index des aktuellen Lehrers
        let feedbackArray = []; // Array für die gesammelten Rückmeldungen

        document.getElementById("students-btn").addEventListener("click", function() {
            document.getElementById("rating-section").style.display = 'block'; // Zeige Bewertung Abschnitt
            this.style.display = 'none'; // Verstecke Schüler-Button
            document.getElementById("teachers-btn").style.display = 'none'; // Verstecke Lehrer-Button
            showNextTeacher(); // Zeige den nächsten Lehrer
        });

        function showNextTeacher() {
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
                document.getElementById("teachers-container").innerHTML += teacherCard; // Füge Lehrerkarte hinzu

                // Füge Ereignis-Listener für die Sternebewertung hinzu
                const ratingContainer = document.getElementById(`rating-${currentTeacherIndex}`);
                const stars = ratingContainer.querySelectorAll('.star');

                stars.forEach(star => {
                    star.addEventListener('click', function() {
                        stars.forEach(s => s.classList.remove('selected')); // Entferne Auswahl von allen Sternen
                        for (let i = 0; i < this.dataset.value; i++) {
                            stars[i].classList.add('selected'); // Füge ausgewählte Sterne hinzu
                        }
                    });
                });

                currentTeacherIndex++; // Erhöhe den Index für den nächsten Lehrer
            } else {
                document.getElementById("submit-button").style.display = 'block'; // Zeige den Absendebutton
            }
        }

        document.getElementById("submit-button").addEventListener("click", submitFeedback); // Ereignis-Listener für den Absendebutton

        function submitFeedback() {
            const allTeachers = document.querySelectorAll('.teacher-card');
            allTeachers.forEach((teacherCard, index) => {
                const selectedStars = teacherCard.querySelectorAll('.star.selected');
                const selectedAdjectives = Array.from(teacherCard.querySelectorAll('input[type="checkbox"]:checked')).map(input => input.value);
                const rating = selectedStars.length; // Anzahl der ausgewählten Sterne
                const name = teachers[index].name; // Name des Lehrers
                feedbackArray.push({ name, rating, adjectives: selectedAdjectives }); // Speichere die Rückmeldung
            });

            document.getElementById("rating-section").style.display = 'none'; // Verstecke den Bewertungsabschnitt
            showTopTeachers(); // Zeige die Top-Lehrer
        }

        function showTopTeachers() {
            const ratings = feedbackArray.map(f => f.rating);
            const teacherScores = {}; // Objekt für die Punktzahlen der Lehrer

            feedbackArray.forEach(({ name, rating }) => {
                if (!teacherScores[name]) teacherScores[name] = 0; // Initialisiere den Lehrer
                teacherScores[name] += rating; // Summiere die Bewertungen
            });

            const sortedTeachers = Object.keys(teacherScores).sort((a, b) => teacherScores[b] - teacherScores[a]).slice(0, 3); // Sortiere die Lehrer und wähle die besten 3
            document.getElementById("first").innerText = sortedTeachers[0] || "N/A"; // Erster Platz
            document.getElementById("second").innerText = sortedTeachers[1] || "N/A"; // Zweiter Platz
            document.getElementById("third").innerText = sortedTeachers[2] || "N/A"; // Dritter Platz

            document.getElementById("top-teachers").style.display = 'block'; // Zeige die Top-Lehrer
            showConfetti(); // Zeige Konfetti
        }

        function showConfetti() {
            const confetti = document.getElementById("confetti");
            confetti.classList.add("show"); // Aktiviere Konfetti
            setTimeout(() => {
                confetti.classList.remove("show"); // Deaktiviere Konfetti nach 3 Sekunden
            }, 3000);
        }
    </script>
</body>
</html>