# Kover Bukhari & Muslim Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Dua kad pertama dalam seksyen `#kitab` di `landing-page/mockup-pro.html` guna kover templat yang sama seperti tujuh kad lain, tanpa mengubah `index.html` atau imej asal.

**Architecture:** Jana dua PNG baru dengan mengklon templat `img/abudaud-ro.png`: tukar warna jalur aksyen melalui interpolasi paksi warna, padam kawasan teks berubah, dan tulis nama kitab Arab dengan `arabic_reshaper` + `bidi` + `Amiri-Bold.ttf`. Kemudian tukar hanya dua atribut `src` dalam HTML. Tiada kod runtime baharu.

**Tech Stack:** Python 12.3.0 / Pillow, `arabic_reshaper`, `bidi`, fon `PustakaHadith/fonts/Amiri-Bold.ttf`; vanilla HTML; browser untuk verifikasi visual.

**Spec:** `docs/superpowers/specs/2026-11-28-kover-bukhari-muslim-design.md`

## Global Constraints

- "Dua fail PNG baru: `landing-page/img/bukh-flat.png` dan `landing-page/img/muslim-flat.png`."
- "Imej asal `bukh-ro.png` / `muslim-ro.png` tidak ditulis semula."
- "Hanya `mockup-pro.html` yang berubah dari segi rujukan imej; `index.html` kekal guna imej asal."
- "Tiada pustaka luar pada halaman; tiada dependency runtime baharu."
- "Shaping Arab mesti melalui `arabic_reshaper` + `bidi`, bukan `ImageDraw.text` terus" (`raqm False`).
- Warna aksyen: Bukhari `#5f8f3f`, Muslim `#8e3b46`. Teks: `صحيح البخاري`, `صحيح مسلم`, warna `#ebf7f3`, medan `#283e54`.
- "Kekal `git add` secara eksplisit, tiada `git add -A`, tiada push tanpa kelulusan."

## Review Focus

- **RF1** — Kover baru ada bingkai gelap, bucu teal, jalur aksyen atas/bawah, dan hiasan tetap yang **bit-identik** dengan kover rujukan; hanya warna jalur dan nama Arab yang berubah. Diuji Task 1 Step 4.
- **RF2** — Nama Arab shaped dengan betul (huruf tersambung, bukan potongan); bukan sekadar `ImageDraw.text` mentah. Diuji Task 1 Step 4 via semakan kod + Task 2 Step 3.
- **RF3** — `muslim-ro.png` asal ber saiz 576×576; kover baru mesti 512×512 supaya `aspect-ratio:3/4.2` dan render 128×179 sama seperti kad lain. Diuji Task 1 Step 4 dan Task 2 Step 3.
- **RF4** — `index.html` dan tujuh PNG asal tidak berubah; `alt`, teks kad, dan `data-i18n` kekal. Diuji Task 2 Step 3.
- **RF5** — Tiada regresi pada nav, i18n MS/EN, slide, atau dialog 7-Zip; 0 ralat konsol. Diuji Task 2 Step 3.

---

### Task 1: Jana dua kover rata

**Files:**
- Create: `landing-page/img/bukh-flat.png`
- Create: `landing-page/img/muslim-flat.png`
- Generator (tidak ditempatkan dalam repo; skrip sementara di `%TEMP%\\opencode\\generate_covers.py`)

**Interfaces:**
- Consumes: `landing-page/img/abudaud-ro.png` (templat, 512×512 RGB), `PustakaHadith/fonts/Amiri-Bold.ttf`.
- Produces: dua PNG RGB 512×512; `src` relatif `img/bukh-flat.png` dan `img/muslim-flat.png` untuk Task 2.

- [ ] **Step 1: Sahkan keadaan RED**

```bash
python -c "from PIL import Image; from collections import Counter; import os; b=r'D:/Pustaka Quran Hadis/Pustaka/landing-page/img'; [print(n, Image.open(os.path.join(b,n)).size, 'alpha' in Image.open(os.path.join(b,n)).mode, len(set(Image.open(os.path.join(b,n)).convert('RGB').resize((32,32)).getdata()))) for n in ['bukh-ro.png','muslim-ro.png','abudaud-ro.png']]"
```

Expected: `bukh-ro.png (512,512)`, `muslim-ro.png (576,576)`; kedua-dua fail sasaran `bukh-flat.png` / `muslim-flat.png` **tidak wujud**.

- [ ] **Step 2: Tulis skrip penjana**

Di `%TEMP%\\opencode\\generate_covers.py`, dengan fungsi `make_cover(title: str, accent: tuple[int,int,int], out: str) -> None`:

