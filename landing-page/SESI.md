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

## Sesi 38 (30 September 2026) — Store v1.0.3 Live + kad Store landing

**FINAL ✅** — pengesahan pengguna: **MSIX 1.0.3.0 dah publish di Microsoft Store**
(halaman Store JS-rendered, versi takdisenaraikan server-side; terima pengesahan).

- Sebelum publish: MSIX v1.0.3 **diuji pasang+lancar LULUS** (1.0.3.0, exe identik
  SHA256 dgn build 29 Sep) + pembersihan pakej/sijil selepas ujian
- Identiti disahkan sepadan dgn pakej Store v1.0.2 (Name/Publisher/DisplayName;
  versi 1.0.3.0 > 1.0.2.0)
- Landing: kad Store `dl1-p` (ms+en) → **"v1.0.3 disahkan & live"** — commit
  `23b65b1` → push `190869e..23b65b1` → Cloudflare auto-deploy
- Semak live: HTTP 200, `dl1-p` HTML + TRANS = v1.0.3 ADA; sisa v1.0.2 hanya dlm
  baris "Keluaran lepas" (dikehendaki)
- Script JS: `node --check` OK

## Sesi 38b - 2 Okt 2026 (update halaman Muat Turun)
- Kad portable: 7z -> ZIP - pautan baru releases/download/v1.0.3/PustakaHadith-portable-1.0.3-x64.zip (993.5 MB, SHA-256 4AD4B2D2...41D9CB)
- Teks ms+en dikemas kini: dl3-h/dl3-p/dl3-btn, faq5-q/faq5-a, start1-p (HTML + i18n JSON) - sisa rujukan "7z": 0
- Ikon landing (img/logo.png, favicon.ico, apple-touch-icon.png, logo.jpg) -> video-promo/thumbnail/icon.png (commit ab8eeb1)
- Fakta semakan: EXE sudah v1.0.3; landing langsung tiada pautan .zip dalam sejarah git

## Sesi 38c - 2 Okt 2026 (versi pada kad EXE + ZIP)
- Tajuk kad dikemas kini (HTML + i18n ms/en): dl2-h "Setup EXE" -> "Setup EXE - v1.0.3"
  dan dl3-h "Portable ZIP" -> "Portable ZIP - v1.0.3" (tanda tengah guna "�")
- NOTA utk kemas kini akan datang: dl2-h/dl3-h kena ikut versi release baharu
- FFFD: 0 (disemak selepas edit)

## Sesi 38d - 2 Okt 2026 (ikon brand dibesarkan)
- CSS .brand img: 38x38 (radius 9px) -> 46x46 (radius 11px) - logo nav + footer
- Alasan: ikon baharu berbentuk segi empat (1123x1135) nampak lebih kecil pada saiz lama

## Sesi 39 - 5 Okt 2026 (nav kemas + Biodata Penerbit live)

**FINAL ✅** — 4 commit pushed -> Cloudflare auto-deploy:
`ad74858` (pop-up biodata + foto + baiki nav melimpah) -> `35ba319` (pulangkan pautan Utama,
kandungan ikut BIODATA_PENERBIT.md, buang fimos) -> `319c5d7` (buang pautan akula69,
ayat lahir 1969 ms+en) -> `aec1488` (typo PUSTAHA->PUSTAKA, "dalam dalam"->"dalam",
badge hero MS 1 baris)

### Header nav (2 Pending Sesi 37 = SELESAI)
- Pautan `#mula` (Mula Pantas) + `#soalan` (Soalan Lazim) ditambah; link "Utama" dipulangkan
  (i18n `nav-home` ms "Utama" / en "Home"); burger di bawah 1180px
- CSS: `.nav-links` gap 16px, `a` .88rem + white-space:nowrap, `.nav-cta` 8px 16px/.88rem,
  `.lang-switch` margin 0 0 0 4px
- Ukur: ruang dlm .wrap 1104px, kegunaan 1037px (slack 67px) -> nav MS + EN **1 baris** (screenshot 1400x760)

