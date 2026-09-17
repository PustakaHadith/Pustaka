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