1. Buka `abudaud-ro.png` sebagai RGB; `px = im.load()`.
2. Untuk setiap piksel dalam `y ∈ [28,54] ∪ [468,486]`: kira `a = (r - 40) / (183 - 40)`; terima hanya jika `|g - (62 + a*(109-62))| ≤ 12` dan `|b - (84 + a*(29-84))| ≤ 12`; tulis semula sebagai `BG + a*(accent - BG)`. Ini menukar jalur aksyen dan anti-alias tepi tanpa menyentuh bucu teal atau bingkai gelap.
3. Padam kawasan teks: `ImageDraw.rectangle((120,175,395,272), fill=(40,62,84))`.
4. `shaped = get_display(arabic_reshaper.reshape(title))`.
5. Cari saiz fon terbesar dalam julat `44..52` dengan `ImageDraw.textbbox((0,0), shaped, font=f)` lebar ≤220 dan tinggi ≤80; guna `Amiri-Bold.ttf`, `anchor='mm'` pada `(256, 227)`, `fill=(235,247,243)`.
6. `im.save(out, 'PNG')` dengan mod RGB.
7. Panggil: `make_cover('صحيح البخاري', (0x5f,0x8f,0x3f), .../bukh-flat.png)` dan `make_cover('صحيح مسلم', (0x8e,0x3b,0x46), .../muslim-flat.png)`.

- [ ] **Step 3: Jalankan penjana**

Run: `python %TEMP%\\opencode\\generate_covers.py`
Expected: dua fail wujud, tanpa ralat.

- [ ] **Step 4: Sahkan sifat imej (RF1–RF3)**

Tulis `%TEMP%\\opencode\\verify_covers.py` dan jalankan `python %TEMP%\\opencode\\verify_covers.py`. Skrip mesti mengandungi assertion berikut untuk setiap `(nama, aksyen)` dalam `[('bukh-flat.png',(0x5f,0x8f,0x3f)), ('muslim-flat.png',(0x8e,0x3b,0x46))]`:

```python
from PIL import Image, ImageChops
import os
b = r"D:\Pustaka Quran Hadis\Pustaka\landing-page\img"
ref = Image.open(os.path.join(b, "abudaud-ro.png")).convert("RGB")
BG = (40,62,84); TEAL = (120,222,208)
for name, accent in [("bukh-flat.png",(0x5f,0x8f,0x3f)), ("muslim-flat.png",(0x8e,0x3b,0x46))]:
    im = Image.open(os.path.join(b, name)).convert("RGB")
    px = list(im.getdata()); total = 512*512
    assert im.size == (512,512) and im.mode == "RGB", name
    assert sum(p==BG for p in px)/total >= 0.60, (name,"medan")
    assert sum(p==accent for p in px)/total > 0.05, (name,"aksyen")
    assert sum(p==TEAL for p in px)/total > 0.01, (name,"teal")
    assert sum(p in ((16,28,42),(8,16,26)) for p in px)/total > 0.04, (name,"bingkai")
    for y0,y1 in [(292,293),(331,353),(391,407)]:
        box=(60,y0,460,y1+1)
        assert ImageChops.difference(im.crop(box), ref.crop(box)).getbbox() is None, (name,"hiasan",y0)
    print(name, "PASS")
```

Expected: `bukh-flat.png PASS` dan `muslim-flat.png PASS`. Jika gagal, baiki penjana di Step 2 dan ulang Step 3–4 sebelum commit.

- [ ] **Step 5: Commit dua PNG**

```bash
git add landing-page/img/bukh-flat.png landing-page/img/muslim-flat.png
git commit -m "feat: kover rata Bukhari dan Muslim mengikut templat 9 kitab"
```

---

### Task 2: Tukar rujukan imej dan verifikasi

**Files:**
- Modify: `landing-page/mockup-pro.html:772-773`

**Interfaces:**
- Consumes: `img/bukh-flat.png`, `img/muslim-flat.png` dari Task 1.
- Produces: tiada API; hanya dua atribut `src`. Tiada task berikutnya.

- [ ] **Step 1: Tukar dua `src` sahaja**

Baris 772: `img/bukh-ro.png` → `img/bukh-flat.png`. Baris 773: `img/muslim-ro.png` → `img/muslim-flat.png`. `alt="Sahih Bukhari"` / `alt="Sahih Muslim"`, `<h4>`, `.ar`, `<p>`, `.n` tidak diubah.

- [ ] **Step 2: Sahkan skop diff**

```bash
git diff --stat -- landing-page/mockup-pro.html index.html landing-page/img
```

Expected: hanya `landing-page/mockup-pro.html` dengan 2 baris berubah; `index.html` dan tujuh `*-ro.png` asal tiada dalam diff bagi task ini.

- [ ] **Step 3: Verifikasi dalam pelayar (RF2–RF5)**

Muat semula `landing-page/mockup-pro.html`, tatal ke `#kitab`, then `browser.evaluate`:

```js
(()=>({cards:[...document.querySelectorAll('.rak .book')].map(c=>{const i=c.querySelector('img');return {title:c.querySelector('h4').textContent,src:i.getAttribute('src'),natural:[i.naturalWidth,i.naturalHeight],rendered:[Math.round(i.getBoundingClientRect().width),Math.round(i.getBoundingClientRect().height)]}})}))()
```

Assert: kesembilan-sembilan `natural == [512,512]` dan `rendered == [128,179]`; dua `src` pertama berakhir `-flat.png`; tujuh selebihnya kekal `-ro.png`.

Kemudian semak popup/i18n/nav tidak regresi seperti ujian reset sebelum ini, dan `browser.console(level:'error')` kosong.

- [ ] **Step 4: Commit**

```bash
git add landing-page/mockup-pro.html
git commit -m "fix: guna kover templat untuk kad Bukhari dan Muslim"
```
