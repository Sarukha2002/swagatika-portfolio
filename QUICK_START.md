# 🚀 Quick Start: Deploy Your Portfolio in 15 Minutes

---

## **Step 1: Prepare Your Files (2 min)**

### Create folder structure:
```
portfolio-root/
├── index.html                    (your portfolio file)
├── robots.txt                    (provided)
├── sitemap.xml                   (provided)
├── vercel.json                   (if using Vercel)
├── _redirects                    (if using Netlify)
├── _headers                      (if using Netlify)
└── public/assets/
    ├── resume.pdf                (your resume)
    └── og-image.png              (1200x630 for social media)
```

### Files you received:
- ✅ `DEPLOYMENT_README.md` — Full setup guide
- ✅ `QUICK_START.md` — This file
- ✅ `ANALYTICS_SETUP.md` — Analytics configuration
- ✅ `PERFORMANCE_OPTIMIZATION.md` — Speed checklist
- ✅ `HTML_CODE_SNIPPETS.md` — Code templates
- ✅ `robots.txt` — Copy to root
- ✅ `sitemap.xml` — Copy to root
- ✅ `vercel.json` — Copy to root (Vercel only)
- ✅ `_redirects` — Copy to root (Netlify only)
- ✅ `_headers` — Copy to root (Netlify only)

---

## **Step 2: Update Your HTML (3 min)**

### In `index.html`:

**Find and replace this line (line 7):**
```html
<meta name="description" content="Swagatika Arukha — Senior Technical Product Manager...">
```

**Replace all instances of `my-portfolio.com` with your actual domain:**

1. Open Find & Replace (Ctrl+H or Cmd+H)
2. Find: `my-portfolio.com`
3. Replace with: `your-domain.com` (e.g., `swagatika-arukha.com`)
4. Click "Replace All"

**Add favicon to `<head>` (line 40, after `<title>`)**:
```html
<!-- Inline SVG Favicon -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%236575DE' width='100' height='100'/><text x='50%' y='50%' dominant-baseline='middle' text-anchor='middle' fill='%23F6F2E7' font-size='60' font-weight='bold' font-family='monospace'>&gt;_</text></svg>" type="image/svg+xml">
```

**Add analytics before closing `</body>` (line 841)**:
```html
<!-- Plausible Analytics -->
<script defer data-domain="your-domain.com" src="https://plausible.io/js/script.js"></script>

<!-- Custom Event Telemetry -->
<script>
  // [Copy full script from HTML_CODE_SNIPPETS.md — SNIPPET 6]
</script>
```

---

## **Step 3: Create Asset Files (2 min)**

### Create `/public/assets/` folder with:

1. **resume.pdf** — Your actual resume
2. **og-image.png** — 1200x630px image for social sharing
   - Include: Your name, headline, key stats
   - Use Figma, Canva, or Photoshop

### If you don't have og-image yet:
Use this temporary placeholder (update later):
```html
<meta property="og:image" content="https://via.placeholder.com/1200x630?text=Swagatika+Arukha">
```

---

## **Step 4: Push to GitHub (3 min)**

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial portfolio setup"

# Rename to main branch (optional)
git branch -M main

# Add remote
git remote add origin https://github.com/YOUR_USERNAME/portfolio.git

