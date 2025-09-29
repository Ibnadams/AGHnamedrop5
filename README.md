<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Plateau Pop Culture & IQ Challenge: 60-Second Challenge (Multiple Choice)</title>
    
    <style>
        /* --- CSS STYLES --- */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: flex-start;
            min-height: 100vh;
            margin: 0;
            padding: 10px;
            
            /* Lava Red Background */
            background-color: #A31F2A; /* Deep Lava Red */
            color: white; 
        }

        #game-container {
            width: 90%;
            max-width: 600px;
            background-color: rgba(0, 0, 0, 0.8);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 30px rgba(255, 230, 0, 0.5); 
            position: relative;
            overflow: hidden;
            border: 1px solid #FFEB3B;
            margin-top: 5vh; 
        }

        /* --- MOBILE OPTIMIZATION --- */
        @media (max-width: 600px) {
            body {
                align-items: flex-start;
                min-height: 100dvh;
            }
            #game-container {
                margin-top: 2vh; 
            }
            #header-main {
                flex-direction: column;
                align-items: flex-start;
            }
            #stats {
                width: 100%;
                display: flex;
                justify-content: space-between;
                margin-top: 5px;
            }
            #clue-area {
                height: 220px; /* Increased height to fit options */
                padding: 10px;
            }
        }
        /* ---------------------------------------------------- */

        #header {
            margin-bottom: 15px;
            text-align: center;
        }
        
        #header-main {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 5px;
        }
        
        #creator-ref {
            font-size: 0.9em;
            font-style: italic;
            opacity: 0.7;
            text-align: right;
            margin-top: -15px; 
            margin-right: 5px;
            color: #ccc;
        }

        h1 {
            color: #FFEB3B; /* Neon Yellow for the title */
        }

        #stats p {
            margin: 5px 0;
            font-size: 1.2em;
            font-weight: bold;
            color: #E0E0E0;
        }

        #clue-area {
            width: 100%;
            height: 180px; /* Base height for clue and options */
            display: flex;
            flex-direction: column;
            justify-content: space-around; /* Distribute space */
            align-items: center;
            margin-bottom: 20px;
            background-color: #1a080a;
            border-radius: 8px;
            padding: 15px;
            text-align: center;
            border: 2px solid #A31F2A;
        }
        
        #clue-text {
            font-size: 1.1em;
            font-weight: 500;
            color: #FFEB3B; /* Neon Yellow for clue text */
            margin-bottom: 10px;
            text-shadow: 0 0 5px rgba(255, 230, 0, 0.8);
        }

        #options-container {
            display: flex;
            flex-direction: column;
            gap: 8px; /* Space between buttons */
            width: 100%;
            margin-top: 10px;
        }

        .option-button {
            padding: 10px;
            background-color: #333; /* Dark button background */
            color: #FFEB3B; /* Neon Yellow text */
            border: 1px solid #FFEB3B;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            text-transform: uppercase;
            transition: background-color 0.2s, color 0.2s;
        }

        .option-button:hover:not(:disabled) {
            background-color: #FFEB3B;
            color: #1a080a; /* Dark text on hover */
        }

        .option-button:disabled {
            cursor: not-allowed;
            opacity: 0.6;
        }

        #answer-input {
            /* Input field is now hidden as we use buttons */
            display: none; 
        }

        #start-button {
            width: 100%;
            padding: 12px;
            font-size: 1.2em;
            background-color: #FF4500; /* Orange-Red/Vermilion for button */
            color: white; 
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-weight: bold;
            transition: background-color 0.2s;
        }

        #start-button:hover:not(:disabled) {
            background-color: #CC3700;
        }
        
        #start-button:disabled {
            background-color: #444;
            color: #888;
            cursor: not-allowed;
        }

        /* Watermark Styling */
        #watermark {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%) rotate(-30deg);
            font-size: 2.5em; 
            font-weight: 900;
            color: rgba(255, 255, 255, 0.05);
            pointer-events: none; 
            z-index: 0;
            white-space: nowrap;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <div id="header">
            <div id="header-main">
                <h1>Plateau Pop Culture & IQ Challenge 🧠🎶</h1>
                <div id="stats">
                    <p>⌛ Time: <span id="timer">60</span>s</p>
                    <p>Score: <span id="score">0</span></p>
                </div>
            </div>
            <div id="creator-ref">Created by Nazifi Adam | Plateau AGH</div>
        </div>

        <div id="clue-area">
            <div id="clue-text">PRESS START TO BEGIN</div>
            <div id="options-container">
                </div>
        </div>

        <input type="text" id="answer-input" style="display: none;"> 
        
        <button id="start-button">Start 60-Second Challenge!</button>

        <div id="watermark">POP CULTURE JOS IQ HUB</div>
    </div>
    
    <script>
        /* --- JAVASCRIPT LOGIC --- */
        const QUIZ_ITEMS = [
            { clue: "The Jos-born Hip-Hop artist known for the song 'African Rapsody'.", answer: "ICE PRINCE", options: ["P-SQUARE", "MI ABAGA", "ICE PRINCE"] },
            { clue: "The Plateau State indigene and first Nigerian female professional golfer.", answer: "CHRISTIE IBUDE", options: ["EVELYN OPUTU", "CHRISTIE IBUDE", "PATIENCE OGBO"] },
            { clue: "The famous local music genre of the Berom people.", answer: "GOLDEY", options: ["ASUSU", "GOLDEY", "TIV BEAT"] },
            { clue: "The major annual Plateau festival that showcases arts, culture, and sports.", answer: "JOS CARNIVAL", options: ["CALABAR CARNIVAL", "JOS CARNIVAL", "EKO FESTIVAL"] },
            { clue: "What is 40% of 200?", answer: "80", options: ["40", "80", "120"] },
            { clue: "Which popular Nollywood actor and director hails from Plateau State?", answer: "KATE HENSHAW", options: ["GENEVIEVE NNAJI", "KATE HENSHAW", "OMOTOLA JALADE"] },
            { clue: "The Plateau State Government promotes this primary tourist attraction: 'Home of _____'.", answer: "PEACE AND TOURISM", options: ["TIN MINING", "PEACE AND TOURISM", "ROCK FORMATION"] },
            { clue: "If a farmer plants 5 rows of maize with 12 seeds per row, how many seeds are planted?", answer: "60", options: ["50", "60", "70"] },
            { clue: "The traditional form of storytelling often accompanied by music in local Plateau communities.", answer: "FOLKLORE", options: ["FOLKLORE", "GOSSIP", "TALES"] },
            { clue: "A Plateau-born comedian famous for his pidgin English skits.", answer: "MC LIVELY", options: ["BASKETMOUTH", "MC LIVELY", "AY"] }
        ];

        const clueDisplay = document.getElementById('clue-text');
        const optionsContainer = document.getElementById('options-container');
        const startButton = document.getElementById('start-button');
        const timerDisplay = document.getElementById('timer');
        const scoreDisplay = document.getElementById('score');

        let score = 0;
        let timeLeft = 60;
        let gameInterval;
        let isGameRunning = false;
        let currentAnswer = "";
        let usedClues = [];

        // Helper function to shuffle an array
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        function getNextClue() {
            if (usedClues.length === QUIZ_ITEMS.length) {
                usedClues = [];
            }
            
            let availableClues = QUIZ_ITEMS.filter(item => !usedClues.includes(item.answer.toUpperCase()));
            const randomIndex = Math.floor(Math.random() * availableClues.length);
            
            const nextItem = availableClues[randomIndex];
            
            currentAnswer = nextItem.answer.toUpperCase();
            usedClues.push(currentAnswer);

            clueDisplay.textContent = `Q: ${nextItem.clue}`;
            
            // Generate and display options
            generateOptions(nextItem.options);
        }

        function generateOptions(options) {
            optionsContainer.innerHTML = ''; // Clear previous options
            
            // Shuffle the options before displaying them
            const shuffledOptions = shuffleArray([...options]); 

            shuffledOptions.forEach(optionText => {
                const button = document.createElement('button');
                button.className = 'option-button';
                button.textContent = optionText.toUpperCase();
                
                // Attach click handler to check the answer
                button.addEventListener('click', () => checkAnswer(button.textContent));
                optionsContainer.appendChild(button);
            });
            // Focus is no longer needed on an input field
        }
        
        function disableOptions(status = true) {
            const buttons = optionsContainer.querySelectorAll('.option-button');
            buttons.forEach(button => {
                button.disabled = status;
            });
        }

        // --- Game Functions ---

        function startGame() {
            if (isGameRunning) return;

            // Reset game
            score = 0;
            timeLeft = 60;
            usedClues = [];
            scoreDisplay.textContent = score;
            timerDisplay.textContent = timeLeft;
            startButton.disabled = true;
            isGameRunning = true;
            
            getNextClue(); // Start with the first clue
            disableOptions(false); // Enable options

            // Start the timer
            gameInterval = setInterval(updateGame, 1000);
        }

        function updateGame() {
            timeLeft--;
            timerDisplay.textContent = timeLeft;

            if (timeLeft <= 0) {
                endGame();
            }
        }

        function endGame() {
            clearInterval(gameInterval);
            isGameRunning = false;
            startButton.disabled = false;
            disableOptions(true); // Disable options at the end
            clueDisplay.textContent = "TIME'S UP! Final Score: " + score;
            
            setTimeout(() => {
                alert(`Time's up! Your final score is ${score}. Created by Nazifi Adam | Plateau AGH. Challenge your friends!`);
            }, 100);
        }

        function checkAnswer(selectedAnswer) {
            if (!isGameRunning) return;

            // Normalize the selected answer
            const typedAnswer = selectedAnswer.trim().toUpperCase();
            
            if (typedAnswer === currentAnswer) {
                // Successful guess!
                score++;
                scoreDisplay.textContent = score;
                
                // Visual feedback (Success flash)
                clueDisplay.style.color = '#FFEB3B'; 
                setTimeout(() => {
                    clueDisplay.style.color = '#FFEB3B';
                }, 100);

                // Move to the next clue
                getNextClue();
            } else {
                 // Incorrect guess feedback (Error flash)
                 clueDisplay.style.color = 'red'; 
                 setTimeout(() => {
                    clueDisplay.style.color = '#FFEB3B';
                 }, 150);
                 
                 // Go to the next clue on failed attempt
                 if (isGameRunning) {
                     getNextClue();
                 }
            }
        }

        // --- Event Listeners and Initialization ---

        startButton.addEventListener('click', startGame);

        // Initial setup - options are disabled until game starts
        disableOptions(true);
    </script>
</body>
</html>
