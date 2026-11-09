# User Journey & Interaction Flow
## Forma — Interactive 3D Web Product Showcase

- **Document Version:** 1.0.0
- **Audience:** Product Designers, Frontend Engineers, QA Engineers, UI/UX Researchers
- **Scope:** End-to-End User Experience & Interaction State Lifecycle

---

## 1. Overview & Intent

Dokumen ini mendefinisikan seluruh alur perjalanan pengguna (*user journey*), titik sentuh interaksi (*interaction touchpoints*), dan transisi status sistem (*system state transitions*) pada aplikasi **Forma — Interactive 3D Product Showcase**.

Tujuan utama alur ini adalah memberikan pengalaman eksplorasi produk yang imersif, intuitif, bebas gesekan (*frictionless*), serta mengarahkan minat pengguna secara alami menuju tindakan pemesanan (*conversion/pre-order*).

---

## 2. End-to-End User Journey Map

```
+-----------------------------------------------------------------------------------------------------+
|                                          USER JOURNEY MAP                                           |
+-------------------+--------------------+---------------------+------------------+-------------------+
| 1. DISCOVERY &    | 2. SPATIAL         | 3. PRODUCT          | 4. MATERIAL &    | 5. EVALUATION &   |
|    FIRST IMPRESSION|    EXPLORATION     |    SWITCHING        |    COLORING      |    CONVERSION     |
+-------------------+--------------------+---------------------+------------------+-------------------+
| Pengguna membuka  | Mengorbit, zoom,   | Mengganti lini      | Menguji varian   | Membaca spesifikasi|
| halaman web; 3D   | dan panning kamera | produk via tab 01,  | warna fisik      | teknis dan klik   |
| scene langsung    | pada produk aktif  | 02, atau 03         | Sand, Slate, Rose| Pre-order / Buy   |
| berputar otomatis |                    |                     |                  |                   |
+-------------------+--------------------+---------------------+------------------+-------------------+
| Emosi: Terpukau & | Emosi: Penasaran & | Emosi: Tertarik     | Emosi: Terlibat  | Emosi: Yakin &    |
| Tertarik          | Memegang Kontrol   | Menjelajah          | Personalisasi    | Siap Membeli      |
+-------------------+--------------------+---------------------+------------------+-------------------+
```

---

## 3. Detailed Step-by-Step Narrative Flow

### Tahap 1: Initial Landing & Hero Experience
1. **Akses URL:** Pengguna membuka tautan showcase web melalui peramban desktop atau mobile.
2. **Pemuatan Panggung 3D:**
   - Kanvas WebGL diinisialisasi dari geometri procedural tanpa local model/texture assets; durasi loading aktual belum diukur.
   - Produk default (**Sonic One Speaker**) muncul di tengah panggung dengan material bawaan (Sand `#c5a982`).
   - Lampu studio menyoroti detail bodi produk, menciptakan bayangan lembut pada lantai panggung.
3. **Auto-Rotate Indikator:**
   - Panggung berputar secara perlahan dan halus pada sumbu Y (kecepatan $0.22 \text{ rad/s}$).
   - Status visual `"Interactive preview"` dengan indikator hijau di pojok kiri atas menginformasikan bahwa objek dapat digerakkan secara langsung.
   - UI overlay menampilkan teks produk, spesifikasi utama (360° Spatial Sound, 24 h Battery, IP67 Waterproof), dan panel pemilih warna.

### Tahap 2: 3D Spatial Exploration (360° Navigation)
1. **Interaksi Pengguna Dimulai:**
   - Pengguna mengklik dan menyeret mouse (*left-click drag*) pada desktop, atau menyentuh dan menggeser satu jari pada layar sentuh ponsel.
2. **Respon Sistem:**
   - Mode rotasi otomatis (*idle auto-rotate*) seketika berhenti secara mulus tanpa sentakan.
   - Orbit kamera Three.js merespon langsung dengan inersia (*damping factor: 0.06*), memberikan sensasi fisik yang berbobot.
3. **Pemeriksaan Detail (Zooming & Panning):**
   - **Zoom:** Pengguna memutar roda mouse atau melakukan gestur cubit (*pinch*) di ponsel. Kamera mendekat hingga batas aman `minDistance: 4.2` unit untuk memeriksa tekstur tombol atau menjauh hingga `maxDistance: 12.0` unit untuk melihat proporsi keseluruhan.
   - **Pan:** Pengguna melakukan klik kanan dan menyeret mouse untuk menggeser sudut pandang horizontal/vertikal.
   - **Batas Elevasi Kamera:** Sistem menahan sudut pandang kamera agar tidak menembus bagian bawah lantai studio melalui batas sudut polar maksimum $88.2^\circ$.

