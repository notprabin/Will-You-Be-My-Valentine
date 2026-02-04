<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Be My Valentine?</title>

<style>
  body {
    margin: 0;
    height: 100vh;
    background: #800020;
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Poppins', sans-serif;
    overflow: hidden;
  }

  .card {
    background: #fff;
    padding: 40px 50px;
    border-radius: 20px;
    text-align: center;
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);
    width: 320px;
    z-index: 2;
  }

  h1 {
    color: #800020;
    margin-bottom: 30px;
  }

  .buttons {
    position: relative;
    height: 80px;
  }

  button {
    padding: 12px 28px;
    border: none;
    border-radius: 30px;
    font-size: 18px;
    cursor: pointer;
    position: absolute;
    transition: all 0.25s ease;
  }

  #yesBtn {
    background: #800020;
    color: white;
    left: 50%;
    transform: translateX(-120%);
  }

  #noBtn {
    background: #ddd;
    left: 50%;
    transform: translateX(20%);
  }

  /* Floating hearts */
  .heart {
    position: absolute;
    bottom: -20px;
    font-size: 20px;
    animation: floatUp 6s linear infinite;
    opacity: 0.8;
  }

  @keyframes floatUp {
    0% {
      transform: translateY(0) scale(1);
      opacity: 1;
    }
    100% {
      transform: translateY(-100vh) scale(1.5);
      opacity: 0;
    }
  }
</style>
</head>

<body>

<div class="card">
  <h1>Will you be my Valentine? 💖</h1>
  <div class="buttons">
    <button id="yesBtn">Yes 💘</button>
    <button id="noBtn">No 😭</button>
  </div>
</div>

<audio id="crySound">
  <source src="cry.mp3" type="audio/mpeg">
</audio>

<script>
  const noBtn = document.getElementById("noBtn");
  const yesBtn = document.getElementById("yesBtn");
  const crySound = document.getElementById("crySound");

  let noScale = 1;
  let yesScale = 1;

  // No button runs away
  noBtn.addEventListener("mouseenter", () => {
    const x = Math.random() * 220 - 110;
    const y = Math.random() * 120 - 60;
    noBtn.style.transform = `translate(${x}px, ${y}px) scale(${noScale})`;
  });

  // Clicking NO
  noBtn.addEventListener("click", () => {
    crySound.currentTime = 0;
    crySound.play();

    noScale -= 0.15;
    yesScale += 0.15;

    if (noScale < 0.4) noScale = 0.4;

    noBtn.style.transform = `scale(${noScale})`;
    yesBtn.style.transform = `scale(${yesScale}) translateX(-120%)`;
  });

  // YES clicked
  yesBtn.addEventListener("click", () => {
    document.body.innerHTML = `
      <div style="
        height:100vh;
        width:100%;
        display:flex;
        flex-direction:column;
        justify-content:center;
        align-items:center;
        background:#800020;
        text-align:center;
        color:#000000;
        font-family:Poppins;
        position:relative;
        overflow:hidden;">
        
        <h1 style="font-size:3rem; background:white; padding:30px; border-radius:20px;">
          YAYYYY 💖🥰<br><br>
          Jenika, you’re my Valentine 💕
        </h1>

        <div style="font-size:5rem; margin-top:20px;">
          🧸❤️
        </div>
      </div>
    `;

    createHearts();
  });

  // Create floating hearts
  function createHearts() {
    setInterval(() => {
      const heart = document.createElement("div");
      heart.classList.add("heart");
      heart.innerHTML = "❤️";
      heart.style.left = Math.random() * 100 + "vw";
      heart.style.fontSize = Math.random() * 20 + 20 + "px";
      heart.style.animationDuration = Math.random() * 3 + 4 + "s";
      document.body.appendChild(heart);

      setTimeout(() => {
        heart.remove();
      }, 7000);
    }, 300);
  }
</script>

</body>
</html>
