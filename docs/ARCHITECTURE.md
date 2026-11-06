# System Architecture & Technical Specifications
## Forma — Interactive 3D Web Product Showcase

- **Document Version:** 1.0.0
- **Architect:** Senior Software Architect
- **Target Runtime:** Modern Web Browsers (WebGL 2.0 / 1.0 Compatible)
- **Architecture Paradigm:** Zero-Build Vanilla Web Architecture / Immediate-Mode 3D Lifecycle

---

## 1. High-Level Architecture Overview

Aplikasi **Forma** dirancang menggunakan arsitektur web modern *zero-build* yang berfokus pada kesederhanaan, performa eksekusi langsung, dan portabilitas tinggi. Sistem ini memisahkan lapisan visualisasi 3D berbasis WebGL dengan lapisan antarmuka pengguna (UI DOM) secara asinkron dan bersih, disinkronisasikan oleh modul pengendali status (*State Controller*).

```
+-----------------------------------------------------------------------------------+
|                                 BROWSER CLIENT                                    |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |                             PRESENTATION LAYER                              |  |
|  |  +-------------------------+            +--------------------------------+  |  |
|  |  |    DOM Overlay UI       |            |    WebGL 3D Canvas (#stage)    |  |  |
|  |  |  - Topbar & Branding    |            |  - Hardware Accelerated Canvas |  |  |
|  |  |  - Product Tabs (01-03) |            |  - Three.js WebGLRenderer      |  |  |
|  |  |  - Typography & Specs   |            |  - Real-time Shadow Mapping    |  |  |
|  |  |  - Color Swatches       |            +--------------------------------+  |  |
|  |  |  - Action CTA Link      |                            ^                   |  |
|  |  +-------------------------+                            |                   |  |
|  |               |                                         |                   |  |
|  +---------------+-----------------------------------------+-------------------+  |
|                  | User Gestures                           | Renders           |
|                  v (Click, Touch, Scroll)                  | Continuous Frames |
|  +---------------------------------------------------------+-------------------+  |
|  |                           APPLICATION LOGIC LAYER                           |  |
|  |                                                                             |  |
|  |  +--------------------------+           +--------------------------------+  |  |
|  |  |     State Controller     |           |     3D Scene Graph Manager     |  |  |
|  |  |  - activeProduct state   |---------->|  - stage (THREE.Group)         |  |  |
|  |  |  - activeColor index     |           |  - Procedural Product Meshes   |  |  |
|  |  |  - idle / cooldown timer |           |  - Material Palette Manager    |  |  |
|  |  +--------------------------+           +--------------------------------+  |  |
|  |               ^                                         |                   |  |
|  |               |                                         v                   |  |
|  |  +--------------------------+           +--------------------------------+  |  |
|  |  |     Interaction Loop     |           |        Camera & Lighting       |  |  |
|  |  |  - OrbitControls Damping |---------->|  - PerspectiveCamera (34 deg)  |  |  |
|  |  |  - Delta-time Calculation|           |  - 4-Point Lighting Rig        |  |  |
|  |  |  - Auto-rotation Engine  |           |  - Floor Shadow Receiver       |  |  |
|  |  +--------------------------+           +--------------------------------+  |  |
|  +-----------------------------------------------------------------------------+  |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |                     RUNTIME DEPENDENCIES & LIBRARIES                        |  |
|  |  - Three.js (r169 via jsDelivr CDN ESM)                                     |  |
|  |  - Three.js OrbitControls Add-on                                            |  |
|  |  - W3C Standard Import Maps                                                 |  |
|  +-----------------------------------------------------------------------------+  |
+-----------------------------------------------------------------------------------+
```

---

## 2. Tech Stack & Dependencies

### 2.1 Core Technologies
1. **HTML5:**
   - Menyediakan struktur dokumen semantik (`<main>`, `<header>`, `<nav>`, `<section>`, `<aside>`).
   - Elemen `<canvas>` diinjeksikan secara terisolasi di dalam container `#stage` untuk memfasilitasi rendering WebGL layar penuh (*fixed inset: 0*).
   - Penggunaan W3C Standard `<script type="importmap">` untuk memetakan modul Three.js tanpa memerlukan *bundler* seperti Webpack, Vite, atau Rollup.

2. **CSS3:**
   - Desain responsif menggunakan fungsi matematis `clamp(min, preferred, max)` untuk skalabilitas tipografi dan posisi kontainer.
   - Efek antarmuka modern *frosted glass* menggunakan `backdrop-filter: blur(16px)` dan transparansi RGBA/HEX oktet.
   - Aturan optimasi rendering: `touch-action: none` pada kanvas WebGL guna mencegah konflik gestur bawaan peramban (seperti *swipe to navigate* atau *pull to refresh*).
   - Dukungan aksesibilitas via `@media (prefers-reduced-motion: reduce)`.

