<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Modern Music Player</title>

<style>
body {
    margin: 0;
    height: 100vh;
    background: linear-gradient(135deg, #0f172a, #1e293b);
    font-family: "Segoe UI", Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #fff;
}

.player {
    width: 360px;
    background: rgba(255,255,255,0.05);
    backdrop-filter: blur(15px);
    border-radius: 25px;
    padding: 25px;
    box-shadow: 0 30px 60px rgba(0,0,0,0.5);
    text-align: center;
}

.cover {
    width: 200px;
    height: 200px;
    border-radius: 20px;
    background: linear-gradient(135deg, #38bdf8, #6366f1);
    margin: 0 auto 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 50px;
}

.song-title {
    font-size: 18px;
    font-weight: 600;
}

.artist {
    font-size: 14px;
    opacity: 0.8;
    margin-bottom: 15px;
}

.controls {
    display: flex;
    justify-content: center;
    gap: 20px;
    margin: 15px 0;
}

button {
    background: #38bdf8;
    border: none;
    border-radius: 50%;
    width: 55px;
    height: 55px;
    font-size: 20px;
    cursor: pointer;
    transition: 0.3s;
}

button:hover {
    background: #0ea5e9;
    transform: scale(1.1);
}

.progress-container {
    width: 100%;
    height: 6px;
    background: #1e293b;
    border-radius: 10px;
    margin: 10px 0;
    cursor: pointer;
}

.progress {
    height: 100%;
    width: 0%;
    background: #38bdf8;
    border-radius: 10px;
}

.volume {
    margin-top: 10px;
}

input[type=range] {
    width: 100%;
}
</style>
</head>
<body>

<div class="player">
    <div class="cover">🎵</div>
    <div class="song-title" id="title">Demo Track</div>
    <div class="artist">Unknown Artist</div>

    <div class="progress-container" id="progressContainer">
        <div class="progress" id="progress"></div>
    </div>

    <div class="controls">
        <button onclick="togglePlay()">▶</button>
    </div>

    <div class="volume">
        Volume
        <input type="range" min="0" max="1" step="0.01" value="0.5" id="volume">
    </div>
</div>

<audio id="audio">
    <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
</audio>

<script>
const audio = document.getElementById("audio");
const progress = document.getElementById("progress");
const progressContainer = document.getElementById("progressContainer");
const volumeControl = document.getElementById("volume");
let isPlaying = false;

function togglePlay() {
    if (isPlaying) {
        audio.pause();
    } else {
        audio.play();
    }
}

audio.onplay = () => isPlaying = true;
audio.onpause = () => isPlaying = false;

audio.ontimeupdate = () => {
    const percent = (audio.currentTime / audio.duration) * 100;
    progress.style.width = percent + "%";
};

progressContainer.addEventListener("click", e => {
    const width = progressContainer.clientWidth;
    const clickX = e.offsetX;
    audio.currentTime = (clickX / width) * audio.duration;
});

volumeControl.oninput = () => {
    audio.volume = volumeControl.value;
};
</script>

</body>
</html>
