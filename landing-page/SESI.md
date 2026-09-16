# SESI PEMBANGUNAN — Landing Page PustakaHadith

## Tarikh
31 Ogos – 2 September 2026

## Matlamat
Bina landing page untuk promosi **PustakaHadith** v1.0 dan kongsi di Facebook.
Domain: `pustakahadith.site.je`

---

## Sesi 11 (2 September): Landing Page Dwibahasa Melayu/Inggeris

### Fail diubah
- `index.html` — ditulis semula dengan sistem dwibahasa satu halaman
- `D:\Pustaka Quran Hadis\Pustaka\PustakaHadith\docs\superpowers\specs\2026-09-02-landing-dwibahasa-design.md` — spec reka bentuk (diluluskan pengguna)

### Perubahan
1. **Toggle satu halaman (pendekatan 1)** — semua teks diberi atribut `data-i18n`/`data-i18n-ph`/`data-i18n-alt`; objek `TRANS` mengandungi ~90 kunci dalam `ms` dan `en`.
2. **Butang MS | EN** dalam navbar (`lang-switch`/`lang-btn`); bahasa aktif ditanda.
3. **Bahasa lalai automatik** — `bacaLang()`: `localStorage.ph-lang` jika ada, jika tidak `navigator.language` (mulai "en" → EN, lain-lain → MS).
4. **Pilihan diingati** — pilihan manual disimpan dalam `localStorage`, kekal merentas lawatan.
5. **Nama Latin kitab kekal** (tidak diterjemah); atribusi hadis.my kekal.
6. **Meta dinamik** — `title`, `description`, `og:title`, `og:description`, `og:locale`, `twitter:*` bertukar mengikut bahasa.

### Status
- ✅ Ditulis & di-deploy ke FTP — saiz server **61,138 B = HASH SEPADAN** dengan tempatan
- ✅ **Semakan mudah alih (render sebenar Chromium, emulasi 320–1366 px, 6 lebar)**: tiada limpahan mendatar; menu burger `<980px`, susun atur turun ke 1 kolum; titik putus 980 px & 600 px disahkan berfungsi
- 🔧 **2 pembetulan semasa semakan**:
  1. `.hubungi-grid` pada `≤600px` → `minmax(0,1fr)` (sebelum ini `1fr` memaksa page melebar ke 345 px pada telefon 320 px)
  2. `@media(max-width:600px)` hilang `}` penutup semasa edit → menelan block 980 px; `}` dikembalikan (keseimbangan 176/176 disahkan)
- ✅ Deploy semula ke FTP — **61,248 B = HASH SEPADAN**
- ⚠️ Pemeriksaan visual dwibahasa masih perlu (anti-bot JS) — buka `pustakahadith.site.je` dalam pelayar, cuba MS/EN + muat semula

---

## Sesi 12 (3 September): Migrasi ke Netlify + Redirect site.je

### Perubahan
1. **Berpindah dari hosting FTP profreehost (`pustakahadith.site.je`) ke Netlify**:
   - Landing page dwibahasa penuh (dengan imej) kini live di **`https://pustakahadith.netlify.app`** (HTTP 200 semua aset: `index.html`, 6 webp, cover kitab, `app-home.png`, favicon).
   - Deploy ZIP via API menggunakan **`tar.exe -a -c -f`** (bukan `Compress-Archive`) supaya path guna **forward slash** `img/` (backslash → imej 404); header `Content-Type: application/zip`; `POST .../sites/{id}/deploys`; deploy `6a9949c23ab1c51f2f6c9a81` state `ready`.

2. **Custom domain `pustakahadith.site.je`** dikunci milik profreehost — tidak boleh diimport ke Netlify. Pengguna pilih **'Kekal profreehost, redirect'**.

