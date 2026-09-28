# 💡 zz-fixture — Stage Lighting Fixture Definitions

> **Koleksi Profil Definisi Fixture Lampu Panggung Resmi (.qxf) untuk QLC+ (Q Light Controller Plus) dan Konsol Pencahayaan ZZLUXORA v10.**  
> Dirancang, diuji, dan dipelihara oleh **Andreas Restuawanta Christwara (`zzdree`)** untuk riset komputasi pencahayaan panggung dan tata ibadah Gereja Isa Almasih (GIA) Deliksari Semarang.

[![Format](https://img.shields.io/badge/Format-QLC%2B%20.qxf-blue?style=flat-square)](https://www.qlcplus.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Compatibility](https://img.shields.io/badge/Compatibility-QLC%2B%20v4%20%7C%20v5%203D%20%7C%20ZZLUXORA%20v10-orange?style=flat-square)](https://github.com/zzdree/zzluxora-v10)
[![Research](https://img.shields.io/badge/Research-Skripsi%20FT%20UNNES-red?style=flat-square)](https://github.com/zzdree/script)

---

## 📌 Ringkasan Inventaris & Peruntukan Fisik

| Parameter | Alien AL36 (`Alien-AL36.qxf`) | Kumastb STL47 (`Kumastb-STL47.qxf`) |
| :--- | :--- | :--- |
| **Pabrikan (Brand)** | **Alien** | **Kumastb** |
| **Model** | **AL36** | **STL47** |
| **Konfigurasi Mata LED** | **36 Mata LED** (36 × 1W High-Power LED) | **12 Mata LED** (12 × 1W High-Power LED) |
| **Dimensi Fisik** | Sedang / Sedengan (*Medium Compact PAR*) | Ringkas (*Mini PAR LED*) |
| **Sistem Emisi Warna** | **RGB Murni** (Additive Tri-Color) | **Physical RGBW** (Tri-Color + Dedicated Pure White) |
| **Daya Listrik** | 36 Watt | 12 Watt |
| **Jumlah Unit Fisik** | **4 Unit** (Milik Andreas) | **1 Unit** (Milik Andreas) |
| **Lokasi & Peran** | **Terpasang Aktif di GIA Deliksari Semarang** | **Unit Laboratorium (Bench Testing)** |
| **Peran dalam Skripsi** | Panggung Utama Riset & Pengujian Lapangan DMX512 | Validasi Algoritma Dekomposisi 4-Kanal RGBW ZZLUXORA |

---

## 🔬 Pembedahan Mendalam Karakteristik Fixture

### 1. Alien AL36 (PAR LED 36 Mata — 4 Unit di GIA Deliksari)
* **Karakter Cahaya:** Memiliki 36 titik emisi LED dengan pancaran cahaya solid berintensitas menengah (*medium wash coverage*). Menggunakan konfigurasi warna aditif **RGB (Red, Green, Blue)**.
* **Peruntukan Lapangan:** Menjadi instrumen pencahayaan utama (*front/back wash lighting*) di panggung ibadah **GIA Deliksari Semarang**, sebagaimana dirumuskan pada denah panggung (Gambar 3.4) naskah Skripsi FT UNNES.
* **Koneksi Panggung:** Keempat unit dihubungkan secara *daisy-chain* menggunakan kabel XLR 3-pin standar RS-485 menuju modul hardware **ESP32 Art-Net to DMX512 Node** (`artnet_dmx_final.ino`).

#### 🎛️ Tabel Alokasi Kanal DMX (Alien AL36 — 8 Channels):
| QLC+ Index | DMX Channel | Fungsi / Parameter | Rentang Nilai | Karakteristik Operasional |
| :---: | :---: | :--- | :---: | :--- |
| **0** | **Ch 1** | **Master Dimmer** | `0 - 255` | Mengatur intensitas keseluruhan lampu secara linear (0% - 100%). |
| **1** | **Ch 2** | **Red** | `0 - 255` | Intensitas LED Merah. |
| **2** | **Ch 3** | **Green** | `0 - 255` | Intensitas LED Hijau. |
| **3** | **Ch 4** | **Blue** | `0 - 255` | Intensitas LED Biru. |
| **4** | **Ch 5** | **Empty / Reserved** | `0 - 255` | Kanal kosong / tidak terhubung pada firmware internal fixture. |
| **5** | **Ch 6** | **Built-in Program (Macro)** | `0 - 255` | Memanggil pola animasi bawaan (strobe internal, color jump, fade). |
| **6** | **Ch 7** | **Program Speed** | `0 - 255` | Kecepatan transisi pola makro internal pada Ch 6. |
| **7** | **Ch 8** | **Emptz / Reserved** | `0 - 255` | Kanal cadangan firmware internal. |

---

### 2. Kumastb STL47 (Mini PAR LED 12 Mata RGBW — 1 Unit Bench Test)
* **Karakter Cahaya:** Berukuran mini dan portabel dengan 12 mata LED. Keunggulan utamanya adalah kehadiran **chip LED White (W) murni** yang terpisah dari LED RGB.
* **Peruntukan Riset:** Didedikasikan sebagai **unit uji laboratorium meja (*bench testing*)** di meja pengembang untuk memvalidasi algoritma dekomposisi ruang warna fisik 4-kanal pada aplikasi **ZZLUXORA v10**:
  $$\begin{aligned}
  W &= \min(R, G, B) \\
  R' &= R - W \\
  G' &= G - W \\
  B' &= B - W
  \end{aligned}$$
* **Manfaat Pengujian RGBW:** Ketika sistem mendeteksi lagu rohani beralih dari suasana *Praise* (penuh warna dinamis) ke suasana *Deep Worship* (khidmat), algoritma mengaktifkan kanal White murni (`Ch 5`) dan meredam saturasi RGB untuk menghasilkan warna putih hangat yang natural tanpa efek *color washout*.

#### 🎛️ Tabel Alokasi Kanal DMX (Kumastb STL47 — 8 Channels):
| QLC+ Index | DMX Channel | Fungsi / Parameter | Rentang Nilai | Karakteristik Operasional |
| :---: | :---: | :--- | :---: | :--- |
| **0** | **Ch 1** | **Master Dimmer** | `0 - 255` | Intensitas master fixture (0% - 100%). |
| **1** | **Ch 2** | **Red** | `0 - 255` | Intensitas LED Merah. |
| **2** | **Ch 3** | **Green** | `0 - 255` | Intensitas LED Hijau. |
| **3** | **Ch 4** | **Blue** | `0 - 255` | Intensitas LED Biru. |
| **4** | **Ch 5** | **White (Murni)** | `0 - 255` | **Kanal Putih Fisik Dedicated** (Anti-washout, ibadah khidmat). |
| **5** | **Ch 6** | **Strobe / Shutter** | `0 - 255` | Efek kedip strobo fisik (0 = nonaktif, 1-255 = lambat ke cepat). |
| **6** | **Ch 7** | **Built-in Program** | `0 - 255` | Mode otomatis dan makro warna internal fixture. |
| **7** | **Ch 8** | **Program Speed** | `0 - 255` | Kecepatan eksekusi program internal Ch 7. |

---

## 🚀 Panduan Instalasi & Penggunaan

### 1. Pemasangan Profil ke QLC+ (Linux & Windows)

#### Linux (Linux Mint / Ubuntu / Debian):
```bash
# Buat folder fixtures QLC+ pengguna jika belum ada
mkdir -p ~/.qlcplus/fixtures/

# Salin seluruh berkas .qxf
cp Alien-AL36.qxf Kumastb-STL47.qxf ~/.qlcplus/fixtures/
```

#### Windows 10/11:
Salin berkas `.qxf` ke salah satu jalur direktori berikut:
```text
C:\Users\<NamaUser>\QLC+\Fixtures\
atau
C:\Program Files\QLC+\Fixtures\
```

### 2. Memuat Fixture di Aplikasi QLC+
1. Buka aplikasi **QLC+** (`qlc+4` atau `qlc+5`).
2. Buka tab **Fixtures**.
3. Klik tombol **Add Fixtures (+)**.
4. Pada daftar pabrikan (*Manufacturer*), pilih:
   - `Alien` ➔ model `AL36` (untuk konfigurasi 4 unit panggung GIA).
   - `Kumastb` ➔ model `STL47` (untuk konfigurasi 1 unit bench testing RGBW).
5. Tentukan Universe (Universe 0 atau 1) dan Address DMX awal.

### 3. Integrasi ke Software ZZLUXORA v10
* Profil fixture ini kompatibel dengan modul parser `core/project_io.py` dan tab editor `ui/panels/fixture_editor.py` pada konsol **ZZLUXORA v10**.
* Format QLC+ `.qxf` dapat dikonversi ke format JSON `.zfx` berstandar industri konsol untuk otomatisasi patching 256 kanal DMX.

---

## 📄 Lisensi

Proyek ini dirilis secara bebas dan terbuka di bawah lisensi resmi [MIT License](LICENSE).
Semua pengembang, operator pencahayaan, dan gereja dipersilakan mengunduh, menggunakan, dan memodifikasi profil fixture ini.
