# Product Requirement Document (PRD)
## Forma — Interactive 3D Web Product Showcase

- **Document Version:** 1.1.0
- **Status:** Prototype / Pre-production hardening
- **Author:** Senior Software Architect & Technical Product Manager
- **Target Release:** UNKNOWN; deployment and production verification are not configured
- **Technology Base:** Three.js (r169), HTML5, CSS3, ES6+

---

## 1. Spesifikasi Produk Lengkap (Product Line-up)

### 1. Sonic One — Smart Speaker
- **Seri:** 01 · Audio
- **Desain:** Silinder minimalis, bold grille audio, vertical tactile buttons, bottom weighted.
- **Material:**
  - Matte Polycarbonate Premium
  - Brushed Aluminum (accent)
  - Acoustic-fabric grille
- **Dimensi:** 120 × 220 mm
- **Berat:** 1.45 kg
- **Warna Varian:**
  - Sand (`#c5a982`): Premium matte
  - Slate (`#647f9e`): Industrial smooth
  - Rose (`#a56768`): Stylish terracotta
- **Fitur Hardware:**
  - Sistem Speaker 360° Spatial (multi-driver, passive bass)
  - Baterai 24 jam (Lithium 8,000mAh, fast charging USB-C)
  - Sertifikasi IP67 Waterproof
  - Panel kontrol sentuh dan tombol taktil di upper deck
  - Dual far-field microphones (voice assistant ready)
- **Spesifikasi Audio:**
  - Output: 40W RMS / Dual mid-bass driver / Dual passive radiator
  - Respon frekuensi: 45Hz–18kHz
  - Support lossless streaming (AirPlay 2, Bluetooth 5.3, USB Audio)
- **Packaging:** Recycled kraft box, protective foam, quick guide, USB-C charging cable.

### 2. Studio Arc — Over-Ear Headphones
- **Seri:** 02 · Audio
- **Desain:** Dynamic Catmull-Rom headband, floating earcup, magnetic cushion pad swap.
- **Material:**
  - CNC Aluminum Earplate (anodized finish)
  - Vegan Leather Earpad (memory foam)
  - Polycarbonate arms
- **Dimensi:** 189 × 83 × 214 mm (extendable band)
- **Berat:** 294 g
- **Warna Varian:**
  - Sand (`#c5a982`): Soft matte
  - Slate (`#647f9e`): Frosted cool
  - Rose (`#a56768`): Rose gold accent
- **Fitur Hardware:**
  - Dynamic 40 mm drivers (tuned for punchy bass and sparkling detail)
  - Active Noise Cancelling (ANC) Hybrid, 4-mic array
  - Adaptive Transparency Mode
  - 38 jam pemakaian (900mAh cell), fast charge (10 mnt = 7 jam play)
  - Bluetooth 5.3/Multi-device Switch
  - Integrated digital DAC (USB-C audio)
  - Touch gesture: Tap/slide untuk volume & skip
- **Spesifikasi Audio:**
  - Distorsi < 0.2%@1kHz/100dBSPL
  - Sensitivitas: 108dB/mW
  - Frequency: 18Hz–22kHz

### 3. Form Watch — Premium Smartwatch
- **Seri:** 03 · Wearable
- **Desain:** Rounded rectangle, CNC stainless steel case, full-glass AMOLED, integrated soft touch strap.
- **Material:**
  - 316L Stainless Steel
  - Emissive AMOLED always-on display (sapphire glass cover)
  - Silicone textured strap (quick release)
- **Dimensi:** 43 × 38 × 10.5 mm (case) | Strap 22 mm
- **Berat:** 48 g (tanpa strap)
- **Warna Varian:**
  - Sand (`#c5a982`): Champagne bezel
  - Slate (`#647f9e`): Shadow blue
  - Rose (`#a56768`): Rose mist
- **Fitur Hardware:**
  - AMOLED Always-on Display (326ppi, 800 nits peak)
  - Battery life: 7 hari typical use (LiPo 320mAh)
  - Layar sentuh Gorilla Glass
  - Water resistant 5ATM (swim proof)
  - 24/7 Heart Rate, SpO2, Sleep & Stress Monitor
  - Built-in GNSS (GPS, GLONASS, Galileo)
  - 5 ATM, Wireless payment (NFC-ready), Notification bridge (iOS/Android), Customizable watchface

---

## 2. Varian Warna & Material Finishes

|  Nama Varian  | Hex      | Deskripsi Visual                         |
|:-------------:|:--------:|:-----------------------------------------|
|    Sand       | #c5a982  | Warm, premium matte, soft sunlit gold    |
|    Slate      | #647f9e  | Modern cool blue-grey, metallic accent   |
|    Rose       | #a56768  | Subtle rose-gold, modern terracotta      |

Material dan tone pada setiap produk diadaptasi dengan clearcoat PBR serta multiple lighting agar visualisasi 3D di Forma match 99% spek fisik asli.

---

## 3. Alur Pemesanan D2C (Direct-to-Consumer)

**1. Eksplorasi 360° Produk:**
- User memilih produk (tab 01–03), dapat mengganti warna varian, memutar/zoom detail hardware lewat UI orbit & gestures.

**2. Pre-order Langsung / Buy Now:**
- Setiap produk menampilkan CTA button berbeda:
    - **Sonic One Speaker & Form Watch:** "Pre-order"
    - **Studio Arc Headphones:** "Buy now" (launch ready stock)

**3. CTA — Satu Klik Email Order:**
- Klik tombol akan membuka aplikasi email default user via protokol `mailto:`
    - Alamat: hello@forma.example
    - Template subject: `Order <Nama Produk+Varian>` (ex: "Order Studio Arc - Slate")
    - Body email auto-prefill (opsional, versi lanjutan):
      - Nama, alamat, no. telp, varian warna yang dipilih

**4. *Order Confirmation Workflow* (opsional, roadmap next):**
- Tim sales Forma akan membalas konfirmasi manual (atau webhook otomatis next release) untuk validasi ketersediaan, pembayaran, verifikasi data, serta pengiriman calon invoice.

**5. Payment & Pengiriman:**
- Untuk V1 (MVP): Channel pembayaran manual (bank transfer/info invoice) via email. Integrasi payment gateway (Stripe/Midtrans/QRIS) masuk di roadmap future release.

**6. Customer Journey Summary**
- Eksplorasi → Pre-order/Buy → Submit Email → Konfirmasi → Bayar → Kirim

---

## 4. Catatan Kualitas Visual & Realisme
- **Material 3D & Lighting:** Semua model 3D pada Forma dioptimasikan agar mendekati karakter fisik nyata sesuai varian warna, tekstur, serta efek highlight (difuse/matte, polished, metal edge, bezel watch, fabric grille, dst) dengan kombinasi advanced lighting scene Three.js.
- **WYSIWYG Color-matching:** Penyesuaian kalibrasi tone warna, shadow, dan highlight pada renderings agar sama seperti unit retail sebenarnya (dibandingkan sRGB display, toleransi <2% DeltaE dengan referensi lab color).

---

## 5. Addendum: Future Channel Automation (Optional)
- **Add to Cart / D2C Automation:** Integrasi API pesanan langsung ke backend webstore Forma atau Google Sheets/Notion sebagai sumber data order pipeline batch pre-order.
- **Automated fulfillment webhook:** Email order trigger webhook ke backend sales system (Google Apps Script, n8n, Zapier, atau custom NodeJS microservice).
