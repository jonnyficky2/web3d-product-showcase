# Product Requirement Document (PRD)
## Forma — Interactive 3D Web Product Showcase

- **Document Version:** 1.0.0
- **Status:** Approved / Production Ready
- **Author:** Senior Software Architect & Technical Product Manager
- **Target Release:** Q1 2025
- **Technology Base:** Three.js (r169), HTML5, CSS3, ES6+

---

## 1. Executive Summary & Project Background

### 1.1 Latar Belakang
Dalam lanskap e-commerce dan presentasi produk digital modern, media visual 2D konvensional (foto statis dan video pra-render) kerap kali gagal memberikan gambaran spasial, skala, detail tekstur material, serta interaktivitas yang memadai bagi calon pembeli. Hal ini berkontribusi pada keraguan dalam pengambilan keputusan pembelian dan tingginya tingkat retur barang di industri hardware premium.

**Forma — Interactive 3D Product Showcase** adalah aplikasi web interaktif *zero-install* berbasis WebGL dan Three.js yang memungkinkan calon konsumen mengeksplorasi lini produk hardware premium secara 360 derajat secara langsung di dalam peramban web (*browser*), baik pada perangkat desktop maupun mobile. 

Melalui kombinasi *Physically Based Rendering* (PBR), pencahayaan sinematik multi-sumber, kontrol orbit kamera yang halus, dan kustomisasi warna *real-time*, Forma menghadirkan pengalaman digital setara *showroom* fisik dengan performa tinggi tanpa memerlukan plugin pihak ketiga atau waktu pemuatan (*loading time*) yang berat.

### 1.2 Visi Produk
Menjadi fondasi pengalaman belanja digital generasi baru yang menjembatani produk fisik dengan ruang digital melalui visualisasi 3D real-time berkinerja tinggi, elegan, responsif, dan mudah diintegrasikan ke platform e-commerce manapun.

---

## 2. Problem Statement & Target Audience

### 2.1 Problem Statement
1. **Kurangnya Pemahaman Spasial:** Konsumen kesulitan memvisualisasikan proporsi, dimensi nyata, dan sudut pandang ergonomis produk hanya dari foto katalog 2D standar.
2. **Keterbatasan Evaluasi Material:** Material premium (seperti *matte polycarbonate*, *brushed metal*, kaca dengan indeks refraksi khusus) memerlukan pantulan cahaya dinamis untuk dinilai kualitasnya secara autentik.
3. **Pemuatan Aset Berat pada 3D Konvensional:** Banyak implementasi 3D web membebani jaringan pengguna dengan file GLTF berukuran puluhan megabyte, menurunkan performa dan meningkatkan rasio pentalan (*bounce rate*).
4. **Disiplin Navigasi Mobile yang Buruk:** Interaksi navigasi 3D pada perangkat layar sentuh (*touchscreen*) sering kali bentrok dengan gestur *scroll* halaman web (*gesture conflict*).

### 2.2 Target Pengguna (User Personas)

#### Persona Primer: Calon Pembeli Gadget Premium ("The Design-Conscious Buyer")
- **Profil:** Usia 22–40 tahun, mengutamakan estetika, *build quality*, dan fungsionalitas produk teknologi.
- **Kebutuhan:** Memeriksa detail fisik produk dari berbagai sudut (360°), membandingkan varian warna material secara instan, serta memverifikasi spesifikasi inti sebelum melakukan *pre-order*.
- **Pain Point:** Ragu membeli produk tanpa melihat bagaimana warna berinteraksi dengan cahaya ambient nyata; frustrasi jika situs lambat dimuat di ponsel.

#### Persona Sekunder: Tim Pemasaran & Brand Manager ("The Digital Merchandiser")
- **Profil:** Tim produk dan perancang web e-commerce.
- **Kebutuhan:** Media promosi produk yang interaktif untuk meningkatkan *time on site* dan konversi *lead* pre-order tanpa ketergantungan pada backend kompleks.
- **Pain Point:** Biaya pembuatan aset animasi video 3D pra-render yang mahal dan tidak fleksibel ketika ada perubahan varian warna produk.

---

## 3. Product Goals & Success Metrics (KPIs)

