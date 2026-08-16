# plan.md — SIPRO — Lanjut Development (Slice A + Slice B + Slice Finance) — Fokus: MVP end-to-end

## ✅ STATUS (update terakhir — **pemulihan repo ke-6** + **FASE 37 DITUTUP**)
- **Pemulihan repo (sesi ini, ke-6)**: `/app` kembali kosong/template → repo GitHub `sipro` dipulihkan.
  Langkah pasca-restore §3b dijalankan: `backend/.env` dibuat ulang, `pip install APScheduler reportlab`,
  `yarn install`, `memory/test_credentials.md` ditulis ulang (hilang karena di-gitignore), `seed_reset.sh`.
  **Bukti sehat**: `bash scripts/run_all_gates.sh` → **OVERALL PASS (18 gates)** pada DB bersih.
- **FASE 37 DITUTUP** (Kalibrasi Sekali Klik): `poc_37` **85/85**, `verify_37` **91/91**,
  `run_all_gates` **18 gates PASS**, 12 user story dibuktikan di browser oleh main agent
  **dan** dikonfirmasi ulang testing agent (iterasi 55: 0 bug). Satu cacat kejujuran angka
  ditemukan main agent sendiri saat menonton layar (badge "0 hari") → diperbaiki, lihat §FASE 37.
- **FASE 38 DITUTUP** (Sapuan permukaan tampilan): alat baru `scripts/ui_audit_dialogs.py`
  (audit DI DALAM dialog) menemukan 5 panel tanpa latar, 21 field bisu, 79 label tak tertaut,
  dan legenda grafik berkontras 2.1:1 → semuanya diperbaiki. Gate baru
  `scripts/verify_ui_surfaces.py` (20 pemeriksaan, diuji-mutasi) menjaga agar tidak kembali →
  `run_all_gates.sh` kini **19 gates PASS**. Bukti sebelum→sesudah ada di §FASE 38.

## Riwayat STATUS sebelumnya (pemulihan ke-5 + FASE 36 DITUTUP)
- **Pemulihan repo (ke-5)**: `/app` kembali ditemukan kosong/template → repo GitHub `sipro` dipulihkan lagi.
  Langkah pasca-restore §3b dijalankan ulang: buat ulang `backend/.env` (JWT_SECRET, EMERGENT_LLM_KEY,
  PORTAL_MASTER_OTP=000000, DEFAULT_ORG_ID=org-sipro, DEFAULT_ORG_NAME, COOKIE_SECURE, BOOKING_HOLD_DAYS,
  STORAGE_PROVIDER, PHOTO_*), **`pip install APScheduler reportlab`**, `yarn install`, lalu `bash scripts/seed_reset.sh`.
  **Bukti sehat**: `bash scripts/run_all_gates.sh` → **OVERALL PASS (17 gates)** pada DB bersih.
- **FASE 36 DITUTUP** (Kalender Jadwal): `poc_36` **132/132**, `verify_36` **135/135**,
  `run_all_gates` **17 gates PASS**, dan seluruh 12 user story **dibuktikan di browser**
  (testing agent iterasi 50 + 51 + 52). Lihat §FASE 36 untuk daftar cacat yang ditemukan & diperbaiki —
  termasuk **satu bug HIGH yang hanya terlihat dari sisa data pengujian**, bukan dari laporan tester.
- **Kredensial uji dipulihkan**: `memory/test_credentials.md` ditulis ulang (sandi `Sipro#2026`, 9 akun demo).
- **FASE 35 DITUTUP** (Papan Mandor tahan sinyal hilang — antrean offline): `poc_35` **43/43**,
  `verify_35` **52/52**, dan **dibuktikan di browser nyata**
  (offline sungguhan lewat Playwright: ajukan → antre → muat ulang saat offline → sinyal kembali → terkirim sendiri,
  tanpa dobel). Lihat §FASE 35 untuk daftar cacat yang ditemukan & diperbaiki.
- **FASE 33 DITUTUP**: testing_agent iterasi 44 + 45 → **0 bug kritis, 0 bug medium, 0 error konsol**.
- **FASE 34 DITUTUP** (jadwal massal per blok/cluster + geser tanggal serentak): `poc_34` 57/57,
  `verify_34` 40/40, testing_agent iterasi 46/47/48 → invarian terpenting (**bukti terikat waktu**) terbukti di layar.
- **Fase berikutnya (dipilih owner & disepakati detailnya)**:
  - **Fase 37 = Kalibrasi Sekali Klik** (ubah durasi/waktu tunggu template langsung dari Analitik Telat) — **BERIKUTNYA**.
- Integrasi eksternal (WhatsApp/e-Sign/e-Faktur/BI-SLIK) **tetap mode simulasi** (belum ada kredensial resmi).
- Tombol **"Masuk cepat"** di halaman login tetap ada untuk pengujian (memanggil login normal; bukan backdoor).


## Riwayat STATUS sebelumnya (pemulihan repo + Fase 33 dimulai)
- **Pemulihan repo (15 Agu 2026)**: repo GitHub dipulihkan lagi ke `/app`. `.env` (di-gitignore) dibuat ulang: `JWT_SECRET`, `EMERGENT_LLM_KEY`, `PORTAL_MASTER_OTP`, `DEFAULT_ORG_ID/NAME`, `COOKIE_SECURE`, `PHOTO_*`. Dependensi backend dipasang ulang (`reportlab`, `APScheduler`, dll; `litellm`+`emergentintegrations` sudah ada di image).
- **Dua gate merah pasca-restore diperbaiki (bukan diakali)**:
  - `build_policies` kini punya **dokumen kebijakan nyata** hasil seed (dulu kosong → audit forensik HIGH & admin tak bisa lihat "sejak kapan/oleh siapa").
  - **Laporan mingguan pekan berjalan** dibangkitkan dari jadwal nyata saat seed (dulu direksi melihat halaman kosong sampai Senin berikutnya).
  - Hasil: `verify_32` **28/28**, `forensic_audit` **PASS**, `bash scripts/run_all_gates.sh` → **OVERALL PASS (13 gates)**.