### Tahap 3: Product Switching (Koleksi Produk)
1. **Aksi Pengguna:**
   - Pengguna mengklik salah satu tombol switcher angka di sisi kiri layar:
     - `01` $\rightarrow$ Sonic One (Speaker Silinder)
     - `02` $\rightarrow$ Studio Arc (Headphone Over-Ear)
     - `03` $\rightarrow$ Form Watch (Smartwatch Premium)
2. **Respon Sistem:**
   - **Visibilitas 3D:** Model 3D sebelumnya disembunyikan, dan model produk yang baru langsung ditampilkan.
   - **Penyesuaian Kamera Spasial:** Ketinggian titik fokus kamera (`controls.target`) disesuaikan secara otomatis (misal: naik ke $Y = 1.45$ saat beralih ke headphone agar headband dan earcup berada tepat di tengah pandangan).
   - **Sinkronisasi Teks & Tipografi:**
     - Kategori seri diperbarui (contoh: `"Series 02 · Audio"`).
     - Judul produk diperbarui secara instan dengan efek tipografi responsif.
     - Deskripsi produk menampilkan narasi desain terkait.
     - Blok spesifikasi diperbarui dengan data perangkat keras yang relevan (misal: 40 mm Drivers, 38 h Battery, ANC Adaptive).
   - **Sinkronisasi Status Pembelian:** Label tombol aksi diperbarui secara kontekstual (misal menjadi `"Buy now"` untuk headphone atau `"Pre-order"` untuk produk seri lainnya).
   - **Reset Palet:** Pilihan warna dikembalikan ke warna standar pertama (Sand), dan rotasi otomatis diberi jeda *cooldown* selama 1200 ms.

### Tahap 4: Material & Color Personalization
1. **Aksi Pengguna:**
   - Pengguna melihat panel mengambang di pojok kanan bawah bertajuk `"PILIH WARNA"`.
   - Pengguna mengklik salah satu dari tiga lingkaran warna (*swatches*):
     - Lingkaran 1: **Sand** (`#c5a982`)
     - Lingkaran 2: **Slate** (`#647f9e`)
     - Lingkaran 3: **Rose** (`#a56768`)
2. **Respon Sistem:**
   - Warna material fisik 3D produk berganti secara instan di layar tanpa jeda pemuatan atau kedipan (*flicker*).
   - Kilauan lapisan *clearcoat* dan refleksi pencahayaan tetap bereaksi secara realistis terhadap warna baru.
   - Tombol warna yang dipilih menampilkan cincin penanda fokus ganda (*double-ring focus indicator*) dan status ARIA diperbarui menjadi `aria-pressed="true"`.

### Tahap 5: Action & Pre-Order Conversion
1. **Aksi Pengguna:**
   - Pengguna merasa yakin setelah memeriksa detail 360 derajat, kecocokan warna, dan spesifikasi produk.
   - Pengguna menekan tombol aksi utama (`Pre-order` / `Buy now`).
2. **Respon Sistem:**
   - Klien membuka aplikasi email bawaan pengguna (*default mail client*) melalui protokol `mailto:hello@forma.example`.
   - Subjek email terisi secara otomatis sesuai produk yang sedang aktif (contoh: `subject=Order%20Sonic%20One` atau `subject=Order%20Studio%20Arc`).
   - Membuka kanal komunikasi langsung antara calon pembeli dengan tim penjualan Forma.

---

## 4. State Diagram & Interaction Logic Flowchart

### 4.1 Diagram Alir Logika Pengguna (Flowchart)

```
                     +---------------------------+
                     |   Pengguna Membuka Web    |
                     +---------------------------+
                                   |
                                   v
                     +---------------------------+
                     |  Inisialisasi Three.js    |
                     |  Render Speaker + Sand    |
                     |  Idle Auto-Rotate: ON     |
                     +---------------------------+
                                   |
            +----------------------+----------------------+
            |                                             |
            v (Sentuhan / Drag Kamera)                    v (Klik Tab Produk)
+-----------------------+                     +-------------------------+
| Event: controls.start |                     | Event: click .product-tab|
| idle = false          |                     | Switch activeProduct    |
| Hentikan Auto-Rotate  |                     | Update UI & Specs DOM   |
+-----------------------+                     | Adjust Camera Target    |
            |                                 | Set Cooldown: +1200ms   |
            v                                 +-------------------------+
+-----------------------+                                 |
| Pengguna Melakukan    |                                 v
| Orbit / Zoom / Pan    |                     +-------------------------+
+-----------------------+                     | Kembali ke Idle Loop    |
            |                                 +-------------------------+
            v (Lepas Sentuhan / Mouse)                    |
+-----------------------+                                 |
| Event: controls.end   |                                 v (Klik Swatch Warna)
| Cooldown: +2400ms     |                     +-------------------------+
| resumeRotationAt diisi|                     | Event: click .swatch    |
+-----------------------+                     | Mutasi Material Color   |
            |                                 | Update ARIA & Highlight |
            v                                 +-------------------------+
+-----------------------+                                 |
| Waktu >= Cooldown?    |                                 v (Klik Tombol CTA)
|  --> idle = true      |                     +-------------------------+
|  --> Lanjut Berputar  |                     | Trigger mailto: link    |
+-----------------------+                     | Pre-filled Product Info |
                                              +-------------------------+
```

