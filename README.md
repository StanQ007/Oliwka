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
  font-family: 'Arial', sans-serif;
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
  to { transform: translateY(-120vh) rotate(20deg); opacity: 0; }
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
  max-width: 600px;
  text-align: center;
  color: white;
  z-index: 2;
  padding: 30px;
  background: rgba(0, 0, 0, 0.6);
  border-radius: 20px;
  backdrop-filter: blur(5px);
}

h1 {
  font-size: 2em;
  text-shadow: 2px 2px 8px #000;
  margin-bottom: 30px;
  line-height: 1.4;
}

.buttons {
  display: flex;
  justify-content: center;
  gap: 25px;
  margin-top: 20px;
  flex-wrap: wrap;
}

button {
  font-size: 1.2em;
  padding: 15px 40px;
  border-radius: 30px;
  border: none;
  cursor: pointer;
  font-weight: bold;
  transition: transform 0.3s, box-shadow 0.3s;
  min-width: 120px;
}

#yes, .yes-btn {
  background: linear-gradient(45deg, #ff4d6d, #ff8fa3);
  color: white;
  box-shadow: 0 4px 15px rgba(255, 77, 109, 0.4);
}

#yes:hover, .yes-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 6px 20px rgba(255, 77, 109, 0.6);
}

#no, .no-btn {
  background: linear-gradient(45deg, #4a4a4a, #666);
  color: white;
  position: fixed;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
}

#no:hover, .no-btn:hover {
  transform: scale(1.05);
}

.hidden {
  display: none !important;
}

#music-btn {
  margin-top: 30px;
  background: #ffd166;
  color: #333;
  padding: 12px 25px;
  font-size: 1em;
}

#music-btn:hover {
  background: #ffc043;
  transform: scale(1.05);
}

.hearts-fall {
  position: fixed;
  top: -50px;
  font-size: 30px;
  animation: fall linear forwards;
  z-index: 1000;
}

