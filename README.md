<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ZaboloteVPN</title>

<script src="https://telegram.org/js/telegram-web-app.js"></script>

<style>
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg, #38bdf8, #22c55e);
    color: white;
    text-align: center;
}

.screen {
    display: none;
    padding: 20px;
}

.active {
    display: block;
}

.card {
    background: rgba(255,255,255,0.15);
    backdrop-filter: blur(10px);
    border-radius: 20px;
    padding: 20px;
    margin: 15px 0;
}

button {
    width: 100%;
    padding: 15px;
    margin-top: 10px;
    border: none;
    border-radius: 15px;
    font-size: 16px;
    cursor: pointer;
    color: white;
    font-weight: bold;
    transition: 0.3s;
}

button:hover {
    transform: scale(1.05);
}

.basic { background: #22c55e; }
.premium { background: #3b82f6; }
.vip { background: #a855f7; }
.back { background: #64748b; }
.buy { background: #f59e0b; }

h1 {
    margin-top: 20px;
}
</style>
</head>

<body>

<!-- Главный экран -->
<div id="home" class="screen active">
    <h1>🌴 ZaboloteVPN</h1>
    <p>Выберите тариф</p>

    <div class="card">
        <button class="basic" onclick="openTariff('Базовый', '100₽ / месяц')">⚡ Базовый</button>
        <button class="premium" onclick="openTariff('Премиум', '249₽ / 3 месяца')">⭐ Премиум</button>
        <button class="vip" onclick="openTariff('VIP', '799₽ / 12 месяцев')">💎 VIP</button>
    </div>

    <div class="card">
        <button onclick="openRef()">🎁 Реферальная система</button>
    </div>
</div>

<!-- Экран тарифа -->
<div id="tariff" class="screen">
    <h1 id="tariffName"></h1>
    <p id="tariffPrice"></p>

    <div class="card">
        <button class="buy" onclick="buy()">💳 Купить</button>
        <button class="back" onclick="goHome()">⬅️ Назад</button>
    </div>
</div>

<!-- Рефералка -->
<div id="ref" class="screen">
    <h1>🎁 Реферальная система</h1>

    <div class="card">
        <p>Получайте 10% с каждого друга</p>
        <p>Выплаты 1 числа каждого месяца</p>
    </div>

    <button class="back" onclick="goHome()">⬅️ Назад</button>
</div>

<script>
const tg = window.Telegram.WebApp;
tg.expand();

let selectedPlan = "";

// открыть тариф
function openTariff(name, price) {
    selectedPlan = name;
    document.getElementById("tariffName").innerText = name;
    document.getElementById("tariffPrice").innerText = price;

    showScreen("tariff");
}

// открыть рефералку
function openRef() {
    showScreen("ref");
}

// назад
function goHome() {
    showScreen("home");
}

// переключение экранов
function showScreen(id) {
    document.querySelectorAll(".screen").forEach(el => el.classList.remove("active"));
    document.getElementById(id).classList.add("active");
}

// покупка → отправка в бот
function buy() {
    tg.sendData(selectedPlan);
}
</script>

</body>
</html>