- **Titik berhenti Fase 32 direproduksi**: Papan Mandor + instruksi kerja + dialog ajukan (kamera + panel syarat) tampil normal, **0 error console**.
- **Fase 33 (RAB/BoQ ↔ jadwal → opname & termin subkon)**: **SELESAI & TERVERIFIKASI** — lihat §FASE 33.
- **Repo & environment**: repo GitHub dipulihkan ke `/app` (workspace persisten). Backend + frontend jalan via supervisor.
  - Env yang hilang saat pemulihan sudah dibuat ulang: `JWT_SECRET`, `EMERGENT_LLM_KEY`, `PORTAL_MASTER_OTP`, `DEFAULT_ORG_ID/NAME`, `COOKIE_SECURE`, `PHOTO_WATERMARK` → bug **login 500 (`KeyError: JWT_SECRET`) FIXED**.
- **Integrations (ready, config-driven)**: `EMERGENT_LLM_KEY` tersedia → **Emergent Object Storage** aktif (managed). Mode simulasi masih dipakai untuk WhatsApp Cloud API live (tanpa kredensial Meta), e-sign, BI/SLIK, dan e-Faktur.
- **Guardrails**: `bash scripts/run_all_gates.sh` → **OVERALL PASS (12 gates)**.
- **POC Fase 31**: `python3 scripts/poc_31.py` → **63 PASS / 0 FAIL**. Gate `scripts/verify_31.py` → **30 PASS / 0 FAIL**.
- **Phase 28b/28c (Site Plan + Photo Storage + Bukti Perbaikan Berpasangan)**: **SELESAI & TERVERIFIKASI**.
- **Phase 29 (Work Hub v2 + Lead Lifecycle + UI/UX + Report/Kanban)**: **SELESAI & TERVERIFIKASI**.
- **Phase 30 (Qualification Hub / SLIK prescreen + photo optimize + capture.failed queue)**: **SELESAI & TERVERIFIKASI**.
- **Phase 31 (Construction Progress Engine v2)**: **SELESAI & TERVERIFIKASI**.
- **Phase 32 (Task-based Execution + Papan Mandor + Laporan Mingguan + Analitik Telat)**: **SELESAI & TERVERIFIKASI**.

---

## 1) Objectives

### Objective A — Work Hub Engine “bernilai bisnis” (P0)
Membangun ulang Work Hub agar benar-benar memandu pekerjaan lintas divisi, bukan sekadar menu.
Fokus owner (disepakati):
- **Domain kerja**: 4 divisi — **Sales & Marketing**, **Teknis/Proyek**, **Digital Marketing**, **Finance**.
- Tiap divisi punya **Supervisor + Staff** (field pada user: `division` + `level`).
- RBAC modul tetap seperti sekarang, tetapi **peran baru ditambahkan** untuk mendukung pola supervisor/staff.
- Work Hub harus memetakan **jobdesk** berdasarkan fitur yang sudah ada dan menjadikan action sebagai task.
- Supervisor mengatur konfigurasi: **auto event**, **manual**, **recurring**, SLA, prioritas, aturan assignee.
- Task memiliki alur: **open → in_progress → submitted → verified/rejected → done**.

### Objective B — Lead Lifecycle sebagai “gerbang bukti” + WA terintegrasi (P0)
Menutup gap bisnis proses sales:
- Stage tidak boleh dipilih bebas; harus berdasarkan **aksi + bukti**.
- **Won otomatis** dari event deal legal/akad/BAST (tidak manual).
- WA harus terintegrasi langsung ke record lead dan memicu task/lifecycle.
- Tambahkan penilaian **kualitatif** (disposition/intent) setelah kontak pertama.

### Objective C — UI/UX stability sweep (P0)
Sambil membangun fitur P0, lakukan perbaikan UI/UX yang paling terlihat:
- Konsistensi **Card background** (pakai `bg-card`).
- Tambah **pagination** di daftar utama.
- Tambah **sticky** header/toolbar/footer aksi pada halaman panjang.
- Perbaiki **CTA mati**, dan empty/loading/error state sesuai `design_guidelines.md`.

### ✅ Objective D — Construction Progress Engine v2 (P0) — SELESAI
**FASE 31 (permintaan owner): CONSTRUCTION PROGRESS ENGINE v2 — Jadwal Berbukti, Gerbang Mutu, Reminder & Eskalasi, per TIPE UNIT.**

### ✅ Objective E — Task-based Execution + Papan Mandor + Laporan Mingguan + Analitik Telat (P0) — SELESAI
**FASE 32 BARU (permintaan owner):**
- Papan Mandor (HP) + foto bukti (kamera) + kebijakan GPS on/off admin.
- Laporan mingguan Senin (in-app + PDF) + analitik telat + rekomendasi kalibrasi.

### 🎯 Objective F (BARU) — Kalender Jadwal (P0)
**FASE 36 (permintaan owner): Kalender bulanan seluruh tenggat rumah untuk Manajer Proyek** agar bentrok terlihat **SEBELUM** terjadi.

Pilihan owner (WAJIB dipatuhi):
1. Cakupan: bisa dipilih **SATU PROYEK** atau **SEMUA PROYEK** (portofolio).
2. Isi kalender per tanggal: **(a) build_items + jadwal unit, (b) QC/inspeksi + punch list, (c) tugas Work Hub tim proyek**.
3. Bentrok yang diperingatkan: **beban pelaksana**, **tumpukan pekerjaan KRITIS/hold-point**, dan **tenggat jatuh di hari non-kerja/libur**.
4. Aksi dari kalender: lihat + klik detail + **geser tanggal lewat dialog Fase 34** (bukan drag & drop).
5. Hari kerja/libur: buat **master data hari libur & pola hari kerja** yang dipakai **kalender DAN mesin jadwal**.

---

## 2) Implementation Steps

### Phase 1 — Core POC / Isolation (SELESAI)
- Sudah tervalidasi.

---

### Phase 2 — V1 App Development (Slice A — Sales funnel tipis) (SELESAI)
- Backend + Frontend selesai dan teruji.

---

### Phase 3 — Add More Features (Slice B — Konstruksi tipis) (SELESAI)
- Backend + Frontend selesai dan teruji.

---

### Phase 4 — Stabilization / Guardrails Growth (SELESAI)
- Stabilitas + compliance + gates hijau.

---

### Phase 5 — Slice Finance & Real-Time Notifications (SSE) (SELESAI)
- Foundation finance + SSE + UI finance lulus testing_agent_v3.

---

### Phase 6 — EPIC 3.5 Cashflow/Collections + EPIC M5 Reports/BI (SELESAI)
- Lulus testing_agent_v3 dan gates hijau.

---

