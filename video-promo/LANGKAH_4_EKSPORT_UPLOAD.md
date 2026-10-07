# Langkah 4: Eksport & Upload — Arahan Lengkap

## Eksport Video

### Eksport dari CapCut
1. Klik **Export** di bahagian atas
2. Tetapan:
   - **Resolution:** 1080p
   - **Frame rate:** 30fps
   - **Format:** MP4
   - **Quality:** High
3. Klik **Export**
4. Fail disimpan di: `D:\Pustaka Quran Hadis\Pustaka\video-promo\`

### Eksport dari DaVinci Resolve
1. Klik **Deliver** (rocket icon)
2. Tetapan:
   - **Format:** MP4
   - **Codec:** H.264
   - **Resolution:** 1920x1080 ATAU 1080x1920
   - **Frame rate:** 30fps
   - **Bitrate:** 8-10 Mbps
3. Klik **Add to Render Queue** → **Render**

### Eksport dari Adobe Premiere
1. Klik **File → Export → Media**
2. Tetapan:
   - **Format:** H.264
   - **Preset:** Match Source - High bitrate
   - **Resolution:** 1920x1080
3. Klik **Export**

---

## Enam Versi: Tiga Bahasa, Dua Orientasi

Setiap bahasa ada versi **horizontal** (YouTube standard) dan **vertical**
(YouTube Short / Reels / TikTok). Pilih bahasa mengikut fail metadata masing-masing.

| Bahasa | Horizontal | Vertical | Metadata |
|---|---|---|---|
| Melayu | `videos\brag-voice5.mp4` | `videos\brag-voice5-vertical.mp4` | `METADATA-UPLOAD-YOUTUBE.md` |
| Inggeris | `videos\brag-voice6-en.mp4` | `videos\brag-voice6-en-vertical.mp4` | `METADATA-UPLOAD-YOUTUBE-EN.md` |
| Indonesia | `videos\brag-voice7-id.mp4` | `videos\brag-voice7-id-vertical.mp4` | `METADATA-UPLOAD-YOUTUBE-ID.md` |

- **Horizontal:** 1920 x 1080 (16:9), ~57-58.5s
- **Vertical:** 1080 x 1920 (9:16), ~57-58.5s

**Nota:** Metadata penuh (tajuk, penerangan, tag, tetapan) ada di fail metadata
sesuai bahasa. Fail yang disebut sebagai `PustakaHadith_promo_youtube.mp4` /
`PustakaHadith_promo_shorts.mp4` dalam versi lama dokumen ini tidak pernah wujud.

**Penting:** jangan gunakan metadata Melayu untuk video Inggeris atau Indonesia.
Tajuk, penerangan dan tag mesti dalam bahasa yang sama dengan narasi.

---

## Upload ke YouTube

> Metadata penuh untuk kedua-dua versi (standard + Shorts) ada di `METADATA-UPLOAD-YOUTUBE.md`. Gunakan fail itu sebagai sumber kebenaran.

### 1. Log Masuk YouTube
1. Buka https://youtube.com
2. Log masuk akaun Google anda
3. Klik ikon **Create** (bulat +) di bahagian atas
4. Klik **Upload video**

### 2. Pilih Fail
1. Klik **Select files** atau drag fail video
2. Pilih fail video ikut bahasa:

| Bahasa | Standard (horizontal) | Shorts (vertical) |
|---|---|---|
| Melayu | `videos\brag-voice5.mp4` | `videos\brag-voice5-vertical.mp4` |
| Inggeris | `videos\brag-voice6-en.mp4` | `videos\brag-voice6-en-vertical.mp4` |
| Indonesia | `videos\brag-voice7-id.mp4` | `videos\brag-voice7-id-vertical.mp4` |

### 3. Isi Detail

Buka fail metadata yang sepadan dengan bahasa fail video:

| Bahasa | Fail metadata |
|---|---|
| Melayu | `METADATA-UPLOAD-YOUTUBE.md` |
| Inggeris | `METADATA-UPLOAD-YOUTUBE-EN.md` |
| Indonesia | `METADATA-UPLOAD-YOUTUBE-ID.md` |

Fail metadata itu mengandungi tajuk, penerangan, tag, poster, dan tetapan
siap pakai untuk kedua-dua orientasi. Salin terus — jangan terjemah semula
atas akun sendiri.

Contoh untuk Bahasa Indonesia:

**Tajuk:**
```
PustakaHadith — 62.169 Hadis dari 9 Kitab Utama | Gratis & Offline
```

**Penerangan:**
```
PustakaHadith — perpustakaan hadis digital untuk Windows.

