# UI/UX PustakaHadith — Indeks Perbincangan

**Folder khusus:** `UIUX_PustakaHadith/`
**Fokus:** pembangunan halaman utama dan pengalaman pengguna
**Status:** mockup + kod produksi - dikemas kini 1 November 2026 (Sesi 48; audit asal Sesi 32, 22 Sep)

---

## Status Pelaksanaan (22 September 2026)

**Kod vs Mockup:** 30 daripada 35 keputusan UI/UX telah dilaksanakan.
**13 ciri kod tidak terdokumentasi** dalam folder ini sebelum ini — kini direkodkan di bawah.

### Ciri yang telah dibina

| Ciri | Fail Kod | Nota |
|---|---|---|
| Split Command Center | `pages_home.py` | Dua panel kiri 62% / kanan 38% |
| Rak Digital Interaktif | `pages_rak.py` | 546 baris, JilidRak custom-painted |
| Panel glass alpha 20/255 | `theme.py` | Tanpa blur, border-radius 14px |
| Background globe (2 imej) | `widgets.py` | timeline (home) + dunia (detail) |
| Header Pustaka/Hadith | `app_qt.py` | Bold 800 / Light 300 |
| Gear icon Tetapan | `app_qt.py` | Slide-in panel, bukan full page |
| Bilingual carian | `pages_carian.py` | terjemahan kiri, Arab kanan |
| Bilingual senarai | `pages_kitab.py` | Sama pattern `hadith_card_dwibahasa` |
| Pilihan Hari Ini | `pages_home.py` | Panel kanan bawah |
| 5 tema (AQUA default) | `theme.py` | DARK, NEUTRAL, LIGHT_NEUTRAL, LIGHT, AQUA |
| Scroll-to-top | Semua halaman | Floating button |
| Keyboard nav Rak | `pages_rak.py` | Arrow keys + Enter |
| Sambung Pembacaan | `pages_home.py` | Hadis terakhir dibaca |
| Loading states carian | `pages_carian.py` | Indikator jam berputar (12 muka + QTimer) + laluan gagal melengkapkan paparan - dikunci gate 8l `semak.py` |
| 5 tema terang/gelap | `theme.py` | AQUA lalai, NEUTRAL, DARK, LIGHT_NEUTRAL, LIGHT - semua tier teks AA 4.5:1 (gate 13, 150 pasangan) |
| Responsif 900x560 | `app_qt.py` | `setMinimumSize(900, 560)` + auto-klamp + panel melimpah (`pages_detail.py:353`) + `tests/uji_responsif_viewport.py` (6 halaman x 4 saiz, DPI 150%) |
| Buka mod max (85%) | `main.py` | Arahan 24 Nov 2026 (Sesi 52): `_toggle_maksimum()` sebelum `show()` - apl buka terus 85% `availableGeometry`, restore-down balik 1280x720; tiada flash saiz lama |

> **Dikemas kini 1 November 2026 (Sesi 48):** tiga baris berikut
> (Loading states, Tema terang/gelap, Responsif 900x560) sebelum ini
> tersenarai dalam "belum dibina" akibat audit 22 Sep yang lebih awal
> daripada kerja sebenar. Semakan semula mendapati ketiga-tiganya sudah
> siap dalam kod + ujian - kini dipindahkan ke atas.

### Ciri yang belum dibina

| Ciri | Nota |
|---|---|
| Spesifikasi komponen PyQt5 | Dokumen teknikal belum ditulis |
| Drawer Jelajah 9 Kitab | Belum dilaksanakan (rak + halaman penuh ada) |

(Ketiga-tiga baris lain telah dipindahkan ke "Ciri yang telah dibina"
selepas semakan semula 1 November 2026 - lihat nota di atas.)

---

## Keputusan Semasa