### Phase 7 — EPIC 1.5 KPR/Financing + Adoption Completion (SELESAI)
- Customer Portal + object storage + portal security sudah berjalan.

---

### Phase 8 — EPIC M1 Customer Portal (SELESAI)
- Portal OTP (master `000000`), overview/payments/progress/documents + complaints: teruji.

---

## ✅ Phase 29 — Rebuild Work Hub + Lead Lifecycle + UI/UX (P0) (SELESAI & TERVERIFIKASI)
> Ringkasan fase 29 tetap berlaku seperti di dokumen sebelumnya (29a/29b/29c/29d), dengan POC PASS, gates PASS, dan verifikasi manual UI.

---

## ✅ PHASE 31 — SELESAI & TERVERIFIKASI (Construction Progress Engine v2)
> Dipertahankan sebagai arsip bukti (jangan dihapus).

---

## ✅ PHASE 32 — SELESAI & TERVERIFIKASI
> Dipertahankan sebagai arsip bukti (jangan dihapus).

---

## ✅ FASE 33 — SELESAI & TERVERIFIKASI
> Dipertahankan sebagai arsip bukti (jangan dihapus).

---

## ✅ FASE 34 — SELESAI & TERVERIFIKASI
> Dipertahankan sebagai arsip bukti (jangan dihapus).

---

## ✅ FASE 35 — SELESAI & TERVERIFIKASI
> Dipertahankan sebagai arsip bukti (jangan dihapus).

---

## ✅ FASE 37 — KALIBRASI SEKALI KLIK (dari Analitik Telat langsung ke template) — SELESAI & TERVERIFIKASI

### Bukti penutupan (DB tersegar)
- `python3 scripts/poc_37.py` → **85 PASS / 0 FAIL** (INV-37-1..10 lewat API nyata).
- `python3 scripts/verify_37.py` → **91 PASS / 0 FAIL** (termasuk aturan baru soal `changeText`).
- `bash scripts/run_all_gates.sh` → **OVERALL PASS (18 gates)**; `verify_31..36` tidak regresi.
- Browser: 12 user story dibuktikan **main agent** (screenshot + assertion) lalu dikonfirmasi
  **testing agent iterasi 55** (jalur panel Analitik Telat end-to-end, kalibrasi dari baris
  tabel telat, rollback + validasinya, regresi render 5 halaman) → **0 bug, 0 error konsol**.
- **Baseline kembali utuh setelah pengujian** (diperiksa langsung di database, bukan dari layar):
  RUMAH-9W 60 hari kerja / 20 langkah, RUKO-14W 90 / 16, `calibrated_steps=0`, rekomendasi=4,
  4 baris riwayat semuanya sudah dibatalkan/berupa pembatalan (jejak audit tetap ada — memang begitu).

### ⚠️ CACAT yang ditemukan main agent sendiri (bukan dari laporan tester)
**Badge & riwayat berbunyi "sudah diterapkan 0 hari" pada kalibrasi `wait_into_plan`.**
Untuk jenis ini pengguna tidak mengetik jumlah hari — sistem menghitung kekurangan jeda —
sehingga `delta_days` = 0 sementara tanggal rencana benar-benar bergeser `shift_days` hari.
Semua badge yang membaca `delta_days` mentah karena itu menyatakan "0 hari" padahal template
bergeser 3 hari kerja; perencana yang membaca riwayat akan menyimpulkan "tidak ada yang berubah".
Ini persis jenis angka menyesatkan yang Fase 37 dibuat untuk menutup.

**Perbaikan (Fase 37b):**
1. `build_calibration._targets()` ikut mengirim `kind` + `shift_days` pada objek `applied`.
2. Pembantu baru **`changeText(cal)`** di `utils/calibrationUi.js` — satu tafsir angka untuk
   semua panel: pakai `delta_days` bila ada, jatuh ke `shift_days` + keterangan
   **"(geser rencana)"** bila delta 0, dan "tanpa perubahan hari" bila keduanya 0.
   Angka pergeseran **tetap datang dari backend** (frontend tidak menghitung sendiri).
3. Enam tempat pemakaian diganti: kartu usulan, tabel telat, daftar langkah template,
   riwayat, dialog pembatalan, dan baris hasil di dialog.
4. `verify_37` diperketat: yang dilarang bukan lagi *menyebut* `shift_days` di frontend
   (aturan lama justru memaksa angka bohong), melainkan **melakukan aritmatika** atasnya;
   ditambah pemeriksaan bahwa 4 panel badge/riwayat memakai `changeText()`.
   Bukti di layar: `sudah diterapkan +3 hari (geser rencana)`, riwayat
   `Masukkan waktu tunggu ke tanggal rencana +3 hari (geser rencana)`, pembatalan
   `pembatalan −3 hari (geser rencana)`.

### Catatan pengujian (agar tidak terulang)
Testing agent iterasi 54 berhenti setelah US-1 dengan alasan **"sesi cepat kedaluwarsa"** —
itu **keliru**: access token berumur **24 jam** (`backend/security.py`) dan disimpan di
`localStorage` (`services/apiClient.js`). Penyebab sebenarnya: setiap skrip Playwright baru
memakai browser bersih. Instruksi yang benar: **login sekali, kerjakan semua skenario dalam
satu sesi**, dan hanya bersihkan `localStorage` saat berganti peran.

### Rancangan asli (arsip)
Masalah nyata yang ditutup: Analitik Telat sudah menunjuk pekerjaan yang selalu telat dan
memberi rekomendasi, tetapi ujungnya hanya kalimat "buka Template Jadwal lalu ubah hari
mulai/selesai" — menyimpan template menuntut payload penuh, jadi perencana harus mengetik
ulang seluruh template. Akibatnya kalibrasi tidak pernah dilakukan dan analitik hanya hiasan.
Selain itu perubahan durasi tidak punya jejak (siapa/kapan/atas dasar data apa) dan tidak bisa
dikembalikan. Ditambah **kebutaan model** yang ketahuan saat merancang: `wait_days` (curing)
tidak pernah masuk `day_from/day_to`, sehingga rencana sistematis terlalu optimistis.

### 37a — Kelakuan yang dijanjikan
- Dari kartu rekomendasi **dan** dari setiap baris tabel "Pekerjaan paling sering telat":
  tombol **"Kalibrasi"** → dialog pratinjau → terapkan. Tanpa pindah halaman, tanpa mengetik ulang template.
