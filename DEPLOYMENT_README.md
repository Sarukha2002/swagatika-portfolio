# Portfolio Deployment Guide
## Production-Grade Setup for Swagatika Arukha's Technical PM Portfolio

---

## 📋 **Table of Contents**
1. [Project Structure](#project-structure)
2. [Platform-Specific Deployment Steps](#platform-specific-deployment-steps)
3. [Configuration Files Included](#configuration-files-included)
4. [HTML Head Element Updates](#html-head-element-updates)
5. [Analytics & Telemetry Integration](#analytics--telemetry-integration)
6. [Performance Optimization Checklist](#performance-optimization-checklist)
7. [Testing & Validation](#testing--validation)

---

## 🗂️ **Project Structure**

Before deployment, organize your files as follows:

```
portfolio-root/
├── index.html                    (your main portfolio file)
├── robots.txt                    (SEO crawl configuration)
├── sitemap.xml                   (XML sitemap for search engines)
├── vercel.json                   (Vercel deployment config)
├── _redirects                    (Netlify redirects)
├── _headers                      (Netlify headers & security)
├── public/                       (optional folder for assets)
│   ├── assets/
│   │   └── resume.pdf            (your resume file)
│   └── images/
│       └── headshot.png          (optional: profile image)
└── .gitignore                    (if using Git)
```

**Note:** If deploying to **Vercel**, the configuration goes in `vercel.json`.  
If deploying to **Netlify**, use `_redirects` and `_headers` files.

---

## 🚀 **Platform-Specific Deployment Steps**

### **Option A: Vercel Deployment**

#### Prerequisites:
- GitHub account (recommended for CI/CD)
- Vercel account (free tier available)

#### Steps:

1. **Push your portfolio to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial portfolio commit"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/portfolio.git
   git push -u origin main
   ```

2. **Connect to Vercel:**
   - Go to [vercel.com](https://vercel.com)
   - Click "New Project"
   - Select "Import Git Repository"
   - Choose your portfolio repository
   - Leave build settings as default (static HTML doesn't need a build step)
   - Click "Deploy"

3. **Configure domain:**
   - After deployment, go to Project Settings → Domains
   - Add your custom domain (e.g., `swagatika-arukha.com`)
   - Follow DNS instructions from your registrar

4. **Verify deployment:**
   - Visit your deployed site
   - Run PageSpeed Insights: `https://pagespeed.web.dev`
   - Check network tab for waterfall performance

---

### **Option B: Netlify Deployment**

#### Prerequisites:
- GitHub account
- Netlify account (free tier available)

#### Steps:

1. **Push portfolio to GitHub** (same as above)

2. **Connect to Netlify:**
   - Go to [netlify.com](https://netlify.com)
   - Click "New site from Git"
   - Connect GitHub and select repository
   - Build settings:
     - **Build command:** (leave blank for static HTML)
     - **Publish directory:** `.` (root of repo)
   - Click "Deploy site"

3. **Configure domain:**
   - Go to Domain settings
   - Add your custom domain
   - Follow DNS setup guide

4. **Verify deployment:**
   - Visit deployed site
   - Check that `_headers` and `_redirects` are being applied (see Network tab)
   - Run PageSpeed Insights

---

### **Option C: GitHub Pages (Free, No Build Required)**

#### Steps:

1. **Push to GitHub:**
   - Create repository named `username.github.io`
   - Push files to main branch

2. **Enable Pages:**
   - Go to repository Settings → Pages
   - Source: Deploy from branch
   - Branch: main, directory: root
   - Save

3. **Add custom domain:**
   - Settings → Pages → Custom domain
   - Enter your domain
   - Add CNAME record to your DNS provider

**Note:** GitHub Pages does NOT support `_redirects` or Netlify `_headers`. Use `vercel.json` approach or manual HTML redirects.

---

## 📄 **Configuration Files Included**

This package contains the following files (see detailed sections below):

| File | Platform | Purpose |
|------|----------|---------|
| `robots.txt` | All | Crawl directives for search engines |
| `sitemap.xml` | All | XML sitemap for indexing |
| `vercel.json` | Vercel only | Security headers & redirects |
| `_redirects` | Netlify only | Route rewrites & redirects |
| `_headers` | Netlify only | HTTP security headers & caching |
| `favicon.inline.svg` | All | Inline SVG favicon snippet (paste in `<head>`) |
| `analytics.snippet.js` | All | Lightweight Plausible Analytics setup |
| `events.telemetry.js` | All | Custom event tracking for buttons |
| `html-head-updates.md` | All | Complete `<head>` replacement guide |
| `pagespeed-optimization.md` | All | Performance checklist for 95+ score |

---

## 🎨 **HTML Head Element Updates**

### **Step 1: Replace Your `<head>` Section**

Open `index.html` and replace lines **3–82** (the entire `<head>` section) with the optimized version below. This includes:
- Favicon as inline SVG
- Preconnect directives for Google Fonts
- Meta tags for SEO
- Tailwind CSS from CDN
- Style optimizations
- Analytics snippet

```html
<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Swagatika Arukha — Senior Technical Product Manager | Platform Engineering & AI</title>
<meta name="description" content="Swagatika Arukha — Senior Technical Product Manager. Platform engineering, DEM, Session Replay, micro frontends, AI recommendation systems. $2M+ ARR influenced, 100M+ users served. Based in Chicago.">
<meta name="keywords" content="product manager, platform engineering, DEM, telemetry, AI infrastructure, Chicago, technical PM">
<meta name="author" content="Swagatika Arukha">

<!-- Open Graph (Social Media) -->
<meta property="og:title" content="Swagatika Arukha — Senior Technical Product Manager">
<meta property="og:description" content="Platform engineering, DEM, AI infrastructure. $2M+ ARR influenced, 100M+ users served.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://my-portfolio.com">
<meta property="og:image" content="https://my-portfolio.com/assets/og-image.png">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Swagatika Arukha — Senior Technical PM">
<meta name="twitter:description" content="Platform engineering, AI infrastructure, 100M+ users.">
<meta name="twitter:image" content="https://my-portfolio.com/assets/og-image.png">
<meta name="twitter:creator" content="@swagatika_arukha">

<!-- Canonical URL (important for SEO) -->
<link rel="canonical" href="https://my-portfolio.com">

<!-- Favicon (Inline SVG - replaces external file) -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%236575DE' width='100' height='100'/><text x='50%' y='50%' dominant-baseline='middle' text-anchor='middle' fill='%23F6F2E7' font-size='60' font-weight='bold' font-family='system-ui'>&gt;_</text></svg>" type="image/svg+xml">

<!-- Preconnect to external resources (critical for performance) -->
<link rel="preconnect" href="https://fonts.googleapis.com" crossorigin>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="dns-prefetch" href="https://cdn.tailwindcss.com">

<!-- Google Fonts (with minimal variants for performance) -->
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@500;600;700;800;900&family=Inter:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Source+Serif+4:ital,opsz,wght@1,8..60,400;1,8..60,500&display=swap" rel="stylesheet">

<!-- Tailwind CSS (defer loading to reduce CLS) -->
<script defer src="https://cdn.tailwindcss.com"></script>

<!-- Tailwind config (must be loaded synchronously, before Tailwind CSS renders) -->
<script>
  tailwind.config = {
    theme: {
      extend: {
        colors: {
          cream:    '#F6F2E7',
          ink:      '#1E1B16',
          soft:     '#57524A',
          lavender: '#CFC2F0',
          tan:      '#EADDBE',
          rose:     '#DCA3AE',
          sky:      '#ABD4E4',
          peri:     '#6575DE',
          periDeep: '#4C5BC2'
        },
        fontFamily: {
          display: ['Archivo', 'system-ui', 'sans-serif'],
          body:    ['Inter', 'system-ui', 'sans-serif'],
          serif:   ['"Source Serif 4"', 'Georgia', 'serif']
        },
        boxShadow: {
          pop:  '5px 6px 0 0 #1E1B16',
          popSm:'3px 4px 0 0 #1E1B16'
        }
      }
    }
  }
</script>

<!-- Critical CSS (inline to prevent render blocking) -->
<style>
  html { scroll-padding-top: 96px; }
  body { -webkit-font-smoothing: antialiased; }
  ::selection { background: #CFC2F0; color: #1E1B16; }

  .hero-wash {
    background: linear-gradient(180deg,
      #F6F2E7 0%, #F6F2E7 42%, #F0E7EC 68%, #E4DCF2 88%, #DCE4F0 100%);
  }

  .marquee { overflow: hidden; white-space: nowrap; }
  .marquee-track {
    display: inline-flex; align-items: center;
    width: max-content;
    animation: scroll-left 36s linear infinite;
  }
  .marquee-track.reverse { animation: scroll-right 42s linear infinite; }
  .marquee:hover .marquee-track { animation-play-state: paused; }
  @keyframes scroll-left  { from { transform: translateX(0); }    to { transform: translateX(-50%); } }
  @keyframes scroll-right { from { transform: translateX(-50%); } to { transform: translateX(0); } }
  @media (prefers-reduced-motion: reduce) {
    .marquee-track, .marquee-track.reverse { animation: none !important; }
    .marquee { overflow-x: auto; }
  }

  .reveal { opacity: 0; transform: translateY(12px); transition: opacity 550ms ease, transform 550ms ease; }
  .reveal.in { opacity: 1; transform: none; }
  @media (prefers-reduced-motion: reduce) {
    html { scroll-behavior: auto !important; }
    .reveal { opacity: 1 !important; transform: none !important; transition: none !important; }
  }

  .acc-body { display: grid; grid-template-rows: 0fr; transition: grid-template-rows 260ms ease; }
  .acc-body > div { overflow: hidden; }
  .acc-body.open { grid-template-rows: 1fr; }
  .acc-chev { transition: transform 200ms ease; display: inline-block; }
  .acc-btn[aria-expanded="true"] .acc-chev { transform: rotate(90deg); }

  a:focus-visible, button:focus-visible { outline: 3px solid #6575DE; outline-offset: 3px; border-radius: 4px; }
  .skip-link { position: absolute; left: -9999px; }
  .skip-link:focus { left: 16px; top: 16px; z-index: 100; background: #1E1B16; color: #F6F2E7; padding: 10px 16px; }
</style>

<!-- Lightweight Analytics (Plausible) - Non-blocking, loaded async -->
<script defer data-domain="my-portfolio.com" src="https://plausible.io/js/script.js"></script>

<!-- Structured Data (JSON-LD for SEO) -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Swagatika Arukha",
  "jobTitle": "Senior Technical Product Manager",
  "url": "https://my-portfolio.com",
  "sameAs": [
    "https://linkedin.com/in/swagatikaarukha",
    "https://github.com/Sarukha2002"
  ],
  "knowsAbout": [
    "Platform Engineering",
    "DEM",
    "Session Replay",
    "AI Infrastructure",
    "Telemetry",
    "Experimentation Platforms"
  ]
}
</script>

</head>
```

---

## 📊 **Analytics & Telemetry Integration**

### **Step 2: Add Lightweight Analytics Snippet**

Add this script **before the closing `</body>` tag** in your `index.html`:

```html
<!-- Lightweight Analytics Script (Plausible) -->
<script defer data-domain="my-portfolio.com" src="https://plausible.io/js/script.js"></script>

<!-- Custom Event Telemetry Tracker -->
<script>
  // Configuration
  const ANALYTICS_CONFIG = {
    trackingEnabled: typeof window.plausible !== 'undefined',
    events: {
      RESUME_DOWNLOAD: 'resume-download',
      EMAIL_CLICK: 'email-click',
      LINKEDIN_CLICK: 'linkedin-click',
      GITHUB_CLICK: 'github-click'
    }
  };

  // Track custom events
  function trackEvent(eventName, data = {}) {
    if (ANALYTICS_CONFIG.trackingEnabled && window.plausible) {
      window.plausible(eventName, { props: data });
      console.log(`[Telemetry] Event tracked:`, eventName, data);
    } else {
      console.warn(`[Telemetry] Analytics not available or disabled. Event: ${eventName}`);
    }
  }

  // Bind to Resume Download (if exists)
  const resumeLink = document.querySelector('a[href*="resume"]');
  if (resumeLink) {
    resumeLink.addEventListener('click', (e) => {
      trackEvent(ANALYTICS_CONFIG.events.RESUME_DOWNLOAD, {
        referrer: document.referrer || 'direct',
        timestamp: new Date().toISOString()
      });
    });
  }

  // Bind to Email link
  const emailLink = document.querySelector('a[href^="mailto:"]');
  if (emailLink) {
    emailLink.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.EMAIL_CLICK, {
        action: 'email-initiated',
        timestamp: new Date().toISOString()
      });
    });
  }

  // Bind to Social Links
  const linkedinLink = document.querySelector('a[href*="linkedin"]');
  if (linkedinLink) {
    linkedinLink.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.LINKEDIN_CLICK, {
        platform: 'linkedin',
        timestamp: new Date().toISOString()
      });
    });
  }

  const githubLink = document.querySelector('a[href*="github"]');
  if (githubLink) {
    githubLink.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.GITHUB_CLICK, {
        platform: 'github',
        timestamp: new Date().toISOString()
      });
    });
  }

  // Console logging for verification (remove in production if desired)
  console.log('[Telemetry] Tracking initialized. Events: ', ANALYTICS_CONFIG.events);
</script>
```

**What this does:**
- ✅ Tracks "Download Resume" clicks
- ✅ Tracks "Email Me" clicks
- ✅ Tracks LinkedIn/GitHub link visits
- ✅ Logs events to Plausible Analytics
- ✅ Outputs console messages for debugging

---

## ⚡ **Performance Optimization Checklist**

### **For 95+ PageSpeed Insights Score:**

#### **1. Image Optimization (CLS Prevention)**

If you add images to your portfolio, always include `width`, `height`, and `loading` attributes:

```html
<!-- ✅ CORRECT: With dimensions to prevent layout shift -->
<img 
  src="/assets/headshot.png" 
  alt="Swagatika Arukha headshot" 
  width="400" 
  height="400" 
  loading="lazy"
  decoding="async"
  class="rounded-2xl"
>

<!-- ❌ WRONG: Missing dimensions causes CLS -->
<img src="/assets/headshot.png" alt="Headshot">
```

#### **2. Script Loading Strategy**

Your scripts are already optimized:
- ✅ Google Fonts: `preconnect` + `display=swap`
- ✅ Tailwind CSS: `defer` attribute
- ✅ Analytics: `defer` attribute
- ✅ Inline critical CSS: No blocking

#### **3. Font Loading Optimization**

Your Google Fonts link is already optimized with `display=swap` (uses system fonts while loading).

#### **4. Preload Critical Resources**

Add this to your `<head>` if you want to preload critical fonts:

```html
<link rel="preload" as="style" href="https://fonts.googleapis.com/css2?family=Archivo:wght@700&display=swap">
```

#### **5. Remove Unused CSS**

Since you're using Tailwind from CDN, all utility classes are included. If you want to optimize further, build Tailwind locally with PurgeCSS (advanced).

#### **6. Minimize Layout Shift (CLS)**

Your site is already well-optimized:
- ✅ Fixed header height (`min-h-[44px]` on buttons)
- ✅ Preconnect to fonts
- ✅ No lazy-loaded fonts or images that shift layout

---

## ✅ **Testing & Validation**

### **Pre-Deployment Checklist**

- [ ] **Run PageSpeed Insights:**
  ```
  https://pagespeed.web.dev/?url=https://my-portfolio.com
  ```
  Target: 95+ score on both Mobile & Desktop

- [ ] **Test robots.txt:**
  ```
  https://my-portfolio.com/robots.txt
  ```
  Should return the file content

- [ ] **Test sitemap.xml:**
  ```
  https://my-portfolio.com/sitemap.xml
  ```
  Should return valid XML

- [ ] **Verify Analytics:**
  - Open Console (F12 → Console tab)
  - Should see: `[Telemetry] Tracking initialized`
  - Click "Email Me" button
  - Should log: `[Telemetry] Event tracked: email-click`

- [ ] **Check Security Headers:**
  - Open Network tab (F12 → Network)
  - Click a request to any page
  - Look for response headers:
    - ✅ `X-Frame-Options: SAMEORIGIN`
    - ✅ `X-Content-Type-Options: nosniff`
    - ✅ `X-XSS-Protection: 1; mode=block`

- [ ] **Mobile Responsiveness:**
  - Test on iPhone, Android, tablet
  - Hamburger menu (if added) works smoothly
  - Touch targets are ≥48px

- [ ] **Accessibility:**
  - Run WAVE tool: https://wave.webaim.org/
  - Check for color contrast issues
  - Verify skip-to-main link works (press Tab at page load)

### **Google Search Console Setup**

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. Add property → Domain
3. Verify ownership via DNS TXT record
4. Submit sitemap:
   - Settings → Sitemaps
   - Add: `https://my-portfolio.com/sitemap.xml`
5. Monitor clicks, impressions, and indexing status

### **Vercel Deployment Checklist**

- [ ] Environment variable for domain set (if needed)
- [ ] HTTPS enabled (automatic on Vercel)
- [ ] Redirects working (`/resume` → `/assets/resume.pdf`)
- [ ] Analytics script loading (check in Network tab)

### **Netlify Deployment Checklist**

- [ ] `_headers` file deployed (check in Network → Response Headers)
- [ ] `_redirects` file deployed (test `/resume` route)
- [ ] Cache headers applied to `/assets/` (check `Cache-Control` header)

---

## 📁 **File Manifest**

| Filename | Purpose | Where to Place | Deploy? |
|----------|---------|-----------------|---------|
| `index.html` | Main portfolio | Root | ✅ Yes |
| `robots.txt` | SEO crawl config | Root | ✅ Yes |
| `sitemap.xml` | XML sitemap | Root | ✅ Yes |
| `vercel.json` | Vercel config | Root (Vercel only) | ✅ Yes (if Vercel) |
| `_redirects` | Netlify routes | Root (Netlify only) | ✅ Yes (if Netlify) |
| `_headers` | Netlify security | Root (Netlify only) | ✅ Yes (if Netlify) |
| `assets/resume.pdf` | Your resume | `/public/assets/` | ✅ Yes |
| `assets/og-image.png` | Social preview | `/public/assets/` | ✅ Yes |

---

## 🆘 **Troubleshooting**

### **Analytics not tracking events?**
- Check Console for `[Telemetry]` messages
- Verify Plausible script is loaded (F12 → Network → search "plausible")
- Check if ad blocker is blocking analytics

### **Resume download not working?**
- Verify `/assets/resume.pdf` file exists
- Test redirect manually: `https://my-portfolio.com/resume`
- Check `_redirects` or `vercel.json` is deployed

### **PageSpeed score below 90?**
- Run lighthouse locally: `https://pagespeed.web.dev`
- Check for render-blocking resources (images, scripts)
- Ensure all images have `width` and `height` attributes
- Verify fonts are loaded with `display=swap`

### **Domain not resolving?**
- Check DNS records are correct in your registrar
- Allow 24-48 hours for DNS propagation
- Test with `nslookup my-portfolio.com`

---

## 🎯 **Next Steps**

1. **Update domain placeholders:**
   - Replace `my-portfolio.com` with your actual domain in:
     - `vercel.json`
     - `_headers` and `_redirects`
     - `robots.txt`
     - `sitemap.xml`
     - Plausible data attribute in `index.html`

2. **Create `/public/assets/` folder:**
   ```
   mkdir -p public/assets
   cp /path/to/your/resume.pdf public/assets/
   cp /path/to/your/og-image.png public/assets/
   ```

3. **Deploy:**
   - Push to GitHub
   - Connect to Vercel or Netlify
   - Verify deployment

4. **Monitor:**
   - Check Google Search Console weekly
   - Monitor PageSpeed Insights monthly
   - Review Plausible Analytics for visitor trends

---

## 📞 **Support Resources**

- **Vercel Docs:** https://vercel.com/docs
- **Netlify Docs:** https://docs.netlify.com
- **PageSpeed Insights:** https://pagespeed.web.dev
- **Google Search Console:** https://search.google.com/search-console
- **Plausible Analytics:** https://plausible.io/docs

---

**Last Updated:** July 2026  
**Portfolio Version:** SA4E v6  
**Deployment Status:** Ready for Production
