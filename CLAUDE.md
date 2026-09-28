# 💡 CLAUDE.md — zz-fixture: Technical Directive & Fixture Profiling Guide

Dokumen ini adalah **single source of truth operasional** untuk Claude Code, AI Agent, dan pengembang dalam membedah, mengintegrasikan, dan memetakan profil lampu panggung **zz-fixture** ke dalam ekosistem riset skripsi dan konsol **ZZLUXORA v10**.

---

## 📌 1. Identitas & Ruang Lingkup Proyek

- **Nama Proyek:** **zz-fixture** (Stage Lighting Fixture Definitions)
- **Repositori:** `https://github.com/zzdree/zz-fixture.git` (Public Repository)
- **Peneliti / Pengembang:** Andreas Restuawanta Christwara (`NIM: 5312422036`)
- **Institusi:** Program Studi S1 Teknik Komputer, Fakultas Teknik, Universitas Negeri Semarang (UNNES)
- **Format Berkas Utama:** XML-based QLC+ Fixture Definition (`.qxf`, schema v4.14.3+)
- **Format Target Konsol:** JSON-based ZZLUXORA Fixture Definition (`.zfx`)

---

## 🔬 2. Pembedahan Spesifikasi Teknis & Relevansi Riset

### A. Fixture 1: Alien AL36 (`Alien-AL36.qxf`)
- **Pabrikan & Model:** Alien AL36
- **Klasifikasi Fisik:** PAR LED 36 mata (36 × 1W diodes), ukuran sedang (*medium-compact stage PAR*), konsumsi daya 36 Watt, konektor DMX 3-pin XLR.
- **Konfigurasi Emisi Warna:** **RGB Murni** (Additive color mixing Red, Green, Blue). Tidak memiliki chip White fisik terpisah.
- **Inventaris Kepemilikan:** **4 unit fisik** dimiliki oleh Andreas Restuawanta Christwara.
- **Penempatan & Penggunaan Lapangan:**
  - Terpasang aktif di **Gereja Isa Almasih (GIA) Deliksari Semarang**.
  - Merupakan unit pencahayaan panggung utama dalam skenario penelitian naskah Skripsi Andreas (*"Rancang Bangun Sistem Audio-Reactive Lighting Design Berbasis Analisis Mood Lagu Rohani..."*).
  - Keempat unit dihubungkan secara *daisy-chain* DMX512 ke node Art-Net ESP32 (`artnet_dmx_final.ino`), dialokasikan berturut-turut pada kanal DMX 1-8, 9-16, 17-24, dan 25-32.
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [DMX Offset 0]: Master Dimmer (0-255)
  Ch 2 [DMX Offset 1]: Red Intensity (0-255)
  Ch 3 [DMX Offset 2]: Green Intensity (0-255)
  Ch 4 [DMX Offset 3]: Blue Intensity (0-255)
  Ch 5 [DMX Offset 4]: Empty / Reserved
  Ch 6 [DMX Offset 5]: Built-in Program / Internal Color Macros (0-255)
  Ch 7 [DMX Offset 6]: Program Speed / Chase Rate (0-255)
  Ch 8 [DMX Offset 7]: Emptz / Reserved
  ```

---

### B. Fixture 2: Kumastb STL47 (`Kumastb-STL47.qxf`)
- **Pabrikan & Model:** Kumastb STL47
- **Klasifikasi Fisik:** Mini PAR LED 12 mata (12 × 1W diodes), ukuran ringkas (*mini PAR LED*), konsumsi daya 12 Watt, konektor DMX 3-pin XLR.
- **Konfigurasi Emisi Warna:** **Physical 4-Kanal RGBW** (Red, Green, Blue, dan Dedicated Pure White).
- **Inventaris Kepemilikan:** **1 unit fisik** dimiliki oleh Andreas Restuawanta Christwara.
- **Peran Riset Khusus:**
  - **Unit Uji Laboratorium (*Bench Testing Unit*)**.
  - Digunakan secara spesifik di meja kerja dev untuk memverifikasi dan memvalidasi keakuratan komputasi algoritma konversi warna lintas-modal pada **ZZLUXORA v10** (`core/color_engine.py`):
    $$W = \min(R, G, B)$$
    $$R' = R - W, \quad G' = G - W, \quad B' = B - W$$
  - Menguji pencegahan fenomena *color washout* saat suasana lagu bertransisi dari Kuadran 1 *Praise* (riang gembira, dominan RGB penuh) menuju Kuadran 3 *Deep Worship* (khidmat teduh, di mana kanal White murni Ch 5 dinyalakan untuk menghasilkan saturasi hangat tanpa silau).
- **Pemetaan Kanal DMX (8-Channel Mode):**
  ```text
  Ch 1 [DMX Offset 0]: Master Dimmer (0-255)
  Ch 2 [DMX Offset 1]: Red Intensity (0-255)
  Ch 3 [DMX Offset 2]: Green Intensity (0-255)
  Ch 4 [DMX Offset 3]: Blue Intensity (0-255)
  Ch 5 [DMX Offset 4]: Pure White Intensity (0-255) -> Target Dekomposisi Physical RGBW
  Ch 6 [DMX Offset 5]: Strobe / Shutter Flash Rate (0-255)
  Ch 7 [DMX Offset 6]: Built-in Program / Macro Modes (0-255)
  Ch 8 [DMX Offset 7]: Program Speed (0-255)
  ```

---

## 🎛️ 3. Pedoman Teknis untuk AI Agent & Pengembang

1. **Ketika Mengintegrasikan ke Tab Address ZZLUXORA v10:**
   - Gunakan kode singkatan warna konsol industri:
     - Ch 1: `DIM` (Amber/Yellow)
     - Ch 2: `RED` (Pure Red)
     - Ch 3: `GRN` (Pure Green)
     - Ch 4: `BLU` (Pure Blue)
     - Ch 5 (Kumastb): `WHT` (Pure White)
     - Ch 6 (Kumastb): `STR` (Cyan/Purple)
   - Selalu perhatikan bahwa Alien AL36 **TIDAK memiliki kanal White** (Ch 5-nya `Empty`), sedangkan Kumastb STL47 **memiliki kanal White aktif** di Ch 5.
2. **Ketika Melakukan Pengujian SITL QLC+:**
   - Gunakan template loopback `/home/zzdree/ANDREAS/zzluxora_test.qxw` atau `zzluxora_v10/fixtures/qlcplus_template.qxw`.
   - Pastikan alamat IP Art-Net mengarah ke `127.0.0.1:6454` (Universe 0/1) dengan mode Passthrough aktif di QLC+.
3. **Standar Penulisan & Ekstensi:**
   - Profil QLC+ asli: `.qxf` (XML).
   - Profil fixture ZZLUXORA: `.zfx` (JSON).
   - Showfile proyek panggung: `.zlx` (JSON terkompresi).