- **Tiga jenis kalibrasi** (SSOT `calibration_kind`):
  1. `step_duration` — ubah durasi langkah (± hari kerja); langkah SETELAHNYA ikut bergeser
     supaya template tetap konsisten (tidak ada tumpang tindih / lompatan), `week` dihitung ulang.
  2. `wait_time` — ubah lamanya waktu tunggu wajib sebelum langkah boleh dimulai.
  3. `wait_into_plan` — **masukkan waktu tunggu ke tanggal rencana**: langkah digeser agar jaraknya
     dari pendahulu ≥ waktu tunggu (rencana berhenti berpura-pura curing bisa dilewati).
- **Pratinjau = hasil**: satu fungsi hitung dipakai pratinjau DAN eksekusi.
- **Wajib alasan (SSOT `calibration_cause`) + catatan ≥10 karakter**, `client_ref` idempoten.
- **Jadwal unit yang SUDAH ada tidak diubah** (bukti kerja tidak boleh bergeser) — pratinjau
  menyebut angkanya secara jujur, dan menyebut berapa rumah **belum terjadwal** yang akan memakai
  durasi baru. Mengubah tanggal jadwal berjalan tetap hanya lewat **Fase 34**.
- **Riwayat kalibrasi** per template: sebelum→sesudah, pelaku, waktu, alasan, angka data yang
  mendasarinya — dengan tombol **kembalikan (rollback)** tepat ke nilai sebelumnya.
- Rekomendasi yang sudah dikalibrasi ditandai **"sudah diterapkan"** (aplikasi tidak menyuruh dua kali).

### 37b — Berkas
- Backend: `build_calibration.py` (mesin: `plan/apply/rollback/candidates`), `models_p37.py`,
  `reference_p37.py` (grup `calibration_kind`, `calibration_cause`; nomor 37 masuk `_PHASES`),
  `routers/build_calibration_router.py` — `GET /build/calibration/candidates`,
  `POST /build/calibration/preview`, `POST /build/calibration/apply`,
  `GET /build/calibration/history`, `POST /build/calibration/{id}/rollback`.
  Koleksi baru **`build_calibrations`** (+ indeks unik `(org_id, client_ref)`).
  `build_analytics._recommend` diperbaiki: rekomendasi kini membawa objek `calibration`
  siap-pakai + kalimatnya jujur (waktu tunggu berlaku **sebelum** langkah, bukan sesudah).
- Frontend: `components/construction/calibration/{CalibrationDialog,CalibrationHistoryPanel}.js`,
  `constants/testIds/buildCalibration.js`, `DelayAnalyticsPanel` diberi tombol kalibrasi + riwayat.
- Gate: `scripts/poc_37.py` (API nyata) + `scripts/verify_37.py` → `run_all_gates.sh` jadi **18 gates**.

### Invarian (INV-37-x) yang harus terbukti
1. Pratinjau = hasil (fungsi hitung sama).
2. Kalibrasi **tidak menyentuh** `build_items`/`build_schedules` yang sudah ada (dibuktikan
   dengan membandingkan tanggal item sebelum & sesudah).
3. Jadwal **BARU** setelah kalibrasi memakai angka baru (dibuktikan dengan membuat jadwal & mengukur).
4. Tanpa alasan / catatan <10 karakter → **400**; `client_ref` sama → tidak dobel.
5. Template tetap konsisten: durasi ≥1 hari, tidak ada tumpang tindih, `week` ikut benar,
   total bobot tidak berubah, `validate_steps` tetap bersih.
6. Rollback mengembalikan **tepat** nilai sebelumnya dan tercatat sebagai kalibrasi balik.
7. RBAC: hanya Manajer Proyek/direksi/admin; pelaksana melihat tanpa tombol; sales 403.
8. Setiap kalibrasi & rollback masuk `audit_logs`.
9. Rekomendasi yang sudah dikalibrasi ditandai "sudah diterapkan".
10. Kalibrasi menghormati kalender Fase 36 (jadwal baru tetap melewati hari libur).

### User stories Fase 37 (dipakai testing agent)
1. PM membuka Progres & Mutu → tab Analitik Telat dan melihat rekomendasi kalibrasi berisi angka nyata.
2. PM menekan "Kalibrasi" pada satu rekomendasi → dialog terbuka **sudah terisi** usulan perubahan.
3. Tombol terapkan **mati** sebelum alasan + catatan (≥10 karakter) diisi.
4. Pratinjau menampilkan sebelum→sesudah tiap langkah terdampak + total durasi template berubah.
5. Pratinjau menyebut jumlah jadwal unit berjalan yang **TIDAK** diubah + jumlah rumah belum terjadwal.
6. Setelah diterapkan: toast sukses, tabel langkah menampilkan durasi baru, kartu rekomendasi
   berubah menjadi "sudah dikalibrasi".
7. PM membuka riwayat kalibrasi dan melihat sebelum→sesudah, alasan, pelaku, waktu.
8. PM menekan "Kembalikan" pada riwayat → nilai template kembali seperti semula (dengan catatan).
9. PM mengalibrasi langsung dari baris tabel "Pekerjaan paling sering telat" (tanpa rekomendasi).
10. Pelaksana (site@sipro.co.id) melihat analitik tanpa tombol kalibrasi.
11. Sales (sales@sipro.co.id) tetap mendapat kartu "AKSES DITOLAK" pada halaman itu.
12. Kalibrasi `wait_into_plan` menjelaskan dengan jujur bahwa waktu tunggu (curing) dimasukkan ke
    tanggal rencana, bukan dipersingkat.

---

## ✅ FASE 36 — KALENDER JADWAL (KALENDER BULANAN + DETEKSI BENTROK + MASTER LIBUR) — SELESAI & TERVERIFIKASI

### Bukti penutupan (DB tersegar)
- `python3 scripts/poc_36.py` → **132 PASS / 0 FAIL** (INV-36-1..14, semuanya lewat API nyata).
- `python3 scripts/verify_36.py` → **135 PASS / 0 FAIL** (termasuk §G regresi pewarisan kalender).
- `bash scripts/run_all_gates.sh` → **OVERALL PASS (17 gates)**; `verify_31..35` tidak regresi.
- Browser (testing agent iterasi **50, 51, 52**): 12 user story terbukti di layar
  (portofolio, bentrok beban September, pratinjau geser Fase 34, ambang, tambah/hapus libur,
  jadwalkan inspeksi QC jalur ditolak & jalur berhasil, filter jenis/pelaksana, bulan kosong,
  RBAC pelaksana & sales). **0 error konsol.**

