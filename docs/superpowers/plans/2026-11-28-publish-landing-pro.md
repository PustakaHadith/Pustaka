# Publish Landing Pro Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Jadikan reka bentuk `mockup-pro.html` sebagai `index.html` yang live di `pustakahadith.my` tanpa kehilangan modal Lesen/Biodata dan borang emel, then push ke Cloudflare Pages.

**Architecture:** `mockup-pro.html` menjadi asas `index.html`. Tiga fungsi dari halaman lama dipindahkan ke asas itu: modal Lesen Data, modal Biodata Penerbit, dan borang `mailto:`. CSS/JS/i18n kekal dalam satu fail `index.html` seperti sebelum ini. Deploy melalui auto-deploy Cloudflare Pages dari `main`.

**Tech Stack:** HTML/CSS/JS vanilla, Cloudflare Pages, Git.

**Spec:** `docs/superpowers/specs/2026-11-28-publish-landing-pro-design.md`

## Global Constraints

- Vanilla JS/CSS sahaja — tiada pustaka luar.
- Hormat `prefers-reduced-motion` (`motionOK`) dan `(hover: hover) and (pointer: fine)` (`hoverOK`) seperti dalam mockup.
- Jangan ubah `landing-page/mockup-pro.html`.
- Jangan commit fail luar skop (`BIODATA_PENERBIT.md`, folder untracked, dokumen SDD lama).
- `git add` eksplisit sahaja — **dilarang `git add -A`**.
- Tiada push tanpa kelulusan pengguna (pengguna sudah melulus push untuk pelan ini).
- Balas dalam Bahasa Melayu.

## Review Focus

- Klik pautan footer selepas tukar ke EN mesti tetap buka modal (kerana `setLang('en')` guna `I18N.en`, MS guna `location.reload()`) → Task 2 Step 4.
- ID bertindih antara markup mockup (`yr`, `z7-*`) dan markup modal yang dipindahkan mesti 0 → Task 2 Step 4.
- `mailto:` mesti mengekod aksara khas/Unicode dalam nama, subjek dan mesej (`encodeURIComponent`) → Task 3 Step 4.
- Sembilan kover mesti render `128×179` dengan `naturalWidth 512` dan 0 ralat konsol selepas gabungan → Task 4 Step 3.
- Auto-deploy mungkin lambat/terlepas: laman live mesti disemak dengan penanda unik selepas push, bukan sekadar andaikan berjaya → Task 5 Step 2.

---

### Task 1: Simpan rujukan lama + pasang asas mockup

**Files:**
- Modify: `landing-page/index.html`
- Reference (sementara, luar repo): `C:\Users\MKAW\AppData\Local\Temp\opencode\index-live-before.html`

**Interfaces:**
- Produces: salinan working-tree `index.html` sebelum timpa, dipakai Task 2/3 sebagai sumber CSS, markup modal, JS handler dan nilai `TRANS.en`.
- Produces: `index.html` dengan kandungan `mockup-pro.html` + penanda `z7-dialog`, `bukh-flat.png`, `muslim-flat.png`.

- [ ] **Step 1: Simpan rujukan sebelum menimpa**

```powershell
Copy-Item 'landing-page\index.html' 'C:\Users\MKAW\AppData\Local\Temp\opencode\index-live-before.html' -Force
```

Run: `Get-Item 'C:\Users\MKAW\AppData\Local\Temp\opencode\index-live-before.html' | Select-Object Length`
Expected: panjang ≈ 102947 bytes (versi working-tree dengan 7 baris nama sudah dikemas).

- [ ] **Step 2: Tulis ujian gagal (semakan penanda asas)**

Cipta `C:\Users\MKAW\AppData\Local\Temp\opencode\verify_publish_base.ps1`:

```powershell
$t = Get-Content 'D:\Pustaka Quran Hadis\Pustaka\landing-page\index.html' -Raw
foreach($m in @('id="z7-dialog"','img/bukh-flat.png','img/muslim-flat.png','id="kitab"','id="toTop"')){
  if($t -notlike "*$m*"){ throw "MISSING: $m" }
}
"BASE OK"
```

