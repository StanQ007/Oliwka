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
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5);
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
  position: relative;
  min-height: 80px;
}

button {
  font-size: 1.2em;
  padding: 15px 40px;
  border-radius: 30px;
  border: none;
  cursor: pointer;
  font-weight: bold;
  transition: all 0.3s ease;
  min-width: 120px;
  position: relative;
  z-index: 10;
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
  position: relative !important;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
  margin: 0 !important;
  transition: all 0.5s cubic-bezier(0.68, -0.55, 0.27, 1.55) !important;
}

#no:hover, .no-btn:hover {
  transform: scale(1.05) rotate(5deg);
}

.hidden {
  display: none !important;
}

#details-btn {
  margin-top: 30px;
  background: linear-gradient(45deg, #ffd166, #ffb347);
  color: #333;
  padding: 12px 25px;
  font-size: 1em;
  font-weight: bold;
}

#details-btn:hover {
  background: linear-gradient(45deg, #ffc043, #ff9900);
  transform: scale(1.05);
  box-shadow: 0 6px 20px rgba(255, 193, 7, 0.4);
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

.details-container {
  margin-top: 25px;
  padding: 20px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  border: 2px solid rgba(255, 255, 255, 0.2);
  text-align: center;
  animation: fadeIn 0.8s ease;
}

.details-title {
  font-size: 1.3em;
  color: #ffd166;
  margin-bottom: 15px;
  font-weight: bold;
}

.details-content {
  font-size: 1.1em;
  line-height: 1.5;
}

.coordinates {
  font-family: 'Courier New', monospace;
  background: rgba(0, 0, 0, 0.3);
  padding: 10px 15px;
  border-radius: 10px;
  margin: 10px 0;
  display: inline-block;
  font-size: 1.2em;
  letter-spacing: 1px;
}

.meeting-time {
  color: #ff8fa3;
  font-weight: bold;
  font-size: 1.3em;
  margin-top: 10px;
}

.map-link {
  display: inline-block;
  margin-top: 15px;
  padding: 8px 20px;
  background: rgba(255, 255, 255, 0.2);
  color: #ffd166;
  text-decoration: none;
  border-radius: 10px;
  transition: all 0.3s;
}

.map-link:hover {
  background: rgba(255, 255, 255, 0.3);
  transform: scale(1.05);
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

.no-move-area {
  position: relative;
  display: inline-block;
}

.no-container {
  display: inline-block;
  position: relative;
}

.no-btn-moving {
  animation: gentleMove 3s infinite ease-in-out;
}

@keyframes gentleMove {
  0%, 100% { transform: translate(0, 0) rotate(0deg); }
  25% { transform: translate(10px, -5px) rotate(2deg); }
  50% { transform: translate(-5px, 8px) rotate(-1deg); }
  75% { transform: translate(8px, 3px) rotate(1deg); }
}

.music-indicator {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 10px 15px;
  border-radius: 20px;
  font-size: 0.9em;
  z-index: 100;
  display: flex;
  align-items: center;
  gap: 8px;
  animation: fadeIn 1s ease;
}

.music-pulse {
  display: inline-block;
  width: 12px;
  height: 12px;
  background: #4CAF50;
  border-radius: 50%;
  animation: pulse 1.5s infinite;
}

@keyframes pulse {
  0% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.2); opacity: 0.7; }
  100% { transform: scale(1); opacity: 1; }
}

.volume-control {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 10px 15px;
  border-radius: 20px;
  font-size: 0.9em;
  z-index: 100;
  display: flex;
  align-items: center;
  gap: 10px;
}