### ⚠️ CACAT HIGH yang ditemukan SETELAH ronde-2 (dan cara menemukannya — jangan diulang)
Tester iterasi 51 melaporkan “angka bentrok tidak kembali ke 3 (30 → 76 → 10)” sebagai temuan
**LOW / “kemungkinan efek state”**. Pemeriksaan DB oleh main agent membuktikan itu **bug HIGH**:
- Menekan **“Simpan pola & ambang”** saat halaman menampilkan SATU proyek membuat dokumen
  kalender **khusus proyek** dengan `holidays: []`, dan `resolve()` memperlakukannya sebagai
  **PENGGANTI UTUH** kalender organisasi.
- Akibat nyata (terverifikasi di database, bukan dugaan): **18 hari libur nasional hilang senyap**
  untuk proyek itu → `summary.holidays` Agustus kosong, bentrok `non_workday` **2 → 0**, dan
  **inspeksi QC BERHASIL dijadwalkan pada 2026-08-17 (Hari Kemerdekaan)** tanpa satu pun peringatan.
- Pelajaran: **angka yang tidak kembali ke baseline setelah pengujian = sinyal cacat**, bukan noise.
  Juga: angka kartu ringkasan harus dibaca dari elemen NILAI (nilai 3 + hint “0 beban · 2 hari libur”
  terbaca “30” bila seluruh teks kartu dipungut digitnya).

### Perbaikan (Fase 36b) — pewarisan kalender, bukan penggantian
1. `build_calendar._merge()` menggantikan `_shape()`: kalender efektif = **organisasi diwarisi**,
   override proyek menimpa **pola & ambang** saja; **hari libur DIGABUNG** (organisasi ∪ proyek).
2. `_ensure_doc()` membuat override sebagai **salinan pola/ambang organisasi** → menyimpan
   pengaturan tidak pernah mengubah perilaku diam-diam. Daftar libur dibiarkan kosong **karena
   diwarisi** (libur nasional yang ditambahkan admin kelak tetap sampai ke proyek itu).
3. Menghapus libur warisan pada cakupan proyek kini menjadi **PENGECUALIAN yang disengaja**
   (`holiday_exclusions`): tercatat di `audit_logs` (`calendar_holiday_exclude`), tampil terpisah
   di UI, dan bisa dibatalkan (`POST /build/calendar/holidays/{day}/restore`).
4. Override bisa dilepas: `DELETE /build/calendar/settings?project_id=` → proyek kembali mengikuti
   organisasi. `GET /settings` juga mengembalikan `overrides[]` supaya **divergensi tidak tersembunyi**.
5. Dialog memaksa memilih cakupan (SSOT baru **`calendar_settings_scope`**, bawaan
   “Kalender organisasi”), setiap baris libur menyebut asalnya (SSOT **`holiday_source`**),
   tombol pada libur warisan berbunyi **“Kecualikan”** (bukan “Hapus”).
   Daftar libur dipecah ke komponen `WorkCalendarHolidays.js` (batas ukuran file tetap patuh).
6. **Bentrok `non_workday` diperluas** ke `inspection` + `punch` (`NONWORK_KINDS`) — dulu inspeksi
   yang jatuh di hari libur tidak ditandai di mana pun; pesannya kini merinci jenis agendanya.
   `outlook` (chip bulan berikutnya) menghitung lapisan yang sama supaya angkanya tidak mengecil.
7. Gate regresi baru: `poc_36` **INV-36-11..14** dan `verify_36` **§G** (termasuk uji fungsi murni
   `_merge` tanpa menyentuh database + sapuan semua dokumen override yang ada di DB).

### Sisa data pengujian dibereskan lewat jalur resmi
Override proyek dilepas (`DELETE /settings`) dan tanggal inspeksi yang terjadwal di hari libur
dibatalkan (`PUT /inspections/{id}/schedule` → `null`) — bukan ditembak langsung ke MongoDB.

---

## 📓 FASE 36 — rancangan asli (arsip)

### Masalah nyata yang ditutup
- Tenggat konstruksi saat ini terlihat **per unit / per daftar** saja → bentrok baru ketahuan setelah telat.
- `build_engine` hanya tahu hari kerja mingguan (5/6/7) + `holidays` yang melekat pada template/jadwal.
  Pada data nyata `holidays` kosong, sehingga tenggat bisa mendarat di libur nasional dan tidak ada UI admin untuk mengatur.
- Operasi massal (Fase 34) memakai perhitungan tanggal yang sama (`plan_for_template`, `plan_shift`) → master kalender harus masuk lewat **satu resolver** agar konsisten.
- `inspections` belum punya tanggal rencana → kalender tidak boleh mengarang. Perlu field `scheduled_date` + aksi menjadwalkan.

### Prinsip Fase 36
1. **Kalender = cermin data nyata** (tidak ada angka/tanggal karangan).
2. **Master kalender kerja** (hari libur + pola hari kerja) dipakai oleh **UI kalender** dan **mesin jadwal**.
3. Perubahan jadwal massal/geser **tidak punya mesin baru**: tetap lewat Fase 34 (beralasan + audit + bukti terverifikasi tidak bergeser).
4. UX harus patuh gate: loading/error/empty state, testIds, tanpa hardcode vocabulary, dan route+nav konsisten.

### Invarian (ditegakkan backend, diuji `poc_36.py`, dijaga `verify_36.py`)
- **INV-36-1** Kalender = cermin data nyata (jumlah acara = hasil query langsung; tidak ada angka karangan).
- **INV-36-2** Pola hari kerja & hari libur master **DIPATUHI mesin jadwal** (jadwal baru/geser tidak mendarat di libur).
- **INV-36-3** Bentrok beban pelaksana dilaporkan dengan nama orang + daftar pekerjaan + ambang yang dipakai.
- **INV-36-4** Tenggat yang jatuh di hari non-kerja ditandai + saran hari kerja terdekat.
- **INV-36-5** Tumpukan pekerjaan kritis/hold point melebihi ambang dilaporkan per tanggal.
- **INV-36-6** Kalender **READ-ONLY**; satu-satunya jalan mengubah tanggal = jalur Fase 34 (penyebab SSOT + catatan ≥10 huruf).
- **INV-36-7** RBAC: PM/direksi penuh, pelaksana melihat tanpa tombol ubah, sales 403.
- **INV-36-8** Pengaturan kalender hanya admin/owner/PM dan tercatat di `audit_logs`.
- **INV-36-9** Portofolio lintas proyek hanya menampilkan proyek yang boleh diakses pengguna.
- **INV-36-10** Bulan tanpa data → empty state yang menjelaskan, bukan grid kosong.

