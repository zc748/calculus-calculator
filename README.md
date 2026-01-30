<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Free online calculus calculator for derivatives, integrals, limits, and more. No installation required.">
    <meta name="keywords" content="calculus, calculator, derivative, integral, limit, math, free">
    <title>Calculus Calculator - Free Online Math Tool</title>
    
    <!-- Favicon -->
    <link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>∂</text></svg>">
    
    <!-- Math Libraries -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjs/12.4.1/math.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/nerdamer@1.1.13/nerdamer.core.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/nerdamer@1.1.13/Calculus.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/nerdamer@1.1.13/Algebra.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/nerdamer@1.1.13/Solve.js"></script>
    
    <!-- KaTeX for LaTeX -->
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.css">
    <script defer src="https://cdn.jsdelivr.net/npm/katex@0.16.9/dist/katex.min.js"></script>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Crimson+Pro:wght@300;400;600&family=JetBrains+Mono:wght@400;500;600&family=Cormorant+Garamond:wght@300;400;600;700&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --primary-bg: #0a0a0f;
            --secondary-bg: #151520;
            --card-bg: #1a1a2e;
            --accent: #e8c547;
            --accent-dim: #b39635;
            --accent-bright: #ffd966;
            --text-primary: #e8e8f0;
            --text-secondary: #a8a8b8;
            --text-dim: #6a6a78;
            --border: #2a2a3e;
            --success: #4ecdc4;
            --error: #ff6b6b;
            --shadow: rgba(232, 197, 71, 0.1);
        }

        [data-theme="light"] {
            --primary-bg: #f8f9fa;
            --secondary-bg: #ffffff;
            --card-bg: #ffffff;
            --accent: #d4a94a;
            --accent-dim: #a67c38;
            --text-primary: #1a1a2e;
            --text-secondary: #4a4a5a;
            --text-dim: #7a7a8a;
            --border: #e0e0ea;
            --success: #2aa89a;
            --error: #e74c3c;
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
            transition: all 0.3s ease;
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

        /* Navigation */
        .navbar {
            position: sticky;
            top: 0;
            background: rgba(10, 10, 15, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 1px solid var(--border);
            z-index: 1000;
            padding: 15px 0;
        }

        .nav-container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .nav-brand {
            display: flex;
            align-items: center;
            gap: 12px;
            font-family: 'Cormorant Garamond', serif;
        }

        .brand-symbol {
            font-size: 2rem;
            color: var(--accent);
        }

        .brand-name {
            font-size: 1.5rem;
            color: var(--text-primary);
        }

        .badge-github {
            background: rgba(232, 197, 71, 0.1);
            border: 1px solid var(--accent);
            color: var(--accent);
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 0.85rem;
            letter-spacing: 1px;
            text-decoration: none;
            transition: all 0.3s ease;
        }

        .badge-github:hover {
            background: rgba(232, 197, 71, 0.2);
            transform: translateY(-2px);
        }

        .theme-toggle {
            background: transparent;
            border: 1px solid var(--border);
            color: var(--text-primary);
            width: 40px;
            height: 40px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1.2rem;
            transition: all 0.3s ease;
        }

        .theme-toggle:hover {
            background: rgba(232, 197, 71, 0.1);
            border-color: var(--accent);
        }

        /* Container */
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 1;
        }

        /* Header */
        header {
            text-align: center;
            margin-bottom: 60px;
            animation: fadeInDown 0.8s ease-out;
        }

        h1 {
            font-family: 'Cormorant Garamond', serif;
            font-size: 4.5rem;
            font-weight: 300;
            color: var(--accent);
            letter-spacing: 3px;
            margin-bottom: 15px;
        }

        .subtitle {
            font-size: 1.3rem;
            color: var(--text-secondary);
            letter-spacing: 4px;
            text-transform: uppercase;
            margin-bottom: 25px;
        }

        .header-badges {
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
        }

        .badge {
            padding: 10px 20px;
            background: rgba(232, 197, 71, 0.1);
            border: 1px solid var(--accent);
            border-radius: 25px;
            color: var(--accent);
            font-size: 0.9rem;
            letter-spacing: 1.5px;
        }

        /* Calculator Grid */
        .calc-grid {
            display: grid;
            grid-template-columns: 320px 1fr;
            gap: 35px;
            margin-bottom: 60px;
        }

        /* Sidebar */
        .sidebar {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 30px;
            height: fit-content;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
            position: sticky;
            top: 100px;
        }

        .nav-title {
            font-size: 0.95rem;
            text-transform: uppercase;
            letter-spacing: 2.5px;
            color: var(--text-secondary);
            margin-bottom: 25px;
            font-weight: 600;
        }

        .calc-type-btn {
            width: 100%;
            padding: 18px 22px;
            background: transparent;
            border: 1px solid var(--border);
            border-radius: 10px;
            color: var(--text-primary);
            font-family: 'Crimson Pro', serif;
            font-size: 1.15rem;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 14px;
            text-align: left;
            display: flex;
            align-items: center;
            gap: 15px;
        }

        .calc-type-btn:hover {
            background: rgba(232, 197, 71, 0.05);
            border-color: var(--accent-dim);
            transform: translateX(8px);
        }

        .calc-type-btn.active {
            background: linear-gradient(135deg, rgba(232, 197, 71, 0.15), rgba(232, 197, 71, 0.05));
            border-color: var(--accent);
            box-shadow: 0 0 25px var(--shadow);
        }

        .btn-icon {
            font-size: 1.6rem;
            color: var(--accent);
            min-width: 30px;
            text-align: center;
        }

        /* Main Content */
        .main-content {
            background: var(--card-bg);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 45px;
            box-shadow: 0 10px 40px rgba(0, 0, 0, 0.3);
        }

        .calc-section {
            display: none;
        }

        .calc-section.active {
            display: block;
            animation: fadeIn 0.4s ease-out;
        }

        .section-header {
            margin-bottom: 40px;
            padding-bottom: 25px;
            border-bottom: 1px solid var(--border);
        }

        .section-title {
            font-family: 'Cormorant Garamond', serif;
            font-size: 2.8rem;
            color: var(--accent);
            margin-bottom: 12px;
        }

        .section-description {
            font-size: 1.1rem;
            color: var(--text-secondary);
        }

        /* Input Groups */
        .input-group {
            margin-bottom: 28px;
        }

        label {
            display: block;
            margin-bottom: 12px;
        }

        .label-text {
            display: block;
            font-size: 0.95rem;
            color: var(--text-secondary);
            letter-spacing: 1.5px;
            text-transform: uppercase;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .label-hint {
            display: block;
            font-size: 0.85rem;
            color: var(--text-dim);
            font-weight: 400;
            text-transform: none;
        }

        .input-field {
            width: 100%;
            padding: 16px 20px;
            background: var(--secondary-bg);
            border: 1px solid var(--border);
            border-radius: 10px;
            color: var(--text-primary);
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.05rem;
            transition: all 0.3s ease;
        }

        .input-field:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 4px rgba(232, 197, 71, 0.1);
        }

        .input-examples {
            margin-top: 12px;
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
        }

        .example-label {
            font-size: 0.85rem;
            color: var(--text-dim);
        }

        .example-btn {
            padding: 6px 12px;
            background: rgba(232, 197, 71, 0.05);
            border: 1px solid var(--border);
            border-radius: 6px;
            color: var(--text-secondary);
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.85rem;
            cursor: pointer;
            transition: all 0.2s ease;
        }

        .example-btn:hover {
            background: rgba(232, 197, 71, 0.1);
            border-color: var(--accent);
            color: var(--accent);
        }

        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 22px;
        }

        .grid-3 {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 22px;
        }

        /* Buttons */
        .btn-primary {
            background: linear-gradient(135deg, var(--accent), var(--accent-dim));
            color: var(--primary-bg);
            padding: 18px 45px;
            border: none;
            border-radius: 10px;
            font-family: 'Crimson Pro', serif;
            font-size: 1.15rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-transform: uppercase;
            letter-spacing: 2.5px;
            box-shadow: 0 6px 25px rgba(232, 197, 71, 0.35);
            display: inline-flex;
            align-items: center;
            gap: 12px;
        }

        .btn-primary:hover:not(:disabled) {
            transform: translateY(-3px);
            box-shadow: 0 10px 35px rgba(232, 197, 71, 0.45);
        }

        .btn-primary:disabled {
            opacity: 0.6;
            cursor: not-allowed;
        }

        /* Result Box */
        .result-box {
            margin-top: 35px;
            padding: 35px;
            background: var(--secondary-bg);
            border: 1px solid var(--border);
            border-radius: 12px;
            display: none;
        }

        .result-box.show {
            display: block;
            animation: slideUp 0.5s ease-out;
        }

        .result-label {
            font-size: 0.95rem;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 2.5px;
            margin-bottom: 18px;
            font-weight: 600;
        }

        .result-content {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.4rem;
            color: var(--success);
            line-height: 1.9;
            padding: 15px;
            background: rgba(78, 205, 196, 0.05);
            border-radius: 8px;
            border-left: 4px solid var(--success);
        }

        .result-content.error {
            color: var(--error);
            background: rgba(255, 107, 107, 0.05);
            border-left-color: var(--error);
        }

        /* Steps */
        .steps-container {
            margin-top: 28px;
            padding-top: 28px;
            border-top: 1px solid var(--border);
        }

        .step {
            margin-bottom: 18px;
            padding: 18px;
            background: rgba(232, 197, 71, 0.03);
            border-left: 4px solid var(--accent);
            border-radius: 6px;
        }

        .step-label {
            font-size: 0.9rem;
            color: var(--accent);
            text-transform: uppercase;
            letter-spacing: 1.5px;
            margin-bottom: 10px;
            font-weight: 600;
        }

        .step-content {
            font-family: 'JetBrains Mono', monospace;
            font-size: 1.05rem;
            color: var(--text-primary);
        }

        /* Footer */
        .footer {
            background: var(--card-bg);
            border-top: 1px solid var(--border);
            padding: 40px 20px;
            text-align: center;
            margin-top: 60px;
        }

        .footer-text {
            color: var(--text-secondary);
            margin-bottom: 10px;
        }

        /* Animations */
        @keyframes fadeInDown {
            from {
                opacity: 0;
                transform: translateY(-40px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Responsive */
        @media (max-width: 968px) {
            .calc-grid {
                grid-template-columns: 1fr;
            }
            
            .sidebar {
                display: flex;
                overflow-x: auto;
                padding: 20px;
                gap: 12px;
                position: static;
            }
            
            .nav-title {
                display: none;
            }
            
            .calc-type-btn {
                min-width: 160px;
                margin-bottom: 0;
            }
            
            h1 {
                font-size: 2.8rem;
            }
            
            .grid-2, .grid-3 {
                grid-template-columns: 1fr;
            }
            
            .main-content {
                padding: 30px 25px;
            }
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar">
        <div class="nav-container">
            <div class="nav-brand">
                <span class="brand-symbol">∂</span>
                <span class="brand-name">Calculus</span>
            </div>
            <div style="display: flex; gap: 15px; align-items: center;">
                <a href="https://github.com/yourusername/calculus-calculator" class="badge-github" target="_blank">⭐ GitHub</a>
                <button class="theme-toggle" onclick="toggleTheme()">☀</button>
            </div>
        </div>
    </nav>

    <div class="container">
        <header>
            <h1>Calculus</h1>
            <p class="subtitle">Free Online Calculator</p>
            <div class="header-badges">
                <span class="badge">100% Free</span>
                <span class="badge">No Backend Required</span>
                <span class="badge">GitHub Pages Ready</span>
            </div>
        </header>
        
        <div class="calc-grid">
            <div class="sidebar">
                <div class="nav-title">Operations</div>
                <button class="calc-type-btn active" onclick="switchCalc('derivative')">
                    <span class="btn-icon">∂</span>
                    <span>Derivatives</span>
                </button>
                <button class="calc-type-btn" onclick="switchCalc('integral')">
                    <span class="btn-icon">∫</span>
                    <span>Integrals</span>
                </button>
                <button class="calc-type-btn" onclick="switchCalc('limit')">
                    <span class="btn-icon">lim</span>
                    <span>Limits</span>
                </button>
                <button class="calc-type-btn" onclick="switchCalc('series')">
                    <span class="btn-icon">∑</span>
                    <span>Series</span>
                </button>
                <button class="calc-type-btn" onclick="switchCalc('equation')">
                    <span class="btn-icon">=</span>
                    <span>Equations</span>
                </button>
            </div>
            
            <div class="main-content">
                <!-- Derivative Section -->
                <div class="calc-section active" id="derivative-section">
                    <div class="section-header">
                        <h2 class="section-title">Derivative Calculator</h2>
                        <p class="section-description">Calculate derivatives with symbolic computation</p>
                    </div>
                    
                    <div class="input-group">
                        <label>
                            <span class="label-text">Function f(x)</span>
                            <span class="label-hint">Use * for multiplication, ^ for powers</span>
                        </label>
                        <input type="text" id="deriv-func" class="input-field" placeholder="x^2 + 3*x + sin(x)">
                        <div class="input-examples">
                            <span class="example-label">Examples:</span>
                            <button class="example-btn" onclick="setExample('deriv-func', 'x^2 + 3*x')">x² + 3x</button>
                            <button class="example-btn" onclick="setExample('deriv-func', 'sin(x)*exp(x)')">sin(x)·eˣ</button>
                            <button class="example-btn" onclick="setExample('deriv-func', 'x^3/(x^2 + 1)')">x³/(x²+1)</button>
                        </div>
                    </div>
                    
                    <div class="grid-2">
                        <div class="input-group">
                            <label><span class="label-text">Variable</span></label>
                            <input type="text" id="deriv-var" class="input-field" value="x">
                        </div>
                        <div class="input-group">
                            <label><span class="label-text">Order</span></label>
                            <select id="deriv-order" class="input-field">
                                <option value="1">First Derivative</option>
                                <option value="2">Second Derivative</option>
                                <option value="3">Third Derivative</option>
                            </select>
                        </div>
                    </div>
                    
                    <button class="btn-primary" onclick="calculateDerivative()">Calculate →</button>
                    <div class="result-box" id="deriv-result"></div>
                </div>
                
                <!-- Integral Section -->
                <div class="calc-section" id="integral-section">
                    <div class="section-header">
                        <h2 class="section-title">Integral Calculator</h2>
                        <p class="section-description">Compute integrals symbolically</p>
                    </div>
                    
                    <div class="input-group">
                        <label>
                            <span class="label-text">Function f(x)</span>
                        </label>
                        <input type="text" id="int-func" class="input-field" placeholder="x^2 + 3*x">
                        <div class="input-examples">
                            <span class="example-label">Examples:</span>
                            <button class="example-btn" onclick="setExample('int-func', 'x^2')">x²</button>
                            <button class="example-btn" onclick="setExample('int-func', 'sin(x)')">sin(x)</button>
                            <button class="example-btn" onclick="setExample('int-func', '1/(x^2 + 1)')">1/(x²+1)</button>
                        </div>
                    </div>
                    
                    <div class="input-group">
                        <label><span class="label-text">Variable</span></label>
                        <input type="text" id="int-var" class="input-field" value="x">
                    </div>
                    
                    <button class="btn-primary" onclick="calculateIntegral()">Calculate →</button>
                    <div class="result-box" id="int-result"></div>
                </div>
                
                <!-- Limit Section -->
                <div class="calc-section" id="limit-section">
                    <div class="section-header">
                        <h2 class="section-title">Limit Calculator</h2>
                        <p class="section-description">Evaluate limits at any point</p>
                    </div>
                    
                    <div class="input-group">
                        <label><span class="label-text">Function f(x)</span></label>
                        <input type="text" id="limit-func" class="input-field" placeholder="(x^2 - 1)/(x - 1)">
                        <div class="input-examples">
                            <span class="example-label">Examples:</span>
                            <button class="example-btn" onclick="setExample('limit-func', '(x^2 - 1)/(x - 1)')">Indeterminate</button>
                            <button class="example-btn" onclick="setExample('limit-func', 'sin(x)/x')">sin(x)/x</button>
                        </div>
                    </div>
                    
                    <div class="grid-2">
                        <div class="input-group">
                            <label><span class="label-text">Variable</span></label>
                            <input type="text" id="limit-var" class="input-field" value="x">
                        </div>
                        <div class="input-group">
                            <label><span class="label-text">Approaches</span></label>
                            <input type="text" id="limit-point" class="input-field" placeholder="0">
                        </div>
                    </div>
                    
                    <button class="btn-primary" onclick="calculateLimit()">Calculate →</button>
                    <div class="result-box" id="limit-result"></div>
                </div>
                
                <!-- Series Section -->
                <div class="calc-section" id="series-section">
                    <div class="section-header">
                        <h2 class="section-title">Series Calculator</h2>
                        <p class="section-description">Taylor and Maclaurin series</p>
                    </div>
                    
                    <div class="input-group">
                        <label><span class="label-text">Function f(x)</span></label>
                        <input type="text" id="series-func" class="input-field" placeholder="exp(x)">
                        <div class="input-examples">
                            <span class="example-label">Examples:</span>
                            <button class="example-btn" onclick="setExample('series-func', 'exp(x)')">eˣ</button>
                            <button class="example-btn" onclick="setExample('series-func', 'sin(x)')">sin(x)</button>
                            <button class="example-btn" onclick="setExample('series-func', 'cos(x)')">cos(x)</button>
                        </div>
                    </div>
                    
                    <div class="grid-3">
                        <div class="input-group">
                            <label><span class="label-text">Variable</span></label>
                            <input type="text" id="series-var" class="input-field" value="x">
                        </div>
                        <div class="input-group">
                            <label><span class="label-text">Point</span></label>
                            <input type="text" id="series-point" class="input-field" value="0">
                        </div>
                        <div class="input-group">
                            <label><span class="label-text">Terms</span></label>
                            <input type="number" id="series-terms" class="input-field" value="5" min="1" max="10">
                        </div>
                    </div>
                    
                    <button class="btn-primary" onclick="calculateSeries()">Calculate →</button>
                    <div class="result-box" id="series-result"></div>
                </div>
                
                <!-- Equation Section -->
                <div class="calc-section" id="equation-section">
                    <div class="section-header">
                        <h2 class="section-title">Equation Solver</h2>
                        <p class="section-description">Solve algebraic equations</p>
                    </div>
                    
                    <div class="input-group">
                        <label>
                            <span class="label-text">Equation (= 0)</span>
                            <span class="label-hint">Enter equation to solve</span>
                        </label>
                        <input type="text" id="eq-func" class="input-field" placeholder="x^2 - 4">
                        <div class="input-examples">
                            <span class="example-label">Examples:</span>
                            <button class="example-btn" onclick="setExample('eq-func', 'x^2 - 4')">x² - 4</button>
                            <button class="example-btn" onclick="setExample('eq-func', 'x^3 - 6*x^2 + 11*x - 6')">Cubic</button>
                        </div>
                    </div>
                    
                    <div class="input-group">
                        <label><span class="label-text">Variable</span></label>
                        <input type="text" id="eq-var" class="input-field" value="x">
                    </div>
                    
                    <button class="btn-primary" onclick="solveEquation()">Solve →</button>
                    <div class="result-box" id="eq-result"></div>
                </div>
            </div>
        </div>
    </div>
    
    <footer class="footer">
        <p class="footer-text">Built with JavaScript • Runs 100% in your browser</p>
        <p class="footer-text" style="color: var(--text-dim); font-size: 0.9rem;">© 2025 Free Calculus Calculator • Hosted on GitHub Pages</p>
    </footer>

    <script>
        // Theme toggle
        function toggleTheme() {
            const body = document.body;
            const btn = document.querySelector('.theme-toggle');
            if (body.hasAttribute('data-theme')) {
                body.removeAttribute('data-theme');
                btn.textContent = '☀';
                localStorage.setItem('theme', 'dark');
            } else {
                body.setAttribute('data-theme', 'light');
                btn.textContent = '🌙';
                localStorage.setItem('theme', 'light');
            }
        }

        // Load saved theme
        if (localStorage.getItem('theme') === 'light') {
            document.body.setAttribute('data-theme', 'light');
            document.querySelector('.theme-toggle').textContent = '🌙';
        }

        // Switch calculator
        function switchCalc(type) {
            document.querySelectorAll('.calc-type-btn').forEach(b => b.classList.remove('active'));
            document.querySelectorAll('.calc-section').forEach(s => s.classList.remove('active'));
            event.target.closest('.calc-type-btn').classList.add('active');
            document.getElementById(type + '-section').classList.add('active');
        }

        // Set example
        function setExample(id, value) {
            document.getElementById(id).value = value;
        }

        // Show result
        function showResult(id, content, isError = false) {
            const box = document.getElementById(id);
            box.innerHTML = `
                <div class="result-label">Result</div>
                <div class="result-content ${isError ? 'error' : ''}">${content}</div>
            `;
            box.classList.add('show');
        }

        // Show steps
        function showSteps(id, steps) {
            const box = document.getElementById(id);
            let html = '<div class="steps-container">';
            steps.forEach(step => {
                html += `
                    <div class="step">
                        <div class="step-label">${step.label}</div>
                        <div class="step-content">${step.content}</div>
                    </div>
                `;
            });
            html += '</div>';
            box.innerHTML += html;
        }

        // Calculate Derivative
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
                let steps = [
                    { label: 'Original Function', content: `f(${variable}) = ${func}` },
                    { label: 'First Derivative', content: `f'(${variable}) = ${result}` }
                ];

                for (let i = 2; i <= order; i++) {
                    result = nerdamer(`diff(${result}, ${variable})`).toString();
                    steps.push({
                        label: i === 2 ? 'Second Derivative' : 'Third Derivative',
                        content: `f${"'".repeat(i)}(${variable}) = ${result}`
                    });
                }

                showResult('deriv-result', result);
                showSteps('deriv-result', steps);
            } catch (error) {
                showResult('deriv-result', `Error: ${error.message}`, true);
            }
        }

        // Calculate Integral
        function calculateIntegral() {
            try {
                const func = document.getElementById('int-func').value;
                const variable = document.getElementById('int-var').value;

                if (!func) {
                    showResult('int-result', 'Please enter a function', true);
                    return;
                }

                const result = nerdamer(`integrate(${func}, ${variable})`).toString();
                const steps = [
                    { label: 'Original Function', content: `f(${variable}) = ${func}` },
                    { label: 'Indefinite Integral', content: `∫ ${func} d${variable} = ${result} + C` }
                ];

                showResult('int-result', result + ' + C');
                showSteps('int-result', steps);
            } catch (error) {
                showResult('int-result', `Error: ${error.message}`, true);
            }
        }

        // Calculate Limit
        function calculateLimit() {
            try {
                const func = document.getElementById('limit-func').value;
                const variable = document.getElementById('limit-var').value;
                const point = document.getElementById('limit-point').value || '0';

                if (!func) {
                    showResult('limit-result', 'Please enter a function', true);
                    return;
                }

                // Try direct substitution first
                let result;
                try {
                    result = nerdamer(func).evaluate({[variable]: point}).toString();
                } catch (e) {
                    result = 'Limit requires L\'Hôpital\'s rule or simplification';
                }

                const steps = [
                    { label: 'Original Function', content: `f(${variable}) = ${func}` },
                    { label: 'Limit', content: `lim(${variable} → ${point}) ${func} = ${result}` }
                ];

                showResult('limit-result', result);
                showSteps('limit-result', steps);
            } catch (error) {
                showResult('limit-result', `Error: ${error.message}`, true);
            }
        }

        // Calculate Series
        function calculateSeries() {
            try {
                const func = document.getElementById('series-func').value;
                const variable = document.getElementById('series-var').value;
                const point = document.getElementById('series-point').value || '0';
                const terms = parseInt(document.getElementById('series-terms').value);

                if (!func) {
                    showResult('series-result', 'Please enter a function', true);
                    return;
                }

                // Calculate Taylor series terms
                let series = [];
                let currentFunc = func;
                
                for (let n = 0; n < terms; n++) {
                    const derivative = n === 0 ? func : nerdamer(`diff(${currentFunc}, ${variable})`).toString();
                    const value = nerdamer(derivative).evaluate({[variable]: point}).toString();
                    
                    let factorial = 1;
                    for (let i = 2; i <= n; i++) factorial *= i;
                    
                    let term;
                    if (n === 0) {
                        term = value;
                    } else {
                        term = `(${value}/${factorial})*(${variable} - ${point})^${n}`;
                    }
                    
                    series.push(term);
                    currentFunc = derivative;
                }

                const result = series.join(' + ');
                const simplified = nerdamer(result).toString();

                const steps = [
                    { label: 'Original Function', content: `f(${variable}) = ${func}` },
                    { label: 'Taylor Series', content: simplified }
                ];

                showResult('series-result', simplified);
                showSteps('series-result', steps);
            } catch (error) {
                showResult('series-result', `Error: ${error.message}`, true);
            }
        }

        // Solve Equation
        function solveEquation() {
            try {
                const func = document.getElementById('eq-func').value;
                const variable = document.getElementById('eq-var').value;

                if (!func) {
                    showResult('eq-result', 'Please enter an equation', true);
                    return;
                }

                const solutions = nerdamer.solveEquations(`${func}=0`, variable);
                
                let result;
                let steps = [
                    { label: 'Original Equation', content: `${func} = 0` }
                ];

                if (Array.isArray(solutions)) {
                    result = solutions.map((sol, i) => `${variable} = ${sol.toString()}`).join(', ');
                    solutions.forEach((sol, i) => {
                        steps.push({ label: `Solution ${i + 1}`, content: `${variable} = ${sol.toString()}` });
                    });
                } else {
                    result = `${variable} = ${solutions.toString()}`;
                    steps.push({ label: 'Solution', content: result });
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
