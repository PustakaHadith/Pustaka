# Mockup Animasi Interaktif — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Tambah animasi tindak balas kursor (entrance hero, parallax, tilt kad, butang magnet, glow drift) pada `landing-page/mockup-pro.html` supaya halaman tidak lagi nampak statik.

**Architecture:** Satu fail HTML sahaja. CSS baharu sebagai satu seksyen baru (21) sebelum `</style>`; JS baharu sebagai satu blok baharu di hujung `<script>` sedia ada. Animasi CSS murni untuk entrance + drift; JS vanilla (guard `prefers-reduced-motion` + `hover/pointer`) untuk parallax/tilt/magnet. Konflik transform diselesaikan dengan sifat individu CSS `translate` (untuk parallax & magnet — berjalan selari dengan `transform` sedia ada) dan dengan menyusun inline `transform` penuh (untuk tilt, yang memang perlukan `rotateX/rotateY`).

**Tech Stack:** HTML + CSS + vanilla JS (tiada pustaka luar). Ujian = `browser.evaluate` pada tab pelayar yang sudah terbuka (`tab_84bcfc1c-738d-43f8-91e5-af5d416ba8e9`).

**Spec:** `docs/superpowers/specs/2026-11-27-mockup-animasi-interaktif-design.md`

## Global Constraints

- Fail disentuh: `landing-page/mockup-pro.html` sahaja (+ fail `docs/superpowers/`). Tiada fail lain.
- Tiada pustaka luar; vanilla JS/CSS sahaja.
- Hanya animasi `transform` / `translate` / `opacity`; `pointermove` mesti di-throttle `requestAnimationFrame`; listener `passive`.
- Hormat `prefers-reduced-motion` — CSS blok sedia ada (baris ~458, `*{animation:none!important}`) melumpuhkan CSS baharu secara automatik; JS baharu mesti ada guard `matchMedia('(prefers-reduced-motion: reduce)').matches`.
- Sentuh / tiada hover: JS baharu mesti dimatikan sepenuhnya apabila `!matchMedia('(hover: hover) and (pointer: fine)').matches`.
- Nilai tetap dari spec: had tilt **8°** (guna `±8`), parallax hero **±8px paksi X, ±6px paksi Y**, butang magnet **had ±5px**, entrance hero leret **90ms** setiap langkah, glow drift tempoh **18s**.
- Jangan rosak: observer `.rv`, kiraan statistik `[data-count]`, i18n MS/EN (`setLang`), nav, `#toTop`.
- Guna pemboleh ubah sedia ada: `--ease`, `--brand`, `--gold`.
- Selepas Task 1, `landing-page/mockup-pro.html` menjadi fail tracked (kini untracked) — commit mesti **scoped**:`git add landing-page/mockup-pro.html` (+ `docs/superpowers/` di Task 5). JANGAN `git add -A` (working tree ada perubahan lain: `index.html`, PNG, `BIODATA_PENERBIT.md`, `in`).

## Review Focus