3. **Redirect `pustakahadith.site.je` → Netlify** (dua lapis, disahkan bertukar oleh pengguna dalam pelayar):
   - `index.php` — **301 header redirect** ke Netlify.
   - `index.html` (ganti landing page lama di server) — **meta-refresh (0s) + JS `window.location.replace()`**.
   - Nota: `.htaccess` **tidak dibaca** profreehost (AllowOverride tak dilaksanakan) — sebab itu guna PHP + HTML redirect.

### Cabaran
- **Anti-bot profreehost** — challenge JS halang semakan automatik; mesti semakan pelayar manusia.
- **Server mengekod semula imej webp/png** — dimensi sama, fail sah, saiz berbeza; `index.html` hash sepadan.
- **Netlify Credit-based** — site baharu private by default (tukar Public di dashboard); site terhenti bila kredit habis.

### Status
- ✅ Landing page penuh live di `pustakahadith.netlify.app`
- ✅ Redirect `site.je` → Netlify berfungsi (disahkan pengguna)
- ✅ Auto-deploy Git dihentikan (`stop_builds=True`); site lama `lovely-kitten-9baf06` dipadam
- ✅ **Site ditukar ke Public** (user, dashboard Netlify) — disahkan HTTP 200 landing page 61,968 B utk pelawat luar

### Keputusan muktamad domain (4 September)
- **`pustakahadith.site.je` tidak lagi digunakan** — TLD `.je` tidak disokong Netlify (endpoint POST domains → 404) dan anti-bot profreehost menyekat akses walaupun dlm pelayar.
- **URL rasmi landing page: `https://pustakahadith.netlify.app`** (live, Public, lengkap). Custom domain masa depan = beli sendiri (`.com`/`.my`/`.net`) yg disokong Netlify.
- Fail redirect profreehost dibiarkan (tidak bernilai; tidak memudaratkan).

### Pembaikan 404 (4 September)
- **Gejala**: `/` jadi 404 (sebelum ini 200). **Punca**: auto-deploy Git aktif balik (`stop_builds=false` selepas site ditukar Public), deploy repo `2d7b0c0` (tiada index.html) → 404.
- **Nota**: deploy ZIP baharu hari ini (`6a9ab1fa`) = 404 (gubahan tar berbeza drp Sesi 12); `6a9949c2` (Sesi 12) masih bagus. Sahkan deploy ZIP via preview URL sebelum current.
- **Pembaikan**: restore `6a9949c2` sbg current (HTTP 200) + `PATCH /sites/{id}` `stop_builds=true` (kekal). Notifikasi Netlify "Builds now stopped" diterima.
- ✅ Landing page live semula; auto-deploy dihentikan (manual sahaja).

---

## Sesi 13 (5 September): Pengecilan MSIX — Slim MSIX 814.8 MB

- Pakej Store dikecilkan: `PustakaHadith-v1.0.0-slim.msix` = **814.8 MB** (dari 1,093.7 MB, jimat ~279 MB / ~25.5%).
- Sebab: `.cache_models` (941 MB) = duplikat `blobs` (470 MB) + `snapshots` (470 MB); app muat model via snapshots → `blobs` selamat dibuang (diuji luar talian, berjaya).
- Kandungan disahkan: `model.safetensors` (448.8 MB) dalam `snapshots`, **tiada `blobs`**; hadis.db + hadis_faiss.index + exe utuh.
- Bonus: berasaskan dist 2 Sept → MSIX baharu ada fix `closeEvent` (MSIX Store lama 1 Sep tiada).
- **GitHub Release v1.0.0 (5 Sep)**: `PustakaHadith-v1.0.0-slim.msix` (814.8 MB) menggantikan MSIX lama (1,093.7 MB); 7z + Setup EXE kekal (dist tidak berubah). Kad muat turun landing (pautan GitHub Release) kekal sah.
- Rujukan penuh: `..\PustakaHadith\SESI.md` (Sesi 13).

---

## Sesi 5 (2 September): Peremajaan Landing Page

### Fail diubah
- `index.html` — favicon, lazy loading, WebP, menu mudah alih
- `img/` — 7 cover kitab baharu + 6 imej WebP
- `favicon.ico`, `apple-touch-icon.png` — baharu

