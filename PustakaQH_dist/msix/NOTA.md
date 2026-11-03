# NOTA — Folder MSIX rasmi

> **WAJIB:** semua pembikinan file distribution Microsoft Store mesti
> dalam folder `PustakaQH_dist\` — lihat `..\NOTA.md` (folder induk).

**Semua pakej MSIX PustakaHadith mesti disimpan di sini** (folder khas).

- Lokasi: `D:\Pustaka Quran Hadis\Pustaka\PustakaQH_dist\msix\`
- Arahan pengguna (30 Sep 2026): msix dipindah ke folder khas ini,
  dan **akan dtg msix di sini** pada masa akan datang.

## Kandungan

| Fail | Versi | Nota |
|---|---|---|
| PustakaHadith_1.1.0_x64.msix | 1.1.0 | **semasa** — Store LIVE, juga di GitHub Release (SHA-256 sepadan) |

> **Pembersihan 21 Okt 2026** — 5 pakej lama dibuang (~4.3 GB) kerana sudah
> digantikan di Microsoft Store dan tiada skrip/dokumen yang merujuknya:
> `v1.0.0.msix` (1,093.7 MB) · `v1.0.0-slim.msix` (814.8 MB) ·
> `v1.0.1.msix` (814.7 MB) · `v1.0.2.0.msix` (781.9 MB) ·
> `v1.0.3.0_x64.msix` (781.9 MB).
> Disahkan selamat: `build_msix.ps1` sentiasa membina semula dari
> `PustakaQH_dist\PustakaHadith` → `msix_staging` (dipadam & dicipta
> semula setiap larian), tidak pernah membaca pakej lama; `semak.py`
> tidak menyemak fail MSIX sama sekali.

## Pembinaan

- Skrip: `PustakaHadith/installer/build_msix.ps1`
- Output skrip sudah diset terus ke folder ini (`$out` →
  `PustakaQH_dist/msix`) — msix baharu **datang automatik ke sini**
- Nota: `signtool verify /pa` akan gagal — sijil self-signed,
  bukan root CA. Tanda `SIGN_EXIT=0` yang menunjukkan berjaya.
