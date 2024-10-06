# Music-Player
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>Simple Music Player</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
    }
    .player {
      background-color: #fff;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      text-align: center;
      width: 300px;
    }
    .player h2 {
      font-size: 1.5em;
      margin-bottom: 10px;
    }
    .controls {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .controls button {
      background-color: #007BFF;
      color: white;
      border: none;
      padding: 10px;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .controls button:hover {
      background-color: #0056b3;
    }
    .progress-bar {
      width: 100%;
      background-color: #ddd;
      border-radius: 5px;
      margin: 15px 0;
      height: 10px;
    }
    .progress {
      background-color: #007BFF;
      height: 100%;
      width: 0%;
      border-radius: 5px;
    }
    .song-info {
      margin: 15px 0;
      font-size: 1.1em;
    }
  </style>
</head>
<body>

  <div class="player">
    <h2>Music Player</h2>
    <div class="song-info" id="song-title">Song 1</div>
    <div class="progress-bar">
      <div class="progress" id="progress"></div>
    </div>
    <div class="controls">
      <button id="prev">Prev</button>
      <button id="play-pause">Play</button>
      <button id="next">Next</button>
    </div>
  </div>

  <script>
    const songs = [
      { title: "Song 1", src: "path/to/song1.mp3" },
      { title: "Song 2", src: "path/to/song2.mp3" },
      { title: "Song 3", src: "path/to/song3.mp3" }
    ];

    let currentSongIndex = 0;
    let isPlaying = false;
    const audio = new Audio(songs[currentSongIndex].src);

    const songTitle = document.getElementById('song-title');
    const playPauseBtn = document.getElementById('play-pause');
    const prevBtn = document.getElementById('prev');
    const nextBtn = document.getElementById('next');
    const progressBar = document.getElementById('progress');

    // Play or Pause the song
    function togglePlayPause() {
      if (isPlaying) {
        audio.pause();
        playPauseBtn.innerText = "Play";
      } else {
        audio.play();
        playPauseBtn.innerText = "Pause";
      }
      isPlaying = !isPlaying;
    }

    
    function updateSong() {
      songTitle.innerText = songs[currentSongIndex].title;
      audio.src = songs[currentSongIndex].src;
      isPlaying = false;
      togglePlayPause();
    }

    
    function playNext() {
      currentSongIndex = (currentSongIndex + 1) % songs.length;
      updateSong();
    }

    
    function playPrev() {
      currentSongIndex = (currentSongIndex - 1 + songs.length) % songs.length;
      updateSong();
    }

    
    audio.addEventListener('timeupdate', () => {
      const progressPercentage = (audio.currentTime / audio.duration) * 100;
      progressBar.style.width = progressPercentage + "%";
    });

    
    playPauseBtn.addEventListener('click', togglePlayPause);
    nextBtn.addEventListener('click', playNext);
    prevBtn.addEventListener('click', playPrev);
  </script>

</body>
</html>