### Perubahan
1. **Cover 7 kitab dijana** (gaya roman/ro, kaca aqua, aksen unik per kitab):
   `abudaud-ro.png`, `tirmizi-ro.png`, `nasai-ro.png`, `iibn-majah-ro.png`, `ahmad-ro.png`, `darimi-ro.png`, `malik-ro.png` — setiap satu tajuk Arab + nama imam.

2. **Favicon** — `favicon.ico` (16–256px) + `apple-touch-icon.png` (180px) daripada logo; `<link rel="icon">` ditambah ke `<head>`.

3. **Lazy loading** — 14 imej bawah lipatan (`loading="lazy"`): 9 cover rak + 5 tangkap layar. Logo & mockup utama kekal eager (LCP).

4. **Optimasi imej → WebP** (q80, method 6): 6 imej 1366/1376×768 dikurangkan **~92%**:
   - `app-home.png` 1.30 MB → 89.7 KB
   - `app-9kitab.png` 1.24 MB → 82.6 KB
   - `app-senarai.png` 1.37 MB → 94.5 KB
   - `app-carian.png` 1.33 MB → 87.0 KB
   - `app-detail.png` 1.35 MB → 92.6 KB
   - `bg-globe.png` 1.92 MB → 73.3 KB
   - Rujukan HTML dikemas kini ke `.webp`; `og:image`/`twitter:image` kekal PNG (keserasian media sosial).

5. **Menu mudah alih diperkukuh** — dropdown absolute dengan `.open`, auto-tutup bila link diklik atau klik luar, animasi hamburger, `aria-expanded`, reset pada `resize`.

### Keadaan Landing Page
- 11 seksyen, rak 9/9 kitab bergambar, ~8 MB imej → ~0.5 MB

### Status
- ✅ 9/9 kitab ada cover
- ✅ Favicon & apple-touch-icon
- ✅ Lazy loading
- ✅ Imej WebP (~92% kecil)
- ✅ Menu mudah alih mantap
- ⚠️ Pemeriksaan visual masih perlu (anti-bot JS) — buka `pustakahadith.site.je` dalam pelayar

---

## Sesi 4 (2 September): Pautan Muat Turun Sebenar

### Fail diubah
- `index.html` — kad Setup EXE & Portable kini aktif dengan pautan GitHub Release

### Perubahan
1. **GitHub Release v1.0.0 dilengkapkan** (akaun `PustakaHadith/PustakaHadith`, token PAT user):
   - `PustakaHadith-Setup-1.0.0-x64.exe` (806.6 MB) — Inno Setup terkini (hadis.db 55 fix + FAISS)
   - `PustakaHadith-portable-1.0.0-x64.7z` (802.1 MB) — 7z dari dist lengkap (2.18 GB)
   - `PustakaHadith-v1.0.0.msix` (1093.7 MB) — sedia ada
   - Penerangan release dikemas kini (Setup EXE bukan lagi "coming soon")

2. **Landing page dikemas kini**:
   - Kad **Setup EXE**: badge SEGERA → SIAP · Windows 10/11, butang aktif "Muat Turun EXE"
   - Kad **Portable ZIP** → **Portable 7z**: badge SEGERA → SIAP, butang aktif "Muat Turun 7z"
   - Nota muat turun: "~1.4 GB" → "0.8–1.1 GB"

3. **FTP deploy berjaya** — `index.html` di-upload ke `htdocs/` (37,732 bytes, saiz server sepadan).

### Status
- ✅ Semua 3 muat turun aktif di GitHub Release v1.0.0
- ✅ Landing page live dengan pautan sebenar
- ⚠️ Anti-bot JS menghalang pemeriksaan kandungan automatik — sahkan dengan pelayar
- ⏳ Tiada favicon
- ⏳ 7/9 kitab tiada gambar cover

---

## Sesi 3 (1 September): Update Muat Turun & FTP Deploy

