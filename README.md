<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Hauptstadt-Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 20px;
        }
        button {
            margin: 5px;
            padding: 10px 20px;
            font-size: 16px;
        }
        #result {
            font-weight: bold;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Rate die Hauptstadt!</h1>
    <p id="question">Frage wird hier angezeigt...</p>
    <div id="answers"></div>
    <p id="result"></p>
    <button onclick="nextQuestion()">Nächste Frage</button>

    <script>
        const quiz = [
            {
                question: "Welche Hauptstadt liegt in Deutschland?",
                answers: ["Wien", "Berlin", "Bern"],
                correct: 1
            },
            {
                question: "Welche Hauptstadt liegt in Frankreich?",
                answers: ["Paris", "Madrid", "Rom"],
                correct: 0
            },
            {
                question: "Welche Hauptstadt gehört zu Australien?",
                answers: ["Sydney", "Canberra", "Melbourne"],
                correct: 1
            },
            {
                question: "Welche Hauptstadt liegt in Kanada?",
                answers: ["Toronto", "Vancouver", "Ottawa"],
                correct: 2
            },
            {
                question: "Welche Hauptstadt gehört zu Italien?",
                answers: ["Neapel", "Rom", "Mailand"],
                correct: 1
            },
            {
                question: "Welche Hauptstadt liegt in Japan?",
                answers: ["Peking", "Seoul", "Tokio"],
                correct: 2
            },
            {
                question: "Welche Hauptstadt gehört zu Russland?",
                answers: ["Sankt Petersburg", "Moskau", "Kiew"],
                correct: 1
            },
            {
                question: "Welche Hauptstadt liegt in Brasilien?",
                answers: ["Brasília", "Rio de Janeiro", "São Paulo"],
                correct: 0
            },
            {
                question: "Welche Hauptstadt gehört zu Indien?",
                answers: ["Mumbai", "Neu-Delhi", "Kalkutta"],
                correct: 1
            },
            {
                question: "Welche Hauptstadt liegt in der Schweiz?",
                answers: ["Zürich", "Bern", "Genf"],
                correct: 1
            }
        ];

        let currentQuestion = 0;
        let score = 0;

        function loadQuestion() {
            const questionElement = document.getElementById("question");
            const answersElement = document.getElementById("answers");
            const resultElement = document.getElementById("result");

            // Reset previous results
            resultElement.textContent = "";

            // Load current question
            const question = quiz[currentQuestion];
            questionElement.textContent = question.question;

            // Load answers
            answersElement.innerHTML = "";
            question.answers.forEach((answer, index) => {
                const button = document.createElement("button");
                button.textContent = answer;
                button.onclick = () => checkAnswer(index);
                answersElement.appendChild(button);
            });
        }

        function checkAnswer(selected) {
            const resultElement = document.getElementById("result");
            const question = quiz[currentQuestion];

            if (selected === question.correct) {
                resultElement.textContent = "Richtig!";
                score++;
            } else {
                resultElement.textContent = `Falsch! Die richtige Antwort war: ${question.answers[question.correct]}`;
            }
        }

        function nextQuestion() {
            if (currentQuestion < quiz.length - 1) {
                currentQuestion++;
                loadQuestion();
            } else {
                document.getElementById("question").textContent = `Quiz beendet! Dein Ergebnis: ${score}/${quiz.length}`;
                document.getElementById("answers").innerHTML = "";
                document.getElementById("result").textContent = "";
            }
        }

        // Load the first question
        loadQuestion();
    </script>
</body>
</html>