### 36a — Mesin Kalender Kerja (Master Data)
- **File baru**: `backend/build_calendar.py`
- **Koleksi baru**: `build_work_calendars`
  - 1 dokumen per org, dengan **opsional override per proyek**.
  - Skema: pola 7 hari (full/half/off), daftar libur `[{date, name, kind}]`, ambang bentrok
    (`max_items_per_person_per_day`, `max_critical_per_day`).
- **Resolver**: `resolve(org, project_id)` digunakan oleh UI kalender dan mesin jadwal.
- **Integrasi ke mesin jadwal**:
  - `backend/build_engine.py` diberi parameter opsional untuk hari off (kompatibel ke belakang).
  - `backend/build_bulk.py` (`plan_for_template`, `plan_shift`) memakai resolver yang sama.
  - Hasil: libur nasional benar-benar **dilewati** oleh jadwal (bukan hanya diwarnai UI).

### 36b — Agregasi Bulanan + Deteksi Bentrok
- **File baru**: `backend/build_calendar_view.py`
- **Endpoint**: `GET /api/build/calendar?month=YYYY-MM&project_id=&kinds=&assignee=`
  - `days[]`: jenis hari, nama libur, jumlah acara, beban per orang.
  - `events[]`: 5 jenis acara (konstruksi item, start/finish jadwal unit, inspeksi/QC terjadwal,
    punch list due, Work Hub due—kecuali task yang punya `meta.build_item_id` agar tidak dobel).
  - `conflicts[]`: `overload / critical_stack / non_workday` + detail orang/daftar pekerjaan + saran.
  - `summary`, `unscheduled` (inspeksi tanpa `scheduled_date`).
- **Lintas proyek**: bila `project_id` kosong, tampil portofolio (dibatasi proyek yang user boleh akses).

### 36c — SSOT & Model
- **SSOT**: `backend/reference_p36.py` (grup baru):
  - `calendar_event_kind`, `calendar_day_kind`, `calendar_conflict_kind`, `holiday_kind`, `calendar_scope`
- Tambahkan **36** ke tuple `_PHASES` di `backend/reference.py`.
- **Model**: `backend/models_p36.py`:
  - `WorkCalendarIn`, `HolidayIn`, `InspectionScheduleIn`.

### 36d — Router & RBAC
- **Router baru**: `backend/routers/build_calendar_router.py`
  - `GET /build/calendar`
  - `GET /build/calendar/settings`
  - `PUT /build/calendar/settings`
  - `POST /build/calendar/holidays`
  - `DELETE /build/calendar/holidays/{date}`
- **Tambahan ke inspeksi**: `PUT /inspections/{id}/schedule` di `inspection_router.py`.
- **RBAC**:
  - lihat kalender: `construction.view` (PM/direksi/pelaksana/keuangan)
  - ubah setting/libur: admin/owner/PM (ditambah `audit_log`)
  - sales: 403 dengan pesan sopan.

### 36e — Seed
- **File baru**: `backend/seed_phase36.py`
  - kalender bawaan: Minggu off, Sabtu setengah hari
  - daftar libur nasional 2026 **bertanda** "bawaan, wajib disesuaikan admin" (jujur)
  - menjadwalkan inspeksi demo (idempoten)
- Dipanggil di `server.py` lifespan **setelah** `seed_phase33`.

### 36f — POC (wajib sebelum frontend)
- **File baru**: `scripts/poc_36.py` (API nyata) harus **100% PASS** untuk INV-36-1..10.

### 36g — Frontend
- Halaman baru **`/build-calendar`**: "Kalender Jadwal".
  - Tambah di `navigationConfig.js` (NAV + PAGE_META) dan `App.js` route.
- Komponen:
  - `CalendarMonthGrid` (grid bulan, badge jenis acara, penanda libur & bentrok)
  - `CalendarDayPanel` (detail hari: daftar acara + tombol buka unit/pekerjaan + tombol geser)
  - `CalendarConflictPanel` (daftar bentrok + penjelasan manusiawi + CTA)
  - `CalendarFilters` (pemilih proyek/semua proyek, bulan, jenis acara, pelaksana)
  - `WorkCalendarDialog` (pengaturan pola hari kerja + CRUD libur; hanya admin/PM)
- Integrasi tombol **"Geser jadwal"** membuka `BulkShiftDialog` Fase 34 (bukan mesin baru).
- **testIds**: file baru `frontend/src/constants/testIds/buildCalendar.js` dan re-export dari index.
- Semua state wajib: loading/error/kosong/akses ditolak (patuh `ux_audit.py`).

### 36h — Gate & Verifikasi
- **Gate baru**: `scripts/verify_36.py` masuk `scripts/run_all_gates.sh` → jadi **17 gates**.
- `verify_api_contract.py` harus hijau: semua `api.get/post` FE cocok route BE.
- `audit_endpoint_sweep.py`: semua GET /api sebagai owner tanpa 5xx.
- Tidak boleh regresi: `verify_31/32/33/34/35` tetap PASS.
- **testing_agent_v3** wajib: user stories Fase 36 + regresi Fase 31–35.

### User stories Fase 36 (dipakai testing agent)
1. PM membuka Kalender Jadwal, memilih bulan, dan langsung melihat tenggat semua rumah dalam satu grid bulanan.
2. PM mengganti cakupan ke "semua proyek" dan melihat portofolio lintas proyek.
3. PM melihat spanduk bentrok "Eko Site kebagian 5 tenggat pada 20 Agustus" lalu membuka detail hari itu.
4. PM melihat tenggat yang jatuh pada hari libur nasional (mis. 17 Agustus) ditandai + saran tanggal kerja terdekat.
5. PM melihat tumpukan pekerjaan KRITIS/hold point pada satu tanggal.
6. Dari kalender PM menekan "Geser jadwal" → dialog Fase 34 terbuka, wajib penyebab + catatan, pratinjau menunjukkan bukti terverifikasi dipertahankan.
7. Admin/PM membuka pengaturan kalender kerja: mengubah Sabtu menjadi setengah hari, menambah/menghapus hari libur; perubahan langsung terlihat di kalender dan dipakai saat jadwal baru dibuat.
8. PM menjadwalkan inspeksi QC yang belum bertanggal dari panel "belum dijadwalkan" lalu inspeksi itu muncul di kalender.
9. Pelaksana (site@sipro.co.id) melihat kalender miliknya tanpa tombol pengubah jadwal.
10. Sales (sales@sipro.co.id) mendapat kartu "AKSES DITOLAK" yang sopan.
11. Filter jenis acara bekerja dan jumlah di ringkasan ikut berubah.
12. Bulan tanpa acara menampilkan keadaan kosong yang menjelaskan.

