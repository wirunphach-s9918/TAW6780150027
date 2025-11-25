<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daily Meal Planner</title>
    <link rel="stylesheet" href="style.css">
    <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;600&family=Noto+Sans+SC:wght@300;400;700&display=swap" rel="stylesheet">
</head>
<body>

    <header>
        <div class="container header-content">
            <h1 id="app-title">Daily Meal Planner</h1>
            <div class="lang-switcher">
                <button onclick="changeLanguage('th')">ไทย</button>
                <button onclick="changeLanguage('en')">EN</button>
                <button onclick="changeLanguage('zh')">中文</button>
            </div>
        </div>
    </header>

    <main class="container">
        
        <section class="control-bar card">
            <div class="date-group">
                <label for="plan-date" id="label-date">Select Date:</label>
                <input type="date" id="plan-date">
            </div>
            <div class="actions">
                <button id="btn-save" class="primary-btn">Save Plan</button>
                <button id="btn-clear" class="danger-btn">Clear</button>
            </div>
        </section>

        <div class="planning-grid">
            <div class="meal-column">
                
                <div class="card meal-section" id="section-breakfast">
                    <h2 id="header-breakfast">Breakfast</h2>
                    <ul class="food-list" id="list-breakfast">
                        </ul>
                    <div class="add-food-controls">
                        <select id="select-breakfast" class="food-select"></select>
                        <input type="number" id="qty-breakfast" value="1" min="0.5" step="0.5" class="qty-input">
                        <button class="add-btn" onclick="addFood('breakfast')">+</button>
                    </div>
                </div>

                <div class="card meal-section" id="section-lunch">
                    <h2 id="header-lunch">Lunch</h2>
                    <ul class="food-list" id="list-lunch"></ul>
                    <div class="add-food-controls">
                        <select id="select-lunch" class="food-select"></select>
                        <input type="number" id="qty-lunch" value="1" min="0.5" step="0.5" class="qty-input">
                        <button class="add-btn" onclick="addFood('lunch')">+</button>
                    </div>
                </div>

                <div class="card meal-section" id="section-dinner">
                    <h2 id="header-dinner">Dinner</h2>
                    <ul class="food-list" id="list-dinner"></ul>
                    <div class="add-food-controls">
                        <select id="select-dinner" class="food-select"></select>
                        <input type="number" id="qty-dinner" value="1" min="0.5" step="0.5" class="qty-input">
                        <button class="add-btn" onclick="addFood('dinner')">+</button>
                    </div>
                </div>

                <div class="card meal-section" id="section-snack">
                    <h2 id="header-snack">Snacks</h2>
                    <ul class="food-list" id="list-snack"></ul>
                    <div class="add-food-controls">
                        <select id="select-snack" class="food-select"></select>
                        <input type="number" id="qty-snack" value="1" min="0.5" step="0.5" class="qty-input">
                        <button class="add-btn" onclick="addFood('snack')">+</button>
                    </div>
                </div>

            </div>

            <div class="summary-column">
                <div class="card summary-card sticky">
                    <h2 id="header-summary">Daily Summary</h2>
                    
                    <div class="total-calories">
                        <span id="display-total-cals">0</span>
                        <small>kcal</small>
                    </div>

                    <hr>

                    <div class="macros">
                        <div class="macro-item">
                            <span class="macro-label" id="label-protein">Protein</span>
                            <span class="macro-val" id="val-protein">0g</span>
                        </div>
                        <div class="macro-item">
                            <span class="macro-label" id="label-carbs">Carbs</span>
                            <span class="macro-val" id="val-carbs">0g</span>
                        </div>
                        <div class="macro-item">
                            <span class="macro-label" id="label-fat">Fat</span>
                            <span class="macro-val" id="val-fat">0g</span>
                        </div>
                    </div>

                    <div id="ai-suggestion-area" style="display:none; margin-top: 20px;">
                        <p class="ai-text">AI Recommendation loading...</p>
                    </div>
                </div>
            </div>
        </div>
    </main>

    <script src="app.js"></script>
</body>
</html>
