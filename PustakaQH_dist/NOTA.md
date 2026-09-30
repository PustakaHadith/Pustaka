# NOTA — PustakaQH_dist = pusat rasmi file distribution Microsoft Store

> **WAJIB (arahan pengguna, 30 Sep 2026):** Folder **`PustakaQH_dist\`**
> ini mesti digunakan untuk pembikinan semua file distribution
> Microsoft Store (MSIX, staging, aset Store). Tiada pembikinan file
> Store di luar folder ini.

## Susunan wajib

| Perkara | Lokasi |
|---|---|
| Output MSIX siap (semua versi) | `PustakaQH_dist\msix\` — lihat `msix\NOTA.md` |
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
- `msix\` (5 versi msix + NOTA) · `msix_staging\` · `PustakaHadith\` (build 29 Sep)
- `PustakaHadith.pfx` (sijil) · semua aset Store (screenshot_*, privacy_*)
- `PustakaHadith-v1.0.0.zip` (683 MB) — **satu-satunya salinan**; Release GitHub
  `v1.0.0` tiada aset. Hanya buang dengan arahan eksplisit.
- `PANDUAN_KEMAS_KINI_STORE_v1.0.1.md` — **dibuang (30 Sep, arahan: tak perlu
  memandangkan v1.0.3 sudah terbit)**; masih boleh dipulihkan dari git (`d10bc51`).

Kandungan selepas pembersihan: ~8.9 GB (bebas ~6.0 GB).
