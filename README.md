<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>💛 For Gem 💛</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<style>
  body {
    margin: 0;
    height: 100vh;
    font-family: 'Poppins', 'Comic Sans MS', sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #fff1a8, #ffd1dc);
    overflow: hidden;
  }

  .card {
    background: white;
    padding: 30px;
    border-radius: 25px;
    text-align: center;
    box-shadow: 0 25px 50px rgba(0,0,0,0.2);
    max-width: 360px;
    z-index: 2;
    position: relative;
  }

  h1 {
    color: #e63946;
    margin-bottom: 15px;
  }

  img {
    width: 240px;
    border-radius: 15px;
    margin-bottom: 20px;
  }

  .buttons {
    display: flex;
    justify-content: center;
    gap: 20px;
    position: relative;
    height: 50px;
  }

  button {
    font-size: 1.1em;
    padding: 12px 24px;
    border-radius: 30px;
    border: none;
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative;
  }

  #yesBtn {
    background: #ff4d6d;
    color: white;
    z-index: 2;
  }

  #noBtn {
    background: #adb5bd;
    color: white;
    z-index: 1;
  }

  .yes-screen {
    position: fixed;
    inset: 0;
    background: linear-gradient(135deg, #ffafcc, #ffc8dd);
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    animation: fadeIn 0.6s ease;
  }

  .yes-screen h1 {
    font-size: 2.8em;
    color: #fff;
    margin-bottom: 20px;
  }

  .yes-screen p {
    color: white;
    font-size: 1.4em;
  }

  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
</style>
</head>

<body>

<div class="card" id="mainCard">
  <h1>Will you be my Valentine, Gem? 💛</h1>

  <img src="https://media1.tenor.com/m/kutFNFXxSIsAAAAd/minion-minion-loves.gif"
       alt="Minion pulling out heart">

  <div class="buttons">
    <button id="yesBtn">Yes 💖</button>
    <button id="noBtn">No 😢</button>
  </div>
</div>

<script>
  const noBtn = document.getElementById("noBtn");
  const yesBtn = document.getElementById("yesBtn");
  const card = document.getElementById("mainCard");
  let scale = 1;
  let moving = false;

  // Standard Yes/No position initially
  noBtn.style.transform = 'translate(0px, 0px)';

  noBtn.addEventListener("click", () => {
    if (!moving) {
      moving = true;
      // Change to absolute so it can move inside card
      noBtn.style.position = "absolute";
      const rect = noBtn.getBoundingClientRect();
      const cardRect = card.getBoundingClientRect();
      noBtn.style.left = rect.left - cardRect.left + "px";
      noBtn.style.top = rect.top - cardRect.top + "px";
      moveNoButton();
    } else {
      scale *= 0.85;
      if (scale < 0.15) scale = 0.15;
      noBtn.style.transform = `translate(${noBtn.dataset.x}px, ${noBtn.dataset.y}px) scale(${scale})`;
      moveNoButton();
    }
  });

  function moveNoButton() {
    const padding = 5; // stay inside the card
    const maxX = card.offsetWidth - noBtn.offsetWidth - padding;
    const maxY = card.offsetHeight - noBtn.offsetHeight - padding;

    const x = Math.random() * maxX;
    const y = Math.random() * maxY;

    noBtn.dataset.x = x;
    noBtn.dataset.y = y;

    noBtn.style.transform = `translate(${x}px, ${y}px) scale(${scale})`;
  }

  yesBtn.addEventListener("click", () => {
    document.body.innerHTML = `
      <div class="yes-screen">
        <h1>YAY 💕</h1>
        <p>Best Valentine ever 💛</p>
        <p>I’m so lucky to have you, Gem 😘</p>
      </div>
    `;
  });
</script>

</body>
</html>