62.169 hadis dari 9 kitab utama (Kutub al-Tis'ah)
4 bahasa: Arab, Melayu, Indonesia, Inggris
Pencarian makna AI — ketik maksud, bukan sekadar kata kunci
Derajat ulama dan syarah ringkas
Berjalan sepenuhnya tanpa internet
Gratis dan open source

Microsoft Store: https://apps.microsoft.com/detail/9MWLXVH2ZC7Q
GitHub: https://github.com/PustakaHadith/PustakaHadith
Situs proyek: https://pustakahadith.netlify.app

#PustakaHadith #Hadis #KutubAlTisah #Ulama #IslamicTech #OpenSource
```

**Thumbnail:**
- Versi standard: poster 1920x1080 mengikut bahasa, contoh `videos\posters\brag-voice7-id.jpg`
- Versi Shorts: **tidak boleh tetapkan** — thumbnail mesti 16:9, jadi poster 1080x1920 tidak sesuai. YouTube pilih bingkai sendiri.
- `screenshots\01_home.png` yang disebut dalam versi lama dokumen ini tidak wujud.

**Kategori:** Education

**Nota nombor:** guna `62.169` (titik) untuk Bahasa Indonesia, `62,169` (koma)
untuk Melayu dan Inggeris. Ini konvensyen penomboran setiap bahasa.

### 4. Tetapan Tambahan
- **Playlist:** PustakaHadith (atau buat baru)
- **Audience:** "Not made for kids"
- **Comments:** On
- **License:** Standard YouTube License

### 5. Publish
1. Klik **Publish**
2. Tunggu processing selesai (2-5 minit)
3. Video akan live di: `https://youtube.com/watch?v=XXXXX`

---

## Upload ke TikTok

### 1. Buka TikTok
1. Buka https://tiktok.com atau app TikTok
2. Log masuk akaun anda

### 2. Upload
1. Klik **+** → **Upload**
2. Pilih fail video (versi vertikal 1080x1920)
3. Tunggu upload

### 3. Isi Detail
**Caption:**
```
PustakaHadith — 62,169 hadis dari 9 kitab utama. Percuma & offline! 🔍📚

#PustakaHadith #Hadis #KutubAlTisah #IlmuAgama #IslamicTech #fyp #foryou
```

### 4. Post
1. Klik **Post**

---

## Upload ke Instagram Reels

### 1. Buka Instagram
1. Buka app Instagram
2. Klik **+** → **Reel**

### 2. Upload
1. Klik icon galeri → pilih video
2. Tunggu process

### 3. Isi Detail
**Caption:**
```
PustakaHadith — 62,169 hadis dari 9 kitab utama. Percuma & offline! 🔍📚

Muat turun: pustakahadith.netlify.app

#PustakaHadith #Hadis #KutubAlTisah #IlmuAgama #Reels
```

### 4. Share
1. Klik **Share**

---

## Upload ke Facebook Reels

### 1. Buka Facebook
1. Buka facebook.com atau app
2. Klik **Reels** → **Create Reel**

### 2. Upload
1. Pilih video dari galeri

### 3. Isi Detail
**Caption:**
```
PustakaHadith — perpustakaan digital hadis untuk Windows. 62,169 hadis, 9 kitab, carian AI, semua offline. Percuma!

🔗 pustakahadith.netlify.app
```

### 4. Share
1. Klik **Share Now**

---

## Senarai Semak Akhir

### Sebelum Publish
- [ ] Fail metadata sepadan dengan bahasa narasi
- [ ] Video berkualiti baik (tiada pixelated/blur)
- [ ] Audio jelas, muzik tidak terlalu kuat
- [ ] Semua teks overlay terbaca
- [ ] Sari kata timing betul
- [ ] Duration 55-60 saat
- [ ] Link dalam description berfungsi
- [ ] Thumbnail menarik

### Selepas Publish
- [ ] Semak video live dan boleh ditonton
- [ ] Semak link dalam description berfungsi
- [ ] Kongsi ke social media lain
- [ ] Reply komen pertama dengan link download
- [ ] Semak analytics selepas 24 jam