| Kategori Metrik | Key Performance Indicator (KPI) | Target |
| :--- | :--- | :--- |
| **Keterlibatan Pengguna** | Rata-rata durasi interaksi (*Session Duration*) | > 60 detik per sesi |
| **Interaktivitas** | Rasio interaksi 3D (Orbiting / Zooming / Color Swatch) | > 75% pengunjung unik |
| **Efisiensi Performa** | *Frame Rate* Rata-rata (*Desktop & High-tier Mobile*) | 60 FPS stabil (min. 45 FPS di low-tier) |
| **Waktu Pemuatan** | *First Contentful Paint* (FCP) & 3D Stage Ready | < 1.5 detik pada koneksi 4G standar |
| **Konversi Bisnis** | *Click-through Rate* (CTR) pada tombol Call to Action (CTA) | > 8.5% dari total pengunjung aktif |

---

## 4. Fitur Utama & Functional Requirements (FR)

### FR-1: Multi-Product Switcher (Koleksi Produk)
- **Deskripsi:** Pengguna dapat berpindah antar lini produk secara mulus melalui panel navigasi tab vertikal (`01`, `02`, `03`).
- **Lini Produk yang Didukung:**
  1. **Series 01 · Audio — Sonic One:** Speaker silinder berdesain minimalis dengan aksen grille audio dan tombol kontrol atas.
  2. **Series 02 · Audio — Studio Arc:** Headphone *over-ear* ergonomis dengan lengkungan headband Catmull-Rom, *cushioned ear pads*, dan *metal acoustic plates*.
  3. **Series 03 · Wearable — Form Watch:** Smartwatch digital berpresisi tinggi dengan casing logam, tali silikon bertekstur, layar digital berpendar (*emissive display*), dan *tactile crown button*.
- **Perilaku Sistem:**
  - Menampilkan produk yang dipilih secara eksklusif dengan mengatur properti visibilitas objek 3D.
  - Memperbarui teks metadata (Kategori, Judul, Deskripsi, Spesifikasi Teknis, dan Status Tombol Aksi) secara sinkron.
  - Menyesuaikan target kamera (`OrbitControls.target`) secara otomatis berdasarkan ketinggian pusat massa produk (misal: penyesuaian khusus untuk headphone pada ketinggian $Y = 1.45$).
  - Menyetel ulang pilihan warna aktif ke palet default (`index: 0`).

### FR-2: Real-Time Material & Color Customizer
- **Deskripsi:** Pengguna dapat memilih dan mengaplikasikan palet warna finishing produk secara instan tanpa proses render ulang atau jeda jaringan.
- **Palet Warna:**
  - **Sand:** `#c5a982` (Nuansa hangat, organik, premium matte).
  - **Slate:** `#647f9e` (Nuansa modern industrial, sejuk, profesional).
  - **Rose:** `#a56768` (Nuansa kontemporer elegan, terracotta lembut).
- **Perilaku Sistem:**
  - Mengubah properti warna `color.set()` pada instance `MeshPhysicalMaterial` inti produk yang bersangkutan.
  - Mempertahankan karakteristik pantulan optik material (`metalness`, `roughness`, `clearcoat`, `clearcoatRoughness`) saat warna berganti.
  - Memperbarui status visual tombol warna (`swatch`) dengan penanda *active state* (`aria-pressed="true"`).

### FR-3: Smooth Orbit Controls & Camera Manipulation
- **Deskripsi:** Sistem kontrol kamera 3D spasial yang memungkinkan pengguna menginspeksi produk dari berbagai sudut pandang.
- **Fitur Kontrol:**
  - **Rotasi (Orbit):** Klik kiri dan seret (Desktop) atau seret satu jari (Mobile).
  - **Pembesaran (Zoom):** Roda mouse / *scroll* (Desktop) atau gestur cubit / *pinch-to-zoom* (Mobile).
  - **Geser Spasial (Pan):** Klik kanan dan seret atau tombol kombinasi.
  - **Damping Inersia:** Damping halus dengan koefisien inersia `0.06` untuk transisi pergerakan yang organik.
  - **Pembatas Sudut Polar:** Membatasi rotasi vertikal kamera dari `minPolarAngle = 0.25 rad` hingga `maxPolarAngle = 1.54 rad` ($\approx 88.2^\circ$), mencegah kamera menembus lantai panggung 3D.
  - **Pembatas Jarak Kamera:** Jarak zoom dibatasi antara radius minimum 4.2 unit hingga maksimum 12.0 unit untuk mencegah kliping objek.

