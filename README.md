#Project Title:
#Interactive Stopwatch Web App
#Description:
#This web-based stopwatch app allows users to start, pause, reset, and record lap times with high accuracy. It provides a clean, responsive UI and displays time in minutes, seconds, and milliseconds. Ideal for sports, study sessions, or productivity tracking.

#coding section

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopwatch App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f4;
      text-align: center;
      padding: 50px;
    }

    .stopwatch {
      background: #fff;
      padding: 30px;
      border-radius: 10px;
      display: inline-block;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }

    #display {
      font-size: 48px;
      margin-bottom: 20px;
    }

    .buttons button {
      padding: 10px 20px;
      margin: 5px;
      font-size: 16px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    .buttons button:hover {
      background-color: #ddd;
    }

    #laps {
      margin-top: 20px;
      text-align: left;
      max-height: 200px;
      overflow-y: auto;
    }

    #laps li {
      margin-bottom: 5px;
      background: #eee;
      padding: 5px 10px;
      border-radius: 4px;
    }
  </style>
</head>
<body>

  <div class="stopwatch">
    <div id="display">00:00:00.000</div>
    <div class="buttons">
      <button onclick="start()">Start</button>
      <button onclick="pause()">Pause</button>
      <button onclick="reset()">Reset</button>
      <button onclick="lap()">Lap</button>
    </div>
    <ul id="laps"></ul>
  </div>

  <script>
    let startTime = 0;
    let elapsedTime = 0;
    let timerInterval;

    function formatTime(ms) {
      const date = new Date(ms);
      const minutes = String(date.getUTCMinutes()).padStart(2, '0');
      const seconds = String(date.getUTCSeconds()).padStart(2, '0');
      const milliseconds = String(date.getUTCMilliseconds()).padStart(3, '0');
      return `${minutes}:${seconds}.${milliseconds}`;
    }

    function updateDisplay() {
      const time = Date.now() - startTime + elapsedTime;
      document.getElementById("display").innerText = formatTime(time);
    }

    function start() {
      if (!timerInterval) {
        startTime = Date.now();
        timerInterval = setInterval(updateDisplay, 10);
      }
    }

    function pause() {
      if (timerInterval) {
        elapsedTime += Date.now() - startTime;
        clearInterval(timerInterval);
        timerInterval = null;
      }
    }

    function reset() {
      clearInterval(timerInterval);
      timerInterval = null;
      startTime = 0;
      elapsedTime = 0;
      document.getElementById("display").innerText = "00:00:00.000";
      document.getElementById("laps").innerHTML = "";
    }

    function lap() {
      if (timerInterval) {
        const time = Date.now() - startTime + elapsedTime;
        const lapTime = formatTime(time);
        const lapItem = document.createElement("li");
        lapItem.innerText = `Lap: ${lapTime}`;
        document.getElementById("laps").appendChild(lapItem);
      }
    }
  </script>

</body>
</html>