### Fail diubah
- `index.html` — update seksyen muat turun & navbar

### Perubahan
1. **Navbar ditambah** — "Utama" & "Hubungi" ditambah pada menu atas
   - Susunan baru: Utama | Tangkap Layar | Ciri Utama | 9 Kitab | Muat Turun | Hubungi | [Muat Turun]
   
2. **Seksyen muat turun dikemas kini** — 3 kad baru:
   - **Microsoft Store (MSIX)** — link ke GitHub Release v1.0.0
   - **GitHub Release** — link ke release page
   - **Setup EXE / Portable** — SEGERA (belum sedia)

3. **Rujukan GitHub dikemas kini** — `opencodemk/PustakaHadith` → `PustakaHadith/PustakaHadith`

4. **FTP deploy berjaya** — upload ke `ftpupload.net/htdocs/`
   - `index.html` — landing page utama
   - `img/` — 9 gambar (screenshots, logo, bg-globe, book covers)

### Keadaan Landing Page
- 11 seksyen: Navbar, Hero, Tangkap Layar (tab), Ciri Utama, 9 Kitab, Disklaimer, Statistik, Muat Turun, Hubungi, Footer
- Reka bentuk gelap teal + glassmorphism, responsif
- Hosting: FTP ke `pustakahadith.site.je`
- Semua gambar sudah diupload

### Status
- ✅ Navbar ditambah (Utama & Hubungi)
- ✅ Seksyen muat turun dikemas kini (MSIX + GitHub Release)
- ✅ Rujukan GitHub dikemas kini
- ✅ FTP deploy berjaya
- ⏳ Tiada favicon lagi
- ⏳ 7/9 kitab tiada gambar cover

---

## Sesi 2 (31 Ogos): Tambah Page Hubungi

### Fail diubah
- `index.html` — tambah seksi Hubungi (CSS + HTML + navbar + footer)

### Perubahan
- Seksi baru **`#hubungi`** sebelum footer, mengandungi:
  - **Maklumat Hubungi** (kiri): emel (pustakahadith@outlook.com), GitHub, sumber terbuka + butang "E-mel Kami" (`mailto:`)
  - **Borang Hubungi** (kanan): Nama, Tajuk, Mesej → hantar via `mailto:` (tiada backend)
- Pautan "Hubungi" ditambah ke navbar & footer

### Keadaan Landing Page
- 11 seksyen sekarang (bertambah Hubungi)

---

## Sesi 1 (31 Ogos): Landing Page & Promosi Facebook

### Fail diubah
- `index.html` — tambah Open Graph + Twitter Card meta tags
- `FACEBOOK_POST.md` — panduan langkah demi langkah post Facebook

### Perubahan
1. **Open Graph + Twitter Card meta tags** — ditambah ke `<head>` dalam `index.html`:
   - `og:title`, `og:description`, `og:image`, `og:url`, `og:type`, `og:locale`, `og:site_name`
   - `twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`
   - URL: `https://pustakahadith.site.je`
   - Gambar: `img/app-home.png`

2. **Post Facebook** — teks promosi lengkap:
   - Hook menarik di baris pertama
   - 6 ciri utama dengan emoji ✅
   - CTA: muat turun dari laman
   - 6 hashtag relevan

3. **Panduan posting** — `FACEBOOK_POST.md`:
   - Langkah 1: Muat naik gambar
   - Langkah 2: Tulis post (copy & paste)
   - Langkah 3: Post
   - Langkah 4: Kongsi ke group Facebook

### Keadaan Landing Page
- Satu fail HTML (`index.html`) — semua CSS/JS inline
- 10 seksyen: Navbar, Hero, Tangkap Layar (tab), Ciri Utama, 9 Kitab, Disklaimer, Statistik, Muat Turun, Footer
- Reka bentuk gelap teal + glassmorphism, responsif
- Hosting: FTP ke `pustakahadith.site.je`

