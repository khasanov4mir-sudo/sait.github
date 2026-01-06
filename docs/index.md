<!DOCTYPE html><html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Обратный отсчёт до Нового года</title>
  <style>
    html, body {
      margin: 0;
      padding: 0;
      height: 100%;
      overflow: hidden;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
      background: radial-gradient(circle at top, #0b1d3a, #020617);
      color: white;
    }.center {
  position: relative;
  z-index: 2;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.timer {
  background: rgba(0,0,0,0.45);
  padding: 32px 40px;
  border-radius: 24px;
  backdrop-filter: blur(6px);
}

.timer h1 {
  margin-bottom: 20px;
  font-size: 2rem;
}

.time {
  display: flex;
  gap: 20px;
  font-size: 2.4rem;
  font-weight: 600;
  justify-content: center;
}

.block {
  min-width: 90px;
}

.label {
  display: block;
  font-size: 0.8rem;
  opacity: 0.8;
  margin-top: 6px;
}

.santa {
  position: fixed;
  right: 20px;
  bottom: 20px;
  font-size: 120px;
  z-index: 2;
}

.snowflake {
  position: fixed;
  top: -10px;
  color: white;
  pointer-events: none;
  user-select: none;
  z-index: 1;
  animation: fall linear;
}

@keyframes fall {
  to {
    transform: translateY(110vh);
  }
}

  </style>
</head>
<body>  <div class="center">
    <div class="timer">
      <h1>До Нового года осталось</h1>
      <div class="time">
        <div class="block"><span id="days">0</span><span class="label">дней</span></div>
        <div class="block"><span id="hours">00</span><span class="label">часов</span></div>
        <div class="block"><span id="minutes">00</span><span class="label">минут</span></div>
        <div class="block"><span id="seconds">00</span><span class="label">секунд</span></div>
      </div>
    </div>
  </div>  <div class="santa">🎅</div>  <script>
    function updateCountdown() {
      const now = new Date();
      const year = now.getFullYear() + 1;
      const newYear = new Date(year, 0, 1, 0, 0, 0);

      const diff = newYear.getTime() - now.getTime();
      if (diff <= 0) return;

      const totalSeconds = Math.floor(diff / 1000);
      const days = Math.floor(totalSeconds / 86400);
      const hours = Math.floor((totalSeconds % 86400) / 3600);
      const minutes = Math.floor((totalSeconds % 3600) / 60);
      const seconds = totalSeconds % 60;

      document.getElementById('days').textContent = days;
      document.getElementById('hours').textContent = String(hours).padStart(2, '0');
      document.getElementById('minutes').textContent = String(minutes).padStart(2, '0');
      document.getElementById('seconds').textContent = String(seconds).padStart(2, '0');
    }

    setInterval(updateCountdown, 1000);
    updateCountdown();

    const snowSymbols = ['❄','❅','❆'];

    function createSnowflake() {
      const snowflake = document.createElement('div');
      snowflake.className = 'snowflake';
      snowflake.textContent = snowSymbols[Math.floor(Math.random() * snowSymbols.length)];

      const size = Math.random() * 16 + 10;
      snowflake.style.fontSize = size + 'px';
      snowflake.style.left = Math.random() * 100 + 'vw';
      snowflake.style.opacity = Math.random() * 0.6 + 0.4;

      const duration = Math.random() * 6 + 6;
      snowflake.style.animationDuration = duration + 's';

      document.body.appendChild(snowflake);
      setTimeout(() => snowflake.remove(), duration * 1000);
    }

    setInterval(createSnowflake, 120);
  </script></body>
</html>