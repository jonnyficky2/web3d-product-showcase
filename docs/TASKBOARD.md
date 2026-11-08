# Forma 3D Showcase — Milestone Taskboard (LifeFlow Style)

> **Project:** FORMA 3D Showcase (Interactive 3D Web Product Showcase)
>
> Dokumen ini berbasis **milestone M1 s.d M5** yang konsisten dan seragam.
> Isi task merujuk ke taskboard sebelumnya (**Task 01–13**) dengan status: **DONE / IN PROGRESS / TODO**.

---

## Legenda Status
- **DONE**: selesai dan lulus Acceptance Criteria.
- **IN PROGRESS**: sedang dikerjakan/testing; belum memenuhi semua Acceptance Criteria.
- **TODO**: belum mulai atau belum melewati Acceptance Criteria.

---

## Milestone M1 — Core Foundation & Commercial UI

- **Status:** ✅ DONE
- **Progress:** **100%**

### Acceptance Criteria (Milestone)
- Scene Three.js terinisialisasi (renderer, camera, lighting) dan memunculkan produk.
- Rig pencahayaan 4-titik + soft shadows + ACES Filmic tone mapping konsisten (tanpa flicker/artefak besar).
- 3 produk procedural tampil dengan switching visibility.
- PBR materials (clearcoat) + real-time color swatches bekerja saat user mengganti warna.
- OrbitControls terasa halus (damping), ada clamped zoom & auto-rotate idle resume.
- UI/UX FORMA: branding, monogram **FM**, tipografi Google Fonts (Plus Jakarta Sans & Syne), glassmorphism, serta konten harga/spec berubah dinamis saat tab diklik.

### Task Breakdown (M1)

| Task ID | Area | Status | Progress % | Acceptance Criteria (detail) | Related Docs |
|---:|---|---|---:|---|---|
| 01 | Core Setup | DONE | 100% | `index.html` memuat Three.js via **Import Map**; kanvas render muncul tanpa error modul; layout dasar tidak mengganggu interaksi canvas. | `index.html` |
| 02 | Rendering | DONE | 100% | Lighting **4-point** berfungsi; `PCFSoftShadowMap` aktif; `ACESFilmicToneMapping` menghasilkan tampilan sinematik konsisten; shadow tidak “berkedip” saat orbit/resize. | `index.html`, `docs/ARCHITECTURE.md` |
| 03 | 3D Content | DONE | 100% | Tiga produk (Sonic One, Studio Arc, Form Watch) terbangun dengan geometri prosedural; visibility switch antar produk berjalan instan; tidak ada produk yang “menyatu”/tertinggal. | `index.html` |
| 04 | Materials & Lookdev | DONE | 100% | Menggunakan `MeshPhysicalMaterial` dengan `clearcoat`; **real-time color swatches** mengubah material inti tanpa re-render model; state swatch & warna sinkron. | `index.html`, `docs/PRD.md` |
| 05 | Interaction | DONE | 100% | OrbitControls: damping halus; clamped zoom mencegah kliping; auto-rotate berhenti saat user interaksi dan resume dengan cooldown; batas polar mencegah kamera menembus lantai. | `index.html`, `docs/USER_FLOW.md` |
| 06 | UI/UX Revamp | DONE | 100% | UI glassmorphism rapi; branding FORMA + monogram FM muncul; Plus Jakarta Sans (body) dan Syne (heading) terpakai; harga/spec/deskripsi berubah dinamis sesuai tab; transisi fade & slide terasa halus. | `index.html`, `docs/USER_FLOW.md`, `README.md` |

---

## Milestone M2 — Mobile UX & Touch Ergonomics

- **Status:** 🟡 IN PROGRESS
- **Progress:** **60%**

### Acceptance Criteria (Milestone)
- Pada viewport **< 680px**, layout panel tidak overflow/terpotong.
- Gestur 3D tidak konflik dengan scroll (touch-action pencegahan efektif).
- CTA + swatches tetap mudah dijangkau di thumb zone.

### Task Breakdown (M2)

| Task ID | Area | Status | Progress % | Acceptance Criteria (detail) | Related Docs |
|---:|---|---|---:|---|---|
| 07 | Frontend UX | IN PROGRESS | 60% | Mobile: (1) posisi panel adaptif, (2) tidak ada horizontal scroll, (3) orbit/zoom tidak “memerangi” scroll, (4) CTA dan swatches tetap clickable pada perangkat sentuh. | `index.html`, `docs/USER_FLOW.md` |