### Isu Yang Dikenal pasti
- ~~Pautan muat turun masih `href="#"` — perlu update dengan URL sebenar~~ ✅ 1 September
- Tiada favicon
- 7/9 kitab tiada gambar cover
- Gambar berat (~8 MB) — tiada lazy loading
- Mobile menu rapuh

### TODO
1. ~~Deploy `index.html` baru ke `pustakahadith.site.je` via FTP~~ ✅ 1 September
2. ~~Pautan muat turun — update dengan URL sebenar~~ ✅ 1 September
3. Tambah favicon
4. Tambah gambar cover untuk 7 kitab lagi
5. Optimize gambar (lazy loading, compress)

## Fail Utama
| Fail | Fungsi |
|---|---|
| `index.html` | Landing page utama (Open Graph tags + seksi Hubungi) |
| `FACEBOOK_POST.md` | Panduan post Facebook |
| `SESI.md` | Fail ini |
| `img/` | Screenshot & gambar laman |

## Rujukan Sesi Lain
- `D:\Pustaka Quran Hadis\PustakaHadith\SESI.md` — sesi pembangunan apl utama

---

## Sesi 15 (11 September): Kemas kini kad Muat Turun → Microsoft Store + v1.0.1

### Perubahan (`index.html`)
1. Kad dl1 "Microsoft Store (MSIX)": pautan MSIX lama (GitHub Release v1.0.0) diganti dengan **Microsoft Store** — `https://apps.microsoft.com/store/detail/9MWLXVH2ZC7Q?cid=DevShareMWAPCS`, `target="_blank"`, label butang → `Buka Microsoft Store`.
2. Teks kad & nota: `Pakej MSIX penuh (1.1 GB)` → **`Pakej MSIX v1.0.1 (814.8 MB)`**; nota bawah `Versi 1.0` → `Versi 1.0.1`.
3. Objek `TRANS` dikemas serentak untuk `dl1-p`, `dl1-btn`, `dl-note` — ms **dan** en.
4. Kad dl2 (Setup EXE) & dl3 (Portable 7z) **tidak diubah** — masih paut GitHub Release v1.0.0 (binaan v1.0.1 belum wujud).

### Deploy
- Netlify CLI 27.5.2 (PST PAT) → deploy `--dir landing-page --site 4af95b07-c40d-4005-855b-2fd0ce95745e`.
- Draft `6aa41542` disahkan: `9MWLXVH2ZC7Q`, `v1.0.1`, `Buka Microsoft Store` semua OK.
- `--prod` → **live `https://pustakahadith.my`** (disahkan 3 item OK).
- Auto-deploy Git masih dihentikan; deploy manual sahaja.

### Status
- ✅ Landing page live, kad Store + v1.0.1 aktif.
- ⏸ Jika EXE/7z v1.0.1 dibina kemudian, kad dl2/dl3 perlu dikemas + redeploy.

---

## Sesi 16 (12 September): Pautan dl2/dl3 → v1.0.1 + Emel Baharu + Deploy

### Perubahan (`index.html`)
1. **dl2 (Setup EXE)** — pautan `https://github.com/PustakaHadith/PustakaHadith/releases/download/v1.0.0/PustakaHadith-Setup-1.0.0-x64.exe` → **v1.0.1/PustakaHadith-Setup-1.0.1-x64.exe** (EXE v1.0.1 kini wujud, dibina 12 Sep).
2. **dl3 (Portable 7z)** — pautan `.../v1.0.0/PustakaHadith-portable-1.0.0-x64.7z` → **v1.0.1/PustakaHadith-portable-1.0.1-x64.7z**.
3. **Emel** `pustakahadith@outlook.com` → **`info2@pustakahadith.my`** (5 tempat: maklumat hubungi line 518, butang "E-mel Kami" `mailto:`, borang `mailto:` line 532, footer copyright + TRANS foot-copy ms/en line 722).
4. Kad dl1 (Microsoft Store/MSIX), teks kad, dl-note — **tidak berubah** (masih v1.0.1, 814.8 MB, 0.8–1.1 GB).

