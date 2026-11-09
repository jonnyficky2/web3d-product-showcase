# Forma — Interactive 3D Web Product Showcase

[![Three.js](https://img.shields.io/badge/Three.js-r169-black?style=for-the-badge&logo=three.js)](https://threejs.org/)
[![JavaScript](https://img.shields.io/badge/JavaScript-ES6+-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)](LICENSE)

> Showroom produk web 3D interaktif berbasis Three.js dengan kontrol kamera orbit 360 derajat, kustomisasi material warna *real-time*, dan antarmuka *glassmorphic* responsif.

---

## 🌟 Fitur Utama (Key Features)

- **🕹️ 360° Smooth Orbit Controls:** Navigasi kamera spasial dengan inersia (*damping*), pembatas jarak (*clamped zoom*), dan batas sudut elevasi agar kamera tidak menembus lantai panggung.
- **📦 Multi-Product Switcher:** Eksplorasi 3 lini produk perangkat keras premium secara instan:
  - **01. Sonic One:** Smart Speaker dengan grille 360° audio spasial.
  - **02. Studio Arc:** Over-ear Headphone ergonomis dengan headband Catmull-Rom dan acoustic plates.
  - **03. Form Watch:** Smartwatch kontemporer dengan layar digital berpendar (*emissive display*) dan tali silikon bertekstur.
- **🎨 Real-Time Material & Color Customizer:** Pergantian varian warna fisik (*Sand*, *Slate*, dan *Rose*) secara instan pada material PBR (*Physically Based Rendering*) dengan pantulan *clearcoat* dinamis.
- **💡 Studio Lighting & Soft Shadows:** Konfigurasi pencahayaan studio dengan key, rim, fill, dan ambient light serta bayangan lembut (*PCFSoftShadowMap* 2048x2048).
- **⏱️ Intelligent Idle Auto-Rotate:** Produk berputar secara otomatis dan halus saat dalam kondisi diam, berhenti seketika saat disentuh, dan berlanjut kembali setelah jeda *cooldown*.
- **📱 Fully Responsive Glassmorphic UI:** Antarmuka modern dengan efek *frosted glass* (`backdrop-filter`) yang menyesuaikan tata letak secara dinamis dari layar smartphone hingga monitor desktop layar lebar.
- **⚡ Zero-Build Architecture:** Berjalan langsung di peramban tanpa memerlukan kompilasi (*no Webpack, Vite, or npm install required*).

---

## 🚀 Cara Menjalankan Project secara Lokal (Quickstart)

Karena aplikasi ini menggunakan arsitektur **ECMAScript Modules (ESM)** dan **W3C Import Maps**, peramban web modern memerlukan protokol HTTP/HTTPS lokal untuk memuat modul (kebijakan keamanan CORS menolak pemuatan modul via `file://`).

### Prasyarat
- Peramban web modern yang mendukung WebGL (Google Chrome, Mozilla Firefox, Apple Safari, atau Microsoft Edge).
- Python 3 terinstal di sistem Anda (tersedia secara bawaan di macOS dan sebagian besar distro Linux).

### Langkah Menjalankan:

1. **Buka Terminal** dan arahkan ke direktori project:
   ```bash
   cd /Users/jofi/Documents/PROJECT/web3d-product-showcase
   ```

2. **Jalankan HTTP Server Lokal** menggunakan Python 3:
   ```bash
   python3 -m http.server 8000
   ```

3. **Buka Browser** dan kunjungi alamat berikut:
   ```
   http://localhost:8000
   ```

### Alternatif Server Lokal Lainnya:
Jika Anda lebih terbiasa dengan ekosistem Node.js atau ekstensi editor:
- **Menggunakan npx serve:**
  ```bash
  npx serve .
  ```
- **Menggunakan VS Code Live Server:**
  Klik kanan pada file `index.html` lalu pilih **"Open with Live Server"**.

---

## 📁 Struktur Repositori (Repository Structure)

```
web3d-product-showcase/
├── index.html              # Aplikasi lengkap (HTML5, CSS3, dan skrip Three.js)
├── README.md               # Dokumentasi utama dan panduan cepat proyek
└── docs/                   # Dokumentasi produk, arsitektur, QA, security, audit, dan task management
    ├── PRD.md              # Product Requirement Document (PRD)
    ├── ARCHITECTURE.md     # Spesifikasi arsitektur sistem & rendering Three.js
    └── USER_FLOW.md        # Legacy diagram alir interaksi pengguna
```

---

## 📚 Navigasi Dokumentasi Teknis

Untuk memahami detail teknis, desain arsitektur grafis, dan persyaratan produk secara menyeluruh, silakan pelajari dokumen di direktori [`docs/`](docs/):

1. **[Product Requirement Document (docs/PRD.md)](docs/PRD.md):**
   - Visi dan latar belakang produk.
   - Persona pengguna dan problem statement industri e-commerce.
   - Persyaratan fungsional (FR) dan non-fungsional (NFR).
   - Matriks KPI performa & *future product roadmap*.

2. **[System Architecture & Tech Stack (docs/ARCHITECTURE.md)](docs/ARCHITECTURE.md):**
   - Diagram arsitektur sistem & scene graph Three.js.
   - Konfigurasi WebGLRenderer, ACES Filmic Tone Mapping, dan PBR Material.
   - Setup pencahayaan studio 4-titik dan kalkulasi inersia *OrbitControls*.
   - Manajemen *state reactive* dan sinkronisasi DOM overlay.

3. **[User Journey & Interaction Flow (docs/USER_FLOW.md)](docs/USER_FLOW.md):**
   - Narasi langkah demi langkah alur pengguna dari landing hingga *pre-order*.
   - Diagram alir interaksi spasial 360° dan mesin transisi status (*state machine*).
   - Penanganan *edge cases* (konflik gestur sentuh mobile, kliping kamera, dan aksesibilitas).

---

## 🎮 Kontrol & Interaksi

| Kontrol Input | Desktop | Mobile / Layar Sentuh |
| :--- | :--- | :--- |
| **Rotasi 360° (Orbit)** | Klik kiri dan seret mouse | Sentuh dan geser 1 jari |
| **Pembesaran (Zoom)** | Putar roda mouse (*scroll*) | Gestur cubit layar (*pinch to zoom*) |
| **Geser Kamera (Pan)** | Klik kanan dan seret mouse | Sentuh dan geser 2 jari |
| **Ganti Produk** | Klik tombol tab `01`, `02`, `03` | Ketuk tombol tab `01`, `02`, `03` |
| **Kustomisasi Warna** | Klik palet lingkaran warna | Ketuk palet lingkaran warna |
| **Pemesanan (CTA)** | Klik tombol `Pre-order` / `Buy now` | Ketuk tombol `Pre-order` / `Buy now` |

---

## 🌐 Kompatibilitas Browser

| Browser | Desktop | Mobile |
| :--- | :--- | :--- |
| **Google Chrome** | ✅ v90+ | ✅ Android Chrome |
| **Apple Safari** | ✅ v15+ | ✅ iOS Safari 15+ |
| **Mozilla Firefox**| ✅ v90+ | ✅ Firefox Mobile |
| **Microsoft Edge** | ✅ v90+ | ✅ Edge Mobile |

---

## 📄 Lisensi & Hak Cipta

Proyek ini dirilis di bawah lisensi **MIT License**. Bebas digunakan untuk keperluan komersial, pengembangan studi, atau modifikasi portofolio.
