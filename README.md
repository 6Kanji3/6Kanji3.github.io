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
            <button class="button" id="next-button">Nächster Lehrer</button>
            <button class="button" id="submit-button" style="display:none;">Bewertung abschicken</button>
        </div>

        <div id="top-teachers">
            <h2>Top 3 Lehrer</h2>
            <div id="podium">
                <div class="podium-position" id="first"></div>
                <div class="podium-position" id="second"></div>
                <div class="podium-position" id="third"></div>
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

        const adjectivesPositive = [
            "Hilfsbereit", "Engagiert", "Kompetent", "Zuverlässig", 
            "Motiviert", "Respektvoll", "Inspirierend", "Flexibel", 
            "Witzig", "Geduldig", "Einfühlsam", "Kreativ", 
            "Fair", "Strukturiert", "Ehrlich", "Zielstrebig", 
            "Verständnisvoll", "Offen", "Loyal", "Pragmatisch", 
            "Analytisch", "Vorausschauend", "Optimistisch", "Diskret", 
            "Harmonisch", "Pünktlich"
        ];

        const adjectivesNegative = [
            "Unorganisiert", "Ungeduldig", "Unfair", "Inkompetent", 
            "Demotivierend", "Unhöflich", "Streng", "Langweilig", 
            "Unflexibel", "Unaufmerksam", "Schüchtern", "Überheblich", 
            "Negativ", "Desinteressiert", "Chaotisch", "Kritiklos", 
            "Unverständlich", "Distanziert", "Passiv", "Einseitig", 
            "Nervös", "Apathisch", "Irritierend", "Skeptisch", 
            "Ressentiment", "Stur"
        ];

        let currentTeacherIndex = 0;
        const ratings = [];

        document.getElementById('students-btn').onclick = function() {
            document.getElementById('students-btn').style.display = 'none';
            document.getElementById('teachers-btn').style.display = 'none';
            showRatingSection();
        }

        document.getElementById('teachers-btn').onclick = function() {
            alert("Lehrer können nicht bewerten.");
        }

        function showRatingSection() {
            document.getElementById('rating-section').style.display = 'block';
            loadTeacher(currentTeacherIndex);
        }

        function loadTeacher(index) {
            const teachersContainer = document.getElementById('teachers-container');
            teachersContainer.innerHTML = ''; // Clear previous content

            const teacher = teachers[index];
            const teacherCard = document.createElement('div');
            teacherCard.classList.add('teacher-card');

            teacherCard.innerHTML = `<strong>${teacher.name}</strong><br>
                <div class="rating-container" data-index="${index}">
                    ${[...Array(10)].map((_, i) => `<span class="star" data-value="${i + 1}">★</span>`).join('')}
                </div>
                <div class="adjectives-container">
                    ${adjectivesPositive.map(adj => `<label><input type="checkbox" value="${adj}"> ${adj}</label>`).join('')}
                    ${adjectivesNegative.map(adj => `<label><input type="checkbox" value="${adj}"> ${adj}</label>`).join('')}
                </div>
            `;

            teachersContainer.appendChild(teacherCard);

            // Add star rating functionality
            const stars = teacherCard.querySelectorAll('.star');
            stars.forEach(star => {
                star.onclick = function() {
                    const ratingContainer = star.parentElement;
                    ratingContainer.querySelectorAll('.star').forEach(s => s.classList.remove('selected'));
                    star.classList.add('selected');
                    for (let i = 0; i < star.dataset.value; i++) {
                        ratingContainer.children[i].classList.add('selected');
                    }
                };
            });

            // Show submit button if this is the last teacher
            if (index === teachers.length - 1) {
                document.getElementById('next-button').style.display = 'none';
                document.getElementById('submit-button').style.display = 'block';
            } else {
                document.getElementById('next-button').style.display = 'block';
                document.getElementById('submit-button').style.display = 'none';
            }
        }

        document.getElementById('next-button').onclick = function() {
            const rating = document.querySelector(`.teacher-card[data-index="${currentTeacherIndex}"] .rating-container .star.selected`);
            const adjectivesChecked = Array.from(document.querySelector(`.teacher-card[data-index="${currentTeacherIndex}"] .adjectives-container input:checked`)).map(input => input.value);

            if (rating) {
                ratings.push({
                    teacher: teachers[currentTeacherIndex].name,
                    rating: parseInt(rating.dataset.value),
                    adjectives: adjectivesChecked,
                });
                currentTeacherIndex++;
                loadTeacher(currentTeacherIndex);
            } else {
                alert("Bitte wähle eine Bewertung aus.");
            }
        };

        document.getElementById('submit-button').onclick = function() {
            const rating = document.querySelector(`.teacher-card[data-index="${currentTeacherIndex}"] .rating-container .star.selected`);
            const adjectivesChecked = Array.from(document.querySelector(`.teacher-card[data-index="${currentTeacherIndex}"] .adjectives-container input:checked`)).map(input => input.value);

            if (rating) {
                ratings.push({
                    teacher: teachers[currentTeacherIndex].name,
                    rating: parseInt(rating.dataset.value),
                    adjectives: adjectivesChecked,
                });

                displayTopTeachers(ratings);
            } else {
                alert("Bitte wähle eine Bewertung aus.");
            }
        };

        function displayTopTeachers(ratings) {
            // Calculate average ratings for each teacher
            const averages = {};

            ratings.forEach(({ teacher, rating }) => {
                if (!averages[teacher]) {
                    averages[teacher] = { total: 0, count: 0 };
                }
                averages[teacher].total += rating;
                averages[teacher].count++;
            });

            const sortedTeachers = Object.keys(averages).map(name => {
                return {
                    name,
                    average: averages[name].total / averages[name].count,
                };
            }).sort((a, b) => b.average - a.average);

            document.getElementById('first').innerText = `1. Platz: ${sortedTeachers[0]?.name || 'N/A'}`;
            document.getElementById('second').innerText = `2. Platz: ${sortedTeachers[1]?.name || 'N/A'}`;
            document.getElementById('third').innerText = `3. Platz: ${sortedTeachers[2]?.name || 'N/A'}`;

            // Show the podium
            document.getElementById('top-teachers').style.display = 'block';

            // Start 30-second timer
            setTimeout(() => {
                alert("Danke für Ihre Teilnahme! Die Umfrage wurde beendet.");
                location.reload(); // Reload the page after 30 seconds
            }, 30000);
        }
    </script>
</body>
</html>