.volume-control button {
  padding: 5px 10px;
  font-size: 0.9em;
  min-width: 40px;
  background: rgba(255, 255, 255, 0.2);
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
    <div class="no-container">
      <button id="no1" class="no-btn">Nie</button>
    </div>
  </div>
</div>

<!-- Drugie pytanie -->
<div class="container hidden" id="question2">
  <h1>Hmm... ale czy na pewno?</h1>
  <div class="buttons">
    <button id="yes2" class="yes-btn">Jeszcze bardziej TAK!</button>
    <div class="no-container">
      <button id="no2" class="no-btn">Chwila... Nie</button>
    </div>
  </div>
</div>

<!-- Trzecie pytanie -->
<div class="container hidden" id="question3">
  <h1>Ostatnie pytanie... ale tak serio serio?</h1>
  <div class="buttons">
    <button id="yes3" class="yes-btn">SERIO SERIO TAK! ❤️</button>
    <div class="no-container">
      <button id="no3" class="no-btn">No nie</button>
    </div>
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
  
  <button id="details-btn">📍 Pokaż szczegóły spotkania</button>
  
  <div id="details-info" class="hidden details-container">
    <div class="details-title">📌 Szczegóły naszego spotkania:</div>
    <div class="details-content">
      <p>Współrzędne miejsca spotkania:</p>
      <div class="coordinates">52°24′11″N 16°59′39″E</div>
      <p>Spotykamy się około <span class="meeting-time">godziny 14:00</span></p>
      <p>Przygotuj się na niespodziankę! 💝</p>
      <a href="https://www.google.com/maps?q=52.403056,16.994167" target="_blank" class="map-link">
        🗺️ Otwórz w Mapach Google
      </a>
    </div>
  </div>
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
const detailsBtn = document.getElementById("details-btn");
const detailsInfo = document.getElementById("details-info");
const backgroundMusic = document.getElementById("background-music");

// Zmienne stanu
let currentQuestion = 1;
let noButtons = [];
let moveIntervals = [];
let musicStarted = false;

// Funkcja do odtwarzania muzyki
function startMusic() {
  if (musicStarted) return;
  
  backgroundMusic.volume = 0.5;
  backgroundMusic.play()
    .then(() => {
      musicStarted = true;
      console.log("Muzyka rozpoczęta");
      showMusicIndicator();
      createVolumeControl();
    })
    .catch(error => {
      console.log("Błąd odtwarzania muzyki:", error);
      musicStarted = false;
    });
}

// Pokazuje wskaźnik odtwarzania muzyki
function showMusicIndicator() {
  const indicator = document.createElement('div');
  indicator.className = 'music-indicator';
  indicator.innerHTML = `
    <div class="music-pulse"></div>
    <span>Muzyka gra w tle</span>
  `;
  document.body.appendChild(indicator);
  
  setTimeout(() => {
    indicator.style.opacity = '0';
    indicator.style.transition = 'opacity 1s';
    setTimeout(() => indicator.remove(), 1000);
  }, 5000);
}

// Tworzy kontrolkę głośności
function createVolumeControl() {
  const volumeControl = document.createElement('div');
  volumeControl.className = 'volume-control';
  volumeControl.innerHTML = `
    <span>🔊</span>
    <button id="volume-down">-</button>
    <span id="volume-level">50%</span>
    <button id="volume-up">+</button>
  `;
  document.body.appendChild(volumeControl);
  
  document.getElementById('volume-down').addEventListener('click', () => {
    if (backgroundMusic.volume > 0.1) {
      backgroundMusic.volume -= 0.1;
      updateVolumeDisplay();
    }
  });
  
  document.getElementById('volume-up').addEventListener('click', () => {
    if (backgroundMusic.volume < 1) {
      backgroundMusic.volume += 0.1;
      updateVolumeDisplay();
    }
  });
  
  function updateVolumeDisplay() {
    document.getElementById('volume-level').textContent = 
      Math.round(backgroundMusic.volume * 100) + '%';
  }
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

// Ruch przycisku "Nie" - delikatne poruszanie się w ograniczonym obszarze
function moveNoButton(button) {
  const container = button.closest('.buttons');
  const containerRect = container.getBoundingClientRect();
  const buttonRect = button.getBoundingClientRect();
  
  // Ograniczenia ruchu - przycisk ma pozostać w obrębie kontenera buttons
  const maxX = containerRect.width - buttonRect.width - 20;
  const maxY = containerRect.height - buttonRect.height - 20;
  
  // Losowe przesunięcie (niewielkie, żeby nie wychodziło poza obszar)
  const newX = Math.random() * maxX;
  const newY = Math.random() * maxY;
  
  // Ustaw nową pozycję WZGLĘDNĄ w kontenerze
  button.style.position = 'relative';
  button.style.left = `${newX}px`;
  button.style.top = `${newY}px`;
  
  // Dodaj efekt rotacji
  button.style.transform = `rotate(${Math.random() * 10 - 5}deg)`;
}

// Ruch przy najechaniu myszką
function setupNoButtonHover(button) {
  button.addEventListener('mouseenter', () => {
    // Przyspiesz ruch przy najechaniu
    moveNoButton(button);
    
    // Dodaj efekt "ucieczki" ale w obrębie kontenera
    const moveInterval = setInterval(() => {
      moveNoButton(button);
    }, 300);
    
    // Zapisz interval, żeby potem go wyczyścić
    moveIntervals.push(moveInterval);
    
    // Dodaj efekt wizualny
    button.style.background = 'linear-gradient(45deg, #666, #888)';
    button.style.boxShadow = '0 6px 20px rgba(0, 0, 0, 0.5)';
    
    // Po opuszczeniu przycisku, wyczyść interval
    const clearOnLeave = () => {
      moveIntervals.forEach(interval => clearInterval(interval));
      moveIntervals = [];
      button.style.background = 'linear-gradient(45deg, #4a4a4a, #666)';
      button.style.boxShadow = '0 4px 15px rgba(0, 0, 0, 0.3)';
    };
    
    button.addEventListener('mouseleave', clearOnLeave, { once: true });
  });
}

// Inicjalizacja przycisków "Nie"
function initNoButtons() {
  noButtons = [];
  const noBtns = document.querySelectorAll('.no-btn');
  
  noBtns.forEach((btn, index) => {
    // Dodaj początkową animację delikatnego ruchu
    btn.classList.add('no-btn-moving');
    
    // Ustaw różne czasy animacji dla każdego przycisku
    btn.style.animationDuration = `${3 + index * 0.5}s`;
    
    // Zapisz przycisk
    noButtons.push(btn);
    
    // Ustaw hover effect
    setupNoButtonHover(btn);
    
    // Dodaj event listener dla kliknięcia (efekt wizualny)
    btn.addEventListener('click', () => {
      // Efekt dla "Nie" - małe serduszko
      const smallHeart = document.createElement("div");
      smallHeart.textContent = "💔";
      smallHeart.style.position = "absolute";
      smallHeart.style.left = "50%";
      smallHeart.style.top = "50%";
      smallHeart.style.fontSize = "24px";
      smallHeart.style.zIndex = "1000";
      smallHeart.style.animation = "explode 1s ease-out forwards";
      smallHeart.style.setProperty("--x", (Math.random() * 100 - 50) + "px");
      smallHeart.style.setProperty("--y", (Math.random() * 100 - 50) + "px");
      btn.appendChild(smallHeart);
      setTimeout(() => smallHeart.remove(), 1000);
    });
  });
}

// Przejście do następnego pytania
function goToNextQuestion() {
  // Zatrzymaj wszystkie interwały ruchu
  moveIntervals.forEach(interval => clearInterval(interval));
  moveIntervals = [];
  
  // URUCHOM MUZYKĘ PRZY PIERWSZYM "TAK"
  if (currentQuestion === 1) {
    startMusic();
  }
  
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
    
    // Inicjalizuj nowe przyciski "Nie"
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
  
  // Przycisk szczegółów spotkania
  detailsBtn.addEventListener('click', () => {
    // Ukryj przycisk
    detailsBtn.classList.add('hidden');
    
    // Pokaż szczegóły
    detailsInfo.classList.remove('hidden');
    
    // Dodaj dodatkowe serduszka
    heartsRainfall(20);
    confettiBurst();
  });
  
  // Automatyczne odtwarzanie muzyki po interakcji (rezerwowe)
  document.addEventListener('click', () => {
    if (!musicStarted && currentQuestion > 1) {
      startMusic();
    }
  }, { once: true });
}

// Start aplikacji
window.addEventListener('load', init);
</script>

</body>
</html>
