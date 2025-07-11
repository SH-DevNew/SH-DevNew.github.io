<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SH_Dev | Developer Portfolio</title>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --primary-color: #4f46e5;
      --bg-dark: #0f0f0f;
      --bg-card: #1e1e1e;
      --text-light: #ccc;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Inter', sans-serif;
    }

    body {
      background: var(--bg-dark);
      color: #fff;
      line-height: 1.6;
      overflow-x: hidden;
    }

    nav {
      background: #1a1a1a;
      padding: 1rem 2rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
      box-shadow: 0 4px 8px rgba(0,0,0,0.4);
    }

    .logo {
      font-size: 1.8rem;
      font-weight: bold;
      color: var(--primary-color);
    }

    .nav-links a {
      margin: 0 1rem;
      text-decoration: none;
      color: #fff;
      font-weight: 500;
      position: relative;
      transition: color 0.3s ease;
    }

    .nav-links a::after {
      content: "";
      position: absolute;
      left: 0;
      bottom: -4px;
      width: 100%;
      height: 2px;
      background: var(--primary-color);
      transform: scaleX(0);
      transform-origin: right;
      transition: transform 0.3s ease;
    }

    .nav-links a:hover {
      color: var(--primary-color);
    }

    .nav-links a:hover::after {
      transform: scaleX(1);
      transform-origin: left;
    }

    .container {
      max-width: 1000px;
      margin: 3rem auto;
      padding: 0 1rem;
    }

    section {
      opacity: 0;
      transform: translateY(40px);
      transition: all 0.6s ease;
    }

    section.active {
      opacity: 1;
      transform: translateY(0);
    }

    h1, h2 {
      margin-bottom: 1rem;
      color: var(--primary-color);
    }

    p {
      color: var(--text-light);
    }

    .tab-section {
      display: flex;
      flex-wrap: wrap;
      gap: 1.5rem;
    }

    .tab-card {
      flex: 1 1 300px;
      background: var(--bg-card);
      padding: 1.5rem;
      border-radius: 16px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.3);
      transition: transform 0.3s;
    }

    .tab-card:hover {
      transform: translateY(-5px);
    }

    footer {
      text-align: center;
      padding: 2rem;
      margin-top: 4rem;
      background: #1a1a1a;
      color: #aaa;
      font-size: 0.9rem;
    }

    .hidden {
      display: none;
    }

    .play-button {
      position: fixed;
      bottom: 20px;
      left: 20px;
      background-color: #1a1a1a;
      color: var(--primary-color);
      border: 2px solid var(--primary-color);
      padding: 10px 16px;
      border-radius: 50px;
      cursor: pointer;
      font-weight: bold;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      transition: background-color 0.3s ease, transform 0.2s;
      z-index: 1000;
    }

    .play-button:hover {
      background-color: var(--primary-color);
      color: #fff;
      transform: scale(1.05);
    }

    /* Volume Slider Styles */
    #volumeControl {
      position: fixed;
      bottom: 70px;
      left: 20px;
      width: 120px;
      cursor: pointer;
      appearance: none;
      background: #333;
      height: 4px;
      border-radius: 5px;
      outline: none;
      z-index: 1000;
    }

    #volumeControl::-webkit-slider-thumb {
      appearance: none;
      width: 12px;
      height: 12px;
      background: var(--primary-color);
      border-radius: 50%;
      cursor: pointer;
      border: none;
      margin-top: -4px; /* Center the thumb */
    }

    #volumeControl::-moz-range-thumb {
      width: 12px;
      height: 12px;
      background: var(--primary-color);
      border-radius: 50%;
      cursor: pointer;
      border: none;
    }

    @media (max-width: 768px) {
      .nav-links {
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
      }
    }
  </style>
</head>
<body>
  <nav>
    <div class="logo">SH_Dev</div>
    <div class="nav-links">
      <a href="#" onclick="showTab('home')">Home</a>
      <a href="#" onclick="showTab('projects')">Projects</a>
      <a href="#" onclick="showTab('read-more')">Read More</a>
    </div>
  </nav>

  <div class="container">
    <section id="home" class="active">
      <h1>Hello, I am SH_Dev</h1>
      <p>I like coding and I like having fun. The languages I mainly code are Python and Lua.</p>
    </section>

    <section id="projects" class="hidden">
      <h2>Projects</h2>
      <div class="tab-section">
        <div class="tab-card">
          <h3>Project Purple</h3>
          <p>A cool scripting project that I’m building using Lua.</p>
        </div>
      </div>
    </section>

    <section id="read-more" class="hidden">
      <h2>Read More</h2>
      <p>I create projects for fun, but also to learn more about development environments and systems.<br /><br />
        When I'm not coding, I enjoy exploring music, tweaking UIs, and collaborating with others in the dev scene.</p>
    </section>
  </div>

  <audio id="audioPlayer" loop></audio>

  <button class="play-button" onclick="startAudio()">▶ Play Music</button>
  <input type="range" id="volumeControl" min="0" max="1" step="0.01" value="0.5" title="Volume Control" />

  <footer>
    &copy; SH_Dev. All rights reserved.
  </footer>

  <script>
    const audioPlayer = document.getElementById('audioPlayer');
    audioPlayer.src = "rockthatbody.mp3";
    audioPlayer.volume = 0.5;

    function startAudio() {
      audioPlayer.play().then(() => {
        document.querySelector('.play-button').style.display = 'none';
      }).catch(err => {
        alert("Playback failed. Try clicking again.");
        console.error("Audio play error:", err);
      });
    }

    const volumeSlider = document.getElementById('volumeControl');
    volumeSlider.addEventListener('input', () => {
      audioPlayer.volume = volumeSlider.value;
    });

    function showTab(tabId) {
      const sections = document.querySelectorAll('section');
      sections.forEach(section => {
        section.classList.remove('active');
        section.classList.add('hidden');
      });

      const target = document.getElementById(tabId);
      target.classList.remove('hidden');
      setTimeout(() => {
        target.classList.add('active');
      }, 10);
    }
  </script>
</body>
</html>
