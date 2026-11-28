# Spesifikasi ringkas: samakan kover Bukhari & Muslim dengan kad lain

## Intent / mengapa

Dalam seksyen `#kitab` di `landing-page/mockup-pro.html`, dua kad pertama (Sahih Bukhari, Sahih Muslim) nampak ganjil berbanding tujuh kad lain. Punca diukur: `bukh-ro.png` (512×512) dan `muslim-ro.png` (576×576) ialah potongan foto dengan ~35% piksel telus, 55–63 warna (kuantisasi 4-bit), dan tiada bingkai; tujuh imej lain ialah kover templat 512×512, 0% telus, ~19–21 warna (4-bit) / ~439 warna RGB, dengan bingkai dan jalur aksyen yang sama.

## Goals

- Kedua-dua kad menggunakan kover templat yang serasi dengan tujuh kad lain.
- Hanya `mockup-pro.html` yang berubah dari segi rujukan imej; `index.html` kekal guna imej asal.
- Imej asal `bukh-ro.png` / `muslim-ro.png` tidak ditulis semula.

## Non-goals

- Tiada perubahan pada teks kad, jumlah hadis, `data-i18n`, susunan grid, animasi, slide, atau popup 7-Zip.
- Tiada perubahan pada tujuh kover lain atau pada `index.html`.
- Tiada pustaka luar pada halaman; tiada dependency runtime baharu.

## Constraints

- Dua fail PNG baru: `landing-page/img/bukh-flat.png` dan `landing-page/img/muslim-flat.png`.
- Pengguna telah meluluskan kemasukan dua fail PNG ini dalam commit (pilihan A); kekal `git add` secara eksplisit, tiada `git add -A`, tiada push tanpa kelulusan.
- Penjanaan imej dibuat sekali dengan Python/Pillow 12.3.0 + `arabic_reshaper` + `bidi` yang sudah terpasang, dan fon `PustakaHadith/fonts/Amiri-Bold.ttf` yang sudah ada dalam repo. Ini alat binaan sekali, bukan dependency halaman.
- Nota pembina: `features.check('raqm')` adalah `False`, jadi shaping Arab mesti melalui `arabic_reshaper` + `bidi`, bukan `ImageDraw.text` terus.

## Approaches

1. **A — Kover rata baru (dipilih pengguna).** Jana dua PNG berasaskan templat kover sedia ada, dengan jalur aksyen warna baru dan nama kitab dalam Arab yang betul.
2. **B — CSS latar pepejal.** Cepat dan satu fail, tetapi tekstur foto tetap berbeza — ditolak.
3. **C — Kover teks CSS.** Konsisten tetapi hilang seni asal — ditolak.

## Keputusan pembina (bukan keputusan pengguna) — dikaji semula selepas pengukuran

Tujuh kover rata bukan gradien, sebaliknya **templat yang sama persis**:

- 512×512, 0% telus.
- Medan rata `#283e54` ≈68.5% piksel.
- Bingkai gelap `#101c2a` / `#08101a` ≈5.8%.
- Jalur aksyen mendatar atas (y≈30–50) dan bawah (y≈472–481), x≈30–481 dengan hujung tirus, ≈15.5% piksel. Warna aksyen berbeza per kitab: `#b76d1d`, `#297c65`, `#5b4b7e`, `#9d4167`, `#106d60`, `#314c79`, `#725f42`.
- Tanda bucu teal `#78ded0` ≈2.3%.
- Teks Arab berubah pada x≈150–361, y≈188–265 (nama kitab, `#ebf7f3`), dan unsur hiasan tetap pada baris 292–293, 331–353, 391–407 (sama pada ketujuh-tujuh kover).

Maka kaedah janaan: **klon templat** `abudaud-ro.png`, (1) tukar warna jalur aksyen melalui interpolasi pada paksi `#283e54 → aksyen lama` supaya anti-alias tepi kekal kemas, (2) padam kawasan teks berubah dengan `#283e54`, (3) tulis nama baru dengan Amiri-Bold saiz auto-fit ≤220px lebar, dijana melalui `arabic_reshaper` + `bidi`, warna `#ebf7f3`, berpusat pada (256, 227). Unsur hiasan tetap tidak disentuh.

Warna aksyen baru (tidak berulang dengan tujuh sedia ada, dan mengingatkan imej asal):

- Sahih Bukhari — `#5f8f3f` (hijau daun, selari dengan foto asal kehijauan).
- Sahih Muslim — `#8e3b46` (merah gelap, selari dengan foto asal kemerahan).

Teks: `صحيح البخاري` dan `صحيح مسلم`.

## Ujian yang akan membuktikan

- RED: dua imej pertama masih 55–63 warna (4-bit) dan ~35% telus; saiz asli 512 & 576.
- GREEN: kedua-dua imej baru 512×512, 0% telus, medan `#283e54` dominan, jalur aksyen warna baru hadir, bingkai + bucu teal + hiasan tetap sepadan dengan kover rujukan, teks Arab terbaca dengan shaping yang betul (bukan huruf terputus), dimensi render 128×179 sama seperti kad lain, 0 ralat konsol.
- `index.html` dan tujuh kover lain tidak berubah dalam `git diff`; pautan nav, i18n, slide, dan popup 7-Zip tidak regresi.
