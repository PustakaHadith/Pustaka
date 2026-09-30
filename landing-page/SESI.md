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
- [x] Nav link ke 3 section baharu — pengguna: **"sudah selesai"** (30 Sep). Nota semakan: nav live masih tanpa `href="#mula"`/`"#soalan"` (keputusan ditutup tanpa tambahan link)
- [ ] Biodata Penerbit — kandungan/isi (baru teks sahaja) — **tunggu input pengguna**
- [x] Verifikasi live selepas deploy Cloudflare — **SEMAKAN AUTOMATIK LULUS (30 Sep)**, lihat entri Sesi 36

---

## Sesi 36 (30 September 2026) — Semakan Live Automatik

Semua diperiksa secara automatik dari `https://pustakahadith.my` (tiada perubahan fail):

### Lulus ✅
- **HTTP 200**, 88,237 B, UTF-8 sah
- **3 section baharu wujud**: `#mula`, `#soalan`, `#kemas-kini`
- **Sinkron dgn repo**: kandungan live == `HEAD:landing-page/index.html` — satu-satunya beza ialah **obfuscasi emel Cloudflare** (`/cdn-cgi/l/email-protection`, 4 lokasi) + beacon Cloudflare Insights (injeksi pelayan, normal)
- **Aset semua 200**: `favicon.ico` (14.7 KB) · `apple-touch-icon.png` (10.9 KB) · `img/ms-badge-light.svg` (26.4 KB) · `img/esrb-everyone.svg` (7.0 KB) · `img/bg-globe.webp` (75.1 KB) · `img/logo.png` (34.2 KB) · `manifest.json`
- **Modal Lesen Data** (`licLink` + `lic-*`) ADA · `scroll-padding-top` ADA · latar `bg-globe` ADA
- **i18n**: 173 `data-i18n` unik — **0 hilang** dalam objek TRANS

### Perhatian ⚠️
- **Nav tiada pautan** ke `#mula`/`#soalan` (nav live & tempatan sama) — pengguna kata item ini "sudah selesai"; kemungkinan ditutup tanpa tambahan link
- Semakan visual penuh (render sebenar) tetap perlu pelayar — bahagian ini hanya kandungan/aset/HTTP

## Sesi 37 (30 September 2026) — Changelog landing → v1.0.3

**FINAL ✅** — commit `92768bb` (`index.html`, +19/−19) → push `8b4e7cc..92768bb`
→ Cloudflare auto-deploy → disemak live (10/10 lulus).

### Perubahan
- `#kemas-kini`: tajuk → **"Yang Baharu dalam v1.0.3"**; kad baharu **v1.0.3 · 30 September 2026 · LIVE**
  4 item: (1) saiz tetingkap 1280×720 + maximize 85% · (2) carian kemas — kolum putih + hero baharu
  · (3) kongsi "Info penuh" papar pustakahadith.my · (4) Makluman permulaan ON/OFF + tarikh Hijri
- `cl-more` → "Keluaran lepas: **v1.0.2 (22 Sep)** · v1.0.1 (12 Sep) · v1.0.0 (2 Sep)" (kad v1.0.2 turun ke senarai lepas)
- i18n **ms + en** dikemas kini: `cl-title`, `cl-date`, `cl1`–`cl4`, `cl-more`, `dl-note`
- Butang Setup & 7z → `releases/download/**v1.0.3**/...` (aset Release v1.0.3 sudah live)
- `dl-note` → **Versi 1.0.3**
- **Kad Store (`dl1-p`) KEKAL v1.0.2** — Store masih serve v1.0.2; tukar hanya selepas upload
  MSIX 1.0.3.0 ke Partner Center (tiada claim palsu)

### Semakan automatik (live pustakahadith.my)
- HTTP 200 · tajuk/vnum/tarikh v1.0.3 ADA · kedua-dua butang → URL v1.0.3 ADA ·
  `dl-note` 1.0.3 ADA · TRANS `cl-title`/`cl-more` ms ADA · kad Store v1.0.2 kekal ADA ·
  item changelog lama hilang
- Sintaks: script JS utama `node --check` OK (script1 = JSON-LD, bukan JS) · 173 `data-i18n` — 0 hilang
- Sisa `v1.0.2` dlm fail = **dikehendaki** (cl-more + kad Store sahaja)

### Pending
- Cadangan link nav → `#mula`/`#soalan` (pengguna kata sudah selesai; link tiada — tunggu keputusan)
- Biodata Penerbit — tunggu input teks
- Kad Store → v1.0.3 selepas muat naik MSIX di Partner Center