3. **JavaScript (ECMAScript 2020+ / ES Modules):**
   - Berjalan dalam mode modular (`<script type="module">`).
   - Pemanfaatan *destructuring*, *spread syntax*, *arrow functions*, *template literals*, dan native Web APIs (`performance.now()`, `requestAnimationFrame`, `window.devicePixelRatio`).

4. **Three.js (Version 0.169.0):**
   - Engine 3D utama berbasis WebGL.
   - Pemuatan library melalui CDN jsDelivr dengan dependensi add-on `OrbitControls.js`.

5. **Local Development Server:**
   - Python 3 built-in HTTP server (`python3 -m http.server 8000`).
   - Server lokal diperlukan untuk memenuhi standar keamanan browser terhadap pemuatan ES Modules (kebijakan CORS pada protokol `file://`).

---

## 3. Directory Structure & File Map

```
web3d-product-showcase/
├── index.html              # Single-file source code (HTML skeleton, CSS styling, Three.js script)
├── docs/                   # Direktori dokumentasi komprehensif
│   ├── PRD.md              # Product Requirement Document
│   ├── ARCHITECTURE.md     # System Architecture & Technical Specifications
│   └── USER_FLOW.md        # User Journey & Interaction Flow
└── README.md               # Dokumentasi utama repositori & panduan lokal
```

### Penjelasan Anatomi `index.html`:
- **Baris 1–7:** Doctype, meta tags (viewport, theme-color `#090d14`), dan title.
- **Baris 8–63:** Lembar gaya CSS komprehensif (reset, layout stage, floating UI topbar, status indicator, product-switcher, typography, glass controls panel, dan responsive media queries).
- **Baris 65–98:** Struktur DOM semantik untuk presentasi visual dan interaktivitas.
- **Baris 99–101:** Konfigurasi Import Map untuk pemetaan dependensi Three.js core dan addons.
- **Baris 102–277:** Skrip logika ES6+ yang mengatur siklus hidup 3D, konstruksi mesh prosedural, manajemen state, dan event listener.

---

## 4. 3D Rendering Engine & Subsystem Design

```
+---------------------------------------------------------------------------------+
|                               THREE.JS SCENE GRAPH                              |
|                                                                                 |
|  [THREE.Scene]                                                                  |
|    |                                                                            |
|    +---> [THREE.AmbientLight] (Color: 0xc3d5ee, Intensity: 1.05)                |
|    +---> [THREE.DirectionalLight (Key)] (0xffe5c7, 3.3, Casts PCF Soft Shadow)  |
|    +---> [THREE.DirectionalLight (Rim)] (0x83a8dc, 2.5)                         |
|    +---> [THREE.PointLight (Fill)] (0x9ab9dd, 18, Distance: 12)                 |
|    +---> [THREE.Mesh (Floor)] (CircleGeometry 200, MeshStandardMaterial)        |
|    |                                                                            |
|    +---> [THREE.Group (stage)] (Position Y: 0.12, Dynamic Yaw Rotation)         |
|            |                                                                    |
|            +---> [Product 1: Speaker Group] (Visible: true/false)               |
|            |       +-- Body Cylinder (MeshPhysicalMaterial)                     |
|            |       +-- Dark Rim Cylinders (MeshPhysicalMaterial)                |
|            |       +-- Speaker Grille (Partial Cylinder Segment)                |
|            |       +-- Accent Band (TorusGeometry)                              |
|            |       +-- Tactile Buttons (SphereGeometries)                       |
|            |                                                                    |
|            +---> [Product 2: Headphones Group] (Visible: true/false)            |
|            |       +-- Headband Tube (CatmullRomCurve3)                         |
|            |       +-- Cushion Pad Tube (CatmullRomCurve3)                      |
|            |       +-- Ear Cups (CylinderGeometries)                            |
|            |       +-- Ear Pads (TorusGeometries)                               |
|            |       +-- Acoustic Trim Plates (CylinderGeometries)                |
|            |                                                                    |
|            +---> [Product 3: Smartwatch Group] (Visible: true/false)            |
|                    +-- Silicon Strap Segments (BoxGeometries)                   |
|                    +-- Watch Case (BoxGeometry)                                 |
|                    +-- Dark Bezel & Cover Glass (BoxGeometries)                 |
|                    +-- Emissive UI Display Bars (MeshStandardMaterial)          |
|                    +-- Digital Crown & Side Push-Button (Cylinder/Box)          |
+---------------------------------------------------------------------------------+
```