```text
Nama/banner     : PustakaHadith
Layout asas     : Layout 1 — Split Command Center + Aqua Glass
Halaman utama   : v9 — opasiti panel dipadankan dengan halaman 9 kitab
Paparan 9 kitab : Rak Digital Interaktif (bukan grid kad 3×3)
Senarai hadis   : Gaya lama dwibahasa — terjemahan kiri, Arab kanan
Halaman detail  : Layout asal dikekalkan; hanya visual Aqua Glass diubah
Pencarian       : Hasil gabungan kata kunci + makna AI, gaya dwibahasa
Tetapan         : Layout asal dikekalkan; gear sebagai halaman aktif
Header          : Rawak dibuang; ikon gear untuk Tetapan
Jalan pantas    : Jelajah 9 Kitab · Carian Makna · Sambung
Panel glass     : alpha sebenar 20/255, tanpa blur
```

Halaman utama tidak lagi menggunakan pola hadis.my:

```text
hero tengah → petikan → carian → grid 9 kad
```

---

## Fail Utama

### Dokumen perbincangan lengkap

```text
CADANGAN_TAJUK_UTAMA.md
```

Mengandungi:

- lima cadangan tajuk dan petikan hadis;
- lima konsep layout halaman utama;
- perbandingan kesegaran, kemudahan dan kerumitan;
- tiga pilihan paparan sembilan kitab untuk Layout 1;
- cadangan gabungan A + C;
- pemetaan kepada `ui/pages_home.py` dan komponen PyQt5;
- checklist sebelum produksi.

### Versi mudah dibuka

```text
CADANGAN_TAJUK_UTAMA_LENGKAP.html
```

Semua imej ditanam dalam fail HTML. Gunakan fail ini jika pembaca Markdown
gagal memuatkan imej relatif.

---

## Tangkap Layar Lima Konsep

```text
00_ringkasan_5_konsep.png
01_split_command_center.png
02_library_shelf.png
03_guided_journey.png
04_search_first_minimal.png
05_knowledge_map.png
```

### Ringkasan konsep

| Konsep | Fokus | Status cadangan |
|---|---|---|
| Split Command Center | Carian + ruang peribadi | **Pilihan utama** |
| Library Shelf | Identiti pustaka/rak buku | Elemen sekunder/Jelajah Kitab |
| Guided Journey | Tiga tindakan pengguna | Digabung ke jalan pantas |
| Search-First Minimal | Fokus carian | Alternatif beta ringkas |
| Knowledge Map | Eksplorasi visual | Roadmap/eksperimen |

---

## Tangkap Layar Paparan 9 Kitab

```text
00_perbandingan_3_opsyen_kitab.png
01A_rak_kitab_selepas_scroll.png
01B_tab_9_kitab_panel_kanan.png
01C_drawer_jelajah_kitab.png
```

### Keputusan paparan kitab terkini

Eksperimen A/B/C di atas dikekalkan sebagai rekod awal. Reka bentuk yang kini
diluluskan untuk halaman penuh ialah:

```text
Rak Digital Interaktif
├── semua 9 kitab sebagai jilid pada satu rak berterusan
├── klik jilid → panel pratonton kitab di sebelah kiri
├── Buka kitab → halaman senarai hadis
└── tiada grid kad 3×3 seperti halaman lama
```

Fail dipilih:

```text
selected/selected_page_9_kitab_1366x768.png
```

---

## Latar Globe dan Jaringan Digital

```text
LATAR_GLOBE_NETWORK.md
LATAR_GLOBE_NETWORK_LENGKAP.html
LATAR_GLOBE_5_LATAR_ASAL.png
LATAR_GLOBE_5_MOCKUP_UI.png
latar_globe/
```

Dokumen ini menggantikan bulatan abstrak dengan globe internet, nod rangkaian,
garis masa ilmu dan tema globalisasi. Pilihan pengguna ialah:

```text
bg_04_timeline_network.png — Garis Masa Ilmu Global
```

Paparan 9 kitab menggunakan latar yang sama:

