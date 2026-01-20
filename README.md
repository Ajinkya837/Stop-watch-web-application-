<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Luxury Stopwatch</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- Google Font -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
        }

        body {
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background: linear-gradient(270deg, #ff0080, #7928ca, #2afadf, #00c6ff);
            background-size: 800% 800%;
            animation: gradientMove 12s ease infinite;
        }

        @keyframes gradientMove {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .stopwatch-container {
            width: 380px;
            padding: 35px;
            border-radius: 25px;
            background: rgba(255, 255, 255, 0.15);
            backdrop-filter: blur(15px);
            box-shadow: 0 30px 60px rgba(0, 0, 0, 0.4);
            text-align: center;
            color: #fff;
        }

        h1 {
            font-size: 28px;
            font-weight: 700;
            letter-spacing: 1px;
            margin-bottom: 20px;
            text-shadow: 0 0 15px rgba(255,255,255,0.4);
        }

        .time-display {
            font-size: 52px;
            font-weight: 700;
            margin: 25px 0;
            color: #fff;
            text-shadow:
                0 0 10px #00e5ff,
                0 0 20px #00e5ff,
                0 0 40px #00e5ff;
        }

        .buttons {
            display: flex;
            gap: 12px;
            margin-top: 20px;
        }

        button {
            flex: 1;
            padding: 14px;
            font-size: 15px;
            font-weight: 600;
            border: none;
            border-radius: 12px;
            cursor: pointer;
            transition: 0.3s ease;
            color: white;
        }

        .start {
            background: linear-gradient(135deg, #00ff87, #00c853);
            box-shadow: 0 0 15px rgba(0, 255, 135, 0.6);
        }

        .pause {
            background: linear-gradient(135deg, #ffd54f, #ff9100);
            box-shadow: 0 0 15px rgba(255, 193, 7, 0.6);
        }

        .reset {
            background: linear-gradient(135deg, #ff1744, #d50000);
            box-shadow: 0 0 15px rgba(255, 23, 68, 0.6);
        }

        button:hover {
            transform: translateY(-3px) scale(1.05);
            box-shadow: 0 0 25px rgba(255,255,255,0.6);
        }

        .laps {
            margin-top: 30px;
            max-height: 160px;
            overflow-y: auto;
            text-align: left;
        }

        .laps h3 {
            font-size: 16px;
            margin-bottom: 10px;
            color: #e0f7fa;
        }

        .lap-item {
            font-size: 14px;
            padding: 6px 0;
            border-bottom: 1px solid rgba(255,255,255,0.25);
            color: #ffffffcc;
        }

        .laps::-webkit-scrollbar {
            width: 6px;
        }

        .laps::-webkit-scrollbar-thumb {
            background: linear-gradient(#00e5ff, #7c4dff);
            border-radius: 10px;
        }
    </style>
</head>

<body>

<div class="stopwatch-container">
    <h1>Luxury Stopwatch</h1>

    <div class="time-display" id="display">00:00:00</div>

    <div class="buttons">
        <button class="start" onclick="start()">Start</button>
        <button class="pause" onclick="lap()">Lap</button>
        <button class="reset" onclick="reset()">Reset</button>
    </div>

    <div class="laps">
        <h3>Lap Records</h3>
        <div id="lapsList"></div>
    </div>
</div>

<script>
    let seconds = 0, minutes = 0, hours = 0;
    let interval = null;
    let running = false;
    let lapCount = 1;

    function updateDisplay() {
        document.getElementById("display").innerText =
            (hours < 10 ? "0" + hours : hours) + ":" +
            (minutes < 10 ? "0" + minutes : minutes) + ":" +
            (seconds < 10 ? "0" + seconds : seconds);
    }

    function stopwatch() {
        seconds++;
        if (seconds === 60) { seconds = 0; minutes++; }
        if (minutes === 60) { minutes = 0; hours++; }
        updateDisplay();
    }

    function start() {
        if (!running) {
            interval = setInterval(stopwatch, 1000);
            running = true;
        }
    }

    function lap() {
        if (running) {
            const lapTime = document.getElementById("display").innerText;
            const lapDiv = document.createElement("div");
            lapDiv.className = "lap-item";
            lapDiv.innerText = `Lap ${lapCount} → ${lapTime}`;
            document.getElementById("lapsList").prepend(lapDiv);
            lapCount++;
        }
    }

    function reset() {
        clearInterval(interval);
        running = false;
        seconds = minutes = hours = 0;
        lapCount = 1;
        updateDisplay();
        document.getElementById("lapsList").innerHTML = "";
    }
</script>

</body>
</html># Stop-watch-web-application-
Devloped Stop Watch web application using HTML Css Javascript 