### Deploy
- Netlify CLI `deploy --prod --dir landing-page --site 4af95b07-c40d-4005-855b-2fd0ce95745e --auth nfp_...` (token PAT user baharu) → **deploy `6aa534cfc5c59aa20fdc1dbd`** live.
- **Disahkan**: HTTP 200; `info2@pustakahadith.my` ada, `outlook` tiada; dl2 & dl3 → v1.0.1. (1 fail di-upload — hanya index.html berubah.)
- Auto-deploy Git masih dihentikan; deploy manual sahaja.

### Status
- ✅ Landing page `https://pustakahadith.my` dikemas (pautan muat turun EXE/7z v1.0.1 + emel baharu) & disahkan live.
- Nota: sesi berkaitan binaan EXE/7z v1.0.1 & GitHub Release — rujuk `..\PustakaHadith\SESI.md` Sesi 17–18.

---

## Sesi 21 (14 September): Kemas Kini Kad Store + Deploy Diblok oleh Kredit Netlify

### Objektif
- Kemas kini kad dl1/Store di landing page supaya papar "v1.0.1 disahkan &amp; live" (ms+en) baharu selepas pensijilan Store Sesi 20.
- Deploy semula pustakahadith.my dengan kandungan baharu.

### Perubahan (fail tempatan — **BELUM live**)
- landing-page\index.html — kad Store dl1-p dikemas: teks "✅ v1.0.1 disahkan &amp; live di Microsoft Store" (ms: 484 / en: 483) + kamus i18n dl1-p (ms & en) dikemas.
- Emel info2@pustakahadith.my & pautan dl2/dl3 v1.0.1 — sudah ada dari Sesi 18 (tidak berubah).

### Semakan & Deploy
- Token API Netlify disahkan sah sepanjang sesi: GET /sites/{id} = **HTTP 200**, PATCH stop_builds = **HTTP 200**, restore deploy = **HTTP 200**.
- CLI 
etlify.cmd deploy --prod melapor **Forbidden/Unauthorized**.
- Punca sebenar dikenal pasti via API POST:
  {"error":"Account credit usage exceeded - new deploys are blocked until credits are added"} — **HTTP 403**.
- **Kesimpulan: akaun Netlify pustakahadith (pelan Free) kehabisan kredit deploy; deploy baharu disekat sehingga kredit ditambah.**

### Status
- Landing page https://pustakahadith.my — **live HTTP 200** (deploy lama v1.0.1 masih berfungsi: emel info2@, pautan v1.0.1 ada; kad Store masih teks lama).
- Kemas kini kad Store **gagal live** kerana blok kredit Netlify.
- Item tertunda: deploy kad Store baharu "v1.0.1 disahkan &amp; live" (perlu setelah kredit Netlify dipulihkan).

### Fail berkaitan
- landing-page\index.html — kad dl1-p (ms:484 / en:483) & kamus i18n dl1-p dikemas (tempatan, belum live).
- SESI.md — rekod ini (Sesi 21).
---

## Sesi 22 (14 September): PENGEṢAHAN AKHIR — Kad Store v1.0.1 SUDAH LIVE di Landing Page

### Penemuan penting (pengesahan bersilang LIVE vs tempatan)
Semakan langsung terhadap https://pustakahadith.my (HTTP **200**) disahkan mengandungi:

| Item | LIVE | Tempatan |
|---|---|---|
| Kad Store dl1-p "✅ v1.0.1 disahkan &amp; live di Microsoft Store" | ✅ TRUE | ✅ TRUE |
| Emel info2@pustakahadith.my (dl2/dl3 & hubungi) | ✅ TRUE | ✅ TRUE |
| Pautan muat turun EXE v1.0.1 & 7z v1.0.1 | ✅ TRUE | ✅ TRUE |
| Kad "../dl1/Store" tidak lagi teks lama "Pasang dari Microsoft Store" | ✅ (tiada teks lama) | ✅ (tiada teks lama) |

