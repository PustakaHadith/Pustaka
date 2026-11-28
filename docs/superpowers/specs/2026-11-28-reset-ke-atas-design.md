# Spesifikasi ringkas: mula pada halaman utama semasa buka/refresh

## Intent / mengapa

Apabila `landing-page/mockup-pro.html` dibuka atau direfresh, pengguna mesti melihat bahagian atas (hero), bukan posisi tatal atau anchor sebelumnya. Punca dispesahkan: URL fragmen (contoh `#muat-turun`, `#z7-dialog`) kekal semasa refresh lalu pelayar melompat ke anchor itu; `history.scrollRestoration` pula `auto`.

## Goals

- Setiap muat halaman bermula di `scrollY === 0`.
- Fragmen URL dibuang semasa muat, supaya URL bersih (`.../mockup-pro.html`).
- Pautan anchor dalam halaman (nav "Muat Turun", dll.) tetap berfungsi seperti biasa **selepas** halaman dimuat.

## Non-goals

- Tidak menukar pilihan bahasa MS/EN yang diingati melalui `localStorage('ph-lang')`.
- Tidak melumpuhkan pautan `#` dalam halaman.
- Tidak menukar animasi, slide, atau popup 7-Zip.

## Constraints

- Vanilla JS sahaja; tiada pustaka luar.
- Kod mesti berada di awal blok `<script>` supaya berjalan sebelum pelayar melakukan anchor scroll/restoration yang boleh dilihat.
- `scroll-behavior:smooth` pada `html` bermakna `scrollTo(0,0)` tanpa `behavior:'instant'` kelihatan animasi — gunakan `behavior:'instant'` untuk reset.
- Commit ter-skop: `landing-page/mockup-pro.html` dan/atau `docs/superpowers/`. Tiada `git add -A`, tiada push tanpa kelulusan.

## Approaches

1. **A — Reset masa muat (dipilih pengguna).** `history.scrollRestoration='manual'`, `history.replaceState(null,'',pathname+search)` apabila hash ada, dan `scrollTo({top:0,behavior:'instant'})`. Pautan anchor kekal berfungsi selepas muat.
2. **B — `scrollTo(0,0)` sahaja.** Hash kekal; pelayar boleh melompat ke anchor semula — ditolak.
3. **C — Lumpuhkan semua pautan anchor.** Memutuskan navigasi sedia ada — ditolak.

## Keputusan pembina (bukan keputusan pengguna)

- Blok reset diletak terus selepas `<script>` pembuka, sebelum inisialisasi nav/i18n.
- `replaceState` hanya dipanggil bila `location.hash` tidak kosong, untuk mengelak sejarah/URL tidak perlu berubah.
- `scrollTo` dipanggil tanpa syarat bagi menampal pemulihan tatal pelayar walaupun URL tidak berfragmen.
- `history.scrollRestoration='manual'` dikunci dengan `"scrollRestoration" in history` untuk pelayar lama.

## Ujian yang akan membuktikan

- RED: dengan hash `#muat-turun`, reload → `scrollY > 0` dan `hash === '#muat-turun'`.
- GREEN: reload → `scrollY === 0`, `hash === ''`, pautan nav ke `#muat-turun` masih membawa ke seksyen itu, popup 7-Zip dan toggle EN/MS tidak regresi, 0 ralat konsol.