1. **Reveal `.rv` vs inline transform** — kad `.book`/`.feat` bermula dengan `transform:translateY(22px)` dan ditetapkan `transitionDelay` inline oleh pemerhati sedia ada. Tilt mesti hanya berfungsi selepas kad ada kelas `.in`, dan mesti menetapkan `transitionDuration='.12s'` + `transitionDelay='0ms'` inline semasa engage supaya tilt tidak dijangka oleh lengahan reveal. *Tes: kad tanpa `.in` kekal `style.transform===''` selepas `pointermove` (Task 3).*
2. **`.win` sudah ada pose 3D** — `.win{transform:perspective(1600px) rotateY(-3deg) rotateX(1deg)}` + `.shot-wrap:hover .win{...}` + media `transform:none`. Parallax mesti guna sifat **`translate`** (bukan `transform`) supaya pose & hover kekal. *Tes: semasa parallax aktif, `getComputedStyle(win).transform` masih mengandungi `perspective(1600px)` (Task 2).*
3. **`.btn-p:hover` sudah guna `transform:translateY(-2px)`** — magnet mesti guna sifat `translate` supaya hover CSS kekal berfungsi; `style.transform` mesti kekal kosong. *Tes: `btn.style.transform===''` semasa magnet aktif (Task 4).*
4. **`setLang` mengganti `innerHTML` elemen `[data-i18n]`** — entrance CSS mesti dipasang pada pembungkus kekal (`.hero .badge`, `.hero h1`, `.hero .lead`, `.hero .cta`, `.hero .stats`), bukan pada span yang diganti. *Tes: selepas `setLang('en')` + kembali `ms`, `animationName` kekal `heroIn` dan teks BM pulih (Task 5).*
5. **Guard touch/reduced-motion** — jika guard gagal, halaman scroll/tilt mungkin janggal pada telefon. *Tes: guard mesti hadir sebagai kod (grep `motionOK`/`hoverOK` dalam fail) dan CSS `*{animation:none!important}` sedia ada melumpuhkan animasi CSS (Task 5).*

---

### Task 1: CSS — entrance hero + glow drift

**Files:**
- Modify: `landing-page/mockup-pro.html` (sisip sebelum `</style>`, baris ~520; seksyen baharu bernombor **21**)

**Interfaces:**
- Consumes: pemboleh ubah `--ease` sedia ada; blok `@media(prefers-reduced-motion:reduce)` sedia ada (baris ~458) melumpuhkan animasi baharu secara automatik.
- Produces (dipakai ujian Task 1 & 5): kelas/@keyframes `heroIn`, `glowDrift`; pemilih `.hero .badge,.hero h1,.hero .lead,.hero .cta,.hero .stats` dan `.bg-glow`.

- [ ] **Step 1: Tulis ujian GAGAL dahulu**

Jalankan pada tab mockup (reload dahulu supaya fail lama dimuat):

```js
// browser.evaluate
await tools.browser.reload({tabID, ignoreCache:true});
return await tools.browser.evaluate({tabID, script:`
const g=s=>{const e=document.querySelector(s);return e?getComputedStyle(e).animationName:'MISSING'};
const d=s=>getComputedStyle(document.querySelector(s)).animationDelay;
return {badge:g('.hero .badge'),h1:g('.hero h1'),lead:g('.hero .lead'),
        cta:g('.hero .cta'),stats:g('.hero .stats'),glow:g('.bg-glow'),
        h1Delay:d('.hero h1')};
`});
```

Expected (SEBELUM): semua `animationName` = `"none"`, `h1Delay` = `"0s"`.

- [ ] **Step 2: Sahkan GAGAL**

Expected: `badge,h1,lead,cta,stats,glow` semuanya `"none"`.

- [ ] **Step 3: Sisip CSS seksyen 21 sebelum `</style>`**

Anchor unik: `#toTop:hover{background:var(--brand-hi); ...}` block, kemudian `</style>`. Kandungan tepat:

```css
/* ---------- 21. ANIMASI INTERAKTIF ---------- */
.hero .badge,.hero h1,.hero .lead,.hero .cta,.hero .stats{animation:heroIn .8s var(--ease) both}
.hero h1{animation-delay:.09s}
.hero .lead{animation-delay:.18s}
.hero .cta{animation-delay:.27s}
.hero .stats{animation-delay:.36s}
@keyframes heroIn{from{opacity:0;transform:translateY(18px)}to{opacity:1;transform:none}}
.bg-glow{animation:glowDrift 18s ease-in-out infinite alternate}
@keyframes glowDrift{from{transform:scale(1.05) translate3d(-1.2%,-.8%,0)}to{transform:scale(1.05) translate3d(1.2%,.8%,0)}}
```

