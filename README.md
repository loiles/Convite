<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Convite Interativo</title>
  <style>
    body {
      margin: 0;
      font-family: 'Poppins', sans-serif;
      background: black;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      overflow: hidden;
      color: white;
    }

    /* Cena inicial */
    .convite {
      position: relative;
      cursor: pointer;
      animation: pulse 2s infinite;
    }

    .convite img {
      width: 350px;
      border-radius: 12px;
      box-shadow: 0 8px 25px rgba(0,0,0,0.6);
    }

    @keyframes pulse {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.05); }
    }

    /* Tela preta de transição */
    .fade {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: black;
      opacity: 0;
      pointer-events: none;
      transition: opacity 1.5s ease;
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
    }

    .fade.active {
      opacity: 1;
      pointer-events: all;
    }

    /* Partículas */
    .star {
      position: absolute;
      width: 3px;
      height: 3px;
      background: white;
      border-radius: 50%;
      opacity: 0.8;
      animation: twinkle linear infinite;
    }

    @keyframes twinkle {
      from { transform: translateY(0); opacity: 1; }
      to { transform: translateY(-200px); opacity: 0; }
    }

    /* Cena de detalhes */
    .detalhes {
      display: none;
      text-align: center;
      animation: fadeIn 2s ease forwards;
    }

    .detalhes.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(50px); }
      to { opacity: 1; transform: translateY(0); }
    }

    button {
      padding: 12px 20px;
      margin: 10px;
      border: none;
      border-radius: 6px;
      background: hotpink;
      color: white;
      font-size: 16px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: deeppink;
    }
  </style>
</head>
<body>

  <!-- Cena inicial -->
  <div class="convite" id="convite">
    <img src="convite.jpg" alt="Convite Especial">
  </div>

  <!-- Tela preta de transição -->
  <div class="fade" id="fade"></div>

  <!-- Cena de detalhes -->
  <div class="detalhes" id="detalhes">
    <h1>✨ Convite Especial ✨</h1>
    <button>📅 Data: 15 de Outubro 2025</button><br>
    <button>⏰ Hora: 20h00</button><br>
    <button>📍 Local: Paris, França</button><br>
    <button onclick="confirmar()">✅ Confirmar Presença (RSVP)</button>
  </div>

  <audio id="sound" src="sound.mp3" preload="auto"></audio>

  <script>
    const convite = document.getElementById("convite");
    const fade = document.getElementById("fade");
    const detalhes = document.getElementById("detalhes");
    const sound = document.getElementById("sound");

    convite.addEventListener("click", () => {
      sound.play();
      fade.classList.add("active");

      // partículas
      for (let i = 0; i < 40; i++) {
        let star = document.createElement("div");
        star.className = "star";
        star.style.left = Math.random() * 100 + "vw";
        star.style.top = Math.random() * 100 + "vh";
        star.style.animationDuration = (Math.random() * 3 + 2) + "s";
        fade.appendChild(star);
      }

      // após a animação mostrar os detalhes
      setTimeout(() => {
        fade.classList.remove("active");
        convite.style.display = "none";
        detalhes.classList.add("active");
      }, 2500);
    });

    function confirmar() {
      alert("🎉 Sua presença foi confirmada! Obrigado!");
    }
  </script>
</body>
</html>