Run: `powershell -File C:\Users\MKAW\AppData\Local\Temp\opencode\verify_publish_base.ps1`
Expected: FAIL dengan `MISSING: id="z7-dialog"`.

- [ ] **Step 3: Timpa kandungan `index.html` dengan kandungan `mockup-pro.html`**

```powershell
Copy-Item 'landing-page\mockup-pro.html' 'landing-page\index.html' -Force
```

Kekalkan nama fail, `lang="ms"`, dan semua rujukan tempatan — jangan sunting kandungan pada langkah ini.

- [ ] **Step 4: Ulang ujian asas**

Run: `powershell -File C:\Users\MKAW\AppData\Local\Temp\opencode\verify_publish_base.ps1`
Expected: `BASE OK`.

- [ ] **Step 5: Commit asas**

```powershell
git add landing-page/index.html
git commit -m "feat: guna reka bentuk Pro sebagai landing page utama"
```

---

### Task 2: Pulihkan modal Lesen Data dan Biodata Penerbit

**Files:**
- Modify: `landing-page/index.html` (footer ≈ baris 1040, sebelum `</footer>`; CSS sebelum blok `@media`; JS selepas IIFE popup 7-Zip ≈ baris 1198; `I18N.en` ≈ baris 1164)

**Interfaces:**
- Consumes: `index-live-before.html` — salinan Task 1 sebagai sumber blok CSS `lic-*`/`bio-*`, markup `#licModal`/`#bioModal`, handler `licBuka()`/`bioBuka()`, dan nilai `TRANS.en` untuk kunci `lic-*`, `bio-*`, `foot-*`.
- Produces: `#licLink`, `#bioLink`, `#licModal`, `#bioModal`, `#licClose`, `#bioClose`, kunci EN `f-lic`, `f-bio`, `lic-*`, `bio-*`.

- [ ] **Step 1: Tulis ujian gagal**

Cipta `C:\Users\MKAW\AppData\Local\Temp\opencode\check_modals.js`:

```js
(() => {
  const ids=['licLink','bioLink','licModal','bioModal','licClose','bioClose'];
  const missing=ids.filter(id=>!document.getElementById(id));
  const dup=[...document.querySelectorAll('[id]')].map(e=>e.id)
    .filter((id,i,a)=>a.indexOf(id)!==i);
  return {missing, dup};
})()
```

Run melalui `tools.browser.evaluate` pada tab `mockup-pro.html`/`index.html` tempatan.
Expected: FAIL — `missing` mengandungi kesemua enam ID.

- [ ] **Step 2: Tambah CSS dan markup modal**

- Salin blok CSS dari `index-live-before.html` untuk selector `.lic-modal`, `.lic-card`, `.lic-x`, `.lic-rows`, `.lic-row`, `.lic-note`, `.bio-top`, `.bio-foto`, `.bio-id`, `.bio-links`, `.bio-quote`, `.bio-row`, `.bio-stats` ke dalam `<style>` `index.html`. Jangan salin selector lain.
- Tambah dua `<li>` dalam senarai footer `ft4` (Sumber): `<a href="#" id="licLink" data-i18n="f-lic">Lesen Data</a>` dan `<a href="#" id="bioLink" data-i18n="f-bio">Biodata Penerbit</a>`.
- Salin markup modal dari `index-live-before.html` baris 913–950 tepat sebelum `<script>` penutup; kekalkan ID, `data-i18n`, dan kandungan `M.K.A.W`.

- [ ] **Step 3: Tambah handler dan terjemahan EN**

- Salin handler buka/tutup dari `index-live-before.html` (`licBuka`, `licTutup`, `bioBuka`, `bioTutup`, pendengar klik `#licLink`/`#bioLink`/`#licClose`/`#bioClose`) ke dalam `<script>`, selepas IIFE popup 7-Zip.
- Tambah kunci EN berikut ke `I18N.en`: `f-lic`, `f-bio`, dan semua kunci `data-i18n` yang digunakan dalam dua modal itu (nilai disalin dari `TRANS.en` dalam fail rujukan).

