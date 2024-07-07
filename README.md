## index.html

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculator</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="calculator">
        <div class="display" id="display">0</div>
        <div class="buttons">
            <button onclick="clearAll()">AC</button>
            <button onclick="clearLast()">Del</button>
            <button class="double-width" onclick="calculate()">=</button>
            <button onclick="appendNumber('1')">1</button>
            <button onclick="appendNumber('2')">2</button>
            <button onclick="appendNumber('3')">3</button>
            <button onclick="operate('add')">+</button>
            <button onclick="appendNumber('4')">4</button>
            <button onclick="appendNumber('5')">5</button>
            <button onclick="appendNumber('6')">6</button>
            <button onclick="operate('subtract')">-</button>
            <button onclick="appendNumber('7')">7</button>
            <button onclick="appendNumber('8')">8</button>
            <button onclick="appendNumber('9')">9</button>
            <button onclick="operate('multiply')">*</button>
            <button onclick="operate('divide')">/</button>
            <button onclick="appendNumber('0')">0</button>
            <button onclick="appendNumber('.')">.</button>
            
            
        </div>
    </div>
    
    <script src="script.js"></script>
</body>
</html>
```

## script.js

```
let currentInput = '0';
let operator = null;
let previousInput = null;
let shouldResetDisplay = false;

function clearAll() {
    currentInput = '0';
    operator = null;
    previousInput = null;
    shouldResetDisplay = false;
    updateDisplay();
}

function clearLast() {
    currentInput = currentInput.slice(0, -1);
    if (currentInput === '') {
        currentInput = '0';
    }
    updateDisplay();
}

function appendNumber(number) {
    if (shouldResetDisplay) {
        currentInput = number;
        shouldResetDisplay = false;
    } else {
        currentInput = currentInput === '0' ? number : currentInput + number;
    }
    updateDisplay();
}

function operate(op) {
    if (operator !== null) {
        calculate();
    }
    previousInput = currentInput;
    operator = op;
    shouldResetDisplay = true;
    updateDisplay();
}

function calculate() {
    let result;
    const prev = parseFloat(previousInput);
    const current = parseFloat(currentInput);

    if (isNaN(prev) || isNaN(current)) return;

    switch (operator) {
        case 'add':
            result = prev + current;
            break;
        case 'subtract':
            result = prev - current;
            break;
        case 'multiply':
            result = prev * current;
            break;
        case 'divide':
            result = prev / current;
            break;
        default:
            return;
    }

    currentInput = result.toString();
    operator = null;
    previousInput = null;
    shouldResetDisplay = true;
    updateDisplay();
}

function updateDisplay() {
    const display = document.getElementById('display');
    if (operator && !shouldResetDisplay) {
        display.innerText = `${previousInput} ${getOperatorSymbol(operator)} ${currentInput}`;
    } else {
        display.innerText = currentInput;
    }
}

function getOperatorSymbol(op) {
    switch (op) {
        case 'add':
            return '+';
        case 'subtract':
            return '-';
        case 'multiply':
            return '*';
        case 'divide':
            return '/';
        default:
            return '';
    }
}
```

styles.css

```
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    margin: 0;
    background: url('your-background-image.jpg') no-repeat center center fixed;
    background-size: cover;
    position: relative;
}

body::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5); /* Adjust the opacity as needed */
    z-index: 0;
}

.calculator {
    border: 1px solid #ccc;
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
    width: 320px;
    background-color: #fff;
    position: relative;
    z-index: 1;
}

.display {
    background-color: #222;
    color: #fff;
    font-size: 2em;
    text-align: right;
    padding: 20px;
    border-top-left-radius: 10px;
    border-top-right-radius: 10px;
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
}

button {
    padding: 20px;
    font-size: 1.5em;
    border: 1px solid #ccc;
    background-color: #f9f9f9;
    cursor: pointer;
    z-index: 1;
}

button:hover {
    background-color: #eaeaea;
}

button:active {
    background-color: #ccc;
}

button:nth-child(4n) {
    background-color: #ff9500;
    color: #fff;
}

button:nth-child(4n):hover {
    background-color: #e18b00;
}

button:nth-child(4n):active {
    background-color: #c77c00;
}

.buttons .double-width{
    flex-grow: 2;;
}
```