---

## ✅ FASE 38 — SAPUAN PERMUKAAN TAMPILAN (latar kartu/field, label, kontras) — SELESAI & TERVERIFIKASI

### Masalah nyata yang ditutup
Keluhan pemakai yang memicu sesi sebelumnya: *"banyak kartu rusak, tidak ada background"*.
Akar pertamanya sudah ditemukan (Input/Textarea/Select bawaan shadcn memakai `bg-transparent`
sehingga field di atas panel berwarna tampak tanpa latar) dan diperbaiki. Yang **belum** ada:
alat untuk membuktikan sisanya, dan penjaga supaya tidak kembali. Terutama karena alat audit
lama (`ui_audit_shots.py`, `ui_audit_tabs.py`) hanya mengukur halaman **pada keadaan awal** —
padahal keluhan itu paling banyak muncul **di dalam dialog**, tempat field bertumpuk di atas
panel berwarna.

### 38a — Alat baru: audit DI DALAM dialog
`scripts/ui_audit_dialogs.py` (baru): masuk sebagai satu peran, membuka setiap dialog di
seluruh halaman (dikenali dari kata kerja pada label tombol, bukan dari testid, supaya tombol
yang lupa diberi testid pun ikut terperiksa), lalu **mengukur** di dalam dialog:
`D1` panel berbingkai/berbayang tanpa latar · `D2` field tanpa latar sendiri ·
`D3` tombol aksi terakhir tak terjangkau (hanya bila panel memang tidak bisa digulir) ·
`D4` teks meluber tanpa elipsis · `D5` field bisu (tanpa label/aria-label/placeholder) ·
`D6` kontras teks < 3:1 terhadap latar efektifnya. Hasil: JSON + tangkapan layar tiap dialog.

### 38b — Temuan (terukur) & perbaikannya
| Temuan | Akibat nyata | Perbaikan |
|---|---|---|
| `D1` panel 698×1826 tanpa latar di layar Kalibrasi; 1 panel tanpa latar di dialog "Jadwal massal"; 3 pembungkus tabel (`LedgerDrillSheet`, `BroadcastPanel`, `SpkScopeSection`) | daftar/tabel tampak "menggantung" tanpa kartu — inilah "kartu rusak" | `bg-card` pada kelima pembungkus |
| `D5` 21 field bisu di 7 dialog (izin, buku harian, subkon, RAB, PO, pengguna, material) | kotak isian tanpa nama: pemakai menebak, pembaca layar bungkam, penguji hanya bisa pegang urutan DOM | `id`+`htmlFor`, `data-testid`, dan **placeholder contoh nyata** (mis. "503/1234/DPMPTSP/2026") |
| Label tidak tertaut di **79** tempat lain | klik tulisan label tidak memindahkan kursor ke kotaknya | codemod mekanis `scripts/_patch_label_ids.py` (hanya `<Label>` tanpa atribut + kontrol tanpa `id`) |
| `D5` semua `ReferenceSelect` | pemicu shadcn adalah `<button>`, jadi label di atasnya tidak pernah tertaut | `aria-label` diambil dari label grup SSOT `/api/reference` (tanpa mengetik ulang teks) |
| `D6` legenda grafik "Rencana" kontras **2.1:1** | tulisan legenda memakai warna garis amber → nyaris tak terbaca di latar putih | pembantu baru `utils/chartUi.js` (`legendLabel`) dipakai 4 grafik; kotak warna seri tetap |
| teks panjang terpotong (kas bon, aset, audit, pemilih template) | isi tidak terbaca | sudah ada `title` (hover) di 3 tempat; pemilih template di layar Kalibrasi ditambahkan |

### 38c — Penjaga baru (gate ke-19)
`scripts/verify_ui_surfaces.py` masuk `run_all_gates.sh` (**19 gates**) dengan 20 pemeriksaan:
`S1` field wajib punya latar sendiri (bukan `bg-transparent`) · `S2` permukaan mengapung
(dialog/sheet/popover/dropdown/select/command) memakai latar **padat**, tidak boleh
semi-transparan · `S3` pembungkus tabel berbingkai wajib menyebut `bg-` ·
`S4` tidak ada `<Label>` menggantung tanpa tautan ke field · `S5` setiap `<Legend>` memakai
`formatter` warna teks yang terbaca.
Gate ini **diuji-mutasi**: `bg-background` pada `input.jsx` sengaja dikembalikan ke
`bg-transparent` → gate GAGAL seperti seharusnya, lalu dipulihkan → PASS (jadi gate ini
benar-benar menjaga, bukan hiasan). Satu bug pada gate sendiri ikut ketemu dari uji ini:
pengambilan class dengan memasangkan tanda kutip dari awal berkas salah membaca komentar,
sehingga sempat lolos padahal class-nya tidak terbaca.

### 38d — Bukti sebelum → sesudah (angka, bukan kesan)
| Ukuran | Sebelum | Sesudah |
|---|---|---|
| Kartu tanpa latar (35 halaman, peran owner) | 1 | **0** |
| Kartu tanpa latar (55 tab) | 0 | **0** |
| Dialog bermasalah / temuan — owner | 11 dialog / 22 temuan | **0 / 0** (37 dialog) |
| Dialog bermasalah / temuan — pm | 13 dialog / 19 temuan | **0 / 0** (40 dialog) |
| Dialog bermasalah / temuan — finance | 0 / 0 | **0 / 0** (43 dialog) |
| Dialog bermasalah / temuan — pelaksana (site) | — | **0 / 0** (44 dialog) |
| Gate | 18 PASS | **19 PASS** |

### Catatan jujur
- Teks panjang yang terpotong dengan elipsis **tetap ada** di kas bon/aset/log audit — itu
  memang disengaja (kolom sempit), dan isi penuhnya muncul saat kursor diarahkan (`title`).
