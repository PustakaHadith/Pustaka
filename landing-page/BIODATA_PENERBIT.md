# Biodata Penerbit — PustakaHadith

<img src="img/penerbit.jpg" alt="Muhamad Khairullah Abd Wahab" width="300">

**Muhamad Khairullah Abd Wahab**
PUSTAKA HADITH · Selangor, Malaysia
<https://www.pustakahadith.my> ·
<muhd.khairullah@pustakahadith.my

> *"Percaya pada Allah, percaya pada diri sendiri, dan jangan berhenti."*

---

## Ringkasan

Lahir di Singapura pada 1969, membesar dan belajar di Malaysia. Lebih **37 tahun** berpengalaman dan berkecimpung dalam kejuruteraan, teknologi dan pengurusan projek :
bermula sebagai jurutera kejuruteraan pengeluaran di **Canon Opto Malaysia**(1989), jurutera pembangunan RnD **Reverse Sensor** syarikat pembekal **Proton**, menjadi pakar **SCADA dan instrumen** bagi loji rawatan air, pernah memimpin beberapa syarikat sebagai Pengarah Urusan dan Pengarah Kumpulan, **COO** sebuah syarikat perisian (2013). Pernah terlibat dengan Syarikat Perisian Keselamatan 'Antivirus' **1 Machine** yang mengeluarkan perisian 'Antivirus' Malaysia Pertama **PERISAI**.

Setelah mengharungi jatuh bangun dalam hidup kini menghabiskan masa di atas katil pesakit setelah dikurniakan ujian. Ketika banyak mencari dan membaca teks Hadis maka timbullah idea untuk menerbit secara **Percuma** — **PustakaHadith**: perpustakaan digital **62,169 hadis** daripada
**9 kitab** (Kutub al-Tis'ah), teks Arab penuh, terjemahan **4 bahasa**,
darjat ulama, huraian ringkas dan carian makna AI — **semuanya berjalan
tanpa internet**.

---

## Sejarah Pembikinan PustakaHadith

PustakaHadith bermula sebagai projek peribadi pada **30 Ogos 2026** dan
sampai ke **versi 1.0.3 di Microsoft Store** pada awal **Oktober 2026** —
kurang daripada enam minggu dari kod pertama kepada edaran awam.

Dibina dengan **Python + PyQt5** untuk antara muka desktop Windows, dengan
data disimpan setempat dalam **SQLite + FTS5** (indeks teks penuh) dan
indeks vektor **FAISS + e5-small** untuk carian makna. Ringkasnya:

| | |
|---|---|
| **62,169 hadis** | 9 kitab Kutub al-Tis'ah, teks Arab + terjemahan BM/Indonesia/Inggeris |
| **63,930 rekod darjat** | Sahih / Hasan / Da'if mengikut penilaian ulama |
| **31,322 pembahagian bab** | navigasi tema |
| **4,237 huraian** | daripada SemakHadis.com (dengan atribusi) |
| **2 lapis carian** | kata kunci (FTS5) **dan** maksud (AI) berjalan serentak |
| **0 kebergantungan internet** | selepas pemasangan, semuanya berjalan luar talian |

Kualiti tidak diserahkan kepada nasib: setiap edaran melalui **381 semakan
automatik** dalam `semak.py` (15 bahagian) — kiraan hadis, konsistensi
peta data, ujian susun atur skrin, ujian regresi visual, hinggalah semakan
bahasa supaya dokumentasi kekal dalam Bahasa Melayu Malaysia.

---

*Muka surat ini disusun daripada profil LinkedIn penerbit dan sejarah
pembangunan repo `PustakaHadith/PustakaHadith` (SESI.md, README.md).*