### 4.1 Inisialisasi Renderer & Konfigurasi Pipeline Grafis
Renderer dikonfigurasi untuk menghasilkan rendering berkualitas tinggi mendekati standar CGI:

```javascript
const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: false });
renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
renderer.setSize(innerWidth, innerHeight);
renderer.shadowMap.enabled = true;
renderer.shadowMap.type = THREE.PCFSoftShadowMap;
renderer.outputColorSpace = THREE.SRGBColorSpace;
renderer.toneMapping = THREE.ACESFilmicToneMapping;
renderer.toneMappingExposure = 1.15;
```

**Keputusan Arsitektur:**
1. **`PCFSoftShadowMap`:** Menghasilkan penumbra bayangan yang halus dan realistis pada lantai studio.
2. **`ACESFilmicToneMapping`:** Standar industri film untuk memetakan rentang dinamis tinggi (HDR) ke layar SDR tanpa saturasi berlebih (*burnout* pada highlight terang).
3. **`setPixelRatio(Math.min(devicePixelRatio, 2))`:** Menghindari penurunan performa drastis pada perangkat dengan layar kerapatan tinggi (seperti smartphone modern dengan DPR 3x atau 4x), menjaga rendering tetap tajam pada batas 2x.

### 4.2 Kamera & Proyeksi Spasial
- **Tipe:** `THREE.PerspectiveCamera`
- **Field of View (FOV):** `34°` (Sudut pandang telephoto moderat untuk mengurangi distorsi perspektif dan memberikan tampilan produk yang lebih elegan dan proporsional).
- **Posisi Awal:** `(X: 4.5, Y: 3.0, Z: 7.5)`
- **Kliping Bidang:** `Near: 0.1`, `Far: 100`

### 4.3 Desain Rig Pencahayaan (4-Point Lighting Rig)
Pencahayaan studio diatur secara presisi untuk meniru teknik fotografi produk komersial:
1. **Key Light (Utama):** `THREE.DirectionalLight` berwarna hangat (`0xffe5c7`, intensitas `3.3`) pada posisi `(-4, 7, 5)`. Cahaya ini menghasilkan bayangan tajam terkontrol dengan *shadow bias* `-0.00015` untuk mengeliminasi artefak *shadow acne*.
2. **Rim Light (Siluet):** `THREE.DirectionalLight` berwarna sejuk (`0x83a8dc`, intensitas `2.5`) pada posisi `(5, 3, -4)`. Menyorot tepi kontur produk untuk memisahkannya dari latar belakang gelap.
3. **Fill Light (Pengisi):** `THREE.PointLight` bernuansa biru langit (`0x9ab9dd`, intensitas `18`, radius `12`) pada posisi `(-3, 2, -1)`. Menghilangkan area bayangan yang terlalu pekat dan menonjolkan detail permukaan samping.
4. **Ambient Light (Dasar):** `THREE.AmbientLight` (`0xc3d5ee`, intensitas `1.05`) yang menjaga visibilitas detail di seluruh bidang objek.

### 4.4 Arsitektur Material & Shading (PBR)
Material utama produk dibangun menggunakan `THREE.MeshPhysicalMaterial` yang memperluas kemampuan standar PBR dengan lapisan pernis (*clearcoat*):
- `metalness`: Dikontrol per komponen (0.22 - 0.55 untuk bodi, 0.72 - 0.82 untuk aksen logam).
- `roughness`: Dikontrol per komponen (0.20 - 0.28 untuk permukaan bodi halus, 0.72 - 0.82 untuk earpad dan kain grille).
- `clearcoat`: `0.7` untuk memberikan lapisan kilau kaca pelindung khas produk elektronik premium.
- `clearcoatRoughness`: `0.18` untuk sedikit membaurkan pantulan cahaya di lapisan pernis.

---

## 5. Animation & Render Loop (`requestAnimationFrame`)

Siklus rendering dijalankan secara berkelanjutan dengan sinkronisasi waktu berbasis *delta time*:

```javascript
let previousTime = 0;
function animate(time) {
  requestAnimationFrame(animate);
  const delta = previousTime ? Math.min((time - previousTime) / 1000, 0.05) : 0;
  previousTime = time;
  
  controls.update(); // Memperbarui inersia pergerakan OrbitControls
  
  if (time >= resumeRotationAt) idle = true;
  if (idle) stage.rotation.y += delta * 0.22; // Rotasi produk halus
  
  renderer.render(scene, camera);
}
```