- Kesalahan konsol yang terlihat saat audit lewat `localhost:3000` (`ws://localhost:443/ws`)
  adalah socket hot-reload webpack, bukan cacat aplikasi: lewat URL pratinjau **0 error**.
  Karena itu audit sekarang dijalankan dengan `SIPRO_UI_BASE=<url pratinjau>`.
- Respons 403 yang tercatat sebagai "console error" pada halaman terlarang adalah **RBAC yang
  bekerja** (halaman menampilkan kartu AKSES DITOLAK), bukan kerusakan.

---


## 3) Next Actions (immediate)
Fase 31–36, **37 (Kalibrasi Sekali Klik)**, dan **38 (Sapuan Permukaan Tampilan)**
selesai & terverifikasi. Urutan berikutnya (owner minta **ditahan dulu** — tunggu arahan):
1. **Kurva-S & laporan portofolio lintas proyek** untuk direksi (laporan mingguan masih per proyek).
2. **Ringkasan laporan mingguan via WhatsApp** (butuh kredensial Meta; WA masih simulasi).
3. Lanjutan sapuan tampilan bila owner menyebut halaman tertentu: alat ukurnya sudah ada
   (`ui_audit_shots.py`, `ui_audit_tabs.py`, `ui_audit_dialogs.py`) sehingga perbaikan
   berikutnya bisa langsung berbasis angka, bukan tebakan.

## 3b) Catatan pemeliharaan
- **`backend/reference.py` sudah menyentuh batas compliance (≤800 baris).** Grup fase baru
  WAJIB dibuat di `reference_p<NN>.py`, lalu cukup **menambahkan nomor fase ke tuple `_PHASES`**
  di `reference.py` (pemuatan sudah dinamis sejak Fase 35).
- **Setelah pull/restore repo (PENTING — sudah EMPAT kali terjadi):**
  1. `/app/backend/.env` di-gitignore → buat ulang: `JWT_SECRET` (acak), `EMERGENT_LLM_KEY`,
     `PORTAL_MASTER_OTP=000000`, `DEFAULT_ORG_ID=org-sipro`, `DEFAULT_ORG_NAME=PT SIPRO Land`,
     `COOKIE_SECURE=true`, `BOOKING_HOLD_DAYS=7`, `STORAGE_PROVIDER=emergent`, `PHOTO_*`.
     Tanpa `JWT_SECRET`, login **500 (`KeyError: JWT_SECRET`)**.
  2. `pip install APScheduler reportlab` — dua paket ini TIDAK ada di image dasar
     (tanpa itu backend gagal start: `ModuleNotFoundError: reportlab`).
     Catatan: `pip install -r backend/requirements.txt` **gagal** (konflik
     `emergentintegrations` vs `litellm` yang sudah ada di image) — cukup dua paket di atas.
     Untuk alat audit tampilan tambahkan `pip install playwright` (hanya untuk
     `scripts/ui_audit_*.py`; SENGAJA tidak dimasukkan `requirements.txt` karena backend
     tidak memakainya — `/usr/bin/google-chrome` sudah tersedia di image, jadi tidak perlu
     `playwright install`).
  3. `cd frontend && yarn install`, lalu `sudo supervisorctl restart backend frontend`.
  4. `bash scripts/seed_reset.sh` → harus **OVERALL PASS (19 gates)**.
  5. Kredensial uji ada di `/app/memory/test_credentials.md` (sandi `Sipro#2026`).
- Sebelum menyatakan sebuah fase selesai, WAJIB hijau semua:
  - `bash scripts/run_all_gates.sh` (**19 gates**, termasuk `verify_37.py` + `verify_ui_surfaces.py`)
  - `poc_31.py` (63) + `poc_32.py` (79) + `poc_33.py` (66) + `poc_34.py` (57) + `poc_35.py` (43) + `poc_36.py` (**132**) + `poc_37.py` (**85**)
  Catatan: `poc_35.py` memakai 3 pekerjaan siap kerja hasil seed — jalankan pada DB tersegar
  (`seed_reset.sh` lalu ulangi drop+restart bila POC lain sudah menghabiskannya).
- **Bypass uji**: tidak ada backdoor auth; pengujian memakai akun demo asli + tombol
  "Masuk cepat" di halaman login (hanya memanggil `POST /auth/login` biasa). Tombol demo ini
  boleh dimatikan sebelum go-live — beri tahu agar dihapus dari `pages/Login.js`.
- **Arsip bukti**: salinan lengkap bukti penutupan Fase 31–35 disimpan di
  `memory/plan_archive_upto_fase35.md` (jangan dihapus).
- **Pelajaran pengujian (dari Fase 36 ronde-2)**: bila sebuah angka **tidak kembali ke baseline**
  setelah pengujian, itu **sinyal cacat** — jangan diterima sebagai "efek state". Dan angka pada
  kartu ringkasan harus dibaca dari elemen NILAI-nya (nilai `3` + hint `0 beban · 2 hari libur`
  akan terbaca `30` bila seluruh teks kartu dipungut digitnya).

---

## 4) Success Criteria
- ✅ WorkHub berfungsi sesuai domain divisi dan menjadi penggerak kerja.
- ✅ Lead lifecycle menjadi gerbang bukti; WA terintegrasi; stage tidak loncat.
- ✅ Construction Progress Engine v2 (Fase 31) stabil.
- ✅ Fase 32 stabil (Papan Mandor, laporan mingguan, analitik telat, policy GPS).
- ✅ Fase 33 stabil (uang mengikuti bukti).
- ✅ Fase 34 stabil (jadwal massal & geser massal menjaga bukti).
- ✅ Fase 35 stabil (offline queue jujur & idempotent).
- ✅ **Fase 36 (Kalender Jadwal) — TERCAPAI**:
  - PM/direksi bisa melihat **kalender bulanan** tenggat lintas unit, dan opsional lintas proyek.
  - Bentrok (beban pelaksana, tumpukan kritis, jatuh di non-kerja) terlihat jelas sebelum telat.
  - Hari libur & pola hari kerja bisa diatur admin dan dipakai **UI + mesin jadwal**.
  - Mengubah tanggal tetap lewat Fase 34 (beralasan + audit + bukti terverifikasi dipertahankan).
  - Semua perubahan menjaga compliance (py<800, js<500, util<300, css<400) dan `bash scripts/run_all_gates.sh` tetap PASS.