---

## Milestone M3 — Premium Switching Motion & Snapshot Export

- **Status:** 🔴 TODO
- **Progress:** **0%**

### Acceptance Criteria (Milestone)
- Saat user berganti tab produk, kamera &/atau target berpindah **halus** (smooth) dengan `lerp` (tidak snap).
- Fitur snapshot berfungsi: tombol unduh menghasilkan **PNG** dari kanvas dengan kualitas stabil mengikuti DPR clamp.

### Task Breakdown (M3)

| Task ID | Area | Status | Progress % | Acceptance Criteria (detail) | Related Docs |
|---:|---|---|---:|---|---|
| 08 | Motion / Camera | TODO | 0% | Switching produk memicu camera tween: transisi terasa premium (< ~350ms), input user tetap responsif, tidak jitter saat resize, tidak merusak auto-rotate state. | `index.html`, `docs/USER_FLOW.md` |
| 09 | Visual Export | TODO | 0% | Tombol snapshot/unduh menghasilkan file PNG (sesuai kebutuhan transparansi), resolusi mengikuti DPR clamp, tidak mengunduh frame blank, dan UX jelas (mis. loading state kecil / disable saat proses). | `index.html`, `docs/PRD.md` |

**Dependency Note:** Task 09 direkomendasikan berjalan setelah Task 08 stabil.

---

## Milestone M4 — Performance Profiling & Loading Quality

- **Status:** 🔴 TODO
- **Progress:** **0%**

### Acceptance Criteria (Milestone)
- FPS dan smoothness stabil khususnya perangkat low-tier mobile.
- Terdapat strategi **pixel ratio dinamis** dan **delta-time clamping** yang menjaga stabilitas.
- Loading state mencegah flash / FOUSC sebelum scene siap.

### Task Breakdown (M4)

| Task ID | Area | Status | Progress % | Acceptance Criteria (detail) | Related Docs |
|---:|---|---|---:|---|---|
| 10 | Performance | TODO | 0% | Pixel ratio adaptif berbasis heuristik (mis. device/performance) dan delta-time clamping tetap dipakai; target minimal: ~45 FPS pada device low-tier (dengan trade-off kualitas yang terukur). | `index.html`, `docs/ARCHITECTURE.md` |
| 11 | Loading / UX Polish | TODO | 0% | Ada loading/skeleton/spinner sampai first render ready; UI muncul mulus (tanpa flash unstyled besar); bila WebGL tidak tersedia → tampil fallback yang jelas. | `index.html`, `docs/USER_FLOW.md` |

---

## Milestone M5 — Docs Ops & Release (GitHub Pages)

- **Status:** 🔴 TODO
- **Progress:** **25%**

### Acceptance Criteria (Milestone)
- Dokumentasi konsisten dan terhubung: README selalu mereferensikan PRD/ARCHITECTURE/USER_FLOW.
- GitHub Pages live tanpa error (tidak 404), dan konfigurasi branch/folder konsisten.
- (Opsional) langkah custom domain siap (CNAME + HTTPS) bila dibutuhkan.

### Task Breakdown (M5)

| Task ID | Area | Status | Progress % | Acceptance Criteria (detail) | Related Docs |
|---:|---|---|---:|---|---|
| 12 | Docs Ops | TODO | 30% | Validasi sinkronisasi: README → link docs benar; istilah konsisten; checklist “docs drift” sederhana terpenuhi (PRD ↔ ARCH ↔ USER_FLOW). | `docs/PRD.md`, `docs/ARCHITECTURE.md`, `docs/USER_FLOW.md`, `README.md` |
| 13 | Release / Hosting | TODO | 20% | GitHub Pages deploy sukses dan dapat diakses (bukan 404); source branch dan folder deploy benar; workflow tidak “cancel” permanen; (opsional) custom domain steps tersusun. | `README.md` |

---

## Progress Roll-up (Ringkas)
- **M1:** 100% ✅
- **M2:** 60% 🟡
- **M3:** 0% 🔴
- **M4:** 0% 🔴
- **M5:** 25% 🔴

---

## Definition of Done (DoD) Umum
- **Correctness:** switching produk & warna sinkron dengan state 3D.
- **UX:** transisi terasa halus dan tidak mengganggu kontrol user.
- **Quality:** tidak ada console error signifikan; tidak ada layout overflow pada breakpoint target.
- **Performance guardrails:** tidak ada drop frame besar yang teramati saat event switch.
- **Docs/Release:** link dan deploy configuration valid.