### FR-4: Studio Lighting & Shadow System
- **Deskripsi:** Sistem pencahayaan studio 4-titik terkalibrasi untuk memunculkan kedalaman bentuk produk secara realistis.
- **Komposisi Lighting:**
  - **Ambient Light (`0xc3d5ee`, intensitas 1.05):** Mengisi bayangan gelap dengan warna dingin lembut.
  - **Key Light (`DirectionalLight` `0xffe5c7`, intensitas 3.3):** Sumber cahaya utama hangat yang menghasilkan bayangan dinamis (*soft shadows* via `PCFSoftShadowMap` 2048x2048).
  - **Rim Light (`DirectionalLight` `0x83a8dc`, intensitas 2.5):** Memberikan siluet kontur produk pada sisi belakang berlawanan.
  - **Fill Light (`PointLight` `0x9ab9dd`, intensitas 18, jarak 12):** Menambah volume visual pada bagian samping bawah produk.

### FR-5: Intelligent Idle Auto-Rotate & Resume Mechanism
- **Deskripsi:** Produk berputar perlahan secara otomatis untuk menarik perhatian visual pengguna saat tidak ada interaksi langsung.
- **Mekanisme Otomatisasi:**
  - Rotasi sumbu Y pada panggung pameran dengan kecepatan angular konstan yang dikalibrasi oleh *delta time* ($\approx 0.22 \text{ rad/s}$).
  - Deteksi interaksi pengguna: Ketika pengguna mulai menyentuh/menggerakkan kontrol kamera (`start`), auto-rotate langsung dinonaktifkan.
  - Resume Timer: Setelah interaksi pengguna selesai (`end`), rotasi otomatis akan aktif kembali setelah jeda *cooldown* selama 2400 ms.
  - Peralihan produk memberikan jeda *cooldown* selama 1200 ms sebelum memulai rotasi kembali.

### FR-6: Contextual Metadata & Direct Action (CTA)
- **Deskripsi:** UI overlay yang menampilkan informasi produk terkini dan mengarahkan pengguna ke alur pemesanan (*pre-order* atau pembelian langsung).
- **Elemen Metadata:**
  - Eyebrow kategori seri produk.
  - Judul produk dengan tipografi besar dan jelas.
  - Deskripsi singkat karakteristik produk.
  - Tiga pilar spesifikasi perangkat keras (misal: Spatial Sound, Daya Tahan Baterai, Rating Tahan Air).
  - Tombol CTA yang secara dinamis memperbarui teks (`Pre-order` / `Buy now`) serta tautan URL `mailto:` dengan subjek terenkode sesuai produk yang sedang aktif.

---

## 5. Non-Functional Requirements (NFR)

### 5.1 Performa & Efisiensi Rendering
- **Frame Rate Target:** Menjaga kestabilan 60 frame per detik pada resolusi standar layar 1080p.
- **Pixel Ratio Limiter:** Penggunaan `Math.min(window.devicePixelRatio, 2)` untuk mencegah pemborosan komputasi pada layar Retina resolusi ekstrem (misal 3x atau 4x DPR).
- **Delta-Time Clamping:** Perhitungan waktu animasi dibatasi maksimal `0.05s` per frame guna mencegah lonjakan rotasi (*stutter/teleport*) saat browser beralih tab.
- **Memory Footprint:** Menggunakan geometri prosedural Three.js berbobot ringan; total konsumsi memori heap JavaScript di bawah 45 MB.

### 5.2 Kompatibilitas Browser & Platform
- **Dukungan Platform:**
  - Desktop: Google Chrome (v90+), Mozilla Firefox (v90+), Apple Safari (v15+), Microsoft Edge (v90+).
  - Mobile: Safari iOS (iOS 15+), Chrome for Android (Android 10+).
- **Standar WebGL:** Mendukung WebGL 1.0 dan WebGL 2.0 dengan ekstensi *standard derivatives* dan *floating-point textures*.

