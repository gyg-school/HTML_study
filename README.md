# HTML_study
## 3초에 맞추는 타이머 코드
```html
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Timer</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }

        .main-container {
            text-align: center;
        }

        #timer {
            font-size: 48px;
            color: red;
            margin-bottom: 30px;
        }

        #targetTime {
            font-size: 24px;
            margin-top: 50px;
        }

        button {
            font-size: 18px;
            margin: 0 10px;
            padding: 10px 20px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="main-container">
        <h1 id="timer">00:00:00</h1>
        <button onclick="startTimer()">시작</button>
        <button onclick="stopTimer()">멈춤</button>
        <button onclick="resetTimer()">초기화</button>
    </div>
    <p id="targetTime">3.00초에 맞추세요!</p>

    <script>
        let timerInterval;
        let startTime;
        let elapsedTime = 0;
        const timerDisplay = document.getElementById("timer");

        function startTimer() {
            startTime = Date.now() - elapsedTime;
            timerInterval = setInterval(updateTimer, 10);
        }

        function updateTimer() {
            const elapsedTime = Date.now() - startTime;
            const minutes = Math.floor(elapsedTime / 60000);
            const seconds = Math.floor((elapsedTime % 60000) / 1000);
            const milliseconds = Math.floor(elapsedTime % 1000 / 10);

            timerDisplay.textContent = formatTime(minutes) + ":" + formatTime(seconds) + ":" + formatTime(milliseconds);
        }

        function formatTime(time) {
            return time < 10 ? "0" + time : time;
        }

        function stopTimer() {
            clearInterval(timerInterval);
            elapsedTime = Date.now() - startTime;
            updateTargetTime(elapsedTime);
        }

        function resetTimer() {
            clearInterval(timerInterval);
            elapsedTime = 0;
            timerDisplay.textContent = "00:00:00";
            document.getElementById("targetTime").textContent = "3.00초에 맞추세요!";
        }

        function updateTargetTime(elapsedTime) {
            const targetTimeText = (elapsedTime / 1000).toFixed(2) + "초에 맞췄습니다!";
            document.getElementById("targetTime").textContent = targetTimeText;
        }
    </script>
</body>
</html>
```
