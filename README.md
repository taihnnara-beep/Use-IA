<!DOCTYPE html><html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quiz sobre Inteligência Artificial</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f5f5f5;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .quiz-container {
      background: #fff;
      padding: 20px;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 400px;
      text-align: center;
    }
    h1 {
      font-size: 22px;
      margin-bottom: 15px;
    }
    .question {
      margin-bottom: 15px;
      font-weight: bold;
    }
    .options button {
      display: block;
      width: 100%;
      padding: 10px;
      margin: 8px 0;
      border: none;
      border-radius: 8px;
      background: #007bff;
      color: #fff;
      cursor: pointer;
      transition: background 0.3s;
    }
    .options button:hover {
      background: #0056b3;
    }
    .feedback {
      margin-top: 10px;
      font-size: 16px;
      font-weight: bold;
    }
    .correct {
      color: green;
    }
    .wrong {
      color: red;
    }
    .next-btn {
      margin-top: 15px;
      padding: 8px 15px;
      background: #28a745;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      display: none;
    }
    .result {
      font-size: 18px;
      font-weight: bold;
      margin-top: 15px;
    }
    .hidden {
      display: none;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <h1>Quiz: Consciência sobre o uso da IA</h1>
    <div id="quiz"></div>
    <div id="feedback" class="feedback hidden"></div>
    <button id="nextBtn" class="next-btn" onclick="nextQuestion()">Próxima</button>
    <div id="result" class="result hidden"></div>
  </div>  <script>
    const quizData = [
      {
        question: "A Inteligência Artificial deve ser usada de forma:",
        options: ["Sem limites", "Ética e responsável", "Para substituir humanos em tudo"],
        correct: 1,
        explanation: "O uso da IA deve ser sempre ético e responsável, para não causar danos à sociedade."
      },
      {
        question: "Qual é um risco do uso inadequado da IA?",
        options: ["Viés e discriminação", "Mais criatividade", "Mais diversidade cultural"],
        correct: 0,
        explanation: "Um dos riscos é a reprodução de vieses e discriminações já presentes nos dados."
      },
      {
        question: "O que significa usar IA com responsabilidade?",
        options: ["Respeitar privacidade e transparência", "Ocultar informações", "Não verificar fontes"],
        correct: 0,
        explanation: "Usar IA com responsabilidade é garantir privacidade, segurança e transparência."
      },
      {
        question: "Quem deve ser responsável pelo uso da IA?",
        options: ["Somente as máquinas", "As pessoas que a utilizam e desenvolvem", "Ninguém"],
        correct: 1,
        explanation: "A responsabilidade pelo uso da IA é das pessoas que a criam e utilizam."
      }
    ];

    let currentQuestion = 0;
    let score = 0;

    const quizEl = document.getElementById("quiz");
    const feedbackEl = document.getElementById("feedback");
    const resultEl = document.getElementById("result");
    const nextBtn = document.getElementById("nextBtn");

    function loadQuestion() {
      if (currentQuestion < quizData.length) {
        const q = quizData[currentQuestion];
        quizEl.innerHTML = `
          <div class="question">${q.question}</div>
          <div class="options">
            ${q.options.map((opt, i) => `<button onclick="checkAnswer(${i})">${opt}</button>`).join('')}
          </div>
        `;
        feedbackEl.classList.add("hidden");
        nextBtn.style.display = "none";
      } else {
        showResult();
      }
    }

    function checkAnswer(answer) {
      const q = quizData[currentQuestion];
      if (answer === q.correct) {
        score++;
        feedbackEl.textContent = "Correto! " + q.explanation;
        feedbackEl.className = "feedback correct";
      } else {
        feedbackEl.textContent = "Errado! " + q.explanation;
        feedbackEl.className = "feedback wrong";
      }
      feedbackEl.classList.remove("hidden");
      nextBtn.style.display = "inline-block";
      disableButtons();
    }

    function disableButtons() {
      const buttons = quizEl.querySelectorAll("button");
      buttons.forEach(btn => btn.disabled = true);
    }

    function nextQuestion() {
      currentQuestion++;
      loadQuestion();
    }

    function showResult() {
      quizEl.innerHTML = "";
      feedbackEl.classList.add("hidden");
      nextBtn.style.display = "none";
      resultEl.classList.remove("hidden");
      resultEl.textContent = `Você acertou ${score} de ${quizData.length} perguntas!`; 
    }

    loadQuestion();
  </script></body>
</html>
