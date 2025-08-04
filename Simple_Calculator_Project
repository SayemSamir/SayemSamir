<!DOCTYPE html>
<html>
<head>
    <title>AI Core Calculator</title>
    <link rel="stylesheet" href="style.css">
    <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;500;700&family=Roboto+Mono:wght@400;500&display=swap" rel="stylesheet">
    <style>
        :root {
    --bg-dark: #1a1a2e; /* Deep dark background */
    --bg-medium: #1f4068; /* Slightly lighter dark blue */
    --accent-blue: #16c79a; /* Vibrant AI-like blue/green */
    --accent-purple: #4c4c8d; /* A complementary purple */
    --text-primary: #e0e0e0; /* Light grey for general text */
    --text-secondary: rgba(224, 224, 224, 0.7); /* Faded text */

    --button-bg-default: rgba(255, 255, 255, 0.08); /* More subtle transparent */
    --button-hover-default: rgba(255, 255, 255, 0.15);
    --button-active-default: rgba(255, 255, 255, 0.25);

    --operator-color: var(--accent-blue);
    --equal-color: #2ecc71; /* Green for success */
    --clear-color: #e74c3c; /* Red for destructive action */
    --scientific-color: var(--accent-purple);
    --utility-color: var(--bg-medium);
    --backspace-color: #7f8c8d;

    --glow-strength: 0 0 10px;
}

body {
    font-family: 'Roboto Mono', monospace; /* Default body font for code-like feel */
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: linear-gradient(to bottom right, var(--bg-dark), var(--bg-medium));
    margin: 0;
    overflow: hidden; /* Prevent unwanted scrollbars */
    perspective: 1000px; /* For 3D transforms */
    position: relative; /* For AI background elements */
    color: var(--text-primary);
}

/* AI Background Grid */
.ai-background-grid {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-image: 
        linear-gradient(to right, rgba(255,255,255,0.05) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255,255,255,0.05) 1px, transparent 1px);
    background-size: 25px 25px; /* Size of the grid cells */
    opacity: 0.1;
    z-index: 0; /* Behind calculator */
    animation: fadeIn 2s ease-out forwards;
}

/* AI Scan Line */
.ai-scan-line {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 3px;
    background: linear-gradient(to right, transparent, var(--accent-blue), transparent);
    box-shadow: 0 0 15px var(--accent-blue);
    opacity: 0.5;
    animation: scanLine 8s infinite linear;
    z-index: 1; /* Above grid, below calculator */
}

@keyframes scanLine {
    0% { transform: translateY(-100%); opacity: 0.5; }
    10% { opacity: 1; }
    90% { opacity: 1; }
    100% { transform: translateY(100vh); opacity: 0.5; }
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

.calculator-container {
    position: relative;
    z-index: 2; /* Ensure calculator is on top */
}

.calculator {
    width: 350px;
    background: rgba(0, 0, 0, 0.6); /* Darker, more solid background */
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 10px 25px rgba(0, 0, 0, 0.7), inset 0 0 10px rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    display: flex;
    flex-direction: column;
    gap: 15px;
    transform: rotateX(2deg) rotateY(-2deg); /* Subtle initial tilt */
    transition: transform 0.5s ease-out;
    position: relative; /* For inner glow */
}

.calculator::before {
    content: '';
    position: absolute;
    top: -5px;
    left: -5px;
    right: -5px;
    bottom: -5px;
    border-radius: 15px;
    background: linear-gradient(45deg, var(--accent-blue) 0%, var(--accent-purple) 100%);
    filter: blur(20px);
    opacity: 0.2; /* Subtle outer glow */
    z-index: -1;
    animation: pulseGlow 5s infinite alternate;
}

@keyframes pulseGlow {
    0% { opacity: 0.15; transform: scale(1); }
    100% { opacity: 0.25; transform: scale(1.02); }
}

.calculator:hover {
    transform: rotateX(0deg) rotateY(0deg);
}

.display-area {
    background: rgba(0, 0, 0, 0.8); /* Very dark for display */
    border-radius: 8px;
    padding: 10px;
    margin-bottom: 10px;
    min-height: 90px;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: flex-end;
    box-shadow: inset 0 0 15px rgba(0,0,0,0.7);
    border: 1px solid rgba(255, 255, 255, 0.08);
    position: relative;
    overflow: hidden;
}

.display-area::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: radial-gradient(circle at 50% 50%, var(--accent-blue) 0%, transparent 70%);
    opacity: 0.1;
    filter: blur(10px);
    z-index: 0;
}