- [ ] **Step 4: Ulang ujian kehadiran**

Run: `tools.browser.evaluate` dengan skrip Step 1.
Expected: `{missing: [], dup: []}`.

- [ ] **Step 5: Ujian tingkah laku MS dan EN**

Run: `tools.browser.evaluate`:

```js
(async () => {
  const click = id => document.getElementById(id).click();
  click('licLink'); const licMS = document.getElementById('licModal').getAttribute('aria-hidden') !== 'true';
  click('licClose'); const licClosed = document.getElementById('licModal').getAttribute('aria-hidden') === 'true';
  click('bioLink'); const bioMS = document.getElementById('bioModal').getAttribute('aria-hidden') !== 'true';
  click('bioClose'); const bioClosed = document.getElementById('bioModal').getAttribute('aria-hidden') === 'true';
  document.querySelector('[data-lang="en"]').click();
  await new Promise(r => setTimeout(r, 400));
  click('licLink'); const licEN = document.getElementById('licModal').getAttribute('aria-hidden') !== 'true';
  return {licMS, licClosed, bioMS, bioClosed, licEN, title: document.getElementById('licTitle').textContent};
})()
```

Expected: semua `true`, `title` bermula `Data &amp; Software License` atau `Data & Software License`. Tiada ralat konsol.

- [ ] **Step 6: Commit**

```powershell
git add landing-page/index.html
git commit -m "fix: pulihkan modal lesen dan biodata penerbit"
```

---

### Task 3: Pulihkan borang hubungi `mailto:`

**Files:**
- Modify: `landing-page/index.html` (form ≈ baris 999; `<script>` selepas handler modal)

**Interfaces:**
- Consumes: borang mockup dengan tiga `<input>`/`<textarea>` tanpa `name`; `I18N.en` kunci `f-n`, `f-s`, `f-m`, `f-b` sudah ada.
- Produces: fungsi global `buildMailto(form)` → `string` URL `mailto:info2@pustakahadith.my?subject=...&body=...`.

- [ ] **Step 1: Tulis ujian gagal**

Run: `tools.browser.evaluate`:

```js
(() => ({
  hasFn: typeof window.buildMailto === 'function',
  form: document.querySelector('#hubungi form')?.getAttribute('onsubmit')
}))()
```

Expected: `hasFn: false`, `form` mengandungi `Terima kasih` (bukan `mailto:`).

- [ ] **Step 2: Tambah atribut `name` dan fungsi `buildMailto`**

- Pada borang `#hubungi form`, beri `name="name"`, `name="subject"`, `name="message"` pada tiga kawalan berturutan; tukar `onsubmit` kepada `event.preventDefault();window.location.href=buildMailto(this)`.
- Takrifkan di `<script>`: `window.buildMailto=function(form){ ... }` yang membaca `form.elements.name/subject/message.value`, membina `subject` = subjek, `body` = `'Nama: ' + nama + '%0A%0A' + mesej`, dan return `'mailto:info2@pustakahadith.my?subject=' + encodeURIComponent(subjek) + '&body=' + encodeURIComponent(body)`.

- [ ] **Step 3: Ulang ujian kehadiran**

Run: skrip Step 1.
Expected: `hasFn: true`, `form` mengandungi `buildMailto(this)`.

- [ ] **Step 4: Ujian pengekodan**

Run: `tools.browser.evaluate`:

```js
(() => {
  const f=document.querySelector('#hubungi form');
  f.elements.name.value='Ali & Co';
  f.elements.subject.value='Hadis 1/2';
  f.elements.message.value='Assalamualaikum\nSaya ±70 tahun';
  const u=buildMailto(f);
  return {u, ok:u.startsWith('mailto:info2@pustakahadith.my?subject=Hadis%201%2F2&body=')
    && u.includes('Ali%20%26%20Co') && !/\s|\+/.test(u.split('body=')[1])};
})()
```

Expected: `ok: true` (tiada ruang kosong atau `+` mentah dalam badan; `&`, `/`, newline dan `±` dikodkan).

