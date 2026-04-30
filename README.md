<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Calculator</title>
    <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gradient-to-br from-blue-500 to-purple-600 min-h-screen flex items-center justify-center">
    <div class="bg-white rounded-lg shadow-2xl p-8 w-full max-w-sm">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-6">Calculator</h1>
        
        <div class="bg-gray-100 rounded-lg p-4 mb-6">
            <input 
                type="text" 
                id="display" 
                class="w-full bg-white border-2 border-gray-300 rounded-lg p-4 text-right text-3xl font-semibold text-gray-800 focus:outline-none focus:border-blue-500"
                value="0"
                readonly
            >
        </div>

        <div class="grid grid-cols-4 gap-3">
            <!-- Row 1 -->
            <button onclick="clearDisplay()" class="col-span-2 bg-red-500 hover:bg-red-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">AC</button>
            <button onclick="appendOperator('/')" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">÷</button>
            <button onclick="appendOperator('*')" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">×</button>

            <!-- Row 2 -->
            <button onclick="appendNumber('7')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">7</button>
            <button onclick="appendNumber('8')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">8</button>
            <button onclick="appendNumber('9')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">9</button>
            <button onclick="appendOperator('-')" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">−</button>

            <!-- Row 3 -->
            <button onclick="appendNumber('4')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">4</button>
            <button onclick="appendNumber('5')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">5</button>
            <button onclick="appendNumber('6')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">6</button>
            <button onclick="appendOperator('+')" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">+</button>

            <!-- Row 4 -->
            <button onclick="appendNumber('1')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">1</button>
            <button onclick="appendNumber('2')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">2</button>
            <button onclick="appendNumber('3')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">3</button>
            <button onclick="toggleSign()" class="bg-orange-500 hover:bg-orange-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">+/−</button>

            <!-- Row 5 -->
            <button onclick="appendNumber('0')" class="col-span-2 bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">0</button>
            <button onclick="appendNumber('.')" class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-4 px-4 rounded-lg text-xl transition">.</button>
            <button onclick="calculate()" class="bg-green-500 hover:bg-green-600 text-white font-bold py-4 px-4 rounded-lg text-xl transition">=</button>
        </div>
    </div>

    <script>
        let display = document.getElementById('display');
        let currentValue = '0';
        let previousValue = '';
        let operator = null;
        let shouldResetDisplay = false;

        function appendNumber(num) {
            if (shouldResetDisplay) {
                currentValue = num;
                shouldResetDisplay = false;
            } else {
                currentValue = currentValue === '0' ? num : currentValue + num;
            }
            updateDisplay();
        }

        function appendOperator(op) {
            if (operator !== null && !shouldResetDisplay) {
                calculate();
            }
            previousValue = currentValue;
            operator = op;
            shouldResetDisplay = true;
            updateDisplay();
        }

        function calculate() {
            if (operator === null || shouldResetDisplay) return;

            let result;
            const prev = parseFloat(previousValue);
            const current = parseFloat(currentValue);

            switch (operator) {
                case '+':
                    result = prev + current;
                    break;
                case '-':
                    result = prev - current;
                    break;
                case '*':
                    result = prev * current;
                    break;
                case '/':
                    result = current !== 0 ? prev / current : 0;
                    break;
                default:
                    return;
            }

            currentValue = result.toString();
            operator = null;
            shouldResetDisplay = true;
            updateDisplay();
        }

        function clearDisplay() {
            currentValue = '0';
            previousValue = '';
            operator = null;
            shouldResetDisplay = false;
            updateDisplay();
        }

        function toggleSign() {
            currentValue = currentValue === '0' ? '0' : (parseFloat(currentValue) * -1).toString();
            updateDisplay();
        }

        function updateDisplay() {
            display.value = currentValue;
        }
    </script>
</body>
</html>
