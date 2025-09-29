# dldjwls.github.io
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>모바일 계산기</title>
    <style>
        body {
            font-family: sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
            margin: 0;
        }

        .calculator {
            width: 90%;
            max-width: 400px;
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
        }

        input {
            width: calc(100% - 22px); /* padding 고려 */
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 1.2em;
        }

        .result {
            font-size: 1.5em;
            font-weight: bold;
            text-align: right;
            margin-bottom: 20px;
            min-height: 1.5em;
        }

        .button-container {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        .button {
            padding: 20px;
            font-size: 1.2em;
            border: none;
            border-radius: 5px;
            background-color: #e0e0e0;
            cursor: pointer;
            transition: background-color 0.2s;
        }

        .button:active {
            background-color: #d0d0d0;
        }

        .operator {
            background-color: #f79232;
            color: white;
        }

        .operator:active {
            background-color: #e58221;
        }

        .equals {
            grid-column: span 2;
            background-color: #4CAF50;
            color: white;
        }

        .equals:active {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" disabled>
        <div class="result" id="result"></div>
        <div class="button-container">
            <button class="button" onclick="clearDisplay()">C</button>
            <button class="button" onclick="append('.')">.</button>
            <button class="button operator" onclick="setOperator('/')">/</button>
            <button class="button operator" onclick="setOperator('*')">*</button>

            <button class="button" onclick="append('7')">7</button>
            <button class="button" onclick="append('8')">8</button>
            <button class="button" onclick="append('9')">9</button>
            <button class="button operator" onclick="setOperator('-')">-</button>

            <button class="button" onclick="append('4')">4</button>
            <button class="button" onclick="append('5')">5</button>
            <button class="button" onclick="append('6')">6</button>
            <button class="button operator" onclick="setOperator('+')">+</button>

            <button class="button" onclick="append('1')">1</button>
            <button class="button" onclick="append('2')">2</button>
            <button class="button" onclick="append('3')">3</button>
            <button class="button equals" onclick="calculate()">=</button>

            <button class="button" onclick="append('0')">0</button>
        </div>
    </div>
    <script>
        let currentInput = '';
        let operator = '';
        let firstOperand = '';

        function append(value) {
            currentInput += value;
            document.getElementById('display').value = currentInput;
        }

        function setOperator(op) {
            if (currentInput === '') return;
            firstOperand = currentInput;
            operator = op;
            currentInput = '';
        }

        function clearDisplay() {
            currentInput = '';
            operator = '';
            firstOperand = '';
            document.getElementById('display').value = '';
            document.getElementById('result').innerText = '';
        }

        function calculate() {
            if (currentInput === '' || operator === '' || firstOperand === '') return;
            const num1 = parseFloat(firstOperand);
            const num2 = parseFloat(currentInput);
            let result = 0;

            switch(operator) {
                case '+':
                    result = num1 + num2;
                    break;
                case '-':
                    result = num1 - num2;
                    break;
                case '*':
                    result = num1 * num2;
                    break;
                case '/':
                    if (num2 === 0) {
                        document.getElementById('result').innerText = '오류: 0으로 나눌 수 없습니다.';
                        return;
                    }
                    result = num1 / num2;
                    break;
            }

            document.getElementById('result').innerText = result;
            currentInput = result.toString();
            operator = '';
        }
    </script>
</body>
</html>
