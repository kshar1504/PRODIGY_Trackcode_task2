android_app
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Stopwatch</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div class="stopwatch">
        <div class="display">
            <span id="minutes">00</span>:<span id="seconds">00</span>:<span id="milliseconds">000</span>
        </div>
        <div class="controls">
            <button id="startPause">Start</button>
            <button id="reset">Reset</button>
            <button id="lap">Lap</button>
        </div>
        <ul id="laps"></ul>
    </div>

    <script src="script.js"></script>
</body>
</html>
body {
    font-family: Arial, sans-serif;
    text-align: center;
    margin: 50px;
}

.stopwatch {
    width: 300px;
    margin: 0 auto;
    border: 2px solid #ccc;
    padding: 20px;
    border-radius: 5px;
}

.display {
    font-size: 24px;
    margin-bottom: 10px;
}

.controls {
    margin-bottom: 10px;
}

button {
    margin: 0 5px;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
}

ul {
    list-style-type: none;
    padding: 0;
}

ul li {
    margin-bottom: 5px;
    font-size: 14px;
}
let timer; // To store the interval of the stopwatch
let startTime; // To store the start time of the current run
let pausedTime = 0; // To store the total paused time
let running = false; // To track if the stopwatch is running
let lapCounter = 1; // To count the number of laps

const minutesDisplay = document.getElementById('minutes');
const secondsDisplay = document.getElementById('seconds');
const millisecondsDisplay = document.getElementById('milliseconds');
const startPauseButton = document.getElementById('startPause');
const resetButton = document.getElementById('reset');
const lapButton = document.getElementById('lap');
const lapsList = document.getElementById('laps');

function formatTime(ms) {
    let minutes = Math.floor(ms / 60000);
    let seconds = Math.floor((ms % 60000) / 1000);
    let milliseconds = ms % 1000;
    return {
        'minutes': minutes < 10 ? '0' + minutes : minutes,
        'seconds': seconds < 10 ? '0' + seconds : seconds,
        'milliseconds': milliseconds < 10 ? '00' + milliseconds : (milliseconds < 100 ? '0' + milliseconds : milliseconds)
    };
}

function updateDisplay() {
    let elapsedTime = pausedTime;
    if (running) {
        elapsedTime += Date.now() - startTime;
    }
    let formattedTime = formatTime(elapsedTime);
    minutesDisplay.textContent = formattedTime.minutes;
    secondsDisplay.textContent = formattedTime.seconds;
    millisecondsDisplay.textContent = formattedTime.milliseconds;
}

function startPause() {
    if (running) {
        clearInterval(timer);
        pausedTime += Date.now() - startTime;
        startPauseButton.textContent = 'Resume';
        lapButton.disabled = true;
    } else {
        startTime = Date.now();
        timer = setInterval(updateDisplay, 10);
        startPauseButton.textContent = 'Pause';
        lapButton.disabled = false;
    }
    running = !running;
}

function reset() {
    clearInterval(timer);
    running = false;
    pausedTime = 0;
    startPauseButton.textContent = 'Start';
    lapButton.disabled = true;
    minutesDisplay.textContent = '00';
    secondsDisplay.textContent = '00';
    millisecondsDisplay.textContent = '000';
    lapsList.innerHTML = '';
    lapCounter = 1;
}

function lap() {
    if (running) {
        const lapTime = Date.now() - startTime + pausedTime;
        const formattedTime = formatTime(lapTime);
        const lapItem = document.createElement('li');
        lapItem.textContent = Lap ${lapCounter}: ${formattedTime.minutes}:${formattedTime.seconds}:${formattedTime.milliseconds};
        lapsList.appendChild(lapItem);
        lapCounter++;
    }
}

startPauseButton.addEventListener('click', startPause);
resetButton.addEventListener('click', reset);
lapButton.addEventListener('click', lap);
