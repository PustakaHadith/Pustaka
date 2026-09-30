PANDUAN KEMAS KINI PUSTAKAHADITH KE MICROSOFT STORE (v1.0.1)
=============================================================
Tarikh: 11 September 2026
Pakej: PustakaHadith-v1.0.1.msix (814.7 MB)

[DIKEMASKINI 30 SEP 2026 — dokumen di bawah adalah SEJARAH v1.0.1]
- Pakej kini disimpan di folder khas: PustakaQH_dist\msix\
  (semua versi: v1.0.0-slim, v1.0.0, v1.0.1, v1.0.2.0, 1.0.3.0)
- Build MSIX: staging PustakaQH_dist\msix_staging\ → output PustakaQH_dist\msix\
  (lihat PustakaQH_dist\NOTA.md dan msix\NOTA.md)
- Status semasa: Store memegang v1.0.2 · build terkini = v1.0.3.0
  (30 Sep 2026, belum dimuat naik ke Store — tunggu arahan)

STATUS SEMASA
-------------
- Store kini memegang v1.0.0 (dimuat naik 1 September 2026).
- Versi terbaru = "slim" (hasil optimum FASA 3: buang duplikat HF blobs,
  model e5 + FAISS + hadis.db kekal lengkap).
- Versi slim asal masih bertanda 1.0.0.0 — TIDAK BOLEH dihantar sebagai
  kemas kini (versi mesti lebih tinggi).
- Kami telah NAHKAN VERSI kepada 1.0.1.0 dan REBUILD pakej.


PERSOALAN: PERLUKAH REBUILD?
----------------------------
YA, wajib. Nombor versi tertanam di dalam AppxManifest.xml DI DALAM
pakej MSIX, bukan pada nama fail. Menamakan semula fail "v1.0.1" sahaja
tidak mengubah versi pakej. Store menolak pakej yang versinya sama atau
lebih rendah daripada yang telah disiarkan.

Pakej v1.0.1 telah dibina semula:
  - Laluan (30 Sep): D:\Pustaka Quran Hadis\Pustaka\PustakaQH_dist\msix\PustakaHadith-v1.0.1.msix
  - Identiti: PUSTAKAHADITH.PustakaHadith (SAMA - tidak berubah)
  - Publisher: CN=1084A5A8-F66F-4B6D-A3EF-455CCC63CDD2 (SAMA)
  - Versi: 1.0.1.0
  - Ditandatangani dengan cert ujian (untuk pengesahan sahaja)


LANGKAH MUAT NAIK KE STORE
---------------------------
1. Buka https://partner.microsoft.com/dashboard
2. Pergi ke Pustaka Hadith  >  "Submit an update" (atau New submission).
3. Bahagian Packages:
   - Muat naik PustakaHadith-v1.0.1.msix
   - SAMBUNGKAN ke "Packages" yang sedia ada untuk naik taraf
     (jangan cipta produk baharu).
4. Lengkapkan bahagian lain jika belum lengkap:
   - Properties (kategori: Books & Reference / Education)
   - Age ratings (IARC questionnaire)
   - Store listings (deskripsi, ikon, minimum 4 tangkapan skrin)
   - Pricing & availability (Percuma / Free)
   - Notes for certification (lihat nota di bawah)
5. Restricted capabilities: runFullTrust — kelulusan terdahulu kekal
   kerana identiti pakej tidak berubah. Tiada perlu ulang.
6. Klik Submit to Store.


NOTES FOR CERTIFICATION (cadangan teks)
---------------------------------------
"Update v1.0.1 — optimisation: reduced package size from ~1.09GB to
~815MB by removing duplicated HuggingFace model cache blobs. The
multilingual e5-small AI model, FAISS index, and local hadith database
remain fully bundled and functional offline. All prior functionality
is unchanged: browse 9 hadith books, keyword + semantic search,
bookmarks, offline access."


SIJIL / TANDATANGAN
-------------------
- Untuk Store: Microsoft menandatangani semula pakej selepas pensijilan.
  Sijil ujian kami tidak perlu dipercayai oleh Store.
- Untuk ujian tempatan (Add-AppxPackage): cert ujian mesti diimport ke
    Root Trusted store dengan hak admin:
    Import-PfxCertificate -FilePath test101.pfx -Password (ConvertTo-SecureString "PustakaTest101" -AsPlainText -Force) -CertStoreLocation Cert:\LocalMachine\Root
  (Folder: D:\tools\sdkbt\test101.pfx)


SELEPAS DISETUJUI
-----------------
- Pengguna yang sudah memasang v1.0.0 akan menerima kemas kini automatik.
- Data pengguna (bookmarks, settings, hadis.db tempatan) kekal kerana
  MSIX naik taraf tidak memadam %LOCALAPPDATA%\PustakaHadith.