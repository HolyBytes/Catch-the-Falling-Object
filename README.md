🎮 **Catch the Falling Object - Game Berbasis Web**
**Catch the Falling Object** adalah game berbasis web di mana pemain mengontrol karakter untuk menangkap **buah, koin, dan bintang** sambil menghindari **bom dan duri**. Game ini dibuat menggunakan **HTML, CSS, dan JavaScript** serta memiliki **kontrol untuk desktop & perangkat mobile**.  

📌 **Mainkan langsung di sini:**  
🔗 **[Klik untuk bermain](https://holybytes.github.io/Catch-the-Falling-Object/)**  

---

## 🏗 **1. Struktur HTML (Tata Letak Game)**
File ini terdiri dari beberapa elemen penting:
- **Container utama**: Tempat berlangsungnya permainan.
- **Karakter pemain (`#player`)**: Dikendalikan oleh pemain.
- **Objek jatuh**: Seperti buah, koin, bintang, bom, dan duri.
- **Tombol kontrol**: Untuk navigasi di perangkat mobile.
- **Overlay (`#overlay`)**: Layar awal dengan tombol **Mulai Permainan** dan **Mode Tantangan**.

```html
<body>
    <div class="container">
        <div id="game-container">
            <div id="score-display">Skor: 0</div>
            <div id="level-display">Level: 1</div>
            <div id="lives-display">❤️❤️❤️</div>
            <div id="countdown"></div>
            <div id="player"></div>

            <div id="left-button" class="control-button d-md-none">←</div>
            <div id="right-button" class="control-button d-md-none">→</div>

            <div id="overlay">
                <h2>Catch the Falling Object</h2>
                <p>Tangkap buah, koin, dan bintang<br>Hindari bom dan duri!</p>
                <button id="start-button" class="btn btn-success btn-lg">Mulai Permainan</button>
                <button id="challenge-button" class="btn btn-warning btn-lg">Mode Tantangan</button>
                <div id="high-score">Skor Tertinggi: 0</div>
            </div>
        </div>
    </div>
</body>
```
---

## 🎨 **2. Tampilan & Desain (CSS)**
Game ini memiliki desain yang **modern & responsif** dengan:
✔ **Latar belakang gradasi biru-hijau**  
✔ **Karakter dengan ekspresi wajah lucu**  
✔ **Efek animasi untuk skor & tabrakan**  

### **🔹 Latar Belakang & Kontainer**
```css
body {
    background: linear-gradient(to bottom, #1a2980, #26d0ce);
    color: white;
    height: 100vh;
    overflow: hidden;
}
#game-container {
    position: relative;
    max-width: 500px;
    height: 600px;
    margin: auto;
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
}
```

### **🔹 Karakter Pemain**
```css
#player {
    position: absolute;
    bottom: 20px;
    left: calc(50% - 40px);
    width: 80px;
    height: 80px;
    background-image: url('data:image/svg+xml;utf8,<svg>...</svg>');
    transition: left 0.1s ease-out;
}
```

### **🔹 Objek Jatuh (Buah, Koin, Bintang, Bom, Duri)**
```css
.falling-object {
    position: absolute;
    width: 50px;
    height: 50px;
    background-size: contain;
}
.fruit { background-image: url('data:image/svg+xml;utf8,<svg>...</svg>'); }
.coin { background-image: url('data:image/svg+xml;utf8,<svg>...</svg>'); }
.star { background-image: url('data:image/svg+xml;utf8,<svg>...</svg>'); }
.bomb { background-image: url('data:image/svg+xml;utf8,<svg>...</svg>'); }
.spike { background-image: url('data:image/svg+xml;utf8,<svg>...</svg>'); }
```
---

## 🎮 **3. Mekanisme Permainan (JavaScript)**
JavaScript mengatur seluruh logika permainan, termasuk:
- **Gerakan pemain**
- **Objek jatuh & tabrakan**
- **Skor, level, dan nyawa**
- **Efek animasi & suara**

### **🔹 Variabel Utama**
```js
let score = 0;
let level = 1;
let lives = 3;
let fallingSpeed = 3;
let spawnRate = 1500;
let gameRunning = false;
```

### **🔹 Memulai Permainan**
```js
function startGame() {
    score = 0;
    level = 1;
    lives = 3;
    gameRunning = true;
    document.getElementById('overlay').style.display = 'none';
    requestAnimationFrame(gameLoop);
    setTimeout(spawnObject, 500);
}
```

### **🔹 Spawn Objek Jatuh**
```js
function spawnObject() {
    if (!gameRunning) return;
    let objectTypes = ['fruit', 'coin', 'star', 'bomb', 'spike'];
    let objectType = objectTypes[Math.floor(Math.random() * objectTypes.length)];
    let object = document.createElement('div');
    object.classList.add('falling-object', objectType);
    gameContainer.appendChild(object);
}
```

### **🔹 Menangani Tabarakan**
```js
function checkCollisions() {
    objects.forEach((obj) => {
        if (obj.type === 'bomb' || obj.type === 'spike') {
            lives--;
        } else {
            score += 10;
        }
    });
}
```

### **🔹 Mode Tantangan (60 Detik)**
```js
function startChallengeMode() {
    challengeMode = true;
    challengeTimeLeft = 60;
    startGame();
    challengeTimer = setInterval(() => {
        challengeTimeLeft--;
        if (challengeTimeLeft <= 0) {
            clearInterval(challengeTimer);
            endGame();
        }
    }, 1000);
}
```

### **🔹 Mengakhiri Permainan**
```js
function endGame() {
    gameRunning = false;
    if (score > highScore) {
        highScore = score;
        localStorage.setItem('highScore', highScore);
    }
    document.getElementById('overlay').style.display = 'flex';
    document.getElementById('high-score').textContent = `Skor Tertinggi: ${highScore}`;
}
```

---

## 🔥 **Fitur Unggulan**
✅ **Gameplay seru dengan tantangan unik**  
✅ **Desain modern dengan animasi & efek visual**  
✅ **Mendukung keyboard & layar sentuh (mobile-friendly)**  
✅ **Mode Tantangan (Challenge Mode) untuk adu skor**  
✅ **Penyimpanan skor tertinggi dengan `localStorage`**  

📌 **Mainkan game ini di sini:**  
🔗 **[Klik untuk bermain](https://holybytes.github.io/Catch-the-Falling-Object/)**  

🎉 **Siap menangkap semua objek & jadi juara?** 🎉  
Jika ada pertanyaan atau ingin fitur tambahan, silakan beri tahu! 😊🚀
