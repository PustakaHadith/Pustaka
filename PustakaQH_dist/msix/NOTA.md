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
| PustakaHadith-v1.0.0-slim.msix | 1.0.0 | slim (blobs dibuang) |
| PustakaHadith-v1.0.0.msix | 1.0.0 | penuh |
| PustakaHadith-v1.0.1.msix | 1.0.1 | Store refresh |
| PustakaHadith-v1.0.2.0.msix | 1.0.2.0 | |
| PustakaHadith_1.0.3.0_x64.msix | 1.0.3.0 | 30 Sep 2026, self-signed |

## Pembinaan

- Skrip: `PustakaHadith/installer/build_msix.ps1`
- Output skrip sudah diset terus ke folder ini (`$out` →
  `PustakaQH_dist/msix`) — msix baharu **datang automatik ke sini**
- Nota: `signtool verify /pa` akan gagal — sijil self-signed,
  bukan root CA. Tanda `SIGN_EXIT=0` yang menunjukkan berjaya.
