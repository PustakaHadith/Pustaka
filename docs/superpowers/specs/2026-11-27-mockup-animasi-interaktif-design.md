# Reka Bentuk: Animasi Interaktif — mockup-pro.html

Tarikh: 2026-11-27 · Status: **MENUNGGU KELULUSAN** · Saiz: perubahan kecil

## Niat

Mockup landing page nampak statik. Tambah animasi **tindak balas kursor** supaya halaman
nampak "hidup" — bukan sekadar lebih banyak gerakan latar.

## Matlamat

- Hero ada koreografi masuk semasa load pertama.
- Gerakan ikut kursor: parallax hero, tilt 3D kad, butang magnet.
- Kekal ringan: CSS + vanilla JS sahaja, tiada pustaka luar.

## Bukan matlamat (Approach C ditolak)

- Parallax ikut scroll, kustom kursor, transisi seksyen besar, easing kiraan statistik.
- Alasan: berat, risiko motion sickness, lebih banyak kod & ujian — berlebihan untuk
  permintaan "sedikit".

## Pendekatan dipertimbangkan

| | A Halus | **B Interaktif (DIPILIH)** | C Sinematik |
|---|---|---|---|
| Isi | entrance hero, glow drift, garis aksen tajuk | A + parallax hero, tilt kad, butang magnet | B + parallax scroll |
| Kesan | mungkin masih senyap — halaman sudah ada animasi ambient (bob, reveal, pulse) tapi tetap rasa statik | ketara sebaik kursor bergerak | dramatic |
| Kos | rendah | sederhana | tinggi |

## Skop B

1. **Entrance hero (dari A)** — badge → tajuk → lead → CTA → imej, leret ~80ms, fade + translateY.
2. **Parallax hero** — imej/kad hero ikut kursor (~8–10px), glow bergerak sedikit bertentangan.
3. **Tilt 3D** — kad kitab (`.rak`/`.book`) & kad ciri (`.feat`) miring ikut kursor (had ~8°),
   `perspective` pada induk.
4. **Butang magnet** — butang `.btn-p` tarik ~4–6px ke arah kursor dalam radius, snap-back bila keluar.
5. **Glow drift (dari A)** — `bg-glow` bergerak perlahan (keyframes).

## Kekangan

- Hormat `prefers-reduced-motion` (blok sedia ada ~baris 458) — semua gerakan baharu dimatikan di situ.
- Touch / `pointer:coarse`: matikan tilt, magnet, parallax.
- Hanya animasi `transform`/`opacity`; pointermove di-throttle `requestAnimationFrame`; listener `passive`.
- Jangan rosak yang sedia ada: observer `.rv`, kiraan statistik, i18n (MS/EN), nav, `#toTop`.
- Guna pemboleh ubah gaya sedia ada (`--ease`, `--brand`, `--gold`).

## Pengesahan

- 0 ralat konsol; BM & EN kekal; ujian mod reduced-motion; screenshot hero; lebar mobile 375px.

## Apa yang tinggal untuk pembina

Tiada — semua keputusan sudah dibuat di atas.