Nota: `.badge` delay kekal `0s` (langkah pertama). `scale(1.05)` mengelak tepi telanjang semasa translate. Animasi pada pemilih kekal bertahan selepas `setLang` (ia tidak menyentuh span `[data-i18n]` yang diganti).

- [ ] **Step 4: Jalankan semula ujian — PASSES**

Expected: `badge:"heroIn"`, `h1:"heroIn"`, `lead:"heroIn"`, `cta:"heroIn"`, `stats:"heroIn"`, `glow:"glowDrift"`, `h1Delay:"0.09s"`.

- [ ] **Step 5: Commit (scoped)**

```bash
git add landing-page/mockup-pro.html
git commit -m "feat(mockup): entrance hero berperingkat + gerak glow"
```

---

### Task 2: JS — guard + parallax hero (guna sifat `translate`)

**Files:**
- Modify: `landing-page/mockup-pro.html` (sisip selepas baris `document.getElementById('yr').textContent=new Date().getFullYear();`, sebelum `</script>`)

**Interfaces:**
- Consumes: `.hero`, `.hero .win`, `.bg-glow` (Task 1 sudah memberi `.bg-glow` animasi `transform` — parallax guna sifat `translate`, kedua-duanya berjalan selari).
- Produces: blok JS berlabel `/* ---------- animasi interaktif ---------- */` dengan pemboleh ubah `motionOK`, `hoverOK` (Task 3 & 4 menyambung ke dalam blok yang sama, selepas guard yang sama).

- [ ] **Step 1: Tulis ujian GAGAL dahulu**

```js
// browser.evaluate — dispatch pointermove pada hero, tunggu 2 frame, baca translate
return await tools.browser.evaluate({tabID, script:`
const hero=document.querySelector('.hero'),win=document.querySelector('.hero .win');
const r=hero.getBoundingClientRect();
hero.dispatchEvent(new PointerEvent('pointermove',{clientX:r.left+r.width*0.9,clientY:r.top+r.height*0.2,bubbles:true}));
await new Promise(res=>requestAnimationFrame(()=>requestAnimationFrame(res)));
return {translate:win.style.translate||'', transform:win.style.transform||'(empty)',
        computedTransform:win.style.transform?'':'(ikut CSS)'};
`});
```

Expected (SEBELUM): `translate:""` (kosong).

- [ ] **Step 2: Sahkan GAGAL** — `translate` kekal `""`.

- [ ] **Step 3: Sisip blok JS — guard + parallax + gerak glow bertentangan**

Struktur tepat (nilai dikunci oleh spec):

```js
/* ---------- animasi interaktif ---------- */
(()=>{
  const motionOK=!matchMedia('(prefers-reduced-motion: reduce)').matches;
  const hoverOK=matchMedia('(hover: hover) and (pointer: fine)').matches;
  if(!motionOK||!hoverOK)return;
  const hero=document.querySelector('.hero'),win=document.querySelector('.hero .win'),
        glow=document.querySelector('.bg-glow');
  let raf=0,px=0,py=0;
  hero.addEventListener('pointermove',e=>{
    const r=hero.getBoundingClientRect();
    px=((e.clientX-r.left)/r.width-.5)*16;   /* had ±8px */
    py=((e.clientY-r.top)/r.height-.5)*12;   /* had ±6px */
    if(!raf)raf=requestAnimationFrame(()=>{
      raf=0;
      win.style.translate=px.toFixed(1)+'px '+py.toFixed(1)+'px';
      glow.style.translate=(-px*.4).toFixed(1)+'px '+(-py*.4).toFixed(1)+'px';
    });
  },{passive:true});
  hero.addEventListener('pointerleave',()=>{win.style.translate='';glow.style.translate=''});
  /* Task 3: tilt · Task 4: magnet — sisip di sini, dalam IIFE yang sama */
})();
```

- [ ] **Step 4: Jalankan semula ujian — PASSES**

Expected: `translate` mengandungi `px` (cth `"7.2px -4.1px"`), dan selepas dispatch `pointerleave` pada `.hero` → `translate:""`.

