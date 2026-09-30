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
| Aset Store (screenshot, privasi, penerangan) | `PustakaQH_dist\` root (screenshot_*.png, privacy_policy.html, PANDUAN_*) |
| Pakej Store rasmi & sejarah | `PustakaQH_dist\msix\` |

## Pembinaan

- Skrip: `PustakaHadith/installer/build_msix.ps1`
  - `$stage` → `PustakaQH_dist\msix_staging` (**wajib ikut folder ini**)
  - `$out` → `PustakaQH_dist\msix` (msix baharu datang automatik)
- Sijil: `PustakaQH_dist\PustakaHadith.pfx` (self-signed, buat msix)

Jangan ubah laluan ini tanpa arahan pengguna.