**Kesimpulan:** deploy **SEBENARNYA BERJAYA** — deploy 6aa75d78 (created 2026-09-14T02:35:36, state **ready/published**, url pustakahadith.my) sudah pun memuat kad Store baharu. Rekod Sesi 21 yang menyebut "kad Store belum live / deploy diblok kredit" adalah **tidak tepat** (ia merujuk percubaan CLI/API tempoh blok kredit, namun deploy akhir yang effective telah dibuat). Ralat rekod ini kini dibetulkan.

### Fail berkaitan
- landing-page\index.html — kad dl1-p (tl 484 / en 483) + kamus i18n dl1-p — **kedua-dua LIVE & tempatan SAMA** (tiada pengecampuran).
- SESI.md — rekod ini (Sesi 22) & pembetulan Sesi 21.
- Item tertunda: **TIADA** — semua itens Sesi 1–21 tertutup.

---

## Sesi 22 (14 September): PEMBETULAN REKOD — Kad Store v1.0.1 SUDAH LIVE 🌐✅

### Penemuan muktamad (bukti langsung dari LIVE)
Semakan curl https://pustakahadith.my (HTTP **200**) menunjukkan:

| Pemeriksaan | LIVE | Tempatan | Status |
|---|---|---|---|
| Kad Store dl1-p "✅ v1.0.1 disahkan &amp; live" | **TRUE** | TRUE | ✅ SAMA |
| Emel info2@pustakahadith.my (kad & halaman) | TRUE | TRUE | ✅ SAMA |
| Pautan muat turun EXE 1.0.1 & 7z 1.0.1 | TRUE | TRUE | ✅ SAMA |
| Kad Store dl2/dl3 (EXE+7z) v1.0.1 | TRUE | TRUE | ✅ SAMA |

### Pembetulan rekod Sesi 21
- ❌ Sesi 21 merekod: "kad Store **belum live**; deploy diblok kredit Netlify (HTTP 403)."
- ✅ **Kebenaran sebenar:** deploy 6aa75d78 (created 2026-09-14, state eady/current) **telah pun diterbitkan** dan mengandungi teks kad Store baharu — landing page live **SUDAH dikemas**. HTTP 200.
- Punca kekeliruan: ujian POST /deploys tambahan (zip upload) pula diblok oleh kekangan kredit akaun Free (403 credit usage exceeded) — ia **bukan** penghalang kepada kad Store yang sudah live, cuma ujian yang berasingan. Mana-mana deploy baharu yang mahu dibuat selepas ini perlu menunggu kredit, tetapi **tujuan landings Sesi 21 (kad Store v1.0.1 disahkan &amp; live) sudah tercapai sepenuhnya.**

### Kesimpulan
- ✅ Landing page https://pustakahadith.my — **live, kad Store "v1.0.1 disahkan &amp; live"**, emel info2@, pautan v1.0.1 (EXE + 7z).
- ✅ **Tiada item tertunda** untuk landing page.
- ⚠️ Satu nota: akaun Netlify Free kekurangan kredit (403) untuk **deploy tambahan/had deploys** — elok dimaklumkan bila kredit dipulihkan, tetapi tidak menghalang kad Store yang telah live.

### Fail berkaitan
- landing-page\index.html — kad dl1-p (ms:484 / en:483) + kamus i18n — sudah live.
- SESI.md — rekod ini (Sesi 22) pada kedua-dua landasan (utama & landing-page).
---

## Sesi 23 — DEPLOY KE CLOUDFLARE PAGES BERJAYA (mulai guna OAuth)

**Latar:** Netlify Free kehabisan kredit → deploy baharu disekat (403 kredit). Keputusan: migrasi landing ke **Cloudflare Pages** (percuma penuh, tiada had kredit).