### Logika Manajemen Keheningan (Idle State Machine):
- Variabel `idle` bernilai boolean yang menentukan apakah panggung (`stage`) berputar otomatis.
- Event `controls.addEventListener("start")`: Menandai pengguna sedang berinteraksi $\rightarrow$ `idle = false`.
- Event `controls.addEventListener("end")`: Menghitung waktu pemulihan rotasi $\rightarrow$ `resumeRotationAt = performance.now() + 2400`.
- Perubahan produk mengeset jeda pemulihan rotasi $\rightarrow$ `resumeRotationAt = performance.now() + 1200`.

---

## 6. State Management & Data Synchronization

Sistem menggunakan manajemen state terpusat berskala ringan (*lightweight centralized reactive state*):

```
+-------------------------------------------------------------+
|                        GLOBAL STATE                         |
|  - activeProduct: "speaker" | "headphones" | "watch"        |
|  - activeColor: 0 | 1 | 2                                   |
|  - idle: boolean                                            |
|  - resumeRotationAt: timestamp (ms)                         |
+-------------------------------------------------------------+
                               |
            +------------------+------------------+
            |                                     |
            v                                     v
+------------------------+           +------------------------+
|   updateProduct(key)   |           |    applyColor(index)   |
+------------------------+           +------------------------+
| 1. Switch visibility   |           | 1. Mutate activeColor  |
| 2. Sync DOM text/specs |           | 2. Iterate colorMats   |
| 3. Set mailto subject  |           | 3. Invoke .color.set() |
| 4. Update tab active   |           | 4. Update swatch ARIA  |
| 5. Reset to color #0   |           +------------------------+
| 6. Adjust Orbit target |
| 7. Set idle resume     |
+------------------------+
```

### 6.1 Sinkronisasi Produk (`updateProduct(key)`)
Ketika pengguna mengklik tab produk:
1. Mengubah `activeProduct = key`.
2. Mengiterasi entri kamus objek 3D `products`: menyetel `product.group.visible = (name === key)`.
3. Memperbarui elemen teks DOM secara selektif (`#product-title`, `#product-category`, `#product-description`, `#product-specs`, dan tautan `#buy-button`).
4. Menyelaraskan status aksesibilitas tombol tab melalui atribut `aria-pressed`.
5. Menyetel kembali varian warna ke opsi pertama (`applyColor(0)`).
6. Mengatur ulang titik tumpu kamera orbit (`controls.target.set(0, yOffset, 0)`), di mana produk headphone memiliki titik tengah elevasi lebih tinggi ($Y = 1.45$) dibanding produk lain ($Y = 1.15$).

### 6.2 Sinkronisasi Warna Material (`applyColor(index)`)
Ketika pengguna memilih warna dari palet:
1. Memperbarui `activeColor = index`.
2. Mengakses array referensi material warna produk aktif (`product.colorMaterials`).
3. Menjalankan mutasi warna langsung pada GPU melalui Three.js Color API:
   ```javascript
   product.colorMaterials.forEach((material) => material.color.set(palette[index]));
   ```
4. Memperbarui atribut visual penanda tombol swatch `aria-pressed="true"`.

---

## 7. Performance & Optimization Architecture

1. **Procedural Geometry vs Network Transfer:**
   - Seluruh model 3D dibangun secara prosedural dari geometri primitif Three.js (`CylinderGeometry`, `BoxGeometry`, `TubeGeometry`, `TorusGeometry`, `SphereGeometry`).
   - Ukuran transfer dokumen HTML adalah $\approx 21 \text{ KB}$ tanpa unduhan file eksternal selain Three.js bundle, menghasilkan waktu pemuatan awal yang hampir instan.
2. **Culling & Visibility Optimization:**
   - Produk yang tidak aktif dinonaktifkan properti visibilitasnya (`group.visible = false`). Three.js secara otomatis melewati (*cull*) objek tidak terlihat selama tahapan *frustum culling* dan *shadow pass*, menghemat *draw calls*.
3. **Clamping Delta Time:**
   - `Math.min((time - previousTime) / 1000, 0.05)` mencegah fenomena *frame skipping* atau lonjakan kalkulasi matematis ketika peramban dibuka kembali setelah diminimalkan.
4. **Dynamic Viewport Resize Handling:**
   - Event listener `resize` memperbarui rasio aspek kamera (`camera.aspect`), matriks proyeksi (`camera.updateProjectionMatrix`), dan resolusi kanvas buffer renderer secara akurat.
