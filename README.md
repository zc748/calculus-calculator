# calculuscalculator
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculus Calculator - Advanced Mathematical Computing</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/11.11.0/math.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.13/nerdamer.core.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.13/Calculus.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/nerdamer/1.1.13/Algebra.min.js"></script>
    <script src="https://cdn.plot.ly/plotly-2.27.0.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Crimson+Pro:wght@300;400;600&family=JetBrains+Mono:wght@400;500&family=Cormorant+Garamond:wght@300;400;600&display=swap');
        
        :root {
            --primary-bg: #0a0a0f;
            --secondary-bg: #151520;
            --card-bg: #1a1a2e;
            --accent: #e8c547;
            --accent-dim: #b39635;
            --text-primary: #e8e8f0;
            --text-secondary: #a8a8b8;
            --border: #2a2a3e;
            --success: #4ecdc4;
            --error: #ff6b6b;
            --shadow: rgba(232, 197, 71, 0.1);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Crimson Pro', serif;
            background: linear-gradient(135deg, var(--primary-bg) 0%, #0f0f1a 100%);
            color: var(--text-primary);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                radial-gradient(circle at 20% 30%, rgba(232, 197, 71, 0.03) 0%, transparent 50%),
                radial-gradient(circle at 80% 70%, rgba(78, 205, 196, 0.03) 0%, transparent 50%);
            pointer-events: none;
            z-index: 0;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }
        
        header {
            text-align: center;
            margin-bottom: 60px;
            animation: fadeInDown 0.8s ease-out;
        }
        
        h1 {
            font-family: 'Cormorant Garamond', serif;
            font-size: 4rem;
            font-weight: 300;
            color: var(--accent);
            letter-spacing: 2px;
            margin-bottom: 10px;
            text-shadow: 0 0 30px var(--shadow);
        }
        
        .subtitle {
            font-size: 1.2rem;
            color: var(--text-secondary);
            letter-spacing: 3px;
            text-transform: uppercase;
            font-weight: 300;
        }
        
        .calc-grid {
            display: grid;
            grid-template-columns: 300px 1fr;
            gap: 30px;
            margin-bottom: 40px;
        }
        
        .sidebar {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 25px;
            height: fit-content;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            animation: fadeInLeft 0.6s ease-out 0.2s backwards;
        }
        
        .nav-title {
            font-size: 0.9rem;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: var(--text-secondary);
            margin-bottom: 20px;
            font-weight: 600;
        }
        
        .calc-type-btn {
            width: 100%;
            padding: 15px 20px;
            background: transparent;
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-primary);
            font-family: 'Crimson Pro', serif;
            font-size: 1.1rem;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 12px;
            text-align: left;
            display: flex;
            align-items: center;
            gap: 12px;
        }
        
        .calc-type-btn:hover {
            background: rgba(232, 197, 71, 0.05);
            border-color: var(--accent-dim);
            transform: translateX(5px);
        }
        
        .calc-type-btn.active {
            background: linear-gradient(135deg, rgba(232, 197, 71, 0.15), rgba(232, 197, 71, 0.05));
            border-color: var(--accent);
            box-shadow: 0 0 20px var(--shadow);
        }
        
        .calc-type-btn::before {
            content: '∂';
            font-size: 1.4rem;
            color: var(--accent);
            font-weight: 600;
        }
        
        .main-content {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 40px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            animation: fadeInRight 0.6s ease-out 0.2s backwards;
        }
        
        .calc-section {
            display: none;
        }
        
        .calc-section.active {
            display: block;
            animation: fadeIn 0.4s ease-out;
        }
        
        .section-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.5rem;
            color: var(--accent);
            margin-bottom: 30px;
            font-weight: 400;
        }
        
        .input-group {
            margin-bottom: 25px;
        }
        
        label {
            display: block;
            font-size: 1rem;
            color: var(--text-secondary);
            margin-bottom: 10px;
            letter-spacing: 1px;
            text-transform: uppercase;
            font-size: 0.85rem;
        }
        
        input, select {
            width: 100%;
            padding: 15px 20px;
            background: var(--secondary-bg);
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text-primary);
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.1rem;
            transition: all 0.3s ease;
        }
        
        input:focus, select:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px rgba(232, 197, 71, 0.1);
        }
        
        .btn-primary {
            background: linear-gradient(135deg, var(--accent), var(--accent-dim));
            color: var(--primary-bg);
            padding: 15px 40px;
            border: none;
            border-radius: 8px;
            font-family: 'Crimson Pro', serif;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2px;
            box-shadow: 0 5px 20px rgba(232, 197, 71, 0.3);
        }
        
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 30px rgba(232, 197, 71, 0.4);
        }
        
        .btn-primary:active {
            transform: translateY(0);
        }
        
        .result-box {
            margin-top: 30px;
            padding: 30px;
            background: var(--secondary-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            min-height: 100px;
            display: none;
        }
        
        .result-box.show {
            display: block;
            animation: slideUp 0.4s ease-out;
        }
        
        .result-label {
            font-size: 0.9rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 2px;
            margin-bottom: 15px;
        }
        
        .result-content {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.3rem;
            color: var(--success);
            line-height: 1.8;
            word-wrap: break-word;
        }
        
        .steps-container {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid var(--border);
        }
        
        .step {
            margin-bottom: 15px;
            padding: 15px;
            background: rgba(232, 197, 71, 0.03);
            border-left: 3px solid var(--accent);
            border-radius: 4px;
        }
        
        .step-label {
            font-size: 0.85rem;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 8px;
        }
        
        .step-content {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1rem;
            color: var(--text-primary);
        }
        
        #graph-container {
            margin-top: 30px;
            padding: 20px;
            background: var(--secondary-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            display: none;
        }
        
        #graph-container.show {
            display: block;
            animation: fadeIn 0.6s ease-out;
        }
        
        .error {
            color: var(--error);
        }
        
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        
        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @keyframes fadeInLeft {
            from {
                opacity: 0;
                transform: translateX(-30px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }
        
        @keyframes fadeInRight {
            from {
                opacity: 0;
                transform: translateX(30px);
            }
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }
        
        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
        
        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        @media (max-width: 968px) {
            .calc-grid {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                display: flex;
                overflow-x: auto;
                padding: 20px;
                gap: 10px;
            }
            
            .nav-title {
                display: none;
            }
            
            .calc-type-btn {
                min-width: 150px;
                margin-bottom: 0;
            }
            
            h1 {
                font-size: 2.5rem;
            }
            
            .grid-2 {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Calculus</h1>
            <p class="subtitle">Advanced Mathematical Computing</p>
        </header>
        
        <div class="calc-grid">
            <div class="sidebar">
                <div class="nav-title">Operations</div>
                <button class="calc-type-btn active" data-calc="derivative">Derivatives</button>
                <button class="calc-type-btn" data-calc="integral">Integrals</button>
                <button class="calc-type-btn" data-calc="limit">Limits</button>
                <button class="calc-type-btn" data-calc="series">Series</button>
                <button class="calc-type-btn" data-calc="equation">Equations</button>
            </div>
            
            <div class="main-content">
                <!-- Derivative Section -->
                <div class="calc-section active" id="derivative-section">
                    <h2 class="section-title">Derivative Calculator</h2>
                    <div class="input-group">
                        <label for="deriv-func">Function f(x)</label>
                        <input type="text" id="deriv-func" placeholder="e.g., x^2 + 3*x + sin(x)">
                    </div>
                    <div class="input-group">
                        <label for="deriv-var">Variable</label>
                        <input type="text" id="deriv-var" value="x" placeholder="x">
                    </div>
                    <div class="input-group">
                        <label for="deriv-order">Order</label>
                        <select id="deriv-order">
                            <option value="1">First Derivative (f')</option>
                            <option value="2">Second Derivative (f'')</option>
                            <option value="3">Third Derivative (f''')</option>
                        </select>
                    </div>
                    <button class="btn-primary" onclick="calculateDerivative()">Calculate Derivative</button>
                    <div class="result-box" id="deriv-result"></div>
                    <div id="deriv-graph"></div>
                </div>
                
                <!-- Integral Section -->
                <div class="calc-section" id="integral-section">
                    <h2 class="section-title">Integral Calculator</h2>
                    <div class="input-group">
                        <label for="int-func">Function f(x)</label>
                        <input type="text" id="int-func" placeholder="e.g., x^2 + 3*x">
                    </div>
                    <div class="input-group">
                        <label for="int-var">Variable</label>
                        <input type="text" id="int-var" value="x" placeholder="x">
                    </div>
                    <div class="input-group">
                        <label for="int-type">Type</label>
                        <select id="int-type" onchange="toggleIntegralLimits()">
                            <option value="indefinite">Indefinite Integral</option>
                            <option value="definite">Definite Integral</option>
                        </select>
                    </div>
                    <div id="integral-limits" style="display: none;">
                        <div class="grid-2">
                            <div class="input-group">
                                <label for="int-lower">Lower Limit</label>
                                <input type="text" id="int-lower" placeholder="0">
                            </div>
                            <div class="input-group">
                                <label for="int-upper">Upper Limit</label>
                                <input type="text" id="int-upper" placeholder="1">
                            </div>
                        </div>
                    </div>
                    <button class="btn-primary" onclick="calculateIntegral()">Calculate Integral</button>
                    <div class="result-box" id="int-result"></div>
                    <div id="int-graph"></div>
                </div>
                
                <!-- Limit Section -->
                <div class="calc-section" id="limit-section">
                    <h2 class="section-title">Limit Calculator</h2>
                    <div class="input-group">
                        <label for="limit-func">Function f(x)</label>
                        <input type="text" id="limit-func" placeholder="e.g., (x^2 - 1)/(x - 1)">
                    </div>
                    <div class="input-group">
                        <label for="limit-var">Variable</label>
                        <input type="text" id="limit-var" value="x" placeholder="x">
                    </div>
                    <div class="input-group">
                        <label for="limit-point">Approaches</label>
                        <input type="text" id="limit-point" placeholder="e.g., 0, infinity">
                    </div>
                    <button class="btn-primary" onclick="calculateLimit()">Calculate Limit</button>
                    <div class="result-box" id="limit-result"></div>
                </div>
                
                <!-- Series Section -->
                <div class="calc-section" id="series-section">
                    <h2 class="section-title">Series Calculator</h2>
                    <div class="input-group">
                        <label for="series-func">Function f(x)</label>
                        <input type="text" id="series-func" placeholder="e.g., e^x, sin(x), cos(x)">
                    </div>
                    <div class="input-group">
                        <label for="series-var">Variable</label>
                        <input type="text" id="series-var" value="x" placeholder="x">
                    </div>
                    <div class="input-group">
                        <label for="series-point">Expansion Point (a)</label>
                        <input type="text" id="series-point" value="0" placeholder="0">
                    </div>
                    <div class="input-group">
                        <label for="series-terms">Number of Terms</label>
                        <input type="number" id="series-terms" value="5" min="1" max="10">
                    </div>
                    <button class="btn-primary" onclick="calculateSeries()">Calculate Series</button>
                    <div class="result-box" id="series-result"></div>
                </div>
                
                <!-- Equation Solver Section -->
                <div class="calc-section" id="equation-section">
                    <h2 class="section-title">Equation Solver</h2>
                    <div class="input-group">
                        <label for="eq-func">Equation (set equal to 0)</label>
                        <input type="text" id="eq-func" placeholder="e.g., x^2 - 4 (solves x^2 - 4 = 0)">
                    </div>
                    <div class="input-group">
                        <label for="eq-var">Variable</label>
                        <input type="text" id="eq-var" value="x" placeholder="x">
                    </div>
                    <button class="btn-primary" onclick="solveEquation()">Solve Equation</button>
                    <div class="result-box" id="eq-result"></div>
                </div>
            </div>
        </div>
    </div>
    
    <script>
        // Navigation
        document.querySelectorAll('.calc-type-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                // Remove active class from all buttons and sections
                document.querySelectorAll('.calc-type-btn').forEach(b => b.classList.remove('active'));
                document.querySelectorAll('.calc-section').forEach(s => s.classList.remove('active'));
                
                // Add active class to clicked button
                this.classList.add('active');
                
                // Show corresponding section
                const calcType = this.dataset.calc;
                document.getElementById(`${calcType}-section`).classList.add('active');
            });
        });
        
        function toggleIntegralLimits() {
            const type = document.getElementById('int-type').value;
            const limitsDiv = document.getElementById('integral-limits');
            limitsDiv.style.display = type === 'definite' ? 'block' : 'none';
        }
        
        function showResult(resultId, content, isError = false) {
            const resultBox = document.getElementById(resultId);
            resultBox.innerHTML = `
                <div class="result-label">Result</div>
                <div class="result-content ${isError ? 'error' : ''}">${content}</div>
            `;
            resultBox.classList.add('show');
        }
        
        function showSteps(resultId, steps) {
            const resultBox = document.getElementById(resultId);
            let stepsHtml = '<div class="steps-container">';
            steps.forEach((step, index) => {
                stepsHtml += `
                    <div class="step">
                        <div class="step-label">Step ${index + 1}</div>
                        <div class="step-content">${step}</div>
                    </div>
                `;
            });
            stepsHtml += '</div>';
            resultBox.innerHTML += stepsHtml;
        }
        
        // Derivative Calculator
        function calculateDerivative() {
            try {
                const func = document.getElementById('deriv-func').value;
                const variable = document.getElementById('deriv-var').value;
                const order = parseInt(document.getElementById('deriv-order').value);
                
                if (!func) {
                    showResult('deriv-result', 'Please enter a function', true);
                    return;
                }
                
                let result = nerdamer(`diff(${func}, ${variable})`).toString();
                let steps = [`Original function: ${func}`, `First derivative: ${result}`];
                
                // Calculate higher order derivatives
                for (let i = 2; i <= order; i++) {
                    result = nerdamer(`diff(${result}, ${variable})`).toString();
                    steps.push(`${i === 2 ? 'Second' : i === 3 ? 'Third' : i + 'th'} derivative: ${result}`);
                }
                
                showResult('deriv-result', result);
                showSteps('deriv-result', steps);
                
            } catch (error) {
                showResult('deriv-result', `Error: ${error.message}`, true);
            }
        }
        
        // Integral Calculator
        function calculateIntegral() {
            try {
                const func = document.getElementById('int-func').value;
                const variable = document.getElementById('int-var').value;
                const type = document.getElementById('int-type').value;
                
                if (!func) {
                    showResult('int-result', 'Please enter a function', true);
                    return;
                }
                
                if (type === 'indefinite') {
                    const result = nerdamer(`integrate(${func}, ${variable})`).toString();
                    const steps = [
                        `Original function: ${func}`,
                        `Indefinite integral: ∫(${func}) d${variable} = ${result} + C`
                    ];
                    showResult('int-result', result + ' + C');
                    showSteps('int-result', steps);
                } else {
                    const lower = document.getElementById('int-lower').value;
                    const upper = document.getElementById('int-upper').value;
                    
                    if (!lower || !upper) {
                        showResult('int-result', 'Please enter both limits', true);
                        return;
                    }
                    
                    const antiderivative = nerdamer(`integrate(${func}, ${variable})`).toString();
                    const upperValue = nerdamer(antiderivative, {[variable]: upper}).evaluate().toString();
                    const lowerValue = nerdamer(antiderivative, {[variable]: lower}).evaluate().toString();
                    const result = nerdamer(`${upperValue} - (${lowerValue})`).evaluate().toString();
                    
                    const steps = [
                        `Original function: ${func}`,
                        `Antiderivative: ${antiderivative}`,
                        `Evaluate at upper limit (${upper}): ${upperValue}`,
                        `Evaluate at lower limit (${lower}): ${lowerValue}`,
                        `Definite integral: ${result}`
                    ];
                    
                    showResult('int-result', result);
                    showSteps('int-result', steps);
                }
                
            } catch (error) {
                showResult('int-result', `Error: ${error.message}`, true);
            }
        }
        
        // Limit Calculator
        function calculateLimit() {
            try {
                const func = document.getElementById('limit-func').value;
                const variable = document.getElementById('limit-var').value;
                const point = document.getElementById('limit-point').value;
                
                if (!func || !point) {
                    showResult('limit-result', 'Please enter function and limit point', true);
                    return;
                }
                
                let result;
                let steps = [`Original function: ${func}`];
                
                if (point.toLowerCase() === 'infinity' || point === '∞') {
                    // For limits at infinity, try substitution or simplification
                    steps.push(`Limit as ${variable} → ∞`);
                    try {
                        result = nerdamer(`limit(${func}, ${variable}, infinity)`).toString();
                    } catch (e) {
                        // Fallback: evaluate at very large number
                        result = nerdamer(func, {[variable]: 1000000}).evaluate().toString();
                        steps.push('(Approximated with large value)');
                    }
                } else {
                    steps.push(`Limit as ${variable} → ${point}`);
                    // Try direct substitution first
                    try {
                        result = nerdamer(func, {[variable]: point}).evaluate().toString();
                        if (result === 'NaN' || result.includes('Infinity')) {
                            throw new Error('Indeterminate form');
                        }
                        steps.push('Direct substitution successful');
                    } catch (e) {
                        steps.push('Indeterminate form detected, simplifying...');
                        result = 'Use L\'Hôpital\'s rule or algebraic simplification';
                    }
                }
                
                showResult('limit-result', result);
                showSteps('limit-result', steps);
                
            } catch (error) {
                showResult('limit-result', `Error: ${error.message}`, true);
            }
        }
        
        // Series Calculator
        function calculateSeries() {
            try {
                const func = document.getElementById('series-func').value;
                const variable = document.getElementById('series-var').value;
                const point = document.getElementById('series-point').value;
                const terms = parseInt(document.getElementById('series-terms').value);
                
                if (!func) {
                    showResult('series-result', 'Please enter a function', true);
                    return;
                }
                
                let steps = [`Original function: ${func}`, `Taylor series expansion about ${variable} = ${point}`];
                let series = [];
                
                // Calculate Taylor series terms
                let currentFunc = func;
                for (let n = 0; n < terms; n++) {
                    // Evaluate derivative at point
                    let derivative = n === 0 ? func : nerdamer(`diff(${currentFunc}, ${variable})`).toString();
                    let value = nerdamer(derivative, {[variable]: point}).evaluate().toString();
                    
                    // Create term
                    let factorial = 1;
                    for (let i = 2; i <= n; i++) factorial *= i;
                    
                    let term;
                    if (n === 0) {
                        term = value;
                    } else if (n === 1) {
                        term = `${value}*(${variable} - ${point})`;
                    } else {
                        term = `(${value}/${factorial})*(${variable} - ${point})^${n}`;
                    }
                    
                    series.push(term);
                    steps.push(`f${'\''.repeat(n)}(${point}) = ${value}`);
                    
                    currentFunc = derivative;
                }
                
                const result = series.join(' + ');
                const simplified = nerdamer(result).toString();
                
                steps.push(`Taylor series: ${simplified}`);
                showResult('series-result', simplified);
                showSteps('series-result', steps);
                
            } catch (error) {
                showResult('series-result', `Error: ${error.message}`, true);
            }
        }
        
        // Equation Solver
        function solveEquation() {
            try {
                const func = document.getElementById('eq-func').value;
                const variable = document.getElementById('eq-var').value;
                
                if (!func) {
                    showResult('eq-result', 'Please enter an equation', true);
                    return;
                }
                
                const solutions = nerdamer.solveEquations(`${func}=0`, variable);
                const steps = [
                    `Original equation: ${func} = 0`,
                    `Solving for ${variable}...`
                ];
                
                let result;
                if (Array.isArray(solutions)) {
                    result = solutions.map((sol, i) => `${variable}${i + 1} = ${sol.toString()}`).join('<br>');
                    steps.push(`Found ${solutions.length} solution(s)`);
                } else {
                    result = `${variable} = ${solutions.toString()}`;
                    steps.push('Solution found');
                }
                
                showResult('eq-result', result);
                showSteps('eq-result', steps);
                
            } catch (error) {
                showResult('eq-result', `Error: ${error.message}`, true);
            }
        }
    </script>
</body>
</html>
