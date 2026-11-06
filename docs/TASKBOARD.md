# Forma 3D Showcase — Taskboard & Product Backlog

> **Project:** FORMA 3D Showcase (Interactive 3D Web Product Showcase)
>
> Dokumen ini merangkum **status pengembangan** dan **backlog terstruktur** untuk memastikan eksekusi rapi dari foundation sampai release.
>
> Struktur Kanban:
> - 🟢 DONE
> - 🟡 IN PROGRESS
> - 🔴 TO-DO / BACKLOG

---

## 🟢 DONE (Completed Foundation & UI)

| Task ID | Area | Task Summary | Deliverable / Verifikasi | Notes / Risk |
|---:|---|---|---|---|
| 01 | Core Setup | Inisialisasi Core Three.js Scene, Camera, dan WebGLRenderer (`index.html`). | Single-file app berjalan; kanvas render muncul tanpa error modul. | Pastikan import map + ESM load OK di local server. |
| 02 | Rendering | Konfigurasi Rigging Pencahayaan Studio 4-Titik, Soft Shadows (PCFSoftShadowMap), dan ACESFilmicToneMapping. | Shadow map aktif; tone-mapping konsisten dan visual “cinematic”. | Bias shadow & ukuran map perlu konsisten saat optimize. |
| 03 | 3D Content | Konstruksi Geometri Prosedural 3 Produk Utama (Sonic One, Studio Arc, Form Watch). | Tiga produk terbentuk dari geometri prosedural; visibility switch bekerja. | Pastikan bounding/camera target cocok tiap produk. |
| 04 | Materials & Lookdev | Implementasi Sistem Material PBR (`MeshPhysicalMaterial`) dengan Clearcoat dan Real-time Color Swatches. | Warna material berubah real-time; swatch state sinkron dengan material. | Hindari re-instancing material berulang (performance). |
| 05 | Interaction | Integrasi OrbitControls dengan Damping Inersia, Clamped Zoom, dan Smart Idle Auto-Rotate. | Orbit stabil; auto-rotate berhenti saat user interaksi dan resume dengan cooldown. | Clamping sudut & jarak harus mencegah “kamera menembus lantai”. |
| 06 | UI/UX Revamp | Desain ulang UI/UX komersial modern (“FORMA” Branding, Monogram FM, Plus Jakarta Sans & Syne Fonts, Glassmorphism, Dynamic Pricing & Specs). | Panel UI glassmorphic; harga/deskripsi/spec berubah dinamis saat tab diklik; animasi transisi halus. | Pastikan aksesibilitas dasar (ARIA, focus states) tetap OK. |

---

## 🟡 IN PROGRESS (Active Development & Testing)

| Task ID | Area | Task Summary | Status Saat Ini | Acceptance Criteria |
|---:|---|---|---|---|
| 07 | Frontend UX | Optimasi Responsivitas Mobile (< 680px), Touch-Action Prevention, dan Ergonomi Layout Panel. | Sedang dikerjakan/testing | 
- Tidak ada overflow/elemen terpotong di mobile portrait
- Gestur orbit tidak konflik dengan scroll (touch-action: none pada stage canvas)
- CTA + swatches mudah dijangkau (thumb-friendly) |

---

## 🔴 TO-DO / BACKLOG (Upcoming Tasks)

| Task ID | Area | Task Summary | Priority | Dependencies | Acceptance Criteria |
|---:|---|---|---|---|---|
| 08 | Motion / Camera | **Camera Tweening / Smooth Transition** saat ganti produk (lerp posisi kamera &/atau OrbitControls target). | High | Task 07 stabil | 
- Transisi ganti produk terlihat halus (< ~350ms terasa “premium”)
- Tidak membuat user “kehilangan kontrol” (user input segera prioritas)
- Tidak menyebabkan jitter pada resizing |
| 09 | Visual Export | **Snapshot / Download 3D Render Feature (PNG transparan)** langsung dari kanvas. | Medium | Task 08 (disarankan) | 
- Tombol download menghasilkan file PNG
- Target: latar transparan (atau setara, sesuai konfigurasi renderer)
- Kualitas gambar mengikuti DPR clamp tanpa blur berlebihan |
| 10 | Performance | Performance Profiling & FPS Limiting (pixel ratio dinamis + delta-time clamping untuk low-tier mobile). | High | Task 07 | 
- Stabil FPS saat device low-end (target: min ~45 FPS)
- Pixel ratio adaptif (mis. 1.0–2.0) berbasis heuristik FPS
- Shadow/renderer settings tidak merusak kualitas terlalu signifikan |
| 11 | Loading / UX Polish | Loading State & Asset Ready Transition (hindari FOUSC/flash dari UI/scene). | Medium | Task 01-06 workable | 
- Ada skeleton/spinner sampai first render ready
- Setelah scene siap, UI tampil mulus (tanpa flash unstyled)
- Error fallback tampil bila WebGL tidak tersedia |
| 12 | Docs Ops | Automated README & Dokumentasi Sinkronisasi (validasi kelengkapan PRD & ARCHITECTURE). | Medium | Docs sudah ada | 
- README selalu mereferensikan dokumen & feature terbaru
- Validasi link dan konsistensi istilah (PRD ↔ ARCHITECTURE ↔ UI behavior)
- (Opsional) ada checklist “docs drift” |
| 13 | Release / Hosting | GitHub Pages Live Deployment & Custom Domain Preparation. | High | Repo access & workflow | 
- Pages terdeploy sukses (tidak 404)
- Source branch/folder konsisten (index.html ter-publish)
- (Opsional) langkah custom domain: CNAME + HTTPS ready |

---

## Roadmap yang Disarankan (Milestones)

1. **Stabilkan mobile** (Task 07) sampai UX/gestur solid.
2. **Premium switching feel** → Camera tweening (Task 08).
3. **Export capability** → Snapshot PNG (Task 09).
4. **Jaga performa** → Profiling + FPS/pixel ratio control (Task 10).
5. **Polish** → Loading state & graceful fallback (Task 11).
6. **Docs & release readiness** → Sinkronisasi docs (Task 12) dan Pages deployment + domain prep (Task 13).

---

## Definition of Done (DoD) — Reusable

- **Quality:** tidak ada console error signifikan; visual selaras dengan spesifikasi brand.
- **Interaction:** tab switch & swatch update 100% sinkron dengan state 3D.
- **Responsiveness:** layout aman pada breakpoint < 680px.
- **Accessibility (minimum):** elemen interaktif punya aria-label/aria-pressed dan tidak mengunci keyboard focus.
- **Performance guardrails:** tidak ada drop frame besar akibat operasi berat pada event switch.