@keyframes fall {
  0% {
    transform: translateY(-100px) rotate(0deg);
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  100% {
    transform: translateY(110vh) rotate(360deg);
    opacity: 0;
  }
}

.final-message {
  font-size: 1.5em;
  line-height: 1.6;
  margin-top: 20px;
}

.final-message span {
  color: #ff4d6d;
  font-weight: bold;
}
</style>
</head>

<body>

<div class="overlay"></div>
<div id="hearts"></div>
<div id="confetti"></div>

<!-- Pierwsze pytanie -->
<div class="container" id="question1">
  <h1>Bombelku, czy będziesz moją walentynką?</h1>
  <div class="buttons">
    <button id="yes1" class="yes-btn">Tak</button>
    <button id="no1" class="no-btn">Nie</button>
  </div>
</div>

<!-- Drugie pytanie -->
<div class="container hidden" id="question2">
  <h1>Hmm... ale czy na pewno?</h1>
  <div class="buttons">
    <button id="yes2" class="yes-btn">Jeszcze bardziej TAK!</button>
    <button id="no2" class="no-btn">Chwila... Nie</button>
  </div>
</div>

<!-- Trzecie pytanie -->
<div class="container hidden" id="question3">
  <h1>Ostatnie pytanie... ale tak serio serio?</h1>
  <div class="buttons">
    <button id="yes3" class="yes-btn">SERIO SERIO TAK! ❤️</button>
    <button id="no3" class="no-btn">No nie</button>
  </div>
</div>

<!-- Ostateczny ekran -->
<div class="container hidden" id="final">
  <h1>❤️ Wiedziałem! ❤️</h1>
  <div class="final-message">
    <p>Bardzo mnie to cieszy moja droga!</p>
    <p>Bądź gotowa na <span>14.02.2026</span></p>
    <p>To będzie wyjątkowy dzień! 🥰</p>
    <p><em>"W twoich oczach jest mój cały świat..."</em></p>
  </div>
  <button id="music-btn">🎵 Włącz muzykę</button>
</div>

<audio id="background-music" loop>
  <source src="nazwa.mp3" type="audio/mpeg">
  Twoja przeglądarka nie obsługuje elementu audio.
</audio>

<script>
// Elementy DOM
const heartsContainer = document.getElementById("hearts");
const confettiContainer = document.getElementById("confetti");
const question1 = document.getElementById("question1");
const question2 = document.getElementById("question2");
const question3 = document.getElementById("question3");
const finalScreen = document.getElementById("final");
const musicBtn = document.getElementById("music-btn");
const backgroundMusic = document.getElementById("background-music");

// Zmienne stanu
let currentQuestion = 1;
let noButtons = [];
let mouseX = 0;
let mouseY = 0;

// Śledzenie pozycji myszy
document.addEventListener('mousemove', (e) => {
  mouseX = e.clientX;
  mouseY = e.clientY;
  
  // Aktualizuj pozycję przycisków "Nie" w czasie rzeczywistym
  updateNoButtonsPosition();
});

// Funkcja uciekania przycisków "Nie"
function updateNoButtonsPosition() {
  noButtons.forEach(btn => {
    if (!btn.parentElement.parentElement.classList.contains('hidden')) {
      const btnRect = btn.getBoundingClientRect();
      const btnCenterX = btnRect.left + btnRect.width / 2;
      const btnCenterY = btnRect.top + btnRect.height / 2;
      
      // Oblicz odległość od kursora
      const distance = Math.sqrt(
        Math.pow(mouseX - btnCenterX, 2) + 
        Math.pow(mouseY - btnCenterY, 2)
      );
      
      // Jeśli kursor jest zbyt blisko, przesuń przycisk
      if (distance < 150) {
        const angle = Math.atan2(
          btnCenterY - mouseY,
          btnCenterX - mouseX
        );
        
        // Nowa pozycja (ucieka w przeciwnym kierunku)
        const newX = mouseX + Math.cos(angle) * 200;
        const newY = mouseY + Math.sin(angle) * 200;
        
        // Ogranicz do obszaru ekranu
        const safeX = Math.max(20, Math.min(window.innerWidth - btnRect.width - 20, newX));
        const safeY = Math.max(20, Math.min(window.innerHeight - btnRect.height - 20, newY));
        
        btn.style.left = safeX + 'px';
        btn.style.top = safeY + 'px';
      }
    }
  });
}

// Serca w tle (stałe)
function createBackgroundHeart() {
  const heart = document.createElement("div");
  heart.className = "heart";
  heart.textContent = "❤️";
  heart.style.left = Math.random() * 100 + "%";
  heart.style.animationDuration = (Math.random() * 3 + 4) + "s";
  heart.style.opacity = Math.random() * 0.5 + 0.3;
  heartsContainer.appendChild(heart);
  setTimeout(() => heart.remove(), 7000);
}

// Lawina serduszek
function heartsRainfall(count = 50) {
  for (let i = 0; i < count; i++) {
    setTimeout(() => {
      const heart = document.createElement("div");
      heart.className = "hearts-fall";
      heart.textContent = "❤️";
      heart.style.left = Math.random() * 100 + "%";
      heart.style.animationDuration = (Math.random() * 2 + 2) + "s";
      heart.style.fontSize = (Math.random() * 20 + 20) + "px";
      heart.style.color = `hsl(${Math.random() * 360}, 100%, 65%)`;
      document.body.appendChild(heart);
      
      setTimeout(() => heart.remove(), 3000);
    }, i * 50);
  }
}

// Konfetti
function confettiBurst() {
  for (let i = 0; i < 40; i++) {
    const confetti = document.createElement("div");
    confetti.className = "confetti-heart";
    confetti.textContent = "❤️";
    confetti.style.left = "50%";
    confetti.style.top = "50%";
    confetti.style.color = `hsl(${Math.random() * 360}, 100%, 65%)`;
    confetti.style.setProperty("--x", (Math.random() * 600 - 300) + "px");
    confetti.style.setProperty("--y", (Math.random() * 600 - 300) + "px");
    confettiContainer.appendChild(confetti);
    setTimeout(() => confetti.remove(), 1500);
  }
}

// Zmiana tła
function changeBackground(imageName) {
  document.body.style.backgroundImage = `url("${imageName}")`;
}

// Przejście do następnego pytania
function goToNextQuestion() {
  // Ukryj aktualne pytanie
  document.getElementById(`question${currentQuestion}`).classList.add('hidden');
  
  // Zwiększ numer pytania
  currentQuestion++;
  
  // Jeśli to jeszcze nie finał, pokaż następne pytanie
  if (currentQuestion <= 3) {
    document.getElementById(`question${currentQuestion}`).classList.remove('hidden');
    
    // Zmień tło i dodaj efekty
    changeBackground(`yes${currentQuestion-1}.jpg`);
    heartsRainfall(60);
    confettiBurst();
    
    // Inicjalizuj nowy przycisk "Nie"
    initNoButtons();
  } else {
    // Ostatni ekran
    finalScreen.classList.remove('hidden');
    changeBackground('final.jpg');
    heartsRainfall(100);
    
    // Intensywniejsze efekty
    for (let i = 0; i < 5; i++) {
      setTimeout(() => confettiBurst(), i * 300);
    }
    
    // Uruchom serca w tle
    setInterval(() => createBackgroundHeart(), 100);
  }
}

// Inicjalizacja przycisków "Nie"
function initNoButtons() {
  noButtons = [];
  const noBtns = document.querySelectorAll('.no-btn');
  noBtns.forEach(btn => {
    // Ustaw losową początkową pozycję
    btn.style.left = Math.random() * (window.innerWidth - 120) + 'px';
    btn.style.top = Math.random() * (window.innerHeight - 60) + 'px';
    btn.style.position = 'fixed';
    noButtons.push(btn);
    
    // Dodaj event listener dla kliknięcia
    btn.addEventListener('click', () => {
      // Efekt dla "Nie" - małe serduszko
      const smallHeart = document.createElement("div");
      smallHeart.textContent = "💔";
      smallHeart.style.position = "fixed";
      smallHeart.style.left = (parseFloat(btn.style.left) + 60) + "px";
      smallHeart.style.top = (parseFloat(btn.style.top) + 30) + "px";
      smallHeart.style.fontSize = "24px";
      smallHeart.style.zIndex = "1000";
      smallHeart.style.animation = "fall 2s linear forwards";
      document.body.appendChild(smallHeart);
      setTimeout(() => smallHeart.remove(), 2000);
    });
  });
}

// Inicjalizacja
function init() {
  // Uruchom tło serc
  setInterval(createBackgroundHeart, 300);
  
  // Inicjalizuj przyciski "Nie"
  initNoButtons();
  
  // Przyciski "Tak"
  document.getElementById('yes1').addEventListener('click', goToNextQuestion);
  document.getElementById('yes2').addEventListener('click', goToNextQuestion);
  document.getElementById('yes3').addEventListener('click', goToNextQuestion);
  
  // Przycisk muzyki
  musicBtn.addEventListener('click', () => {
    backgroundMusic.play()
      .then(() => {
        musicBtn.textContent = "🎵 Muzyka gra";
        musicBtn.style.background = "#4CAF50";
      })
      .catch(e => {
        musicBtn.textContent = "🎵 Kliknij ponownie";
        console.log("Autoplay blocked:", e);
      });
  });
  
  // Automatyczne odtwarzanie muzyki po interakcji
  document.addEventListener('click', () => {
    if (backgroundMusic.paused && currentQuestion === 4) {
      backgroundMusic.play().catch(e => console.log("Music autoplay blocked"));
    }
  }, { once: true });
}

// Start aplikacji
window.addEventListener('load', init);
</script>

</body>
</html>
