<!DOCTYPE html>
<html lang="pl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>💘 Walentynka 💘</title>

<style>
html, body {
  margin: 0;
  padding: 0;
  height: 100%;
  overflow: hidden;
  font-family: Arial, sans-serif;
}

body {
  background: url("start.jpg") center/cover no-repeat fixed;
  transition: background-image 1s ease-in-out;
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
  font-size: 24px;
  animation: floatUp linear infinite;
}

@keyframes floatUp {
  from { transform: translateY(0); opacity: 1; }
  to { transform: translateY(-120vh); opacity: 0; }
}

.confetti-heart {
  position: absolute;
  font-size: 20px;
  animation: explode 1.6s ease-out forwards;
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
  font-size: 1.9em;
  margin-bottom: 30px;
  text-shadow: 2px 2px 8px black;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 20px;
}

button {
  font-size: 1.2em;
  padding: 12px 28px;
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
  position: fixed;
}

.hidden { display: none; }

#result {
  font-size: 1.6em;
  text-shadow: 2px 2px 8px black;
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
  Bardzo mnie to cieszy ❤️<br>bądź gotowa 14.02.2026
</div>

<div id="music">
  <iframe id="ytplayer" allow="autoplay"></iframe>
</div>

<script>
// serca
function createHeart(extra=false) {
  const h = document.createElement("div");
  h.className = "heart";
  h.textContent = "❤️";
  h.style.left = Math.random()*100 + "%";
  h.style.fontSize = Math.random()*20+16 + "px";
  h.style.animationDuration = (extra?2:Math.random()*3+4)+"s";
  hearts.appendChild(h);
  setTimeout(()=>h.remove(),7000);
}
setInterval(()=>createHeart(),300);

// konfetti
function confetti() {
  for(let i=0;i<40;i++){
    const c=document.createElement("div");
    c.className="confetti-heart";
    c.textContent="❤️";
    c.style.left="50%";
    c.style.top="50%";
    c.style.setProperty("--x",(Math.random()*600-300)+"px");
    c.style.setProperty("--y",(Math.random()*600-300)+"px");
    confetti.appendChild(c);
    setTimeout(()=>c.remove(),2000);
  }
}

// NIE ucieka
const no=document.getElementById("no");
function moveNo(){
  no.style.left=Math.random()*(innerWidth-120)+"px";
  no.style.top=Math.random()*(innerHeight-60)+"px";
}
no.addEventListener("mouseenter",moveNo);
no.addEventListener("touchstart",moveNo);

// TAK
document.getElementById("yes").addEventListener("click",()=>{
  confetti();
  document.body.style.backgroundImage='url("yes.jpg")';
  question.classList.add("hidden");
  result.classList.remove("hidden");

  setInterval(()=>createHeart(true),120);

  ytplayer.src="https://www.youtube.com/embed/RB-RcX5DS5A?autoplay=1&loop=1&playlist=RB-RcX5DS5A";
});
</script>
</body>
</html>