# typing-hero
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Typing Hero 🎯</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background-color: #f0f4ff;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .game-container {
      text-align: center;
      background: white;
      padding: 30px;
      border-radius: 20px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
      width: 400px;
      position: relative;
    }
    #word-container {
      font-size: 32px;
      margin: 30px 0;
      height: 50px;
      color: #333;
    }
    #input-box {
      width: 80%;
      padding: 10px;
      font-size: 18px;
    }
    #score-board, #timer {
      margin-top: 10px;
      font-size: 18px;
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>Typing Hero 🎯</h1>
    <div id="score-board">Score: <span id="score">0</span></div>
    <div id="timer">Time: <span id="time">60</span>s</div>
    <div id="word-container"></div>
    <input type="text" id="input-box" placeholder="Type here..." autofocus />
  </div>
  <script>
    const words = [
      "friend", "guitar", "drums", "rock", "band", "happy", "laugh", "together", "neighbor",
      "nod", "magic", "guide", "bake", "subject", "science", "math", "reading", "dancing",
      "singing", "strong", "special"
    ];

    let currentWord = '';
    let score = 0;
    let timeLeft = 60;
    let timerInterval;
    let gameStarted = false;

    const wordContainer = document.getElementById('word-container');
    const inputBox = document.getElementById('input-box');
    const scoreDisplay = document.getElementById('score');
    const timeDisplay = document.getElementById('time');

    function getRandomWord() {
      return words[Math.floor(Math.random() * words.length)];
    }

    function setNewWord() {
      currentWord = getRandomWord();
      wordContainer.textContent = currentWord;
    }

    function updateTimer() {
      if (timeLeft > 0) {
        timeLeft--;
        timeDisplay.textContent = timeLeft;
      } else {
        clearInterval(timerInterval);
        wordContainer.textContent = "⏰ Game Over!";
        inputBox.disabled = true;
      }
    }

    function startGame() {
      if (gameStarted) return;
      gameStarted = true;
      setNewWord();
      timeDisplay.textContent = timeLeft;
      timerInterval = setInterval(updateTimer, 1000);
    }

    inputBox.addEventListener('input', () => {
      if (!gameStarted) startGame();
      if (inputBox.value.trim() === currentWord) {
        score++;
        scoreDisplay.textContent = score;
        inputBox.value = '';
        setNewWord();
      }
    });

    // Removed window.onload = startGame to prevent early execution
  </script>
</body>
</html>