- [ ] **Step 5: Commit**

```powershell
git add landing-page/index.html
git commit -m "fix: borang hubungi hantar melalui mailto"
```

---

### Task 4: Komit tujuh kover yang dikemas kini

**Files:**
- Modify: `landing-page/img/abudaud-ro.png`, `landing-page/img/tirmizi-ro.png`, `landing-page/img/nasai-ro.png`, `landing-page/img/iibn-majah-ro.png`, `landing-page/img/ahmad-ro.png`, `landing-page/img/darimi-ro.png`, `landing-page/img/malik-ro.png` — tujuh PNG yang belum dikomit. `bukh-flat.png` dan `muslim-flat.png` sudah dikomit.

**Interfaces:**
- Consumes: perubahan working-tree sedia ada pada tujuh PNG (jangan jana semula, jangan ubah piksel).
- Produces: kesembilan-sembilan kover berada dalam HEAD.

- [ ] **Step 1: Semak senarai tepat sebelum `git add`**

Run: `git status --short -- landing-page/img`
Expected: tujuh baris ` M landing-page/img/*-ro.png` untuk `abudaud`, `tirmizi`, `nasai`, `iibn-majah`, `ahmad`, `darimi`, `malik`. `bukh-flat.png` dan `muslim-flat.png` tidak muncul (sudah dikomit).

- [ ] **Step 2: Stage eksplisit dan commit**

```powershell
git add landing-page/img/abudaud-ro.png landing-page/img/tirmizi-ro.png landing-page/img/nasai-ro.png landing-page/img/iibn-majah-ro.png landing-page/img/ahmad-ro.png landing-page/img/darimi-ro.png landing-page/img/malik-ro.png
git commit -m "chore: kemas kini tujuh kover kitab sedia ada"
```

- [ ] **Step 3: Verifikasi integriti kover dalam pelayar**

Run: `tools.browser.evaluate` selepas reload `index.html`:

```js
(() => {
  const imgs=[...document.querySelectorAll('.rak .book img')];
  return {count:imgs.length, bad:imgs.filter(i=>i.naturalWidth!==512||i.naturalHeight!==512).map(i=>i.src)};
})()
```

Expected: `count: 9`, `bad: []`, 0 ralat konsol.

Semak juga tiada rujukan tempatan rosak:

```powershell
$t = Get-Content 'landing-page\index.html' -Raw
$m = [regex]::Matches($t,'(?:src|href)="([^"#][^"]*)"') | ForEach-Object { $_.Groups[1].Value } | Where-Object { $_ -notmatch '^(https?:|mailto:|data:|tel:)' } | Sort-Object -Unique
$m | Where-Object { -not (Test-Path (Join-Path 'landing-page' $_)) }
```

Expected: tiada baris output.

---

### Task 5: Push dan sahkan laman live

**Files:** tiada perubahan fail.

**Interfaces:**
- Consumes: HEAD dengan `index.html` + 9 kover + tujuh PNG komit.
- Produces: `origin/main` sepadan dengan `main`; `https://pustakahadith.my` memaparkan reka bentuk baru.

- [ ] **Step 1: Push**

```powershell
git push origin main
```

Expected: `main -> main` tanpa `--force`.

- [ ] **Step 2: Sahkan deploy**

Run: `webfetch https://pustakahadith.my` (format `text`) dan `git status -sb`.
Expected: teks mengandungi `Muat Turun 7-Zip`, `Lesen Data`, `Biodata Penerbit`, `info2@pustakahadith.my`; `## main...origin/main` tanpa `ahead`/`behind`.

Jika penanda belum muncul selepas 1–2 minit, **jangan** cuba push semula atau force — laporkan status deploy dan minta arahan.

- [ ] **Step 3: Rekod keputusan**

Tambah ringkasan (commit, status deploy, sebarang ruling) ke `.superpowers/sdd/2026-11-28-publish-landing-pro/progress.md` (cipta folder jika perlu). Jangan commit ledger ini melainkan pengguna minta.
