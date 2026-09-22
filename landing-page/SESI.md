# Sesi Landing Page — Todo List

## Sesi 23 (17 September 2026) — v1.0.2

### Selesai
- [x] Fon Arab bundle: KFGQPC Uthmanic Script HAFS + Amiri (Regular/Bold)
- [x] Buang tetapan API dari UI (pages_tetapan.py + settings_panel.py + ApiDialog)
- [x] API key hanya dari config/env (get_api_key())
- [x] Butang WhatsApp → butang Kongsi dengan menu popup (WhatsApp/Telegram/Facebook/Instagram)
- [x] Pautan "Baca penuh" tukar dari sunnah.com ke pustakahadith.my/{slug}/{id}
- [x] PustakaHadith.spec: tambah ('fonts', 'fonts') ke datas
- [x] AppxManifest.xml untuk MSIX
- [x] Logo Store: 44x44, 71x71, 150x150, 310x310, Wide, SplashScreen, StoreLogo
- [x] Skrip build_msix.bat

### Pending — Uji Apl (manual)
- [ ] Uji apl — pastikan fon bundel muncul dalam senarai fon Tetapan
- [ ] Uji apl — pastikan teks Arab dipaparkan dengan fon bundel
- [ ] Uji apl — pastikan apl berfungsi tanpa panel API

### Pending — Build
- [ ] Rebuild .exe dengan PyInstaller — JALANKAN MANUAL di terminal:
  ```
  cd D:\Pustaka Quran Hadis\Pustaka\PustakaHadith
  .venv-build\Scripts\python.exe -m PyInstaller PustakaHadith.spec --clean --noconfirm
  ```
- [ ] Run build_msix.bat untuk package MSIX
- [ ] Sign MSIX dengan signtool
- [ ] Upload ke Microsoft Partner Center

### Pautan Baru
- Kongsi multi-platform: WhatsApp, Telegram, Facebook, Instagram (salin teks)
- Pautan "Baca penuh": pustakahadith.my/{slug}/{hadis_id}

---

## Sesi 28–29 (21 September 2026) — Store v1.0.2 Live + Pindah ke Cloudflare

### Selesai
- [x] **Store submission BERJAYA diterbitkan** — v1.0.2.0 live di Microsoft Store (`https://apps.microsoft.com/detail/9MWLXVH2ZC7Q`)
- [x] **Pindah hosting/DNS ke Cloudflare** (Pages + DNS) — URL rasmi kekal `https://pustakahadith.my`
- [x] **Kad Store dl1-p dikemas** ke "v1.0.2 disahkan &amp; live" (781.9 MB) — ms + en
- [x] EXE/7z kekal v1.0.1 (tidak dibina semula) — pautan dl2/dl3 tidak berubah

### Pending
- [ ] Deploy semula landing page di Cloudflare dengan kad Store v1.0.2 (perlu arahan/sijil akses)

---

## Sesi 33 (22 September 2026) — Pautan Download → v1.0.2

### Selesai
- [x] **EXE + 7z v1.0.2 dibina** di repo PustakaHadith:
  - `Output/PustakaHadith-Setup-1.0.2-x64.exe` (820,210,212 bait)
  - `Output/PustakaHadith-portable-1.0.2-x64.7z` (802,754,038 bait)
- [x] **`index.html` dikemas ke v1.0.2** (ms + en):
  - dl2 EXE href → `.../v1.0.2/PustakaHadith-Setup-1.0.2-x64.exe`
  - dl3 7z href → `.../v1.0.2/PustakaHadith-portable-1.0.2-x64.7z`
  - dl-note → "Versi 1.0.2" / "Version 1.0.2"
  - dl1 Store kekal v1.0.2 ✅
- [x] `PustakaHadith.iss` Source path → canonical `PustakaQH_dist`

### Pending
- [ ] GitHub Release v1.0.2 (upload EXE + 7z) — menunggu `gh auth login`
- [ ] Commit + push landing page → Cloudflare auto-deploy — menunggu arahan
- [ ] Verifikasi `https://pustakahadith.my` papar pautan v1.0.2 selepas deploy
