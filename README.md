<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <title>Catch the Dot</title>
  <style>
    body { font-family: system-ui; display:flex; height:100vh; margin:0; align-items:center; justify-content:center; background:#111; color:#fff; }
    #box { width: 420px; height: 420px; border: 2px solid #444; position: relative; border-radius: 12px; background:#1a1a1a; }
    #dot { width: 38px; height: 38px; border-radius: 50%; position: absolute; cursor: pointer; background: #fff; }
    .row { display:flex; gap:14px; align-items:center; justify-content:space-between; margin-top:12px; }
    button { padding:8px 12px; border-radius:10px; border:0; cursor:pointer; }
  </style>
</head>
<body>
  <div>
    <h2 style="margin:0 0 10px 0;">Catch the Dot 🎯</h2>
    <div id="box"><div id="dot" title="Click me!"></div></div>
    <div class="row">
      <div>Score: <b id="score">0</b> | Time: <b id="time">20</b>s</div>
      <button id="start">Start</button>
    </div>
    <p style="opacity:.8; margin:10px 0 0 0;">Click the dot as many times as you can before time runs out.</p>
  </div>

  <script>
    const box = document.getElementById("box");
    const dot = document.getElementById("dot");
    const scoreEl = document.getElementById("score");
    const timeEl = document.getElementById("time");
    const startBtn = document.getElementById("start");

    let score = 0;
    let timeLeft = 20;
    let timer = null;
    let playing = false;

    function randPos() {
      const pad = 2;
      const maxX = box.clientWidth - dot.clientWidth - pad;
      const maxY = box.clientHeight - dot.clientHeight - pad;
      const x = Math.floor(Math.random() * (maxX + 1));
      const y = Math.floor(Math.random() * (maxY + 1));
      dot.style.left = x + "px";
      dot.style.top = y + "px";
    }

    function reset() {
      score = 0;
      timeLeft = 20;
      scoreEl.textContent = score;
      timeEl.textContent = timeLeft;
      randPos();
    }

    function start() {
      if (playing) return;
      playing = true;
      startBtn.textContent = "Restart";
      reset();

      clearInterval(timer);
      timer = setInterval(() => {
        timeLeft--;
        timeEl.textContent = timeLeft;
        if (timeLeft <= 0) end();
      }, 1000);
    }

    function end() {
      playing = false;
      clearInterval(timer);
      timer = null;
      alert("Time! Your score: " + score + " 🏁");
    }

    dot.addEventListener("click", () => {
      if (!playing) return;
      score++;
      scoreEl.textContent = score;
      randPos();
    });

    startBtn.addEventListener("click", start);

    // Put dot somewhere on load
    randPos();
  </script>
</body>
</html>