# Push
git push -u origin main
```

---

## **Step 5: Choose Your Platform (3 min)**

### **Option A: Vercel (Recommended)**

1. Go to [vercel.com](https://vercel.com)
2. Sign in with GitHub
3. Click "New Project"
4. Select your `portfolio` repository
5. **Build settings:** Leave as default (no build needed)
6. Click "Deploy"
7. After deployment → "Domains" → Add your custom domain

**File needed:** `vercel.json` ✅

---

### **Option B: Netlify**

1. Go to [netlify.com](https://netlify.com)
2. Click "New site from Git"
3. Connect GitHub account
4. Select `portfolio` repository
5. **Build command:** Leave blank
6. **Publish directory:** `.` (root)
7. Click "Deploy site"
8. Settings → Domain → Add custom domain

**Files needed:** `_redirects`, `_headers` ✅

---

### **Option C: GitHub Pages (Free, No Setup)**

1. Create repo named `username.github.io`
2. Push files to `main` branch
3. Settings → Pages → Source: main, directory: root
4. Add custom domain in DNS settings

**Note:** GitHub Pages doesn't support `_redirects`. `/resume` redirect won't work automatically.

---

## **Step 6: Configure Custom Domain (2 min)**

### In your domain registrar (GoDaddy, Namecheap, etc.):

**For Vercel:**
1. Copy nameservers from Vercel dashboard
2. In registrar, update nameservers to Vercel's

**For Netlify:**
1. Copy nameservers from Netlify dashboard
2. In registrar, update nameservers to Netlify's

**For GitHub Pages:**
1. Create CNAME file in root: `username.github.io`
2. Add DNS record: `CNAME → your-domain.com → username.github.io`

---

## **Step 7: Set Up Analytics (1 min)**

1. Go to [plausible.io](https://plausible.io)
2. Sign up → Start free trial
3. Add website: `your-domain.com`
4. Copy tracking script
5. Paste in your HTML `<head>` (should already be there with domain replaced)
6. Deploy

Analytics will start collecting data immediately (no setup needed).

---

## **Step 8: Verify & Test (1 min)**

After deployment:

- ✅ Visit your domain: `https://your-domain.com`
- ✅ Check favicon loads (appears in browser tab)
- ✅ Open Console (F12) → Should see telemetry initialization log
- ✅ Click "Email Me" button → Should log `[Telemetry] Event tracked: email-click`
- ✅ Test `/resume` redirect → Should download PDF

---

## **Step 9: Run PageSpeed Test (1 min)**

1. Go to [pagespeed.web.dev](https://pagespeed.web.dev)
2. Enter your domain
3. Wait for report (30-60 seconds)
4. Check:
   - ✅ Mobile score ≥ 90
   - ✅ Desktop score ≥ 95
   - ✅ Core Web Vitals all green

---

## **Troubleshooting**

### **Domain not working?**
- Wait 24-48 hours for DNS propagation
- Test: `nslookup your-domain.com`

### **Resume download not working?**
- Check `/public/assets/resume.pdf` exists
- Verify `vercel.json` or `_redirects` is deployed
- Test manually: `https://your-domain.com/assets/resume.pdf`

### **Analytics not tracking?**
- Check Console: `F12 → Console`
- Should see: `✓ [Telemetry] Portfolio analytics initialized`
- Wait 30 seconds, refresh Plausible dashboard

### **PageSpeed score below 90?**
- Run Lighthouse locally: `https://pagespeed.web.dev`
- Common issues:
  - Images missing `width`/`height` (see PERFORMANCE_OPTIMIZATION.md)
  - Render-blocking scripts (check for missing `defer`)
  - Check _Complete File Manifest_ in DEPLOYMENT_README.md

---

## **Next Steps (After Deployment)**

1. **Google Search Console:**
   - Add property at [search.google.com/search-console](https://search.google.com/search-console)
   - Verify ownership via DNS
   - Submit sitemap: `https://your-domain.com/sitemap.xml`

2. **Update Content:**
   - Replace article placeholders in #writing section
   - Update projects section with real examples
   - Add headshot and project images

3. **Monitor:**
   - Check Plausible dashboard weekly
   - Monitor PageSpeed score monthly
   - Review Search Console for indexing status

---

## **Files Checklist**

| File | Location | Deploy? |
|------|----------|---------|
| index.html | root | ✅ |
| robots.txt | root | ✅ |
| sitemap.xml | root | ✅ |
| vercel.json | root | ✅ (Vercel) |
| _redirects | root | ✅ (Netlify) |
| _headers | root | ✅ (Netlify) |
| resume.pdf | public/assets/ | ✅ |
| og-image.png | public/assets/ | ✅ |

---

## **Support Resources**

- **Vercel Docs:** https://vercel.com/docs
- **Netlify Docs:** https://docs.netlify.com
- **Plausible Setup:** https://plausible.io/docs
- **PageSpeed Insights:** https://pagespeed.web.dev
- **Google Search Console:** https://search.google.com/search-console

---

## **You're Done! 🎉**

Your portfolio is now live, optimized, and ready to impress recruiters.

**Key metrics:**
- ✅ 95+ PageSpeed score
- ✅ GDPR-compliant analytics
- ✅ Secure headers
- ✅ SEO optimized
- ✅ Mobile responsive

Next: Update your LinkedIn and email it to your network! 🚀

---

**Questions?** See the full guide in `DEPLOYMENT_README.md`
