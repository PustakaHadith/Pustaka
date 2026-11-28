# Spesifikasi ringkas: Pautan 7-Zip + popup di kad Portable ZIP

## Intent / mengapa

Kad "Portable ZIP" di `landing-page/mockup-pro.html` meminta pengguna mengekstrak arkib ±1 GB. "Extract All" bawaan Windows boleh lambat atau gagal pada arkib besar/laluan panjang. Beri pautan ke 7-Zip dan penjelasan ringkas supaya pengguna boleh memilih cara ekstrak yang lebih boleh dipercayai.

## Goals

- Di dalam kad Portable ZIP sahaja, tambah pautan "Muat Turun 7-Zip".
- Klik pautan itu membuka popup penerangan kegunaan 7-Zip — tidak navigasi terus.
- Di dalam popup ada butang ke laman muat turun rasmi 7-Zip.
- Popup boleh ditutup dengan butang ×, Esc, atau klik luar.
- Teks popup tersedia dalam MS (asal) dan EN (melalui `data-i18n` + `I18N.en`).

## Non-goals

- Tidak mengubah kad Microsoft Store atau Setup EXE.
- Tidak menukar pautan muat turun ZIP sedia ada.
- Tidak memasang atau menyediakan fail 7-Zip dalam repo.
- Tidak menambah pustaka luar.

## Constraints

- Vanilla HTML/CSS/JS sahaja, selari dengan halaman ini.
- Mekanisme dwibahasa sedia ada: teks MS ialah kandungan HTML dengan `data-i18n`; `setLang('en')` menggantikan `innerHTML` daripada `I18N.en`.
- `prefers-reduced-motion` sudah dimatikan secara global oleh media query sedia ada — popup tidak perlu animasi khas.
- Commit mesti ter-skop: hanya `landing-page/mockup-pro.html` dan/atau `docs/superpowers/`. Tiada `git add -A`, tiada push tanpa kelulusan.

## Approaches

1. **`<dialog>` asli + `showModal()` (dipilih).** Pelayar mengurus dialog modal, Esc, klik latar, dan pemulihan fokus. Kod minimum, tiada pustaka, aksesibiliti baik.
2. **Overlay `<div>` buatan sendiri.** Perlu focus-trap, pengendalian Esc, dan `aria-modal` manual. Lebih kod dengan tiada kelebihan visual — ditolak.

## Keputusan (call pembina, bukan keputusan pengguna)

- URL sasaran butang popup: `https://www.7-zip.org/download.html` (laman rasmi, stabil). Dipilih berbanding URL `.exe` bernombor versi yang mudah lapuk.
- Butang dalam popup dibuka dengan `target="_blank" rel="noopener"`.
- Pautan dalam kad diletak selepas butang "Muat Turun ZIP", sebagai pautan tekstual kecil.
- Kunci i18n baru berimbuhan `z7-` (contoh `z7-title`, `z7-body`, `z7-step1`, `z7-cta`).

## Isi popup (ayat ringkas)

Tajuk: *Kenapa guna 7-Zip?*

Penerangan: arkib ±1 GB kadang lambat/gagal dengan "Extract All" Windows; 7-Zip percuma dan sumber terbuka, ekstrak lebih laju, mengendalikan laluan panjang, dan boleh terus "Extract to PustakaHadith\".

Langkah: muat turun 7-Zip → klik kanan ZIP → 7-Zip → Extract to → jalankan `PustakaHadith.exe`.

CTA: *Buka muat turun 7-Zip*.

## Yang masih terbuka kepada pembina

- Susunan markup dan nama kelas CSS mengikut gaya sedia ada (`.card`, `.btn`, `var(--*)`).
- Butiran ujian RED→GREEN dan urutan commit ditentukan oleh pelan.
