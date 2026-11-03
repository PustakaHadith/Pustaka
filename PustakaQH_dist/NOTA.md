# NOTA — PustakaQH_dist = pusat rasmi file distribution Microsoft Store

> **WAJIB (arahan pengguna, 30 Sep 2026):** Folder **`PustakaQH_dist\`**
> ini mesti digunakan untuk pembikinan semua file distribution
> Microsoft Store (MSIX, staging, aset Store). Tiada pembikinan file
> Store di luar folder ini.

## Susunan wajib

| Perkara | Lokasi |
|---|---|
| Output MSIX siap (versi semasa) | `PustakaQH_dist\msix\` — lihat `msix\NOTA.md` |
| Staging build MSIX | `PustakaQH_dist\msix_staging\` (dibina semula setiap build) |
| Build aplikasi (untuk disalin ke staging) | `PustakaQH_dist\PustakaHadith\` |
| Aset Store (screenshot, privasi) | `PustakaQH_dist\` root (screenshot_*.png, privacy_policy.html) |
| Pakej Store rasmi & sejarah | `PustakaQH_dist\msix\` |

## Pembinaan

- Skrip: `PustakaHadith/installer/build_msix.ps1`
  - `$stage` → `PustakaQH_dist\msix_staging` (**wajib ikut folder ini**)
  - `$out` → `PustakaQH_dist\msix` (msix baharu datang automatik)
- Sijil: `PustakaQH_dist\PustakaHadith.pfx` (self-signed, buat msix)

Jangan ubah laluan ini tanpa arahan pengguna.

## Kemas kini & pembersihan (arahan 30 Sep 2026)

**Dibuang (lapuk, boleh dibina semula dari git tag / skrip build):**
- `PustakaHadith_lama_1.0.2\` — pokok build lama (12 Sep)
- `PustakaHadith_sep2026\` — staging MSIX era v1.0.0 (31 Ogo)
- `msix_v101_staging\` — staging MSIX v1.0.1 (diganti `msix_staging\`)

**Dikekalkan (wajib / bukan lapuk):**
- `msix\` (**1 versi semasa** — 1.1.0, selepas pembersihan 21 Okt) · `PustakaHadith\` (build 9 Okt)
- `msix_staging\` — **dipadam 21 Okt**; dicipta semula automatik oleh `build_msix.ps1`
- `PustakaHadith.pfx` (sijil) · semua aset Store (screenshot_*, privacy_*)
- `PustakaHadith-v1.0.0.zip` (683 MB) — **satu-satunya salinan**; Release GitHub
  `v1.0.0` tiada aset. Hanya buang dengan arahan eksplisit.
- `PANDUAN_KEMAS_KINI_STORE_v1.0.1.md` — **dibuang (30 Sep, arahan: tak perlu
  memandangkan v1.0.3 sudah terbit)**; masih boleh dipulihkan dari git (`d10bc51`).

Kandungan selepas pembersihan 30 Sep: ~8.9 GB (bebas ~6.0 GB).

## Pembersihan 21 Okt 2026 (arahan pengguna: "bersihkan folder projek")

Semakan mendalam dibuat **sebelum** hapus — setiap fail disahkan, bukan andaian.

**Dibuang (4,287.0 MB):**
- `msix\PustakaHadith-v1.0.0.msix` (1,093.7 MB)
- `msix\PustakaHadith-v1.0.0-slim.msix` (814.8 MB)
- `msix\PustakaHadith-v1.0.1.msix` (814.7 MB)
- `msix\PustakaHadith-v1.0.2.0.msix` (781.9 MB)
- `msix\PustakaHadith_1.0.3.0_x64.msix` (781.9 MB)
- `msix_staging\` (1,692.9 MB; 6,128 fail)

**Bukti selamat:** `build_msix.ps1` sentiasa membina semula dari
`PustakaQH_dist\PustakaHadith` → `msix_staging` (baris 21 padam & cipta
semula) dan menulis `$out` baharu; ia **tidak pernah membaca** pakej MSIX
lama. `semak.py` **tiada** semakan fail MSIX (0 padanan). Rujukan nama fail
lama hanya wujud dalam `SESI.md` (rekod sejarah) dan `NOTA.md` (jadual).

**Dikekalkan:** `msix\PustakaHadith_1.1.0_x64.msix` (782 MB — versi semasa,
juga di GitHub Release dengan SHA-256 sepadan) · `PustakaHadith\`
(pokok binaan kanonik 2,163.3 MB) · `PustakaHadith-v1.0.0.zip` (683.5 MB) ·
semua aset Store · sijil pfx.

Kandungan selepas pembersihan 21 Okt: **~3.63 GB** (dari ~8.9 GB).