### 4.2 State Transition Table

| State Saat Ini | Input / Trigger Event | Kondisi / Guard | State Berikutnya | Aksi Sistem |
| :--- | :--- | :--- | :--- | :--- |
| `IDLE_ROTATING` | Pointer Down / Touch Start pada kanvas | - | `MANUAL_ORBITING` | `idle = false`, setel `stage.rotation.y` statis |
| `MANUAL_ORBITING` | Pointer Move / Touch Drag | - | `MANUAL_ORBITING` | Kalkulasi pergerakan kamera via `OrbitControls.update()` |
| `MANUAL_ORBITING` | Pointer Up / Touch End | - | `INTERACTION_PAUSED` | Catat `resumeRotationAt = now() + 2400ms` |
| `INTERACTION_PAUSED`| Timer Tick (`animate()`) | `now() >= resumeRotationAt` | `IDLE_ROTATING` | `idle = true`, lanjutkan inkrementasi rotasi |
| *Any State* | Klik Tab Produk (`01/02/03`)| Tab berbeda dari produk aktif | `PRODUCT_SWITCHING`| Sembunyikan mesh lama, tampilkan mesh baru, update DOM, `resumeRotationAt = now() + 1200ms` |
| *Any State* | Klik Swatch Warna | Indeks warna berbeda | `COLOR_APPLIED` | Ubah nilai warna material PBR, perbarui `aria-pressed` |
| *Any State* | Jendela Browser Diubah Ukurannya | Ukuran window berubah | `VIEWPORT_RESIZED` | Hitung ulang rasio aspek kamera dan ukuran renderer |

---

## 5. Edge Cases & Exception Handling

### 5.1 Konflik Gestur Layar Sentuh Mobile (Gesture Collision)
- **Tantangan:** Pada perangkat mobile, gestur *drag* vertikal pengguna sering memicu *scroll* halaman atau *pull-to-refresh* bawaan browser daripada memutar objek 3D.
- **Solusi Sistem:** Menerapkan CSS `touch-action: none` pada elemen `#stage canvas`. Hal ini memerintahkan mesin rendering browser untuk menyerahkan kendali penanganan gestur sentuh sepenuhnya kepada modul `OrbitControls`.

### 5.2 Kliping Objek & Disorientasi Sudut Kamera (Extreme Camera Angles)
- **Tantangan:** Pengguna dapat memutar kamera hingga melihat bagian bawah lantai studio atau memperbesar terlalu dekat hingga masuk ke dalam geometri produk.
- **Solusi Sistem:** 
  - `controls.minPolarAngle = 0.25`: Mencegah gimbal-lock tepat di sumbu kutub atas.
  - `controls.maxPolarAngle = Math.PI * 0.49`: Memotong sudut pandang tepat sebelum permukaan lantai, sehingga bagian bawah tanah tidak pernah terlihat.
  - `controls.minDistance = 4.2` dan `controls.maxDistance = 12.0`: Menjaga pembesaran kamera selalu berada dalam zona proporsional.

### 5.3 Perubahan Orientasi Layar (Device Orientation Change / Window Resize)
- **Tantangan:** Rotasi perangkat dari portrait ke landscape atau perubahan ukuran jendela browser desktop menyebabkan gambar terdistorsi (gepeng/melar).
- **Solusi Sistem:** Handler `onResize()` secara aktif membaca `innerWidth / innerHeight`, mengupdate proyeksi kamera dengan `camera.updateProjectionMatrix()`, dan mereset buffer canvas menggunakan `renderer.setSize()`.

### 5.4 Preferensi Pengurangan Gerakan Pengguna (Accessibility - Reduced Motion)
- **Tantangan:** Pengguna dengan gangguan vestibular mengalami pusing jika antarmuka web memutar objek atau melakukan transisi gerakan secara konstan.
- **Solusi Sistem:** CSS dilengkapi dengan `@media (prefers-reduced-motion: reduce)` yang memangkas waktu animasi UI ke `0.01ms`. Pada level JavaScript, kontrol kamera orbit tetap memberikan kendali penuh kepada pengguna tanpa memaksa akselerasi mendadak.