**Apa dibuat (turn ini):**
1. **Wrangler 4.132** dipasang; **wrangler login (OAuth)** berjaya — log masuk sebagai emel pustakahadith@gmail.com, Account ID 35c6dc9…bd39 (Pustakahadith@gmail.com's Account).
2. **Projek Pages dicipta:** nama pustakahadith-landing — subdomain auto pustakahadith-landing.pages.dev, branch produksi main.
3. **Deploy 30 fail landing** (index.html 60,932 B) → URL produksi:
   https://pustakahadith-landing.pages.dev
4. **Pengesahan HTTP 200** di kedua-dua URL (produksi + alias deploy):
   - Kad Store **"✅ v1.0.1 disahkan &amp; live"** ✅ (dl1-p, pautan v1.0.1)
   - Emel **info2@pustakahadith.my** ✅
   - Judul "PustakaHadith - Perpustakaan Digital Hadis | 62,169 Hadis & 9 Kitab" ✅

**Nota Domain:** Zon pustakahadith.my **BELUM wujud di Cloudflare** (0 zon) — untuk paut domain ke CF perlu tambah zon + tukar nameserver di pendaftar .my. Sehingga itu:
- pustakahadith.my → kekal di **Netlify** (live & stabil)
- pustakahadith-landing.pages.dev → **Cloudflare Pages** (sandaran percuma, tiada had kredit)

**Status:** MIGRASI ASAS SELESAI & LIVE di CF Pages. Item tertunda: (pilihan) pautan domain pustakahadith.my ke Cloudflare (jalan 1 — perlu akses dashboard + pendaftar), atau kekal hibrid (jalan 2). Rekod ini TIDAK di-commit/push (menunggu arahan pengguna).

---

## Sesi 24 (16 September): MIGRASI DOMAIN pustakahadith.my → Cloudflare (SELESAI)

### Objektif
Pindahkan `pustakahadith.my` daripada Netlify ke Cloudflare sepenuhnya.

### Langkah
1. **Dashboard Cloudflare baharu (2026)** — pengguna tak jumpa "Add a site" / "Websites" kerana UI baru:
   - Menu sisi: Account home, Recents, **Domains**, Observe, Investigate, Analytics, **Compute**, AI, dll.
   - "Workers & Pages" → kini di bawah **"Compute"** (bukan menu berasingan).
2. **Pages project** — klik `pustakahadith-landing` → tab **"Setup custom domain"** → taip `pustakahadith.my` → **"Continue"** → **"connect domain"**.
3. **Nameserver Cloudflare** diberikan:
   - `cloe.ns.cloudflare.com`
   - `quinton.ns.cloudflare.com`
4. **Pengguna tukar NS di pendaftar .my** — ganti 4 nameserver lama (NSONE) dengan 2 CF nameserver.
5. **DNS propagate** — disahkan via Google DoH:
   - `quinton.ns.cloudflare.com` ✅
   - `cloe.ns.cloudflare.com` ✅

### Pengesahan Akhir
| Semakan | Status |
|---|---|
| HTTPS | ✅ 200 |
| HTTP | ✅ 301 → HTTPS |
| CF-RAY | ✅ aktif (Cloudflare) |
| Kad Store v1.0.1 dl1-p | ✅ |
| 62,169 hadis | ✅ |
| emel info2@ | ✅ |

### Keputusan Muktamad
- **`pustakahadith.my`** → **Cloudflare** (live, penuh)
- **`pustakahadith-landing.pages.dev`** → **Cloudflare Pages** (sandaran)
- **Netlify** → **ditinggalkan** (tiada lagi)
- Tiada item tertunda.

### Nota Teknikal
- OAuth token wrangler (`cfoat_XW`) **tidak boleh** cipta zon (403 `Invalid access token` untuk POST `/zones`).
- Zon `pustakahadith.my` dicipta melalui **Pages → Custom domains** (bukan "Add a site").
- Dashboard Cloudflare 2026: "Add a site" mungkin tiada pada sesetengah akaun; "Domains" hanya papar "Register a domain".
