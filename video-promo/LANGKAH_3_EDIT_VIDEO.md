# Langkah 3: Edit Video — Arahan Lengkap

## Alat Editing

### Pilihan A: Wondershare Filmora (DIGUNAKAN ✅)
1. Buka Filmora → projek baru
2. Set: 1080x1920 (vertikal) ATAU 1920x1080 (horizontal)
3. Frame rate: 30fps

### Pilihan B: CapCut (PERCUMA — Alternatif untuk Shorts)
1. Muat turun: https://www.capcut.com atau Microsoft Store
2. Buka CapCut → projek baru
3. Set: 1080x1920 (vertikal) ATAU 1920x1080 (horizontal)
4. Frame rate: 30fps

### Pilihan B: DaVinci Resolve (PERCUMA — Profesional)
1. Muat turun: https://www.blackmagicdesign.com/products/davinciresolve
2. Lebih kompleks tapi lebih kawalan

### Pilihan C: Adobe Premiere (BERBAYAR)
Jika ada, guna — paling popular

### Pilihan D: Clipchamp (TERBINA DALAM Windows 11)
1. Buka Start → taip "Clipchamp"
2. Buka → Create new video
3. Percuma dengan had eksport 1080p

---

## Susun Atur Timeline

### Struktur Timeline
```
Track 1 (Video):  [Scene 3] [Scene 4] [Scene 5] [Scene 6] [Scene 7] [Scene 8] [Scene 9]
Track 2 (Text):   [Teks 3]  [Teks 4]  [Teks 5]  [Teks 6]  [Teks 7]  [Teks 8]  [Teks 9]
Track 3 (Audio):  [Voiceover penuh ─────────────────────────────────────────────────────]
Track 4 (Music):  [Muzik latar ─────────────────────────────────────────────────────────]
Track 5 (SRT):    [Sari kata ──────────────────────────────────────────────────────────]
```

### Timing Setiap Scene

| Scene | Mula | Tamat | Durasi | Video Source |
|-------|------|-------|--------|--------------|
| 1 (Hook) | 0:00 | 0:05 | 5s | Globe background + teks |
| 2 (Logo) | 0:05 | 0:10 | 5s | Logo fade in |
| 3 (Home) | 0:10 | 0:18 | 8s | `scene_03_home.mp4` |
| 4 (Rak) | 0:18 | 0:25 | 7s | `scene_04_rak.mp4` |
| 5 (Carian) | 0:25 | 0:33 | 8s | `scene_05_carian.mp4` |
| 6 (Detail) | 0:33 | 0:40 | 7s | `scene_06_detail.mp4` |
| 7 (Offline) | 0:40 | 0:45 | 5s | Teks animasi |
| 8 (CTA) | 0:45 | 0:52 | 7s | `scene_08_cta.mp4` |
| 9 (Tutup) | 0:52 | 0:58 | 6s | Logo + tagline |

---

## Langkah demi Langkah (CapCut)

### 1. Import Fail
1. Klik **Import** atau drag fail ke media pool
2. Import semua: footage video, voiceover, muzik latar

### 2. Susun Video
1. Drag `scene_03_home.mp4` ke timeline, mula di 0:10
2. Drag `scene_04_rak.mp4` selepas scene 3 (0:18)
3. Drag `scene_05_carian.mp4` selepas scene 4 (0:25)
4. Drag `scene_06_detail.mp4` selepas scene 5 (0:33)
5. Drag `scene_08_cta.mp4` selepas scene 7 (0:45)

### 3. Tambah Scene 1 & 2 (Hook & Logo)
**Scene 1 (Hook):**
1. Klik **Text** → **Add text**
2. Taip: "Pernah tak anda cari hadis..."
3. Font: Segoe UI Bold, 48px, putih
4. Posisi: tengah skrin
5. Kesan: **Typewriter** atau **Fade In**
6. Durasi: 5 saat

**Scene 2 (Logo):**
1. Import `logo.png`
2. Drag ke timeline di 0:05
3. Kesan: **Zoom In** dari kecil ke besar
4. Tambah teks "PustakaHadith" di bawah logo
5. Font: Segoe UI Extra Bold, 56px, teal `#3EC9B0`

### 4. Tambah Teks Overlay
Untuk setiap scene, tambah teks overlay:

| Scene | Teks | Font | Saiz | Warna | Kesan |
|-------|------|------|------|-------|-------|
| 3 | "62,169 Hadis · 9 Kitab" | Segoe UI Bold | 36px | Putih | Slide kanan |
| 4 | "9 Kitab Kutub al-Tis'ah" | Segoe UI Bold | 32px | Teal | Fade in |
| 5 | "🔍 Carian Makna AI" | Segoe UI Bold | 32px | Teal | Slide kiri |
| 6 | "4 Bahasa · Darjat · Syarah" | Segoe UI Bold | 32px | Putih | Fade in |
| 7 | "Offline · Percuma" | Segoe UI Bold | 40px | Teal | Besar tengah |
| 8 | "⬇ Muat Turun Percuma" | Segoe UI Bold | 36px | Putih | Bounce |
| 9 | Logo + tagline | Segoe UI Extra Bold | 48px | Teal | Fade in |

### 5. Tambah Audio
1. Drag `voiceover_pustakahadith.mp3` ke timeline
2. Padankan dengan video (voiceover mula di 0:00)
3. Import muzik latar → drag ke track berasingan
4. Laras volume muzik: -15dB hingga -20dB

### 6. Tambah Transition
- Scene 1 → 2: Crossfade (0.5s)
- Scene 2 → 3: Slide left (0.3s)
- Scene 3 → 4: Cut (tiada transition)
- Scene 4 → 5: Cut
- Scene 5 → 6: Cut
- Scene 6 → 7: Fade to black (0.3s)
- Scene 7 → 8: Slide up (0.3s)
- Scene 8 → 9: Crossfade (0.5s)

### 7. Tambah Sari Kata
1. Import fail `pustakahadith-promo.srt`
2. Tambah ke timeline sebagai subtitle track
3. Font: Segoe UI, 24px, putih dengan shadow hitam
4. Posisi: 10% dari bawah skrin
5. Pastikan timing sepadan dengan voiceover

---

## Tips Editing

### Presentasi Visual
- Jangan terlalu banyak transition — biarkan video "bernafas"
- Teks overlay jangan tutup bahagian penting skrin
- Gunakan space/ruang negatif dengan bijak

### Timing
- Setiap scene 5-8 saat (cukup untuk difahami)
- Jangan terlalu laju — penonton perlu masa baca
- Jeda 0.5 saat sebelum scene terakhir

### Warna & Branding
- Teks: Putih (#FFFFFF) atau Teal (#3EC9B0)
- Shadow: Hitam 50% opacity
- Background: Gelap (ikuti tema Aqua Glass apl)

---

## Pre-Preview Checklist

Sebelum eksport, semak:
- [ ] Semua video tersusun mengikut timeline
- [ ] Voiceover sepadan dengan visual
- [ ] Muzik tidak terlalu kuat
- [ ] Teks overlay jelas dan tidak bertindih
- [ ] Sari kata timing betul
- [ ] Tiada scene yang terlalu pendek/panjang
- [ ] Transisi smooth
- [ ] Keseluruhan durasi 55-60 saat
