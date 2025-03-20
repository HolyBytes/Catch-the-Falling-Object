 **Penjelasan Lengkap Game "Catch the Falling Object"**
Game ini adalah **permainan berbasis web** yang dibuat menggunakan **HTML, CSS, dan JavaScript**. Pemain mengontrol sebuah karakter yang harus **menangkap objek jatuh** seperti buah, koin, dan bintang sambil **menghindari rintangan** seperti bom dan duri. Skor akan bertambah setiap kali menangkap objek yang benar, dan nyawa akan berkurang jika terkena bom atau duri. Permainan akan berakhir jika nyawa habis atau waktu habis dalam **mode tantangan**.

---

## 🏗 **1. Struktur HTML (Tata Letak Game)**
File **index2.html** memiliki struktur HTML yang terdiri dari elemen-elemen berikut:

### **🔹 Elemen `<head>`**
Berisi **meta tag, judul halaman, dan link ke Bootstrap** untuk mempercantik tampilan.
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Catch the Falling Object</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
```
- `meta charset="UTF-8"` → Agar teks dapat mendukung berbagai karakter.
- `meta viewport` → Memastikan tampilan responsif di berbagai perangkat.
- `title` → Menampilkan judul **"Catch the Falling Object"** di tab browser.
- `link` → Menggunakan **Bootstrap 5.3** untuk mendukung tampilan yang lebih modern.

---

### **🔹 Elemen `<body>`**
Bagian utama yang menampilkan elemen-elemen game, seperti:
- **Container game**
- **Pemain (karakter)**
- **Skor, level, nyawa**
- **Overlay (tampilan awal dan game over)**
- **Tombol navigasi untuk perangkat mobile**
  
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
📌 **Penjelasan komponen utama:**
- **`#game-container`** → Area bermain di mana objek jatuh dan pemain bergerak.
- **`#score-display`** → Menampilkan skor pemain.
- **`#level-display`** → Menampilkan level permainan.
- **`#lives-display`** → Menampilkan nyawa dengan simbol ❤️.
- **`#countdown`** → Menampilkan waktu tersisa dalam **mode tantangan**.
- **`#player`** → Karakter yang dikontrol oleh pemain.
- **Tombol kiri/kanan (`#left-button`, `#right-button`)** → Untuk kontrol pada **perangkat mobile**.
- **Overlay (`#overlay`)** → Layar awal dengan tombol **mulai permainan** dan **mode tantangan**.

---

## 🎨 **2. Desain Tampilan (CSS)**
CSS digunakan untuk memperindah tampilan game. Berikut adalah beberapa elemen penting:

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
    width: 100%;
    max-width: 500px;
    height: 600px;
    margin: 20px auto;
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 10px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
    overflow: hidden;
}
```
✔ **Latar belakang gradasi biru-hijau**  
✔ **Kontainer game transparan dengan efek bayangan**

---

### **🔹 Karakter Pemain**
```css
#player {
    position: absolute;
    bottom: 20px;
    left: calc(50% - 40px);
    width: 80px;
    height: 80px;
    background-image: url('data:image/svg+xml;utf8,<svg>...</svg>');
    background-size: contain;
    transition: left 0.1s ease-out;
}
```
✔ **Berbentuk lingkaran dengan wajah tersenyum**  
✔ **Bergerak ke kiri dan kanan dengan transisi halus**

---

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
✔ **Buah, koin, dan bintang menambah skor**  
✔ **Bom dan duri mengurangi nyawa**  

---

## 🎮 **3. Mekanisme Permainan (JavaScript)**
JavaScript mengontrol seluruh permainan, termasuk **gerakan pemain, objek jatuh, skor, dan efek animasi**.

### **🔹 Variabel Penting**
```js
let score = 0;
let level = 1;
let lives = 3;
let fallingSpeed = 3;
let spawnRate = 1500;
let gameRunning = false;
```
✔ **Menyimpan status permainan**  

---

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
✔ **Menyiapkan skor, nyawa, dan level awal**  
✔ **Menjalankan loop permainan**

---

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
✔ **Menghasilkan objek jatuh secara acak**  

---

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
✔ **Jika menangkap koin → skor bertambah**  
✔ **Jika kena bom → nyawa berkurang**  

---
📌 Mainkan game "Catch the Falling Object" di sini:
Klik untuk bermain

✅ **Game ini sudah siap dimainkan dengan kontrol keyboard & mobile!**  