### 5.3 Responsivitas & Desain Antarmuka (Responsive UI)
- **Viewport Fluidity:** Desain antarmuka memanfaatkan fungsi CSS modern seperti `clamp()`, Flexbox, dan CSS Grid untuk adaptasi layar dari ukuran mobile (320px) hingga layar lebar 4K.
- **Mobile Mode (< 680px):**
  - Penyederhanaan header (navigasi teks disembunyikan untuk memprioritaskan ruang 3D).
  - Reposisi panel kontrol ke bagian bawah layar secara penuh.
  - Tombol aksi ditempatkan secara ergonomis pada zona jangkauan ibu jari (*thumb zone*).

### 5.4 Aksesibilitas (a11y) & Standar Web
- **Semantik HTML5:** Pemanfaatan tag `<main>`, `<header>`, `<nav>`, `<section>`, dan `<aside>`.
- **Atribut WAI-ARIA:** Elemen interaktif dilengkapi dengan `aria-label`, `aria-pressed`, dan `aria-labelledby` untuk dukungan *screen reader*.
- **Prefers-Reduced-Motion:** Menyediakan query CSS `@media (prefers-reduced-motion: reduce)` yang mematikan durasi transisi CSS bagi pengguna dengan sensitivitas vestibular.

---

## 6. Ruang Lingkup (Scope & Boundaries)

### 6.1 Dalam Ruang Lingkup (In-Scope — V1.0)
- Rendering 3D real-time 3 produk hardware berbasis geometri prosedural presisi.
- Kontrol kamera orbit penuh dengan pembatas elevasi dan jarak.
- Kustomisasi 3 variasi warna fisik produk.
- UI overlay minimalis dengan panel kaca *frosted glass* (`backdrop-filter: blur(16px)`).
- Tautan pemesanan via email terstruktur (`mailto`).

### 6.2 Di Luar Ruang Lingkup (Out-of-Scope — V1.0)
- Sistem pembayaran langsung (*checkout payment gateway* seperti Stripe/Midtrans).
- Akun pengguna atau sistem otentikasi.
- Fitur Augmented Reality (WebXR / QuickLook).
- Modul pemutar audio interaktif untuk simulasi suara speaker/headphone.

---

## 7. Future Product Roadmap

```
2025 Q1 (Current V1.0)  -->  2025 Q2 (Phase 2: Asset Pipeline)  -->  2025 Q3 (Phase 3: Immersive XR)  -->  2025 Q4 (Phase 4: Commerce API)
[Procedural 3D Models]        [GLTF / Draco Compression]            [WebXR & Apple AR QuickLook]         [Shopify & Cart API Hook]
[PBR Material Switching]      [Texture Maps (Normal, Roughness)]     [Interactive Audio Simulator]        [Analytics & Heatmap Event]
```

### Fase 2 (Q2 2025): Peningkatan Pipeline Aset & Tekstur Fotorealistik
- Migrasi dari geometri prosedural ke pemuatan model eksternal berkualitas tinggi format `.glb`/`.gltf` dengan kompresi **DRACO** dan tekstur terkompresi **KTX2/Basis Universal**.
- Penambahan peta tekstur mikro (*Normal Map*, *Roughness Map*, dan *Ambient Occlusion Map*) untuk mensimulasikan serat kain pada earpad headphone dan sikat logam pada bodi smartwatch.

### Fase 3 (Q3 2025): Augmented Reality & Eksplorasi Imersif
- Integrasi tombol "View in your room" menggunakan modul **WebXR Device API** untuk perangkat Android dan **USDZ / AR Quick Look** untuk perangkat Apple iOS.
- Fitur *Exploded View Animation* (animasi pembongkaran komponen internal) untuk memamerkan arsitektur driver speaker dan sensor detak jantung jam tangan.
- Audio preview simulator yang memutar cuplikan suara spasial 3D interaktif.

### Fase 4 (Q4 2025): Integrasi E-Commerce & Telemetri Analitik
- Integrasi langsung dengan API e-commerce (Shopify Storefront API, WooCommerce, atau custom GraphQL checkout).
- Sistem pelacak telemetri interaksi pengguna (misal: waktu orientasi sudut pandang kamera terlama, kombinasi warna terfavorit) yang terhubung ke platform analitik produk.
