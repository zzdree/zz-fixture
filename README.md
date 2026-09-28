# 💡 zz-fixture

> **Custom Stage & Church Lighting Fixture Definitions for QLC+ (Q Light Controller Plus) & ZZLUXORA.**  
> Authored and maintained by **Andreas Restuawanta Christwara (`zzdree`)**.

[![Format](https://img.shields.io/badge/Format-QLC%2B%20.qxf-blue?style=flat-square)](https://www.qlcplus.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Compatibility](https://img.shields.io/badge/Compatibility-QLC%2B%20v4%20%7C%20v5%20%7C%20ZZLUXORA-orange?style=flat-square)](https://github.com/zzdree/zzluxora-v10)

---

## 📋 Fixture Catalog

| File | Manufacturer | Model | Type | Channels | Description / Channel Map |
| :--- | :--- | :--- | :--- | :---: | :--- |
| **`Alien-AL36.qxf`** | **Alien** | `AL36` | Color Changer (PAR LED) | **8-CH** | Ch 1 Dimmer, Ch 2 Red, Ch 3 Green, Ch 4 Blue, Ch 5 Empty, Ch 6 Program, Ch 7 Speed, Ch 8 Emptz |
| **`Kumastb-STL47.qxf`** | **Kumastb** | `STL47` | Color Changer (PAR LED RGBW) | **8-CH** | Ch 1 Dimmer, Ch 2 Red, Ch 3 Green, Ch 4 Blue, Ch 5 White, Ch 6 Strobe, Ch 7 Program, Ch 8 Speed |

---

## 🛠️ Cara Penggunaan di QLC+

### 1. Salin File Profil ke Direktori User Fixtures QLC+

#### Linux (Ubuntu / Mint / Debian):
```bash
mkdir -p ~/.qlcplus/fixtures/
cp *.qxf ~/.qlcplus/fixtures/
```

#### Windows:
Salin berkas `.qxf` ke:
```text
C:\Users\<Username>\QLC+\Fixtures\
```
Atau direktori instalasi global QLC+:
```text
C:\QLC+\Fixtures\
```

### 2. Memuat di QLC+
1. Buka aplikasi **QLC+** (`qlc+4` atau `qlc+5`).
2. Masuk ke tab **Fixtures**.
3. Klik tombol **Add Fixtures (+)**.
4. Pilih Manufacturer: **Alien** atau **Kumastb**.
5. Pilih model yang sesuai dan tentukan Universe serta DMX Address awal.

---

## 📄 Lisensi

Open-source di bawah lisensi [MIT](LICENSE).
