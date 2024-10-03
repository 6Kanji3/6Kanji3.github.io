<!DOCTYPE html>
<html lang="de">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Monthly Lehrer Rating GSS</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f0f4f8;
            color: #333;
        }

        .container {
            width: 90%;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            border-radius: 15px;
            background: #fff;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        h1, h2 {
            text-align: center;
            color: #4a90e2;
        }

        .hidden {
            display: none;
        }

        .menu {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
        }

        .menu button {
            padding: 10px 20px;
            border: none;
            border-radius: 10px;
            background-color: #4a90e2;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
        }

        .menu button:hover {
            background-color: #357ab8;
        }

        .teacher-card {
            display: none;
            border: 2px solid #4a90e2;
            border-radius: 15px;
            padding: 20px;
            margin: 15px 0;
            text-align: center;
            background-color: #f9f9f9;
            transition: transform 0.3s;
        }

        .teacher-card.active {
            display: block;
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
            font-size: 30px;
            cursor: pointer;
        }

        .rating-container .highlighted {
            color: gold;
        }

        .adjectives-container {
            margin: 10px 0;
            text-align: left;
        }

        .adjectives-container label {
            display: block;
        }

        #submit-button {
            display: block;
            width: 100%;
            padding: 10px;
            border: none;
            border-radius: 10px;
            background-color: #4caf50;
            color: white;
            cursor: pointer;
            transition: background-color 0.3s;
            margin-top: 20px;
        }

        #submit-button:hover {
            background-color: #45a049;
        }

        .results-page {
            text-align: center;
        }

        .medal {
            font-size: 24px;
        }

        #timer {
            margin-top: 20px;
            font-size: 18px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Monthly Lehrer Rating GSS</h1>
        <div id="menu-screen">
            <h2>Wählen Sie Ihre Rolle</h2>
            <div class="menu">
                <button id="lehrer-btn">Lehrer</button>
                <button id="schueler-btn">Schüler</button>
            </div>
        </div>

        <div id="rating-screen" class="hidden">
            <h2>Bewerten Sie die Lehrer</h2>
            <div id="teachers">
                <div class="teacher-card" data-teacher="frau-milani">
                    <img src="https://upload.wikimedia.org/wikipedia/en/7/7d/Rammstein_-_Reise_Reise.jpg" alt="Frau Milani" class="teacher-image">
                    <h3>Frau Milani</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="frau-heuser">
                    <img src="https://upload.wikimedia.org/wikipedia/en/d/d6/Isaac_Newton_portrait.jpg" alt="Frau Heuser" class="teacher-image">
                    <h3>Frau Heuser</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-gesner">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/2/23/Ed_Sheeran_2019.jpg/640px-Ed_Sheeran_2019.jpg" alt="Herr Geßner" class="teacher-image">
                    <h3>Herr Geßner</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="frau-koelker">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/3e/LGBT_Pride_Flag.jpg/640px-LGBT_Pride_Flag.jpg" alt="Frau Kölker" class="teacher-image">
                    <h3>Frau Kölker</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="frau-luckey">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Flag_of_France.svg/640px-Flag_of_France.svg.png" alt="Frau Luckey" class="teacher-image">
                    <h3>Frau Luckey</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-leitner">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/92/Flag_of_Croatia.svg/640px-Flag_of_Croatia.svg.png" alt="Herr Leitner" class="teacher-image">
                    <h3>Herr Leitner</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-menzel">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/c/c4/Hourglass_Movements_Behind_The_Globe.jpg/640px-Hourglass_Movements_Behind_The_Globe.jpg" alt="Herr Menzel" class="teacher-image">
                    <h3>Herr Menzel</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="frau-leistikow">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Calf_2.jpg/640px-Calf_2.jpg" alt="Frau Leistikow" class="teacher-image">
                    <h3>Frau Leistikow</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="frau-selenkowitch">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Calf_2.jpg/640px-Calf_2.jpg" alt="Frau Selenkowitch" class="teacher-image">
                    <h3>Frau Selenkowitch</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-oehlke">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Calf_2.jpg/640px-Calf_2.jpg" alt="Herr Oehlke" class="teacher-image">
                    <h3>Herr Oehlke</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-tost">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Calf_2.jpg/640px-Calf_2.jpg" alt="Herr Tost" class="teacher-image">
                    <h3>Herr Tost</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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

                <div class="teacher-card" data-teacher="herr-zahlen">
                    <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/Calf_2.jpg/640px-Calf_2.jpg" alt="Herr Zahlen" class="teacher-image">
                    <h3>Herr Zahlen</h3>
                    <div class="rating-container">
                        <span data-value="1">★</span>
                        <span data-value="2">★</span>
                        <span data-value="3">★</span>
                        <span data-value="4">★</span>
                        <span data-value="5">★</span>
                        <span data-value="6">★</span>
                        <span data-value="7">★</span>
                        <span data-value="8">★</span>
                        <span data-value="9">★</span>
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
            </div>

            <button id="submit-button">Submit Feedback</button>

            <script>
                const teachers = document.querySelectorAll('.teacher-card');
                const submitButton = document.getElementById('submit-button');

                submitButton.addEventListener('click', () => {
                    teachers.forEach(teacher => {
                        const name = teacher.querySelector('h3').innerText;
                        const rating = teacher.querySelector('.rating-container input:checked') ? 
                            teacher.querySelector('.rating-container input:checked').value : 'No rating';
                        const adjectives = Array.from(teacher.querySelectorAll('.adjectives-container input:checked'))
                            .map(input => input.value);
                        
                        console.log(`Feedback for ${name}: Rating - ${rating}, Adjectives - ${adjectives.join(', ')}`);
                    });
                });
            </script>
        </main>
    </body>
</html>