### Biodata Penerbit (Pending Sesi 37 = SELESAI)
- `#bioModal` dibuka dari pautan bio (foto `img/penerbit.jpg`, 768x1024); kandungan ikut
  `BIODATA_PENERBIT.md`: Ringkasan 3 perenggan (lahir Singapura 1969 ms+en, Reverse Sensor/Proton,
  SCADA, COO 2013, PERISAI/1 Machine, katil pesakit, 62,169 hadis/9 kitab) + Sejarah + jadual
  `bio-stats` 6 baris + nota kaki (SESI.md/README.md)
- CSS: `.lic-row.bio-row` (label `b` kekal inline, bukan display:block) + `.bio-stats`
- Pautan kini `pustakahadith.my · muhd.khairullah@pustakahadith.my` (akula69 = 0 hit, fimos = 0)
- Typo: `PUSTAKA HADITH` (3 tempat: static + ms + en) + buang kata ulang "dalam"
- Disahkan: modal terbuka (`lic-modal open`) + teks via DOM dump; screenshot modal MS

### Badge hero `.eyebrow`
- Masalah: teks MS natural 569px > ruang lajur 552px -> wrap 2 baris + titik gantung
- Fix: font .8rem -> .74rem, letter-spacing 2.5 -> 1.7px, padding 14 -> 12px, gap 8 -> 7px,
  text-align:center + media `min-width:981px and max-width:1099px` (.68rem/1.1px)
- Ukur (probe DOM, clone nowrap): 492/552 @1400 · 426/450 @981 · 1-lajur @600-900 -> **1 baris semua**;
  <=420px wrap tetapi rata tengah (tiada titik gantung kiri)
- EN: 396/552 -> 1 baris sebelum & selepas

### Belum / menunggu pengesahan
- Pengesahan visual pengguna: Kongsi FB (salin + tampal) dari app v1.0.3
- Kad Store `dl1-p` kekal v1.0.2 sehingga Store serve v1.0.3

## Sesi 39b - 5 Okt 2026 (pop-up biodata: selesa di HP + kurang scroll di desktop)

**FINAL ✅** — belum commit (tunggu arahan push).

### Punca sebenar di HP: halaman overflow mendatar
- `.foot-grid{1.2fr 2fr}` + `.foot-cols{repeat(3,1fr)}` tak runtuh pd <=980px -> pd vp 390px
  halaman jadi **543px** (24 elemen terlebih kanan; boleh swipe sisi bawah popup)
- Fix @980px: `foot-grid` 1 lajur + `foot-cols` `repeat(3,minmax(0,1fr))`;
  @600px: `foot-cols` 2 lajur -> **docW 543 -> 375, count 0** (360/390/414 semua lulus)

### Pop-up biodata di HP (<=600px)
- Kad ditahan `max-width:376px` (baris ~40 aksara, senang dibaca) + `.lic-modal` padding 18px,
  padding kad 28/26 -> 22/18
- Teks bio `.88rem` -> **`.95rem`** (lh 1.72); foto `132x176` -> `104x139`
- Jadual `bio-stats` **bertindan** (label atas nilai) — dulu kolum pertama 42% terhimpit
- Ukuran kad: 360->309px · 390->339px · 414->363px · 600->376px (overflowX=false semua)

### Desktop (>=760px) — besar & panjang supaya tak payah scroll banyak
- `#bioModal .lic-card`: `max-width` **520 -> 880px**, `max-height` 85 -> 88vh,
  padding 34/36/30
- `#bioModal .lic-rows` jadi **grid 2 lajur** (Ringkasan | Sejarah) — kandungan kolum kanan
  (jadual 6 baris) jadi lebih pendek dari susunan bertindan
- Kesan: `scrollHeight` 1562 -> 1199; skrin **1400x900: scroll perlu 916 -> 407px (-55%)**
- 820px (2 lajur mula) hingga 1400px disemak; pop-up Lesen `#licModal` kekal 520px/1 lajur
