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

### Pending (Sesi 28–29 — sudah diselesaikan dalam Sesi 33)
- [x] Deploy semula landing page di Cloudflare dengan kad Store v1.0.2

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
- [x] **Commit + push** landing page (`3525f54`) → Cloudflare auto-deploy
- [x] **GitHub Release `v1.0.2`** — upload EXE + 7z; buang 3 asset v1.0.1 tersalah letak
- [x] **Verifikasi live** — `https://pustakahadith.my` HTTP 200, pautan `.../v1.0.2/...` aktif
- [x] Download EXE + 7z → HTTP 200, saiz betul

### Pending
- [ ] (tiada — Sesi 33 selesai)

---

## Sesi 35 (25 September 2026) — 3 Section Baharu + Footer Lengkap

Semua kerja **landing page sahaja**. 4 commit, semua sudah push (`bd4ce70..d616991` → Cloudflare auto-deploy).

### Selesai

**Section baharu (ikut mockup `mockup_tambah/mockup_3section.html` — diluluskan):**
- [x] **`#mula` — Cara Guna 3 Langkah** (selepas Hero, sebelum `#tampil`)
- [x] **`#soalan` — Soalan Lazim** — 6 item accordion (aria-expanded, buka satu-satu; item pertama dibuka) — antara "Kedudukan Jujur" sebelum band statistik
- [x] **`#kemas-kini` — Changelog v1.0.2** (kad + badge LIVE + 4 item + pautan GitHub Releases) — sebelum `#muat-turun`
- [x] CSS ketiga-tiga section + i18n ms/en penuh → **177 key, semua lengkap** (`node --check` lulus, 2 script)

**Footer KHAS (`#ciri-ai` / `#ciri-darjat` / `#ciri-penanda` — kad Ciri dapat id):**
- [x] 4 item `href="#"` → pautan ke kad Ciri + tooltip penjelasan
- [x] `scroll-padding-top:82px` supaya anchor tak sembunyi bawah nav tetap

**Footer Sumber:**
- [x] Dokumentasi → GitHub `dokumen/`; Kemas Kini → `#kemas-kini`
- [x] **Lesen Data → bukan pautan luar — modal kad penerangan** (4 baris: MIT · teks hadis hadis.my · terjemahan/darjat domain awam · huraian beratribusi + nota komersial; tutup via ✕/klik luar/ESC)
- [x] Biodata Penerbit ditambah — **teks biasa tanpa pautan** (`.foot-plain`)
- [x] "Syarah & Komentar" → **"Syarah & Huraian"** (KM: "komentar" kebiasaan BI)

**Kad Microsoft Store (dl-card MSIX):**
- [x] Badge rasmi **"Get it from Microsoft"** (`img/ms-badge-light.svg` dari get.microsoft.com — variant light sebab tema gelap) + pautan ke Store
- [x] Lencana **ESRB "E" Everyone** (`img/esrb-everyone.svg` dari Wikimedia Commons)
- [x] CSS `.dl-badges`

**Betulan:**
- [x] **Favicon tak muncul** — punca `href="/favicon.ico"` (absolut, gagal bila buka `file://`) → relatif `favicon.ico` + `apple-touch-icon.png`
- [x] `img/store-logo.png` (tak guna) & `ms-badge-dark.svg` (tak guna) dipadam

### Komitmen (push ke main)
| Commit | Kandungan |
|---|---|
| `4e73dc0` | 3 section baharu + mockup + cloudflare.md |
| `24f573f` | Footer KHAS bernaut + tooltip + scroll-padding |
| `64d7326` | Footer Sumber pautan + Biodata Penerbit + Syarah & Huraian |
| `d616991` | Badge MS Store + ESRB + favicon relatif + modal Lesen Data |

### Semakan
- [x] Latar `img/bg-globe.webp` kekal (`.globe-fixed` + div)
- [x] Susunan section: hero → `#mula` → `#tampil` → `#ciri` → kitab → jujur → `#soalan` → statistik → `#kemas-kini` → `#muat-turun` → `#hubungi`
- [x] i18n: semua `data-i18n` ada dalam TRANS; JS `node --check` lulus
- [x] 3 `href="#"` tinggal — sengaja (logo brand ×2, nav "Utama" → ke atas)

### Pending
- [ ] Nav link ke 3 section baharu (tunggu arahan)
- [ ] Biodata Penerbit — kandungan/isi (baru teks sahaja)
- [ ] Verifikasi live selepas deploy Cloudflare (favicon + badge SVG + modal)