#history-display {
    font-family: 'Roboto Mono', monospace; /* Consistent mono font */
    color: rgba(22, 199, 154, 0.7); /* Faded accent color */
    font-size: 14px;
    min-height: 20px;
    text-align: right;
    width: 100%;
    overflow-x: auto;
    white-space: nowrap;
    z-index: 1;
}

#display {
    font-family: 'Orbitron', sans-serif; /* Main digital font for impact */
    width: 100%;
    background: transparent;
    border: none;
    color: var(--accent-blue); /* Strong accent for main display */
    font-size: 42px;
    text-align: right;
    padding: 0;
    margin-top: 5px;
    outline: none;
    box-sizing: border-box;
    z-index: 1;
    text-shadow: var(--glow-strength) var(--accent-blue); /* Stronger glow */
}

.buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 10px;
}

button {
    padding: 18px;
    font-size: 20px;
    cursor: pointer;
    border: 1px solid rgba(255, 255, 255, 0.05); /* Subtle border */
    border-radius: 6px; /* Sharper edges */
    background-color: var(--button-bg-default);
    color: var(--text-primary);
    transition: background-color 0.2s ease, transform 0.1s ease, box-shadow 0.2s ease, color 0.2s ease;
    box-shadow: 0 3px 8px rgba(0,0,0,0.5); /* Deeper shadow */
    font-weight: 500;
    text-shadow: 0 0 3px rgba(0,0,0,0.5); /* Subtle text shadow */
    position: relative; /* For button glow */
    overflow: hidden; /* For button ripple effect if added */
}

/* Button glow effect on hover */
button::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background: radial-gradient(circle at center, rgba(255,255,255,0.2) 0%, transparent 70%);
    opacity: 0;
    transition: opacity 0.3s ease;
    z-index: 0;
}

button:hover::before {
    opacity: 1;
}

button:hover {
    background-color: var(--button-hover-default);
    transform: translateY(-2px);
    box-shadow: 0 5px 12px rgba(0,0,0,0.6);
    color: var(--accent-blue); /* Text changes color on hover */
    text-shadow: var(--glow-strength) var(--accent-blue);
}

button:active {
    transform: translateY(0);
    box-shadow: 0 1px 4px rgba(0,0,0,0.6);
    background-color: var(--button-active-default);
}

/* Specific button styles with AI-inspired colors */
button.operator {
    background-color: var(--operator-color);
    color: var(--bg-dark); /* Dark text on vibrant button */
    font-weight: 700;
    text-shadow: none; /* No glow on operator text itself */
}
button.operator:hover {
    background-color: color-mix(in srgb, var(--operator-color) 90%, white);
    color: white; /* White text on hover */
    text-shadow: var(--glow-strength) var(--operator-color);
}
button.operator:active {
    background-color: color-mix(in srgb, var(--operator-color) 80%, black);
}


button.clear {
    background-color: var(--clear-color);
    color: var(--bg-dark);
    font-weight: 700;
    text-shadow: none;
}
button.clear:hover {
    background-color: color-mix(in srgb, var(--clear-color) 90%, white);
    color: white;
    text-shadow: var(--glow-strength) var(--clear-color);
}
button.clear:active {
    background-color: color-mix(in srgb, var(--clear-color) 80%, black);
}

button.equal {
    background-color: var(--equal-color);
    grid-column: span 2;
    font-size: 24px;
    font-weight: 700;
    color: var(--bg-dark);
    text-shadow: none;
}
button.equal:hover {
    background-color: color-mix(in srgb, var(--equal-color) 90%, white);
    color: white;
    text-shadow: var(--glow-strength) var(--equal-color);
}
button.equal:active {
    background-color: color-mix(in srgb, var(--equal-color) 80%, black);
}

