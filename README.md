<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Math Game</title>
<style>
body {
  font-family: Arial, sans-serif;
  background-color: #FFB6C1; 
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center; 
  align-items: center;
  height: 100vh; 
}

.container {
  max-width: 800px; /* Change the maximum width to your desired size */
  width: 80%; /* Adjust the width as needed */
  padding: 20px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  text-align: center;
}

h1 {
  color: #333;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
}

input[type="number"] {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  margin-top: 10px;
}

button:hover {
  background-color: #45a049;
}

#question {
  margin-top: 20px;
  font-weight: bold;
  display: none;
  font-size: 24px; 
}

#result {
  margin-top: 20px;
  font-weight: bold;
  display: none;
}

#answer {
  display: none;
}

#submitBtn {
  display: none;
}

#continueBtn {
  display: none;
  margin-top: 20px;
}

#leaveBtn {
  display: none;
  margin-top: 20px;
}

#points {
  display: none;
}
</style>
</head>
<body>
<div class="container">
<h1>Math Game</h1>
<label for="age" id="ageLabel">Enter your age:</label>
<input type="number" id="age" min="1">
<button onclick="startGame()" id="startBtn">Start</button>
<div id="question"></div>
<input type="text" id="answer">
<button id="submitBtn" onclick="checkAnswer()">Submit</button>
<div id="result"></div>
<button id="continueBtn" onclick="continueGame()">Continue</button>
<button id="leaveBtn" onclick="leaveGame()">Leave</button>
<p id="points">Points: <span id="pointsCount">0</span></p>
</div>
<script>
var age;
var gameTitle; 
var questionDiv;
var answerInput;
var submitBtn;
var resultDiv;
var continueBtn;
var leaveBtn;
var startBtn; 
var pointsCount = 0;

function startGame() {
  age = parseInt(document.getElementById("age").value);
  gameTitle = document.querySelector("h1"); 
  questionDiv = document.getElementById("question");
  answerInput = document.getElementById("answer");
  submitBtn = document.getElementById("submitBtn");
  resultDiv = document.getElementById("result");
  continueBtn = document.getElementById("continueBtn");
  leaveBtn = document.getElementById("leaveBtn");
  startBtn = document.getElementById("startBtn"); 
  gameTitle.style.display = "none"; 
  document.getElementById("points").style.display = "block"; 
  document.getElementById("ageLabel").style.display = "none"; 
  document.getElementById("age").style.display = "none"; 
  questionDiv.style.display = "block"; 
  startBtn.style.display = "none"; 
  askQuestion(); 
}

function askQuestion() {
  var num1, num2, operator;
  
  if (age >= 1 && age <= 13) {
    num1 = Math.floor(Math.random() * 10) + 1;
    num2 = Math.floor(Math.random() * 10) + 1;
    operator = Math.random() < 0.5 ? "+" : "-";
  } else if (age >= 14 && age <= 18) {
    num1 = Math.floor(Math.random() * 20) + 1;
    num2 = Math.floor(Math.random() * 20) + 1;
    operator = Math.random() < 0.5 ? "*" : "/";
  } else {
    num1 = Math.floor(Math.random() * 50) + 1;
    num2 = Math.floor(Math.random() * 50) + 1;
    operator = Math.random() < 0.5 ? "+" : "-";
  }
  
  questionDiv.innerText = num1 + " " + operator + " " + num2 + " = ?";
  answerInput.style.display = "inline";
  submitBtn.style.display = "inline";
  continueBtn.style.display = "none";
  leaveBtn.style.display = "none";
  resultDiv.style.display = "none";
}

function checkAnswer() {
  var answer = parseInt(document.getElementById("answer").value);
  var question = questionDiv.innerText;
  var correctAnswer;
  if (question.includes("+")) {
    var nums = question.split("+");
    correctAnswer = parseInt(nums[0]) + parseInt(nums[1]);
  } else if (question.includes("-")) {
    var nums = question.split("-");
    correctAnswer = parseInt(nums[0]) - parseInt(nums[1]);
  } else if (question.includes("*")) {
    var nums = question.split("*");
    correctAnswer = parseInt(nums[0]) * parseInt(nums[1]);
  } else if (question.includes("/")) {
    var nums = question.split("/");
    correctAnswer = parseInt(nums[0]) / parseInt(nums[1]);
  }
  if (answer === correctAnswer) {
    resultDiv.innerText = "Correct!";
    resultDiv.style.color = "green";
    pointsCount++;
    document.getElementById("pointsCount").innerText = pointsCount; 
  } else {
    resultDiv.innerText = "Incorrect. The correct answer is " + correctAnswer;
    resultDiv.style.color = "red";
  }
  resultDiv.style.display = "block";
  continueBtn.style.display = "inline";
  leaveBtn.style.display = "inline";
}

function continueGame() {
  answerInput.value = "";
  answerInput.focus(); 
  askQuestion();
}

function leaveGame() {
  questionDiv.style.display = "none";
  answerInput.style.display = "none";
  submitBtn.style.display = "none";
  resultDiv.style.display = "none";
  continueBtn.style.display = "none";
  leaveBtn.style.display = "none";
  gameTitle.style.display = "block"; 
}
</script>
</body>
</html>
