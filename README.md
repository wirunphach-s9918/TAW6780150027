<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Daily Meal Planner</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<header>
    <h1>Daily Meal Planner</h1>

    <div class="lang-switch">
        <button class="lang-btn" data-lang="th">ไทย</button>
        <button class="lang-btn" data-lang="en">EN</button>
        <button class="lang-btn" data-lang="zh">中文</button>
    </div>
</header>

<main>

    <section class="meal-section" id="breakfast-section">
        <h2 id="breakfast-title">Breakfast</h2>
body {
    font-family: sans-serif;
    margin: 20px;
    background: #fafafa;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

h1 {
    margin: 0;
}

.lang-switch button {
    margin-left: 5px;
    padding: 6px 10px;
    cursor: pointer;
}

.meal-section {
    margin-top: 30px;
    padding: 15px;
    background: white;
    border: 1px solid #ddd;
    border-radius: 6px;
}

.add-btn {
    padding: 5px 10px;
    font-size: 18px;
    cursor: pointer;
}

.meal-row {
    display: flex;
    align-items: center;
    margin-top: 10px;
    gap: 10px;
}

.meal-row select,
.meal-row input {
    padding: 6px;
}

#summary {
    margin-top: 40px;
    padding: 20px;
    background: #fff6d6;
    border: 1px solid #f5d46b;
    border-radius: 6px;
    font-size: 18px;
}
// ----------------------------
//  DATABASE OF FOODS
// ----------------------------
const foods = [
    { id: 1, name_th: "ข้าวกะเพราไก่", name_en: "Basil Chicken Rice", name_zh: "罗勒鸡饭", calories: 550 },
    { id: 2, name_th: "ข้าวผัดหมู", name_en: "Pork Fried Rice", name_zh: "猪肉炒饭", calories: 600 },
    { id: 3, name_th: "ส้มตำ", name_en: "Papaya Salad", name_zh: "木瓜沙拉", calories: 180 },
    { id: 4, name_th: "ผัดไทย", name_en: "Pad Thai", name_zh: "泰式炒粉", calories: 420 }
];

let currentLang = "th";  // th / en / zh

function getFoodName(food) {
    if (currentLang === "en") return food.name_en;
    if (currentLang === "zh") return food.name_zh;
    return food.name_th;
}

// ----------------------------
//  ADD MEAL ROW FUNCTION
// ----------------------------
function addMealRow(mealId) {
    const container = document.getElementById(`${mealId}-list`);

    const row = document.createElement("div");
    row.className = "meal-row";

    // Dropdown
    const select = document.createElement("select");
    foods.forEach(food => {
        const option = document.createElement("option");
        option.value = food.id;
        option.textContent = getFoodName(food);
        select.appendChild(option);
    });

    // Quantity Input
    const qty = document.createElement("input");
    qty.type = "number";
    qty.min = "1";
    qty.value = "1";

    // Kcal display
    const kcalSpan = document.createElement("span");
    kcalSpan.textContent = "0 kcal";

    function recalcRow() {
        const food = foods.find(f => f.id == select.value);
        const total = food.calories * Number(qty.value);
        kcalSpan.textContent = `${total} kcal`;
        updateSummary();
    }

    select.addEventListener("change", recalcRow);
    qty.addEventListener("input", recalcRow);

    row.appendChild(select);
    row.appendChild(qty);
    row.appendChild(kcalSpan);

    container.appendChild(row);

    recalcRow(); // initial calculate
}

// ----------------------------
// SUMMARY CALCULATION
// ----------------------------
function updateSummary() {
    const meals = ["breakfast", "lunch", "dinner", "snacks"];
    let total = 0;

    meals.forEach(meal => {
        const rows = document.querySelectorAll(`#${meal}-list .meal-row`);
        rows.forEach(row => {
            const kcal = row.querySelector("span").textContent.replace(" kcal", "");
            total += Number(kcal);
        });
    });

    document.getElementById("total-kcal").textContent = `Total: ${total} kcal`;
}

// ----------------------------
// LANGUAGE SWITCH
// ----------------------------
document.querySelectorAll(".lang-btn").forEach(btn => {
    btn.addEventListener("click", () => {
        currentLang = btn.dataset.lang;

        // UPDATE FOOD NAMES
        document.querySelectorAll("select").forEach(select => {
            const value = select.value; // keep previous choice
            select.innerHTML = "";

            foods.forEach(food => {
                const option = document.createElement("option");
                option.value = food.id;
                option.textContent = getFoodName(food);
                select.appendChild(option);
            });

            select.value = value;
        });

        // UPDATE TITLES
        if (currentLang === "th") {
            document.getElementById("breakfast-title").textContent = "มื้อเช้า";
            document.getElementById("lunch-title").textContent = "มื้อกลางวัน";
            document.getElementById("dinner-title").textContent = "มื้อเย็น";
            document.getElementById("snacks-title").textContent = "ของว่าง";
            document.getElementById("summary-title").textContent = "สรุปวันนี้";
        }

        if (currentLang === "en") {
            document.getElementById("breakfast-title").textContent = "Breakfast";
            document.getElementById("lunch-title").textContent = "Lunch";
            document.getElementById("dinner-title").textContent = "Dinner";
            document.getElementById("snacks-title").textContent = "Snacks";
            document.getElementById("summary-title").textContent = "Daily Summary";
        }

        if (currentLang === "zh") {
            document.getElementById("breakfast-title").textContent = "早餐";
            document.getElementById("lunch-title").textContent = "午餐";
            document.getElementById("dinner-title").textContent = "晚餐";
            document.getElementById("snacks-title").textContent = "点心";
            document.getElementById("summary-title").textContent = "每日总结";
        }
    });
});

// ----------------------------
// BUTTON SETUP
// ----------------------------
document.getElementById("add-breakfast").addEventListener("click", () => addMealRow("breakfast"));
document.getElementById("add-lunch").addEventListener("click", () => addMealRow("lunch"));
document.getElementById("add-dinner").addEventListener("click", () => addMealRow("dinner"));
document.getElementById("add-snacks").addEventListener("click", () => addMealRow("snacks"));

// create 1 row default
addMealRow("breakfast");