button.scientific {
    background-color: var(--scientific-color);
    color: var(--text-primary);
    font-size: 18px;
    text-shadow: none;
}
button.scientific:hover {
    background-color: color-mix(in srgb, var(--scientific-color) 90%, white);
    color: var(--accent-blue);
    text-shadow: var(--glow-strength) var(--accent-blue);
}
button.scientific:active {
    background-color: color-mix(in srgb, var(--scientific-color) 80%, black);
}

button.utility {
    background-color: var(--utility-color);
    color: var(--text-primary);
    font-size: 18px;
    font-weight: 500;
    text-shadow: none;
}
button.utility:hover {
    background-color: color-mix(in srgb, var(--utility-color) 90%, white);
    color: var(--accent-blue);
    text-shadow: var(--glow-strength) var(--accent-blue);
}
button.utility:active {
    background-color: color-mix(in
    </style>
</head>
<body>
    <div class="calculator-container">
        <div class="ai-background-grid"></div> 
        <div class="ai-scan-line"></div> <div class="calculator">
            <div class="display-area">
                <div id="history-display"></div>
                <input type="text" id="display" disabled value="0">
            </div>
            <div class="buttons">
                <button class="utility" onclick="toggleSign()">+/-</button>
                <button class="utility" onclick="toggleAngleUnit()">RAD</button>
                <button class="utility" onclick="clearEntry()">CE</button>
                <button class="clear" onclick="clearAll()">C</button>

                <button class="scientific" onclick="appendToDisplay('Math.sin(')">sin</button>
                <button class="scientific" onclick="appendToDisplay('Math.cos(')">cos</button>
                <button class="scientific" onclick="appendToDisplay('Math.tan(')">tan</button>
                <button class="operator" onclick="appendToDisplay('/')">÷</button>

                <button class="scientific" onclick="appendToDisplay('Math.sqrt(')">√</button>
                <button class="scientific" onclick="appendToDisplay('Math.pow(')">x<sup>y</sup></button>
                <button class="scientific" onclick="appendToDisplay('Math.log(')">log</button>
                <button class="operator" onclick="appendToDisplay('*')">×</button>
                
                <button class="scientific" onclick="appendToDisplay('Math.PI')">π</button>
                <button class="scientific" onclick="appendToDisplay('Math.E')">e</button>
                <button class="scientific" onclick="appendToDisplay('(')">(</button>
                <button class="operator" onclick="appendToDisplay('-')">-</button>

                <button onclick="appendToDisplay('7')">7</button>
                <button onclick="appendToDisplay('8')">8</button>
                <button onclick="appendToDisplay('9')">9</button>
                <button class="operator" onclick="appendToDisplay('+')">+</button>

                <button onclick="appendToDisplay('4')">4</button>
                <button onclick="appendToDisplay('5')">5</button>
                <button onclick="appendToDisplay('6')">6</button>
                <button class="backspace" onclick="backspace()">DEL</button>

                <button onclick="appendToDisplay('1')">1</button>
                <button onclick="appendToDisplay('2')">2</button>
                <button onclick="appendToDisplay('3')">3</button>
                <button class="equal" onclick="calculate()">=</button>

                <button onclick="appendToDisplay('0')">0</button>
                <button onclick="appendToDisplay('.')">.</button>
                <button class="scientific" onclick="appendToDisplay(')')">)</button>
            </div>
        </div>
    </div>
    <script src="script.js"></script>
    <script>
        let display = document.getElementById('display');
let historyDisplay = document.getElementById('history-display');
let currentInput = '0';
let angleUnit = 'DEG'; // 'DEG' for degrees, 'RAD' for radians

// Initialize display
display.value = currentInput;

function appendToDisplay(value) {
    if (currentInput === '0' && !['.', '+', '-', '*', '/'].includes(value)) {
        currentInput = value;
    } else {
        currentInput += value;
    }
    display.value = currentInput;
}

function clearAll() {
    currentInput = '0';
    display.value = currentInput;
    historyDisplay.textContent = '';
}

function clearEntry() {
    let lastOperatorIndex = Math.max(
        currentInput.lastIndexOf('+'),
        currentInput.lastIndexOf('-'),
        currentInput.lastIndexOf('*'),
        currentInput.lastIndexOf('/'),
        currentInput.lastIndexOf('(')
    );

    if (lastOperatorIndex !== -1 && lastOperatorIndex < currentInput.length - 1) {
        currentInput = currentInput.substring(0, lastOperatorIndex + 1);
        if (currentInput.endsWith('(')) {
            currentInput = currentInput.substring(0, currentInput.length - 1);
        }
    } else {
        currentInput = '0';
    }
    display.value = currentInput;
}


function backspace() {
    if (currentInput.length > 1 && currentInput !== 'Error') {
        currentInput = currentInput.slice(0, -1);
    } else {
        currentInput = '0';
    }
    display.value = currentInput;
}

function toggleSign() {
    try {
        let matches = currentInput.match(/(\d+\.?\d*)$/);
        if (matches) {
            let lastNumber = parseFloat(matches[1]);
            let negatedNumber = -lastNumber;
            currentInput = currentInput.substring(0, matches.index) + negatedNumber;
        } else if (currentInput === '0') {
            currentInput = '-0';
        } else {
            if (!currentInput.startsWith('-')) {
                currentInput = '-' + currentInput;
            } else {
                currentInput = currentInput.substring(1);
            }
        }
        display.value = currentInput;
    } catch (e) {
        display.value = 'Error';
    }
}

function toggleAngleUnit() {
    const unitButton = document.querySelector('.utility[onclick="toggleAngleUnit()"]');
    if (angleUnit === 'DEG') {
        angleUnit = 'RAD';
        unitButton.textContent = 'RAD';
    } else {
        angleUnit = 'DEG';
        unitButton.textContent = 'DEG';
    }
}

function calculate() {
    let expression = currentInput;
    historyDisplay.textContent = expression + ' =';

    try {
        expression = expression.replace(/×/g, '*').replace(/÷/g, '/');

        if (angleUnit === 'DEG') {
            expression = expression.replace(/sin\(([^)]+)\)/g, (match, p1) => `Math.sin((${p1}) * Math.PI / 180)`);
            expression = expression.replace(/cos\(([^)]+)\)/g, (match, p1) => `Math.cos((${p1}) * Math.PI / 180)`);
            expression = expression.replace(/tan\(([^)]+)\)/g, (match, p1) => `Math.tan((${p1}) * Math.PI / 180)`);
        } else {
            expression = expression.replace(/sin\(/g, 'Math.sin(');
            expression = expression.replace(/cos\(/g, 'Math.cos(');
            expression = expression.replace(/tan\(/g, 'Math.tan(');
        }

        expression = expression.replace(/log\(/g, 'Math.log(');
        expression = expression.replace(/sqrt\(/g, 'Math.sqrt(');
        expression = expression.replace(/π/g, 'Math.PI');
        expression = expression.replace(/e/g, 'Math.E');

        let result = eval(expression);

        if (typeof result === 'number' && !Number.isInteger(result)) {
            result = parseFloat(result.toFixed(10));
        }

        display.value = result;
        currentInput = String(result);
    } catch (error) {
        display.value = 'Error';
        currentInput = '0';
        historyDisplay.textContent = '';
    }
}

// Keyboard Support
document.addEventListener('keydown', (event) => {
    const key = event.key;
    if (/[0-9]/.test(key)) {
        appendToDisplay(key);
    } else if (key === '.') {
        appendToDisplay('.');
    } else if (key === '+') {
        appendToDisplay('+');
    } else if (key === '-') {
        appendToDisplay('-');
    } else if (key === '*') {
        appendToDisplay('×');
    } else if (key === '/') {
        appendToDisplay('÷');
    } else if (key === 'Enter') {
        calculate();
    } else if (key === 'Backspace') {
        backspace();
    } else if (key === 'Escape') {
        clearAll();
    } else if (key === '(') {
        appendToDisplay('(');
    } else if (key === ')') {
        appendToDisplay(')');
    }
    if (['+', '-', '*', '/', 'Enter', 'Backspace', 'Escape', '.', '(', ')'].includes(key)) {
        event.preventDefault();
    }
});

document.addEventListener('DOMContentLoaded', () => {
    display.value = '0';
});
    </script>
</body>
</html>