```text
latar_globe/kitab_9/
├── 04A_rak_9_kitab_timeline.png
├── 04B_tab_9_kitab_timeline.png
├── 04C_drawer_9_kitab_timeline.png
└── 04D_halaman_penuh_9_kitab_timeline.png
```

## Halaman 3 — Senarai Hadis

Reka bentuk yang dipilih mengekalkan corak bacaan dwibahasa sedia ada:

```text
Terjemahan ringkas di kiri  |  Petikan bahasa Arab RTL di kanan
```

Komponen utama:

- kitab semasa dan pilihan bab di panel kiri;
- senarai hadis dwibahasa di panel kanan;
- carian dalam kitab;
- tindakan simpan dan `Baca penuh`;
- opasiti panel yang sama dengan halaman utama dan Rak Digital 9 Kitab.

Fail dipilih:

```text
selected/selected_page_senarai_hadis_1366x768.png
```

## Halaman Detail Hadis

Susun atur produksi sedia ada dikekalkan tanpa perubahan struktur. Mockup
hanya menukar latar, panel glass, garisan, sempadan dan warna tema.

Fail dipilih:

```text
selected/selected_page_detail_1366x768.png
```

## Halaman Pencarian

Struktur carian sedia ada dikekalkan dengan hasil gabungan kata kunci dan
makna AI. Hasil dipaparkan dalam gaya dwibahasa yang konsisten.

Fail dipilih:

```text
selected/selected_page_pencarian_1366x768.png
```

## Halaman Tetapan

Susun atur `pages_tetapan.py` dikekalkan. Perubahan terhad kepada latar,
opasiti Aqua Glass, garisan, sempadan dan warna kawalan.

Fail dipilih:

```text
selected/selected_page_tetapan_1366x768.png
```

## Sumber Mockup

Folder berikut menyimpan PNG asal dan SVG sumber:

```text
mockup_halaman_utama/
```

Subfolder:

```text
mockup_halaman_utama/layout1_kitab/
```

---

## Batas Folder Ini

Folder ini hanya untuk:

- reka bentuk halaman utama;
- aliran pengguna;
- mockup visual;
- tema/responsif;
- aksesibiliti;
- spesifikasi komponen UI.

Jangan campurkan:

```text
installer/MSIX
lesen data
Ahmad/Darimi
MyHadith JAKIM
migrasi DB
skrip audit backend
```

Perkara tersebut kekal dalam folder dokumentasi projek yang lain.

---

## Responsif Layout 1

```text
RESPONSIVE_LAYOUT_1.md
RESPONSIVE_LAYOUT_1_LENGKAP.html
responsive/
```

Mockup telah disediakan untuk:

```text
Halaman Utama : 1366×768 dan 900×560
Drawer 9 Kitab: 1366×768 dan 900×560
Halaman Kitab : 1366×768 dan 900×560
```

## Langkah UI/UX Seterusnya

1. Reka keadaan UI:
   - loading;
   - DB kosong;
   - tiada sejarah bacaan;
   - model AI belum tersedia;
   - offline;
   - ralat API.
2. Kunci tema terang dan gelap.
3. Tulis spesifikasi komponen PyQt5.
4. Bina prototaip terasing sebelum mengubah `ui/pages_home.py` produksi.
5. **Implementasi Drawer Jelajah 9 Kitab** (Pilihan A+C dari CADANGAN_TAJUK_UTAMA.md).
6. **Responsif compact mode** — breakpoint 900×560 dengan layout menegak.

---

## Pautan ke Development

Folder ini mesti dikemas kini bersama repo utama setiap kali:
- Komponen UI berubah (layout, tema, warna, saiz)
- Halaman baru ditambah
- Breakpoint responsif ditukar
- Latar belakang atau panel style diubah

Rujuk: `SESI.md` (repo utama) — blok "PENTING — Folder Projek Utama" untuk senarai folder lengkap.
