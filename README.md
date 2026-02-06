<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>💘 Walentynka</title>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
  font-family: Arial, sans-serif;
}

body {
  background-image: url("start.jpg");
  background-size: cover;
  background-position: center;
  transition: background-image 0.8s ease;
}

.overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.35);
}

#hearts, #confetti {
  position: fixed;
  inset: 0;
  pointer-events: none;
}

.heart {
  position: absolute;
  bottom: -40px;
  font-size: 22px;
  animation: floatUp linear infinite;
}

@keyframes floatUp {
  to { transform: translateY(-120vh); opacity: 0; }
}

.confetti-heart {
  position: absolute;
  font-size: 20px;
  animation: explode 1.5s ease-out forwards;
}

@keyframes explode {
  to {
    transform: translate(var(--x), var(--y)) rotate(720deg);
    opacity: 0;
  }
}

.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 90%;
  text-align: center;
  color: white;
  z-index: 2;
}

h1 {
  font-size: 1.8em;
  text-shadow: 2px 2px 8px #000;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 25px;
  margin-top: 30px;
}

button {
  font-size: 1.2em;
  padding: 12px 30px;
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
  position: relative;
}

.hidden {
  display: none;
}

#music {
  width: 0;
  height: 0;
  overflow: hidden;
}
</style>
</head>

<body>

<div class="overlay"></div>
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
  <h1>Bardzo mnie to cieszy ❤️<br>bądź gotowa 14.02.2026</h1>
</div>

<div id="music">
  <iframe id="ytplayer" allow="autoplay"></iframe>
</div>

<script>
const hearts = document.getElementById("hearts");
const confetti = document.getElementById("confetti");
const noBtn = document.getElementById("no");
const yesBtn = document.getElementById("yes");
const question = document.getElementById("question");
const result = document.getElementById("result");
const ytplayer = document.getElementById("ytplayer");

// serca w tle
function createHeart(extra=false) {
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤️";
  h.style.left = Math.random()*100 + "%";
  h.style.animationDuration = (extra ? 2 : Math.random()*3+4) + "s";
  hearts.appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(createHeart, 300);

// konfetti
function confettiBurst() {
  for (let i=0; i<40; i++) {
    const c = document.createElement("div");
    c.className = "confetti-heart";
    c.textContent = "❤️";
    c.style.left = "50%";
    c.style.top = "50%";
    c.style.setProperty("--x", (Math.random()*600-300)+"px");
    c.style.setProperty("--y", (Math.random()*600-300)+"px");
    confetti.appendChild(c);
    setTimeout(()=>c.remove(),1500);
  }
}

// NIE ucieka, ale jest widoczne
function moveNo() {
  noBtn.style.position = "fixed";
  noBtn.style.left = Math.random()*(window.innerWidth-120)+"px";
  noBtn.style.top = Math.random()*(window.innerHeight-60)+"px";
}
noBtn.addEventListener("mouseenter", moveNo);
noBtn.addEventListener("touchstart", moveNo);

// TAK
yesBtn.addEventListener("click", () => {
  confettiBurst();
  document.body.style.backgroundImage = 'url("yes.jpg")';
  question.classList.add("hidden");
  result.classList.remove("hidden");

  setInterval(()=>createHeart(true),120);

  ytplayer.src =
    "https://www.youtube.com/embed/RB-RcX5DS5A?autoplay=1&loop=1&playlist=RB-RcX5DS5A";
});
</script>

</body>
</html>
