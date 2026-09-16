# Langkah 2: Rakam Voiceover — Arahan Lengkap

## Persediaan Mikrofon

### Semak Mikrofon
1. Klik kanan icon speaker di taskbar → **Sounds**
2. Klik tab **Recording**
3. Pilih mikrofon anda → klik **Properties**
4. Klik tab **Levels** → pastikan 70-80 (bukan 100, supaya tidak clipped)
5. Klik **OK**

### Uji Mikrofon
1. Buka **Audacity** (jika ada) atau **Voice Recorder** (terbina dalam Windows)
2. Rakam 10 saat — baca sesuatu
3. Dengar balik — pastikan jelas, tiada hingar latar

---

## Alat Rakaman Audio

### Pilihan A: Audacity (PERCUMA — Disyorkan)
1. Muat turun: https://www.audacityteam.org
2. Install → buka Audacity
3. Klik butang **Record** (bulat merah)
4. Baca skrip → klik **Stop** (segi empat)
5. Klik **File → Export → Export as MP3**
6. Pilih lokasi: `D:\Pustaka Quran Hadis\Pustaka\video-promo\`

### Pilihan B: Windows Voice Recorder (TERBINA DALAM)
1. Buka Start → taip "Voice Recorder"
2. Klik butang **Record**
3. Baca skrip → klik **Stop**
4. Fail disimpan di: `C:\Users\MKAW\Documents\Sound recordings\`
5. Salin ke folder video-promo

### Pilihan C: Adobe Audition (BERBAYAR)
Jika ada, guna — lebih banyak pilihan noise reduction.

---

## Skrip Voiceover

Baca skrip ini semasa merakam. Ikut timing yang ditetapkan:

```
[0:00 – 0:05]
Pernah tak anda cari hadis tapi tak tahu nak mula dari mana?

[0:05 – 0:10]
Kami bina PustakaHadith — perpustakaan digital hadis untuk Windows.

[0:10 – 0:18]
Enam puluh dua ribu seratus enam puluh sembilan hadis dari sembilan kitab utama — semua dalam satu aplikasi.

[0:18 – 0:25]
Bukhari, Muslim, Abu Daud, Tirmizi — lengkap dengan pembahagian bab.

[0:25 – 0:33]
Taip sahaja maksud yang anda cari — carian kata kunci dan carian makna AI berjalan serentak.

[0:33 – 0:40]
Teks Arab, terjemahan empat bahasa, darjat ulama, dan huraian ringkas — semua dalam satu skrin.

[0:40 – 0:45]
Berfungsi sepenuhnya tanpa internet. Pasang sekali, rujuk selamanya.

[0:45 – 0:52]
Muat turun percuma dari GitHub atau Microsoft Store.

[0:52 – 0:58]
PustakaHadith — enam puluh dua ribu hadis. Sembilan kitab. Percuma.
```

---

## Tips Voiceover

### Gaya Bicara
- **Nada:** Tenang, mesra, seperti menerangkan kepada kawan
- **Kelajuan:** Sederhana (150 patah perkataan/minit)
- **Tekanan:** Tekan angka: "62,169", "9 kitab", "4 bahasa"
- **Jeda:** 0.5 saat antara scene (ambil nafas)

### Sebutan
- "62,169" = "enam puluh dua ribu seratus enam puluh sembilan"
- "FTS5" = "full-text search lima" atau "FTS lima"
- "AI" = "A-I" atau "kecerdasan buatan"
- "FAISS" = "face" (sebutan asal)
- "Kutub al-Tis'ah" = "kutub al-tis-ah"

### Elakkan
- Jangan terlalu laju
- Jangan terlalu kuat (pecah)
- Jangan guna nada jualan/agresif
- Jangan skip angka — sebut semua

---

## Pasca-Rakaman

### Buang Hingar (Noise Reduction) — Jika guna Audacity
1. Pilih bahagian senyap (1-2 saat di awal/akhir)
2. Klik **Effect → Noise Reduction → Get Noise Profile**
3. Pilih keseluruhan rakaman (Ctrl + A)
4. Klik **Effect → Noise Reduction → OK** (default sudah OK)

### Normalisasi Volume
1. Pilih keseluruhan rakaman (Ctrl + A)
2. Klik **Effect → Normalize**
3. Set: Remove DC offset: ☑, Normalize amplitude: -3.0 dB
4. Klik **OK**

### Export
1. Klik **File → Export → Export as MP3**
2. Bitrate: 320 kbps
3. Nama: `voiceover_pustakahadith.mp3`
4. Lokasi: `D:\Pustaka Quran Hadis\Pustaka\video-promo\`

---

## Fail yang Dihasilkan

| Fail | Keterangan |
|------|------------|
| `voiceover_pustakahadith.mp3` | Voiceover penuh (~55 saat) |
| `voiceover_pustakahadith_backup.wav` | Backup kualiti tinggi (pilihan) |
