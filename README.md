<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>💘 Walentynka 💘</title>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
  font-family: Arial, sans-serif;
  background: linear-gradient(180deg, #ff9a9e, #fad0c4);
}

#hearts, #confetti {
  position: fixed;
  width: 100%;
  height: 100%;
  pointer-events: none;
  overflow: hidden;
}

.heart {
  position: absolute;
  bottom: -40px;
  font-size: 24px;
  animation: floatUp linear infinite;
}

@keyframes floatUp {
  from { transform: translateY(0); opacity: 1; }
  to { transform: translateY(-120vh); opacity: 0; }
}

/* konfetti-serca */
.confetti-heart {
  position: absolute;
  font-size: 20px;
  animation: explode 1.8s ease-out forwards;
}

@keyframes explode {
  0% {
    transform: translate(0,0) scale(1) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translate(var(--x), var(--y)) scale(0.6) rotate(720deg);
    opacity: 0;
  }
}

.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  width: 90%;
}

h1 {
  font-size: 1.8em;
  font-weight: bold;
  color: #fff;
  text-shadow: 2px 2px 6px rgba(0,0,0,0.3);
  margin-bottom: 30px;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
}

button {
  font-size: 1.2em;
  padding: 12px 26px;
  border-radius: 30px;
  border: none;
}

#yes {
  background: #ff4d6d;
  color: white;
}

#no {
  background: white;
  color: #ff4d6d;
}

.hidden { display: none; }

#result {
  color: white;
}

#result img {
  max-width: 90%;
  border-radius: 20px;
  margin-top: 20px;
}

#music {
  width: 0;
  height: 0;
  overflow: hidden;
}
</style>
</head>

<body>

<div id="hearts"></div>
<div id="confetti"></div>

<div class="container" id="question">
  <h1>Bombelku, czy będziesz moją walentynką?</h1>
  <div class="buttons">
    <button id="yes">Tak</button>
    <button id="no">Nie</button>
  </div>
</div>

<div class="container hidden" id="result">
  <h2>Bardzo mnie to cieszy ❤️<br>bądź gotowa 14.02.2026</h2>
  <img src="https://media.giphy.com/media/3oz8xIsloV7zOmt81G/giphy.gif">
</div>

<div id="music">
  <iframe id="ytplayer" allow="autoplay"></iframe>
</div>

<script>
// tło – serca
function createHeart(extra = false) {
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤️";
  h.style.left = Math.random() * 100 + "%";
  h.style.fontSize = (Math.random() * 20 + 16) + "px";
  h.style.animationDuration = (extra ? 2 : Math.random() * 3 + 4) + "s";
  document.getElementById("hearts").appendChild(h);
  setTimeout(() => h.remove(), 7000);
}
setInterval(() => createHeart(), 300);

// konfetti-serca
function confettiBurst() {
  const centerX = window.innerWidth / 2;
  const centerY = window.innerHeight / 2;

  for (let i = 0; i < 40; i++) {
    const c = document.createElement("div");
    c.className = "confetti-heart";
    c.textContent = "❤️";
    c.style.left = centerX + "px";
    c.style.top = centerY + "px";
    c.style.fontSize = (Math.random() * 18 + 14) + "px";

    c.style.setProperty("--x", (Math.random() * 600 - 300) + "px");
    c.style.setProperty("--y", (Math.random() * 600 - 300) + "px");

    document.getElementById("confetti").appendChild(c);
    setTimeout(() => c.remove(), 2000);
  }
}

// uciekające NIE
const noBtn = document.getElementById("no");
function moveNo() {
  noBtn.style.position = "fixed";
  noBtn.style.left = Math.random() * (window.innerWidth - 100) + "px";
  noBtn.style.top = Math.random() * (window.innerHeight - 60) + "px";
}
noBtn.addEventListener("mouseenter", moveNo);
noBtn.addEventListener("touchstart", moveNo);

// klik TAK
document.getElementById("yes").addEventListener("click", () => {
  confettiBurst();
  document.getElementById("question").classList.add("hidden");
  document.getElementById("result").classList.remove("hidden");

  setInterval(() => createHeart(true), 120);

  document.getElementById("ytplayer").src =
    "https://www.youtube.com/embed/RB-RcX5DS5A?autoplay=1&loop=1&playlist=RB-RcX5DS5A";
});
</script>

</body>
</html>