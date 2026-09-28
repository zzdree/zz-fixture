# 💡 CLAUDE.md — zz-fixture: Lighting Fixture Definition Profiles

Dokumen ini adalah **panduan operasional dan referensi channel mapping** untuk Claude Code dan AI Agent yang bekerja dengan profil fixture tata cahaya panggung milik **Andreas Restuawanta Christwara (`zzdree`)**.

---

## 📌 1. Identitas & Tujuan

- **Repositori:** `https://github.com/zzdree/zz-fixture.git`
- **Tipe Format:** XML-based QLC+ Fixture Definition (`.qxf`).
- **Target Integrasi:** QLC+ v4.14+, QLC+ v5 3D, dan konsol pencahayaan panggung **ZZLUXORA v10** (`.zfx` converter).

---

## 🎛️ 2. Detail Spesifikasi Kanal DMX

### 1. `Alien-AL36.qxf`
- **Pabrikan:** Alien
- **Model:** AL36 (PAR LED Stage Light)
- **Tipe:** Color Changer (8 Channels)
- **Alokasi Kanal DMX:**
  - `Ch 1`: **Dimmer / Master Intensity** (0-255)
  - `Ch 2`: **Red** (0-255)
  - `Ch 3`: **Green** (0-255)
  - `Ch 4`: **Blue** (0-255)
  - `Ch 5`: **Empty / Reserved**
  - `Ch 6`: **Internal Program / Macro** (0-255)
  - `Ch 7`: **Program Speed / Chase Rate** (0-255)
  - `Ch 8`: **Emptz / Reserved**

### 2. `Kumastb-STL47.qxf`
- **Pabrikan:** Kumastb
- **Model:** STL47 (PAR LED RGBW Stage Light)
- **Tipe:** Color Changer (8 Channels)
- **Alokasi Kanal DMX:**
  - `Ch 1`: **Dimmer / Master Intensity** (0-255)
  - `Ch 2`: **Red** (0-255)
  - `Ch 3`: **Green** (0-255)
  - `Ch 4`: **Blue** (0-255)
  - `Ch 5`: **White** (0-255) — *Mendukung dekomposisi fisik 4-kanal RGBW ZZLUXORA anti-washout.*
  - `Ch 6`: **Strobe / Shutter Speed** (0-255)
  - `Ch 7`: **Internal Program / Auto Modes** (0-255)
  - `Ch 8`: **Program Speed** (0-255)

---

## 🔄 3. Integrasi ke ZZLUXORA v10

Profil fixture `.qxf` ini dapat dikonversi ke format JSON `.zfx` pada konsol ZZLUXORA v10 via `Fixture Definition Editor` (`ui/panels/fixture_editor.py`) untuk penggunaan otomatis dalam grid patch DMX 256 kanal.
