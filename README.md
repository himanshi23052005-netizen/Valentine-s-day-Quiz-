<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Valentine's Day Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background: linear-gradient(to bottom, #ffcccc, #ff9999);
            margin: 0;
            padding: 20px;
        }
        .question-container {
            background: rgba(255, 255, 255, 0.8);
            padding: 20px;
            border-radius: 10px;
            margin: 20px auto;
            max-width: 600px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .question1 { background: linear-gradient(to bottom, #ffcccc, #ff6666); }
        .question2 { background: linear-gradient(to bottom, #ccffcc, #66ff66); }
        .question3 { background: linear-gradient(to bottom, #ccccff, #6666ff); }
        .question4 { background: linear-gradient(to bottom, #ffffcc, #ffff66); }
        .options {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
        }
        .option {
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background 0.3s;
        }
        .question1 .option { background: #ff9999; }
        .question1 .option:hover { background: #ff6666; }
        .question2 .option { background: #99ff99; }
        .question2 .option:hover { background: #66ff66; }
        .question3 .option { background: #9999ff; }
        .question3 .option:hover { background: #6666ff; }
        .question4 .option { background: #ffff99; }
        .question4 .option:hover { background: #ffff66; }
        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 20px rgba(0,0,0,0.5);
            z-index: 1000;
        }
        .fireworks {
            position: relative;
            overflow: hidden;
        }
        .firework {
            position: absolute;
            width: 10px;
            height: 10px;
            background: red;
            border-radius: 50%;
            animation: explode 1s ease-out infinite;
        }
        @keyframes explode {
            0% { transform: scale(0); opacity: 1; }
            100% { transform: scale(10); opacity: 0; }
        }
        .hearts {
            font-size: 50px;
        }
        .laughing {
            font-size: 30px;
        }
    </style>
</head>
<body>
    <div id="quiz-container">
        <div class="question-container question1" id="q1">
            <h2>When did we first meet?</h2>
            <div class="options">
                <button class="option" onclick="checkAnswer(1, '13 Feb')">13 Feb</button>
                <button class="option" onclick="checkAnswer(1, '8 July')">8 July</button>
                <button class="option" onclick="checkAnswer(1, '18 March')">18 March</button>
            </div>
        </div>
        <div class="question-container question2" id="q2" style="display: none;">
            <h2>What did you buy me first?</h2>
            <div class="options">
                <button class="option" onclick="checkAnswer(2, 'Teddy')">Teddy</button>
                <button class="option" onclick="checkAnswer(2, 'Chocolate')">Chocolate</button>
                <button class="option" onclick="checkAnswer(2, 'Cake')">Cake</button>
            </div>
        </div>
        <div class="question-container question3" id="q3" style="display: none;">
            <h2>What do I love the most?</h2>
            <div class="options">
                <button class="option" onclick="checkAnswer(3, 'Gold')">Gold</button>
                <button class="option" onclick="checkAnswer(3, 'Chocolate')">Chocolate</button>
                <button class="option" onclick="checkAnswer(3, 'Kurkure')">Kurkure</button>
            </div>
        </div>
        <div class="question-container question4" id="q4" style="display: none;">
            <h2>Will you be my Valentine?</h2>
            <div class="options">
                <button class="option" onclick="checkAnswer(4, 'Yes')">Yes</button>
                <button class="option" onclick="checkAnswer(4, 'No')">No</button>
            </div>
        </div>
    </div>

    <div id="popup" class="popup">
        <p id="popup-message"></p>
        <button onclick="closePopup()">OK</button>
    </div>

    <div id="final-popup" class="popup">
        <div class="fireworks" id="fireworks-container">
            <div class="hearts">❤️❤️❤️</div>
            <p>From now you are my Valentine!</p>
            <div class="firework" style="top: 20%; left: 20%;"></div>
            <div class="firework" style="top: 30%; left: 70%;"></div>
            <div class="firework" style="top: 60%; left: 50%;"></div>
        </div>
        <button onclick="endQuiz()">Finish</button>
    </div>

    <div id="end-popup" class="popup">
        <h2>Buy me Kurkure!</h2>
        <div class="laughing">😂😂😂😂😂</div>
        <button onclick="closeEndPopup()">OK</button>
    </div>

    <script>
        let currentQuestion = 1;
        const answers = {
            1: '18 March',
            2: 'Teddy',
            3: 'Kurkure',
            4: 'Yes'
        };

        function checkAnswer(question, selected) {
            if (selected === answers[question]) {
                showPopup('❤️ Correct! ❤️');
                if (question === 4) {
                    setTimeout(() => {
                        document.getElementById('final-popup').style.display = 'block';
                    }, 1000);
                } else {
                    nextQuestion();
                }
            } else {
                showPopup('You better see me after the quiz!');
            }
        }

        function showPopup(message) {
            document.getElementById('popup-message').textContent = message;
            document.getElementById('popup').style.display = 'block';
        }

        function closePopup() {
            document.getElementById('popup').style.display = 'none';
        }

        function nextQuestion() {
            document.getElementById('q' + currentQuestion).style.display = 'none';
            currentQuestion++;
            if (currentQuestion <= 4) {
                document.getElementById('q' + currentQuestion).style.display = 'block';
            }
        }

        function endQuiz() {
            document.getElementById('final-popup').style.display = 'none';
            document.getElementById('end-popup').style.display = 'block';
        }

        function closeEndPopup() {
            document.getElementById('end-popup').style.display = 'none';
        }
    </script>
</body>
</html>
