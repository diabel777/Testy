<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>ProChat – Strona główna</title>
  <link rel="icon" type="image/png" href="favicon.png" />
  <link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@600&display=swap" rel="stylesheet" />
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      font-family: 'Orbitron', sans-serif;
      background: #000;
      color: white;
      overflow-x: hidden;
      padding: 2rem;
    }
    canvas#stars {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: -1;
    }
    .container {
      text-align: center;
      max-width: 800px;
      margin: auto;
    }
    img { width: 150px; margin-bottom: 1rem; }
    h1 { font-size: 3rem; color: cyan; }
    .btns {
      margin: 1rem 0;
    }
    .btns a {
      background: #00ffff;
      color: black;
      padding: 0.6rem 1.2rem;
      margin: 0.5rem;
      border-radius: 10px;
      text-decoration: none;
      font-weight: bold;
      transition: 0.3s;
    }
    .btns a:hover { background: #00dddd; }
    .section {
      margin-top: 2rem;
      background: rgba(0,0,0,0.6);
      padding: 1.5rem;
      border-radius: 15px;
      box-shadow: 0 0 10px cyan;
    }
    .label { color: #00ffff; font-weight: bold; }
    .value { font-size: 2rem; }
    footer {
      margin-top: 3rem;
      font-size: 0.9rem;
      color: #aaa;
    }
  </style>
</head>
<body>
  <canvas id="stars"></canvas>

  <div class="container">
    <img src="ProChat.png" alt="ProChat Logo" />
    <h1>ProChat</h1>
    <div class="btns">
      <a href="https://discord.com/api/oauth2/authorize?client_id=1359864369793728743&permissions=1644971949559&scope=bot%20applications.commands">➕ Dodaj Bota</a>
      <a href="https://discord.gg/c7gcHErE">💬 Support</a>
      <a href="https://diabel777.github.io/informacje-/index.html">ℹ️ Informacje</a>
      <a href="https://diabel777.github.io/planowane/">🛠 Planowane</a>
    </div>

    <div class="section">
      🤖 <strong>ProChat</strong> to bot Discord z funkcjami moderacji, zabawy i automatyzacji.
      <br><br>⚠️ Obecnie bot jest w <b>trybie beta</b>. Nowości wkrótce!
      masz propozycję skontaktuj się z support
      znalazłeś błąd też skontaktuj się z support
      <br><br>spróbujemy zrobić co tydzień aktualizację bota 
    </div>

    <div class="section">
      <h2>📢 Aktualizacje</h2>
      <p>co zostało dodane
       <br>/ticket po polsku co się znajduje. bilet, raportem graczy, odwołania od bana, zgłoszenie ADM</p>
    </div>

    <div class="section">
      <h2>📊 Statystyki</h2>
      <p><span class="label">👤 Użytkownicy:</span> <span id="users" class="value">218</span></p>
      <p><span class="label">🌐 Serwery:</span> <span id="guilds" class="value">134</span></p>
      <p><span class="label">💻 Komendy:</span> <span id="commands" class="value">8</span></p>
    </div>

    <footer>
      © 2025 ProChat | Stworzone przez diable_777
    </footer>
  </div>

  <script>
    // Gwiazdy w tle
    const canvas = document.getElementById("stars");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
    let stars = [];

    for (let i = 0; i < 100; i++) {
      stars.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 1.5,
        dx: (Math.random() - 0.5) * 0.5,
        dy: (Math.random() - 0.5) * 0.5
      });
    }

    function drawStars() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.fillStyle = "white";
      stars.forEach(s => {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fill();
        s.x += s.dx;
        s.y += s.dy;
        if (s.x < 0 || s.x > canvas.width) s.dx *= -1;
        if (s.y < 0 || s.y > canvas.height) s.dy *= -1;
      });
      requestAnimationFrame(drawStars);
    }
    drawStars();

    // Statystyki z stats.json
    fetch("stats.json")
      .then(res => res.json())
      .then(data => {
        document.getElementById("users").textContent = data.users;
        document.getElementById("guilds").textContent = data.guilds;
        document.getElementById("commands").textContent = data.commands;
      })
      .catch(() => console.warn("Nie znaleziono stats.json"));
  </script>
</body>
</html>