Ujian susulan (konflik #2 — pose `.win` mesti kekal):

```js
return await tools.browser.evaluate({tabID, script:`
const hero=document.querySelector('.hero'),win=document.querySelector('.hero .win');
const r=hero.getBoundingClientRect();
hero.dispatchEvent(new PointerEvent('pointermove',{clientX:r.left+10,clientY:r.top+10,bubbles:true}));
await new Promise(res=>requestAnimationFrame(()=>requestAnimationFrame(res)));
const css=getComputedStyle(win).transform;
hero.dispatchEvent(new PointerEvent('pointerleave',{bubbles:true}));
return {adaTranslate:win.style.translate!=='', poseKekal:css.includes('perspective(1600px)'), cleared:win.style.translate===''};
`});
```

Expected: `{adaTranslate:true, poseKekal:true, cleared:true}`.

- [ ] **Step 5: Commit (scoped)**

```bash
git add landing-page/mockup-pro.html
git commit -m "feat(mockup): parallax hero ikut kursor + glow bertentangan"
```

---

### Task 3: JS — tilt 3D kad `.book` dan `.feat`

**Files:**
- Modify: `landing-page/mockup-pro.html` (sisip dalam IIFE `animasi interaktif`, di tempat bertanda `Task 3: tilt`)

**Interfaces:**
- Consumes: guard `motionOK`/`hoverOK` Task 2; kad mempunyai kelas `.in` daripada pemerhati `.rv` sedia ada.
- Produces: tiada eksport — tingkah laku sahaja.

- [ ] **Step 1: Tulis ujian GAGAL dahulu**

```js
return await tools.browser.evaluate({tabID, script:`
const card=document.querySelector('.rak .book');
const before=card.style.transform;
const r=card.getBoundingClientRect();
card.dispatchEvent(new PointerEvent('pointermove',{clientX:r.left+r.width*0.8,clientY:r.top+r.height*0.2,bubbles:true}));
const during=card.style.transform;
card.dispatchEvent(new PointerEvent('pointerleave',{bubbles:true}));
return {before, during, after:card.style.transform, adaIn:card.classList.contains('in')};
`});
```

Expected (SEBELUM): `before:""`, `during:""` (kosong — handler belum wujud). `adaIn` mungkin `true`/`false` bergantung kedudukan scroll.

- [ ] **Step 2: Sahkan GAGAL** — `during` kekal `""`.

- [ ] **Step 3: Sisip handler tilt dalam IIFE**

Nilai dikunci: had `±8°`, lift sepadan hover CSS sedia ada (`.book` → `-6px`, `.feat` → `-4px`), engage hanya selepas `.in`:

```js
/* Task 3: tilt */
document.querySelectorAll('.rak .book,.bento .feat').forEach(card=>{
  const lift=card.classList.contains('book')?-6:-4;
  card.addEventListener('pointermove',e=>{
    if(!card.classList.contains('in'))return;
    const r=card.getBoundingClientRect();
    const rx=((e.clientY-r.top)/r.height-.5)*-16;  /* ±8° */
    const ry=((e.clientX-r.left)/r.width-.5)*16;   /* ±8° */
    card.style.transitionDuration='.12s';
    card.style.transitionDelay='0ms';
    card.style.transform=`perspective(900px) translateY(${lift}px) rotateX(${rx.toFixed(1)}deg) rotateY(${ry.toFixed(1)}deg)`;
  },{passive:true});
  card.addEventListener('pointerleave',()=>{card.style.transform=''});
});
```

Nota: `transitionDuration`/`transitionDelay` inline mengatasi lengahan reveal `(i%4)*60ms` semasa tilt; `transform` inline mengatasi `.book:hover/.feat:hover` — sebab itu `translateY(lift)` disertakan inline.

- [ ] **Step 4: Jalankan ujian — PASSES**

Paksa reveal dahulu supaya `.in` wujud, kemudian uji kedua-dua jenis kad:

```js
return await tools.browser.evaluate({tabID, script:`
const out={};
for(const [key,sel,lift] of [['book','.rak .book','-6px'],['feat','.bento .feat','-4px']]){
  const card=document.querySelector(sel);
  card.classList.add('in');
  const r=card.getBoundingClientRect();
  card.dispatchEvent(new PointerEvent('pointermove',{clientX:r.left+r.width*0.8,clientY:r.top+r.height*0.2,bubbles:true}));
  out[key]={transform:card.style.transform, dur:card.style.transitionDuration};
  card.dispatchEvent(new PointerEvent('pointerleave',{bubbles:true}));
  out[key].cleared=card.style.transform==='';
}
return out;
`});
```

Expected: `book.transform` mengandungi `perspective(900px)`, `translateY(-6px)`, `rotateX`, `rotateY` (nilai rotateX/rotateY antara `-8` dan `8`); `dur:"0.12s"`; `cleared:true`. `feat` sama tetapi `translateY(-4px)`.

Ujian guard (konflik #1 — kad BELUM `.in` mesti diabaikan):

```js
return await tools.browser.evaluate({tabID, script:`
const card=document.querySelector('.rak .book');
card.classList.remove('in');
const r=card.getBoundingClientRect();
card.dispatchEvent(new PointerEvent('pointermove',{clientX:r.left+5,clientY:r.top+5,bubbles:true}));
return {transform:card.style.transform, sepatutnyaKosong:card.style.transform===''};
`});
```

Expected: `transform:""`, `sepatutnyaKosong:true`. (Kembalikan `.in` selepas ujian dengan `card.classList.add('in')`.)

- [ ] **Step 5: Commit (scoped)**

```bash
git add landing-page/mockup-pro.html
git commit -m "feat(mockup): tilt 3D kad kitab & kad ciri ikut kursor"
```

---

### Task 4: JS — butang magnet `.btn-p`

**Files:**
- Modify: `landing-page/mockup-pro.html` (sisip dalam IIFE yang sama, tempat bertanda `Task 4: magnet`)

**Interfaces:**
- Consumes: guard `motionOK`/`hoverOK` Task 2.
- Produces: tiada eksport.

- [ ] **Step 1: Tulis ujian GAGAL dahulu**

```js
return await tools.browser.evaluate({tabID, script:`
const btn=document.querySelector('.hero .btn-p');
const r=btn.getBoundingClientRect();
btn.dispatchEvent(new PointerEvent('pointermove',{clientX:r.right-2,clientY:r.top+2,bubbles:true}));
const during={translate:btn.style.translate, transform:btn.style.transform};
btn.dispatchEvent(new PointerEvent('pointerleave',{bubbles:true}));
return {before:'(empty)', during, after:btn.style.translate};
`});
```

Expected (SEBELUM): `during.translate` = `""`.

- [ ] **Step 2: Sahkan GAGAL** — `during.translate` kekal `""`.

- [ ] **Step 3: Sisip handler magnet dalam IIFE**

Nilai dikunci: had `±5px`, faktor `.25`, guna sifat `translate` (bukan `transform` supaya hover CSS `.btn-p:hover{transform:translateY(-2px)}` kekal):

```js
/* Task 4: magnet */
document.querySelectorAll('.btn-p').forEach(btn=>{
  btn.addEventListener('pointermove',e=>{
    const r=btn.getBoundingClientRect();
    const x=Math.max(-5,Math.min(5,(e.clientX-(r.left+r.width/2))*.25));
    const y=Math.max(-5,Math.min(5,(e.clientY-(r.top+r.height/2))*.25));
    btn.style.translate=x.toFixed(1)+'px '+y.toFixed(1)+'px';
  },{passive:true});
  btn.addEventListener('pointerleave',()=>{btn.style.translate=''});
});
```

- [ ] **Step 4: Jalankan ujian — PASSES**

Expected: `during.translate` bukan `""`, kedua-dua komponen antara `-5` dan `5` (cth `"-5.0px -4.5px"`), `during.transform` = `""` (konflik #3 — CSS hover tidak dipijak), `after` = `""` selepas leave.

- [ ] **Step 5: Commit (scoped)**

```bash
git add landing-page/mockup-pro.html
git commit -m "feat(mockup): butang magnet tarik ke kursor"
```

---

### Task 5: Pengesahan penuh + commit dokumen

**Files:**
- Modify: tiada kod baharu — pengesahan sahaja.
- Commit: `docs/superpowers/specs/…-design.md`, `docs/superpowers/plans/…-plan.md`

**Interfaces:**
- Consumes: semua Task 1–4.

- [ ] **Step 1: 0 ralat konsol + fungsi teras kekal**

```js
await tools.browser.reload({tabID, ignoreCache:true});
// scroll sedikit supaya reveal & kira naik berjalan, kemudian:
return await tools.browser.evaluate({tabID, script:`
document.documentElement.style.scrollBehavior='auto';
window.scrollTo(0,1200);
await new Promise(r=>setTimeout(r,600));
return {scrollY:window.scrollY, adaToTop:!!document.getElementById('toTop')};
`});
const errs=await tools.browser.console({tabID,level:'error',limit:20});
return errs.messages;
```

Expected: `errs.messages` = `[]`, `adaToTop:true`.

- [ ] **Step 2: i18n MS ↔ EN kekal + entrance bertahan (konflik #4)**

```js
return await tools.browser.evaluate({tabID, script:`
setLang('en');
const en={nav:document.querySelector('[data-i18n="nav1"]').textContent,
          anim:getComputedStyle(document.querySelector('.hero h1')).animationName};
setLang('ms');
const ms={nav:document.querySelector('[data-i18n="nav1"]').textContent,
          anim:getComputedStyle(document.querySelector('.hero h1')).animationName};
return {en,ms};
`});
```

Expected: `en.nav==="Quick Start"`, `ms.nav==="Mula Pantas"`, kedua-dua `anim==="heroIn"`.

- [ ] **Step 3: Guard hadir dalam kod (konflik #5)**

Grep `landing-page/mockup-pro.html` untuk `motionOK` dan `hoverOK` — masing-masing mesti wujud ≥1 padanan, dan `if(!motionOK||!hoverOK)return;` mesti ada tepat satu.

- [ ] **Step 4: Screenshot visual**

Ambil screenshot hero (scroll 0) dan seksyen kitab — sahkan: hero nampak terang (bukan kosong/blur), kad kitab pada kedudukan biasa, tiada elemen terpotong.

- [ ] **Step 5: Commit dokumen (scoped)**

```bash
git add docs/superpowers/
git commit -m "docs: reka bentuk & pelaksanaan animasi interaktif mockup"
```

---

## Self-Review (dijalankan semasa penulisan)

- **Spec coverage:** 5 item skop → Task 1 (item 1 entrance + item 5 glow drift), Task 2 (item 2 parallax + glow bertentangan), Task 3 (item 3 tilt), Task 4 (item 4 magnet). Kekangan reduced-motion → guard Task 2 + CSS sedia ada; touch → guard Task 2; tiada pustaka → Global Constraints. ✓
- **Step scan:** setiap Task = ujian gagal → implement → lulus → commit; nilai dikunci (8°, ±5px, 90ms, 18s). ✓
- **Type consistency:** `motionOK`/`hoverOK` didefinisikan Task 2, digunakan Task 3/4 (dalam IIFE sama). ✓
- **Review Focus:** 5 baris, masing-masing ada tes pada task pemiliknya. ✓
- **Proporsi:** panjang sebanding dengan spesifikasi; blok kod hanya untuk nilai/matematik yang tidak boleh diteka pembina. ✓
