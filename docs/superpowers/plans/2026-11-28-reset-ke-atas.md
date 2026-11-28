# Reset Ke Atas Masa Muat Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Buka/refresh `landing-page/mockup-pro.html` sentiasa bermula di `scrollY === 0` dengan URL tanpa fragmen, tanpa memutuskan pautan anchor dalam halaman.

**Architecture:** Satu blok JS di awal `<script>` menetapkan `history.scrollRestoration='manual'`, membuang `location.hash` dengan `history.replaceState`, dan `scrollTo({top:0,behavior:'instant'})`. Pelayar tidak lagi melompat ke anchor semasa muat; klik pautan anchor selepas muat masih berfungsi seperti biasa.

**Tech Stack:** Vanilla JavaScript; History API (`scrollRestoration`, `replaceState`); `window.scrollTo`.

**Spec:** `docs/superpowers/specs/2026-11-28-reset-ke-atas-design.md`

## Global Constraints

- "Vanilla JS sahaja; tiada pustaka luar."
- "Kod mesti berada di awal blok `<script>` supaya berjalan sebelum pelayar melakukan anchor scroll/restoration yang boleh dilihat."
- "`scroll-behavior:smooth` pada `html` bermakna `scrollTo(0,0)` tanpa `behavior:'instant'` kelihatan animasi — gunakan `behavior:'instant'` untuk reset."
- "Bahasa MS/EN terus diingati seperti sekarang; yang direset hanya posisi halaman dan fragmen URL."
- "Commit ter-skop: `landing-page/mockup-pro.html` dan/atau `docs/superpowers/`. Tiada `git add -A`, tiada push tanpa kelulusan."
- `replaceState` hanya dipanggil bila `location.hash` tidak kosong; `scrollTo` dipanggil tanpa syarat.
- `history.scrollRestoration='manual'` dikunci dengan `"scrollRestoration" in history`.

## Review Focus

- **RF1** — Refresh dengan hash `#muat-turun`: `hash === ''` dan `scrollY === 0`. Diuji Task 1 Step 2 (RED) & Step 4 (GREEN).
- **RF2** — Klik pautan nav ke `#muat-turun` selepas muat: masih menatal ke seksyen itu. Diuji Task 1 Step 4.
- **RF3** — Refresh tanpa hash dan selepas tatal jauh: kekal `scrollY === 0` (pemulihan tatal pelayar ditewaskan). Diuji Task 1 Step 4.
- **RF4** — Popup 7-Zip dan toggle EN/MS tidak regresi; 0 ralat konsol. Diuji Task 1 Step 4.
- **RF5** — Pelayar tanpa `history.scrollRestoration` tidak melempar ralat (guard `in history`). Diuji Task 1 Step 4 melalui semakan kod + 0 ralat konsol.

---

### Task 1: Reset masa muat

**Files:**
- Modify: `landing-page/mockup-pro.html:1067` (awal blok `<script>`, sebelum `/* ---------- nav ---------- */`)

**Interfaces:**
- Consumes: `location.hash`, `history.replaceState`, `window.scrollTo`, `html{scroll-behavior:smooth}` sedia ada.
- Produces: tiada API baharu; hanya kesan sampingan pada masa muat. Tiada task berikutnya.

- [ ] **Step 1: Tulis ujian gagal untuk RF1**

Dalam pelayar yang memuat `landing-page/mockup-pro.html`, jalankan `browser.evaluate`:

```js
(()=>{location.hash='#muat-turun';window.scrollTo(0,3000);return {hash:location.hash,scrollY:Math.round(scrollY)}})()
```

Kemudian `browser.reload({ignoreCache:true})` dan `browser.evaluate`:

```js
(async()=>{await new Promise(r=>setTimeout(r,800));return {hash:location.hash,scrollY:Math.round(scrollY)}})()
```

Assert RED: `hash==='#muat-turun'` dan `scrollY>0` — gagal kerana tiada reset lagi.

- [ ] **Step 2: Sahkan ujian gagal (RED)**

Run: Step 1.
Expected: hash kekal `#muat-turun`, `scrollY` stabil sekitar `7299` (sekitar seksyen muat turun), bukan `0`. Ini bukti punca: fragmen URL + anchor scroll.

- [ ] **Step 3: Implementasi minimum**

Di `landing-page/mockup-pro.html`, terus selepas baris `<script>` (sebelum `/* ---------- nav ---------- */`), tambah blok:

```js
/* ---------- mula di halaman utama ---------- */
if('scrollRestoration' in history)history.scrollRestoration='manual';
if(location.hash)history.replaceState(null,'',location.pathname+location.search);
scrollTo({top:0,behavior:'instant'});
```

Tiada perubahan lain.

- [ ] **Step 4: Sahkan ujian lulus (GREEN) + Review Focus**

Run A — RF1, selepas ulang Step 1 dengan hash:

```js
(async()=>{await new Promise(r=>setTimeout(r,800));return {hash:location.hash,scrollY:Math.round(scrollY)}})()
```

Assert: `hash===''`, `scrollY===0`.

Run B — RF2, klik pautan nav:

```js
(async()=>{
  const a=[...document.querySelectorAll('a[href="#muat-turun"]')][0];
  a.click();
  await new Promise(r=>setTimeout(r,1200));
  const el=document.getElementById('muat-turun');
  return {hash:location.hash,scrollY:Math.round(scrollY),targetTop:Math.round(el.getBoundingClientRect().top)}
})()
```

Assert: `hash==='#muat-turun'`, `scrollY>0`, `Math.abs(targetTop)<150` (anchor masih membawa ke seksyen itu; `scroll-padding-top` sedia ada memberi offset).

Run C — RF3:

`browser.evaluate`:

```js
(()=>{history.replaceState(null,'',location.pathname+location.search);scrollTo({top:0,behavior:'instant'});window.scrollTo(0,5000);return Math.round(scrollY)})()
```

Assert `before > 0`, kemudian `browser.reload({ignoreCache:true})`, then `browser.evaluate`:

```js
(()=>({hash:location.hash,scrollY:Math.round(scrollY)}))()
```

Assert: `hash===''`, `scrollY===0`.

Run D — RF4:

```js
(()=>{
  const link=document.getElementById('z7-link');
  const dlg=document.getElementById('z7-dialog');
  link.click();
  const opened=dlg.open;
  document.getElementById('z7-close').click();
  document.querySelector('[data-lang="en"]').click();
  const en=document.getElementById('z7-title').innerHTML;
  return {opened,closed:!dlg.open,en,lang:document.documentElement.lang}
})()
```

Assert: `opened===true`, `closed===true`, `en==='Why use 7-Zip?'`, `lang==='en'`. Kemudian klik `[data-lang="ms"]`, tunggu reload, sahkan `document.documentElement.lang==='ms'`. `browser.console(level:'error')` kosong.

- [ ] **Step 5: Commit**

```bash
git add landing-page/mockup-pro.html
git commit -m "fix: mula pada halaman utama bila buka atau refresh"
```
