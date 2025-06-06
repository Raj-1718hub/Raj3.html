<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Responsive Quiz & API</title>
  <style>
    * { box-sizing: border-box; }

    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background: #f2f2f2;
      color: #333;
    }

    header {
      background-color: #4CAF50;
      color: white;
      text-align: center;
      padding: 1rem;
    }

    .container {
      max-width: 800px;
      margin: 2rem auto;
      padding: 1rem;
      background: white;
      border-radius: 8px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    h2 {
      margin-bottom: 0.5rem;
    }

    .quiz-question {
      margin-bottom: 1.5rem;
    }

    .quiz-question p {
      font-weight: bold;
    }

    .quiz-question label {
      display: block;
      margin: 0.3rem 0;
    }

    button {
      background-color: #007BFF;
      color: white;
      border: none;
      padding: 0.6rem 1.2rem;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1rem;
    }

    button:hover {
      background-color: #0056b3;
    }

    .result, .joke-box {
      margin-top: 1rem;
      padding: 1rem;
      background-color: #e8f5e9;
      border-left: 4px solid #4CAF50;
      border-radius: 5px;
    }

    @media (max-width: 768px) {
      header h1 {
        font-size: 1.5rem;
      }

      .container {
        margin: 1rem;
        padding: 1rem;
      }

      button {
        width: 100%;
        margin-top: 0.5rem;
      }
    }

    @media (max-width: 480px) {
      .quiz-question label {
        font-size: 0.9rem;
      }
    }
  </style>
</head>
<body>

  <header>
    <h1>Responsive Quiz & Joke Fetcher</h1>
    <p>Test your knowledge and get a laugh!</p>
  </header>

  <div class="container">
    <section id="quiz-section">
      <h2>Quick Quiz</h2>
      <div class="quiz-question">
        <p>1. What is the capital of France?</p>
        <label><input type="radio" name="q1" value="Paris"> Paris</label>
        <label><input type="radio" name="q1" value="London"> London</label>
        <label><input type="radio" name="q1" value="Berlin"> Berlin</label>
      </div>

      <div class="quiz-question">
        <p>2. Which planet is known as the Red Planet?</p>
        <label><input type="radio" name="q2" value="Mars"> Mars</label>
        <label><input type="radio" name="q2" value="Jupiter"> Jupiter</label>
        <label><input type="radio" name="q2" value="Saturn"> Saturn</label>
      </div>

      <div class="quiz-question">
        <p>3. Who wrote 'Romeo and Juliet'?</p>
        <label><input type="radio" name="q3" value="Shakespeare"> William Shakespeare</label>
        <label><input type="radio" name="q3" value="Dickens"> Charles Dickens</label>
        <label><input type="radio" name="q3" value="Hemingway"> Ernest Hemingway</label>
      </div>

      <button onclick="checkAnswers()">Submit Answers</button>
      <div class="result" id="quiz-result"></div>
    </section>

    <hr style="margin: 2rem 0;">

    <section id="api-section">
      <h2>Get a Random Joke</h2>
      <button onclick="fetchJoke()">Show Joke</button>
      <div class="joke-box" id="joke-box">Click the button to load a joke.</div>
    </section>
  </div>

  <script>
    function checkAnswers() {
      const q1 = document.querySelector('input[name="q1"]:checked');
      const q2 = document.querySelector('input[name="q2"]:checked');
      const q3 = document.querySelector('input[name="q3"]:checked');

      let score = 0;
      if (q1 && q1.value === "Paris") score++;
      if (q2 && q2.value === "Mars") score++;
      if (q3 && q3.value === "Shakespeare") score++;

      const resultBox = document.getElementById("quiz-result");
      resultBox.textContent = `You scored ${score} out of 3.`;
    }

    async function fetchJoke() {
      const jokeBox = document.getElementById("joke-box");
      jokeBox.textContent = "Loading...";
      try {
        const response = await fetch("https://official-joke-api.appspot.com/random_joke");
        const data = await response.json();
        jokeBox.innerHTML = `<strong>${data.setup}</strong><br>${data.punchline}`;
      } catch (error) {
        jokeBox.textContent = "Oops! Couldn't load a joke.";
      }
    }
  </script>

</body>
</html>