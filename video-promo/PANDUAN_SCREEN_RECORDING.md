# Panduan Screen Recording — Video Promosi PustakaHadith

## Persediaan Awal

### 1. Tetapkan Resolusi Skrin
```
Settings → System → Display → Scale and layout
Resolution: 1920 x 1080
Scale: 100% (jangan 125% atau 150%)
```

### 2. Tetapkan Aplikasi
- Buka PustakaHadith via `JALANKAN.bat`
- Maximize window (tapi jangan fullscreen supaya taskbar still nampak)
- Pastikan tema Aqua Glass aktif
- Pastikan data hadis lengkap

### 3. Bersihkan Desktop
- Tutup semua folder/explorer
- Tutup semua browser tab
- Matikan notifikasi:
  - Settings → System → Notifications → Matikan
  - Atauaktikan Focus Assist (Windows 10/11)

### 4. Sembunyikan Taskbar
```
Settings → Personalization → Taskbar
Automatically hide the taskbar in desktop mode → ON
```

---

## Alat Rakaman

### Pilihan 1: OBS Studio (Percuma — Disyorkan)
1. Muat turun dari https://obsproject.com
2. Setup:
   - Sources → + → Display Capture
   - Settings → Video → Base Resolution: 1920x1080, Output: 1920x1080
   - Settings → Output → Recording Format: MP4, Encoder: x264
   - Settings → Audio → Sample Rate: 44.1kHz
3. Tekan **Start Recording** sebelum mulakan

### Pilihan 2: ShareX (Percuma)
1. Muat turun dari https://getsharex.com
2. Klik kanan icon → Screen Recording → MPEG-4
3. Pilih kawasan skrin penuh
4. Tekan Shift + Print Screen untuk mulakan

### Pilihan 3: Windows Built-in
1. Tekan **Win + G** untuk buka Xbox Game Bar
2. Klik butang Record atau tekan **Win + Alt + R**
3. Nota: Had 30 saat sahaja — tidak disyorkan untuk video ini

---

## Cara Rakam Setiap Scene

### Scene 3 — Buka Aplikasi (0:10 – 0:18)

**Langkah:**
1. Mulakan rakaman skrin
2. Klik `JALANKAN.bat` (dari Explorer, bukan dari video editor)
3. Tunggu splash screen muncul (2-3 saat)
4. Home page terpapar — biarkan 4-5 saat
5. Hentikan rakaman

**Tips:**
- Jangan gerakkan tetikus semasa splash screen
- Biarkan apl load sepenuhnya
- Pastikan cursor tidak di tengah skrin

---

### Scene 4 — Rak 9 Kitab (0:18 – 0:25)

**Langkah:**
1. Mulakan rakaman
2. Klik butang "Jelajah 9 Kitab" di halaman utama
3. Tunggu paparan rak buku muncul
4. Gerakkan tetikus perlahan ke atas kitab pertama (Bukhari) — hover 1 saat
5. Gerakkan ke kitab kedua (Muslim) — hover 1 saat
6. Gerakkan ke kitab ketiga (Tirmizi) — hover 1 saat
7. Biarkan 2-3 saat lagi
8. Hentikan rakaman

**Tips:**
- Gerakkan tetikus secara diagonal atau melengkung (bukan garis lurus)
- Hover cukup 1 saat — jangan terlalu lama
- Jangan klik mana-mana kitab

---

### Scene 5 — Carian AI (0:25 – 0:33)

**Langkah:**
1. Mulakan rakaman
2. Klik medan carian di halaman utama
3. Taip "shalat" dengan perlahan (penonton perlu nampak taipan)
4. Tekan Enter
5. Tunggu hasil carian muncul (1-2 saat)
6. Pastikan draf AI kelihatan di atas hasil carian
7. Biarkan 3-4 saat
8. Hentikan rakaman

**Tips:**
- Taip dengan kelajuan semula jadi (jangan terlalu laju)
- Pilih kata kunci yang popular: "shalat", "sedekah", "doa", "sabar"
- Pastikan draf AI panel kelihatan jelas

---

### Scene 6 — Detail Hadis (0:33 – 0:40)

**Langkah:**
1. Mulakan rakaman
2. Klik salah satu hadis dari hasil carian
3. Tunggu paparan detail muncul
4. Tunggu 1-2 saat supaya penonton nampak teks Arab
5. Skrol perlahan ke bawah (gunakan wheel mouse, 3-4 putaran)
6. Nampak bahagian darjat dan syarah
7. Biarkan 2-3 saat
8. Hentikan rakaman

**Tips:**
- Skrol perlahan — jangan laju
- Henti skrol apabila sampai bahagian darjat
- Pastikan teks Arab dan terjemahan kelihatan selari

---

### Scene 8 — CTA (0:45 – 0:52)

**Langkah:**
1. Mulakan rakaman
2. Pergi ke halaman utama atau bahagian yang menunjukkan pilihan muat turun
3. Jika tiada halaman muat turun dalam apl, gunakan:
   - Laman web `pustakahadith.netlify.app` (buka dalam browser)
   - ATAU paparan "Tentang" yang mungkin ada pautan muat turun
4. Biarkan 3-4 saat
5. Hentikan rakaman

**Alternatif:**
- Jika apl tidak mempunyai halaman muat turun, skip scene ini
- Guna screenshot dari landing page sebagai ganti

---

## Selepas Rakaman

### Semak Kualiti
- [ ] Buka setiap fail rakaman
- [ ] Pastikan resolusi 1920x1080
- [ ] Pastikan tiada notifikasi/ikon yang muncul
- [ ] Pastikan cursor tidak mengganggu (boleh hide cursor dalam editor)
- [ ] Pastikan setiap scene cukup lama (3-5 saat)

### Fail yang Dihasilkan
| Scene | Nama Cadangan | Durasi |
|-------|---------------|--------|
| 3 | `scene_03_home.mp4` | 8s |
| 4 | `scene_04_rak.mp4` | 7s |
| 5 | `scene_05_carian.mp4` | 8s |
| 6 | `scene_06_detail.mp4` | 7s |
| 8 | `scene_08_cta.mp4` | 7s |

### Import ke Video Editor
1. Buat projek baru: 1920x1080, 30fps
2. Import semua fail video
3. Import fail audio voiceover
4. Import fail muzik latar
5. Ikut storyboard untuk susun scene
6. Tambah teks overlay mengikut storyboard
7. Tambah sari kata dari fail SRT
8. Eksport mengikut spesifikasi dalam SEMAK_PRODUKSI.md
