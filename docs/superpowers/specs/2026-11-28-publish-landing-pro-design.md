# Spesifikasi: Publish reka bentuk Pro sebagai landing page utama

- Tarikh: 2026-11-28
- Status: Menunggu kelulusan
- Skop: `landing-page/index.html`, tujuh `landing-page/img/*-ro.png`

## Matlamat

Jadikan reka bentuk dan tingkah laku `landing-page/mockup-pro.html` sebagai `landing-page/index.html` yang hidup di `https://pustakahadith.my`, tanpa kehilangan fungsi yang ada pada halaman live sekarang, kemudian terbit melalui auto-deploy Cloudflare Pages dari `main`.

## Konteks

- `mockup-pro.html` mengandungi kerja yang sudah disiap dan disemak: animasi interaktif, slide gambar, popup 7-Zip, reset ke atas when refresh, dan kover Bukhari/Muslim yang konsisten dengan tujuh kitab lain.
- `index.html` (live) masih reka bentuk lama, tetapi ada tiga fungsi yang mockup tiada:
  1. Modal **Lesen Data & Perisian** (pautan footer `#licLink`, `#licModal`).
  2. Modal **Biodata Penerbit** (pautan footer `#bioLink`, `#bioModal`).
  3. Borang hubungi yang benar-benar membuka `mailto:` dengan nama, subjek dan mesej.
- `index.html` juga mempunyai tujuh baris perubahan belum dikomit (nama imam dan nama penerbit). Nama-nama itu **sudah sepadan** dengan kandungan `mockup-pro.html`, jadi tidak hilang.
- Tujuh PNG `*-ro.png` mempunyai perubahan working-tree belum dikomit. Pengguna meluluskan ia dikomit sekali supaya kesemua sembilan kover konsisten di web.
- Deploy: Cloudflare Pages, branch `main`, output root folder `landing-page/` (rujuk `landing-page/cloudflare.md`). Push ke `origin/main` mencetuskan deploy.

## Pendekatan

Guna `mockup-pro.html` sebagai **asas** untuk `index.html`, kemudian **pindahkan** tiga fungsi di atas dari `index.html` ke dalam asas itu. Jangan ubah `mockup-pro.html` sendiri. Jangan tambah ciri baru.

## Keperluan (boleh diuji)

1. `index.html` adalah reka bentuk mockup: animasi, slide, popup 7-Zip, reset-to-top, dan sembilan kad kitab dengan kover baru semuanya berfungsi.
2. Footer `index.html` memaparkan pautan **Lesen Data** dan **Biodata Penerbit**; kedua-duanya membuka modal masing-masing, boleh ditutup dengan butang `✕`, dan kandungannya sepadan dengan versi live (termasuk biodata `M.K.A.W`).
3. Borang hubungi `index.html` menghantar melalui `mailto:info2@pustakahadith.my` dengan nama, subjek dan mesej yang dikodkan (`encodeURIComponent`); versi EN/MS bagi label borang tersedia melalui mekanisme i18n sedia ada.
4. Terjemahan EN bagi teks modal dan borang ditambah ke `I18N.en` dalam `index.html`; versi MS kekal sebagai kandungan lalai dalam HTML. Tiada `data-i18n` tanpa padanan apabila ditukar ke EN.
5. Tiada ID bertindih, tiada rujukan fail tempatan rosak, dan 0 ralat konsol dalam pelayar untuk MS dan EN.
6. Tujuh `*-ro.png` versi working-tree dikomit bersama `index.html`; `mockup-pro.html`, dokumen SDD, dan fail luar skop lain tidak dikomit dalam commit ini.
7. Commit di-push ke `origin/main`; laman `https://pustakahadith.my` disemak selepas deploy dan memaparkan reka bentuk baru + fungsi yang dipulihkan.

## Bukan skop

- Menyunting kandungan, warna atau susun atur mockup selain pemindahan tiga fungsi di atas.
- Menyentuh `BIODATA_PENERBIT.md`, folder untracked, atau fail app desktop.
- Mencipta GitHub Release atau tag versi baru.

## Risiko & mitigasi

| Risiko | Mitigasi |
|---|---|
| CSS modal dari `index.html` bercampur dengan CSS mockup | Salin hanya blok `.lic-modal`, `.lic-card`, `.lic-x`, `.bio-*` yang diperlukan; semak tiada pertindihan selector yang mengubah reka bentuk mockup. |
| JS lama bercampur dengan JS mockup (`setLang`, `data-i18n`) | Dua mekanisme i18n berbeza: mockup guna `I18N.en` + `location.reload()` untuk MS. Tambah kunci baru ke `I18N.en` sahaja; jangan salin `TRANS` lama. |
| Borang mockup gaya kad | Kekalkan markup kad mockup, tukar hanya `onsubmit` kepada `mailto:` seperti versi live. |
| Auto-deploy tidak berlaku | Semak `git status -sb` selepas push dan `webfetch https://pustakahadith.my`; jika tidak berubah, laporkan dan minta arahan (tiada token Cloudflare penuh disimpan). |

## Pengesahan

- `grep` untuk kehadiran `licModal`, `bioModal`, `mailto:info2@`, `z7-dialog`, `bukh-flat.png`.
- Pelayar: buka/tutup dua modal, hantar borang (semak `mailto:` URL), tukar MS↔EN, refresh (`hash:''`, `scrollY:0`), 0 ralat konsol.
- `git diff --stat` menunjukkan hanya `index.html` + 7 PNG.
- `webfetch https://pustakahadith.my` mengesahkan kandungan baru selepas push.
