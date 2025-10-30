# practical7_CT11_wt
contains web technology practical 7
<!DOCTYPE html>
<html>
<head>
  <title>Arithmetic Operations</title>
</head>
<body>
  <h2>Arithmetic Operations in JavaScript</h2>
  <script>

    let num1 = parseFloat(prompt("Enter first number:"));
    let num2 = parseFloat(prompt("Enter second number:"));

    
    let sum = num1 + num2;
    let difference = num1 - num2;
    let product = num1 * num2;
    let quotient = num1 / num2;

    
    document.write("<h3>Results:</h3>");
    document.write("Addition: " + sum + "<br>");
    document.write("Subtraction: " + difference + "<br>");
    document.write("Multiplication: " + product + "<br>");
    document.write("Division: " + quotient.toFixed(2));
  </script>
</body>
</html>







<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="pt7b.css">
</head>
<body>
    <div class="calculator">
        <div class="header">
            <h2>Calculator</h2>
        </div>

        <div class="screen">
            <div id="history"></div>
            <div id="result">0</div>
        </div>

        <div class="buttons" id="buttons">
            <button data-action="clear">C</button>
            <button data-action="sign">⌫</button> <!-- Backspace now -->
            <button data-action="percent">%</button>
            <button data-value="/" class="op">÷</button>

            <button data-value="7">7</button>
            <button data-value="8">8</button>
            <button data-value="9">9</button>
            <button data-value="*" class="op">×</button>

            <button data-value="4">4</button>
            <button data-value="5">5</button>
            <button data-value="6">6</button>
            <button data-value="-" class="op">−</button>

            <button data-value="1">1</button>
            <button data-value="2">2</button>
            <button data-value="3">3</button>
            <button data-value="+" class="op">+</button>

            <button data-value="0" class="zero">0</button>
            <button data-value=".">.</button>
            <button data-action="equals" class="eq">=</button>
        </div>

        <div id="joke-box">
            <h3>😂 Random Joke</h3>
            <p id="joke">Click the button to see a joke!</p>
            <button id="joke-btn" style="background-color: red;">Get Random Joke</button>
        </div>
    </div>

    <script src="pt7b.js"></script>
</body>
</html>




const buttons = document.getElementById("buttons");
const result = document.getElementById("result");
const history = document.getElementById("history");

let currentInput = "";
let previousInput = "";
let operator = "";

buttons.addEventListener("click", function (e) {
  const target = e.target;
  const value = target.dataset.value;
  const action = target.dataset.action;

  if (!target.matches("button")) return;

  if (value) {
    currentInput += value;
    result.textContent = currentInput;
  }

  if (action === "clear") {
    currentInput = "";
    previousInput = "";
    operator = "";
    result.textContent = "0";
    history.textContent = "";
  }

  if (target.classList.contains("op")) {
    if (currentInput === "") return;
    operator = value;
    previousInput = currentInput;
    currentInput = "";
    history.textContent = previousInput + " " + operator;
  }

  if (action === "equals") {
    if (!previousInput || !currentInput) return;

    const num1 = parseFloat(previousInput);
    const num2 = parseFloat(currentInput);
    let output = 0;

    switch (operator) {
      case "+": output = num1 + num2; break;
      case "-": output = num1 - num2; break;
      case "*": output = num1 * num2; break;
      case "/": output = num2 !== 0 ? num1 / num2 : "Error"; break;
      default: output = currentInput;
    }

    result.textContent = output;
    history.textContent = `${previousInput} ${operator} ${currentInput} =`;
    currentInput = output.toString();
    previousInput = "";
    operator = "";
  }
});

const swatches = document.querySelectorAll(".swatch");
swatches.forEach((swatch) => {
  swatch.addEventListener("click", () => {
    const color1 = swatch.dataset.p;
    const color2 = swatch.dataset.pf;
    document.body.style.background = `linear-gradient(135deg, ${color1}, ${color2})`;
  });
});

const jokeBtn = document.getElementById("joke-btn");
const jokeText = document.getElementById("joke");

const jokes = [
  "Why do programmers prefer dark mode? Because light attracts bugs!",
  "Why did the function break up with the loop? Because it kept repeating itself!",
  "A SQL query walks into a bar and asks — can I join you?",
  "Why was the JavaScript developer sad? Because they didn’t ‘null’ their feelings!",
  "Debugging: Removing the needles from the haystack of your code!"
];

jokeBtn.addEventListener("click", () => {
  const randomIndex = Math.floor(Math.random() * jokes.length);
  jokeText.textContent = jokes[randomIndex];
});




:root {
    --primary: #06b6d4;
    --accent: #10b981;
    --bg: #0f1724;
    --text: #e6eef8;
}

body {
    margin: 0;
    background: var(--bg);
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    font-family: Arial, sans-serif;
    color: var(--text);
    padding: 20px;
}

.calculator {
    width: 100%;
    max-width: 350px;
    background: rgba(255,255,255,0.05);
    padding: 15px;
    border-radius: 12px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.6);
    animation: slideIn .6s ease forwards;
    transform: translateY(20px);
    opacity: 0;
}

@keyframes slideIn {
    to {
        transform: translateY(0);
        opacity: 1;
    }
}

.header {
    text-align: center;
    margin-bottom: 10px;
}

.screen {
    background: rgba(0,0,0,0.3);
    border-radius: 10px;
    padding: 12px;
    text-align: right;
    margin-bottom: 15px;
    overflow-x: auto;
    scrollbar-width: none;
}

#history {
    font-size: 12px;
    color: #aaa;
}
#result {
    font-size: 28px;
    font-weight: bold;
    word-wrap: break-word;
    white-space: nowrap;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 8px;
}

button {
    padding: 14px;
    border: none;
    border-radius: 8px;
    background: rgba(255,255,255,0.1);
    color: var(--text);
    font-size: 16px;
    cursor: pointer;
    transition: 0.2s;
}
button:hover {
    background: var(--primary);
    color: #fff;
    transform: scale(1.05);
}
button:active {
    transform: scale(0.95);
}
.op {
    background: var(--primary);
    color: #fff;
}
.eq {
    background: var(--accent);
    color: #fff;
}
.zero {
    grid-column: span 2;
}

.palette {
    margin-top: 15px;
    display: flex;
    gap: 8px;
    justify-content: center;
}
.swatch {
    width: 30px;
    height: 30px;
    border-radius: 6px;
    cursor: pointer;
    transition: 0.2s;
}
.swatch:hover {
    transform: scale(1.2);
}

/* Joke Box */
#joke-box {
    margin-top: 20px;
    background: rgba(255,255,255,0.1);
    border-radius: 10px;
    padding: 10px;
    text-align: center;
    animation: fadeIn 1s ease-in-out;
}

#joke-btn {
    margin-top: 8px;
    padding: 10px 14px;
    border: none;
    border-radius: 8px;
    background: var(--primary);
    color: #fff;
    cursor: pointer;
    transition: 0.2s;
}
#joke-btn:hover {
    background: var(--accent);
    transform: scale(1.05);
}
#joke-btn:active {
    transform: scale(0.95);
}

@keyframes fadeIn {
    from {opacity: 0; transform: translateY(10px);}
    to {opacity: 1; transform: translateY(0);}
}

@media (max-width: 480px) {
    .calculator {
        max-width: 100%;
        padding: 10px;
    }
    #result {
        font-size: 22px;
    }
    button {
        padding: 12px;
        font-size: 15px;
    }
}
