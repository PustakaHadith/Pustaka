# Cloudflare Configuration — pustakahadith.my

## Overview

Landing page for PustakaHadith, hosted on **Cloudflare Pages**.

---

## DNS

| Type | Name | Content | Proxy | TTL |
|------|------|---------|-------|-----|
| CNAME | @ | pustakahadith-landing.pages.dev | Proxied | Auto |
| A | www | 98.84.224.111 | Proxied | Auto |
| A | www | 18.208.88.157 | Proxied | Auto |

### Nota tentang www record

`www.pustakahadith.my`指向 AWS IPs (bukan Cloudflare Pages). Ini mungkin dari sebelum migrasi. Jika www tidak digunakan, boleh padam atau tukar ke CNAME yang sama.

- **Nameservers:** `cloe.ns.cloudflare.com`, `quinton.ns.cloudflare.com` (managed by Cloudflare)
- **DNSSEC:** Unknown (check dashboard)
- **Zone ID:** `7b22ed68b5881974026cab24753c708f`
- **Account ID:** `f35c6dc99de15aa8979d2a15a004bd39`

## Email (MX Records — Zoho)

| Priority | Host | Mail Server |
|----------|------|-------------|
| 10 | @ | mx.zoho.com |
| 20 | @ | mx2.zoho.com |
| 50 | @ | mx3.zoho.com |

- Email address: `info2@pustakahadith.my`
- Email provider: **Zoho Mail**

## SSL/TLS

| Setting | Nilai | Status |
|---|---|---|
| SSL Mode | Full | ✅ OK |
| Always Use HTTPS | ON | ✅ Siap (22 Sep 2026) |
| Minimum TLS Version | 1.2 | ✅ Siap (22 Sep 2026) |
| TLS 1.3 | ON | ✅ OK |

## Cloudflare Pages

- **Project Name:** `pustakahadith-my` (check Cloudflare dashboard for exact name)
- **Production Branch:** `main`
- **Build Command:** None (static site — just `index.html` + images)
- **Output Directory:** `/` (root of `landing-page/` folder)
- **Custom Domain:** `pustakahadith.my`
- **GitHub Repo:** `https://github.com/PustakaHadith/Pustaka.git`
- **Local Folder:** `D:\Pustaka Quran Hadis\Pustaka\landing-page\`

### Deployment Method — Direct API & GitHub
- **Priority Method**: Direct API Deployment (via User API Token)
- **Fallback Method**: GitHub Auto-Deploy (`main` branch)
- **Project Name**: `pustakahadith-my` / `pustakahadith-landing`
- **API Token**: `cfut_sJUym...` (Stored in session)
- **GitHub Repo**: `https://github.com/PustakaHadith/Pustaka.git`

Untuk semak GitHub connection: Cloudflare Dashboard → Pages → `pustakahadith-landing` → Settings → "Continuous deployment"

---

## Cara Deploy (GitHub Auto-Deploy)

Cloudflare Pages project `pustakahadith-landing` kemungkinan connected ke GitHub.

```powershell
# 1. Pergi ke folder landing page
cd "D:\Pustaka Quran Hadis\Pustaka\landing-page"

# 2. Commit perubahan
git add -A
git commit -m "Kemas kini: [deskripsi perubahan]"

# 3. Push ke GitHub — Cloudflare auto-deploy
git push origin main

# 4. Semak status deploy di Cloudflare Dashboard → Pages → Deployments
# 5. Verifikasi di https://pustakahadith.my selepas 1-2 minit
```

### Jika auto-deploy tidak berfungsi:

```powershell
# Semak remote git
git remote -v

# Jika remote salah, set semula
git remote set-url origin https://github.com/PustakaHadith/Pustaka.git

# Force push jika perlu
git push origin main --force
```

### Jika perlu deploy manual (fallback):

1. Pergi ke https://dash.cloudflare.com
2. Pages → `pustakahadith-landing` → **Create deployment**
3. Upload folder `D:\Pustaka Quran Hadis\Pustaka\landing-page\`
4. Tunggu ~30 saat

---

## Repository Structure

```text
D:\Pustaka Quran Hadis\Pustaka\landing-page\
├── index.html              ← Halaman utama (dwibahasa MS/EN)
├── manifest.json           ← PWA manifest
├── favicon.ico
├── apple-touch-icon.png
├── logo.jpg
├── img/                    ← Screenshot & logo
│   ├── app-home.webp
│   ├── app-9kitab.webp
│   ├── app-senarai.webp
│   ├── app-carian.webp
│   ├── app-detail.webp
│   ├── bg-globe.webp
│   └── logo.png
├── redirect/               ← .htaccess untuk redirect lama
├── SESI.md                 ← Rekod sesi landing page
├── cloudflare.md           ← Fail ini
└── FACEBOOK_POST.md        ← Kandungan promosi
```

---

## Cache Rules

- `cf-cache-status: DYNAMIC` — Cloudflare does not cache HTML by default
- Images (`img/`): Cache-Control `public, max-age=0, must-revalidate` (browser only; Cloudflare edge may cache based on tier)
- NEL (Network Error Logging) is enabled: `report_to: cf-nel`

## Security Headers

| Header | Value |
|--------|-------|
| `Access-Control-Allow-Origin` | `*` |
| `x-content-type-options` | `nosniff` |
| `referrer-policy` | `strict-origin-when-cross-origin` |
| `Cache-Control` | `public, max-age=0, must-revalidate` |

## Page Rules (if any)

Check Cloudflare dashboard for any page rules (e.g., cache level, security level per path).

## Workers / Functions

None configured.

## Redirects (Old Domain)

- Old domain `pustakahadith.netlify.app` → redirect to `pustakahadith.my` (handled separately via Netlify `.htaccess` in `redirect/` folder)

---

## How to Access Cloudflare Dashboard

1. Go to https://dash.cloudflare.com
2. Login with your Cloudflare account
3. Select domain: `pustakahadith.my`
4. Pages section: check project name, deployment history, custom domains

---

## Deployment Checklist

Apabila mengemas kini landing page:

- [ ] Edit fail dalam `landing-page/` folder
- [ ] Pastikan `index.html` tidak rosak (buka di browser untuk semak)
- [ ] Commit dan push (auto-deploy) ATAU upload manual
- [ ] Tunggu 1-2 minit untuk Cloudflare propagate
- [ ] Verifikasi di `https://pustakahadith.my`
- [ ] Semak mobile responsive (burger menu < 980px)
- [ ] Update `SESI.md` dalam folder landing-page juga

---

*Last updated: Sesi 32*
