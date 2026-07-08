# HTML Code Snippets - Quick Reference
## Copy & Paste Guide for Portfolio Enhancements

---

## 📍 **Where Each Snippet Goes**

```
<!DOCTYPE html>
<html>
  <head>
    <!-- SNIPPET 1: Favicon -->
    <!-- SNIPPET 2: Meta Tags -->
    <!-- SNIPPET 3: Preconnect & Fonts -->
    <!-- SNIPPET 4: Inline CSS -->
    <!-- SNIPPET 5: Analytics Script -->
  </head>
  <body>
    <!-- Your HTML content -->
    
    <!-- SNIPPET 6: Custom Events Telemetry -->
  </body>
</html>
```

---

## 🎨 **SNIPPET 1: Inline SVG Favicon**

**Location:** Inside `<head>` tag (replace any existing favicon link)

**Purpose:** Replace external image file with inline SVG (saves HTTP request)

```html
<!-- Modern inline SVG favicon (1.2KB) -->
<!-- Options: Terminal theme, network nodes, or custom -->

<!-- OPTION A: Terminal/Command Theme (>_) -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%236575DE' width='100' height='100'/><text x='50%' y='50%' dominant-baseline='middle' text-anchor='middle' fill='%23F6F2E7' font-size='60' font-weight='bold' font-family='monospace'>&gt;_</text></svg>" type="image/svg+xml">

<!-- OPTION B: Network Nodes Theme (circles connected) -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%236575DE' width='100' height='100'/><circle cx='30' cy='30' r='8' fill='%23F6F2E7'/><circle cx='70' cy='30' r='8' fill='%23F6F2E7'/><circle cx='50' cy='70' r='8' fill='%23F6F2E7'/><line x1='30' y1='30' x2='70' y2='30' stroke='%23F6F2E7' stroke-width='2'/><line x1='30' y1='30' x2='50' y2='70' stroke='%23F6F2E7' stroke-width='2'/><line x1='70' y1='30' x2='50' y2='70' stroke='%23F6F2E7' stroke-width='2'/></svg>" type="image/svg+xml">

<!-- OPTION C: Minimalist Initials (SA) -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><rect fill='%236575DE' width='100' height='100'/><text x='50%' y='55%' dominant-baseline='middle' text-anchor='middle' fill='%23F6F2E7' font-size='50' font-weight='900' font-family='system-ui'>SA</text></svg>" type="image/svg+xml">

<!-- OPTION D: Gradient Background with Symbol -->
<link rel="icon" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><defs><linearGradient id='grad' x1='0%' y1='0%' x2='100%' y2='100%'><stop offset='0%' style='stop-color:%236575DE;stop-opacity:1' /><stop offset='100%' style='stop-color:%234C5BC2;stop-opacity:1' /></linearGradient></defs><rect fill='url(%23grad)' width='100' height='100'/><circle cx='50' cy='50' r='20' fill='none' stroke='%23F6F2E7' stroke-width='3'/><circle cx='50' cy='50' r='5' fill='%23F6F2E7'/></svg>" type="image/svg+xml">
```

**How it works:**
1. `data:image/svg+xml` embeds SVG directly in HTML
2. No external file needed (saves HTTP request)
3. Colors match your palette (#6575DE peri, #F6F2E7 cream)
4. ~0.5KB gzipped vs ~5KB for PNG favicon

---

## 📊 **SNIPPET 2: Essential Meta Tags**

**Location:** Inside `<head>` tag, after `<title>`

**Purpose:** SEO, social sharing, and browser hints

```html
<!-- Character encoding (must be first) -->
<meta charset="UTF-8">

<!-- Viewport (mobile responsiveness) -->
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<!-- SEO Description -->
<meta name="description" content="Swagatika Arukha — Senior Technical Product Manager. Platform engineering, DEM, Session Replay, AI infrastructure. $2M+ ARR influenced, 100M+ users served.">

<!-- Keywords (optional but helpful) -->
<meta name="keywords" content="product manager, platform engineering, DEM, telemetry, AI infrastructure, Chicago">

<!-- Author -->
<meta name="author" content="Swagatika Arukha">

<!-- Canonical URL (prevents duplicate content issues) -->
<link rel="canonical" href="https://my-portfolio.com">

<!-- ===== OPEN GRAPH (for social media sharing) ===== -->
<meta property="og:title" content="Swagatika Arukha — Senior Technical PM">
<meta property="og:description" content="Platform engineering, DEM, AI infrastructure. $2M+ ARR influenced.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://my-portfolio.com">
<meta property="og:image" content="https://my-portfolio.com/assets/og-image.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">

<!-- ===== TWITTER CARD (for Twitter sharing) ===== -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Swagatika Arukha — Senior Technical PM">
<meta name="twitter:description" content="Platform engineering, AI infrastructure, 100M+ users.">
<meta name="twitter:image" content="https://my-portfolio.com/assets/og-image.png">
<meta name="twitter:creator" content="@swagatika_arukha">

<!-- Theme color (browser chrome on mobile) -->
<meta name="theme-color" content="#6575DE">
<meta name="apple-mobile-web-app-capable" content="yes">
```

**To create OG image:**
1. Use design tool (Figma, Canva) to create 1200x630px image
2. Include your name, headline, and key stats
3. Save to `/public/assets/og-image.png`
4. Update URL above

---

## 🔗 **SNIPPET 3: Preconnect & Font Loading**

**Location:** Inside `<head>` tag, before font links

**Purpose:** Accelerate external resource loading (DNS lookup, handshake)

```html
<!-- ===== CRITICAL PRECONNECTS (load these early) ===== -->

<!-- Google Fonts API -->
<link rel="preconnect" href="https://fonts.googleapis.com" crossorigin>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Tailwind CDN (optional, if using from CDN) -->
<link rel="dns-prefetch" href="https://cdn.tailwindcss.com">

<!-- Plausible Analytics (optional) -->
<link rel="dns-prefetch" href="https://plausible.io">

<!-- ===== GOOGLE FONTS (with display=swap for performance) ===== -->
<!-- Using minimal weights to reduce font file size -->
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@500;600;700;800;900&family=Inter:ital,wght@0,400;0,500;0,600;0,700;1,400&family=Source+Serif+4:ital,opsz,wght@1,8..60,400;1,8..60,500&display=swap" rel="stylesheet">

<!-- Alternative: Preload specific font weights (advanced) -->
<!-- <link rel="preload" as="font" href="https://fonts.gstatic.com/s/archivo/v20/k3klqom_lyVKPgG8lsglb.woff2" type="font/woff2" crossorigin> -->
```

**What each attribute does:**
- `preconnect`: Initiates DNS lookup + TCP handshake early
- `dns-prefetch`: Only initiates DNS lookup
- `crossorigin`: Required for fonts (CORS)
- `display=swap`: Shows system font while Google font loads

---

## 🎨 **SNIPPET 4: Inline Critical CSS**

**Location:** Inside `<head>` tag in `<style>` tag

**Purpose:** Render critical styles immediately (no blocking)

```html
<style>
  /* ===== CRITICAL PATH CSS (must load synchronously) ===== */
  
  /* Smooth scrolling behavior */
  html { 
    scroll-padding-top: 96px;
    scroll-behavior: smooth;
  }
  
  /* Font smoothing */
  body { 
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
  
  /* Selection color (your brand) */
  ::selection { 
    background: #CFC2F0;
    color: #1E1B16;
  }
  
  /* Hero gradient background */
  .hero-wash {
    background: linear-gradient(180deg,
      #F6F2E7 0%, #F6F2E7 42%, #F0E7EC 68%, #E4DCF2 88%, #DCE4F0 100%);
  }
  
  /* ===== ANIMATION KEYFRAMES ===== */
  
  @keyframes scroll-left {
    from { transform: translateX(0); }
    to { transform: translateX(-50%); }
  }
  
  @keyframes scroll-right {
    from { transform: translateX(-50%); }
    to { transform: translateX(0); }
  }
  
  /* Marquee (scrolling text) */
  .marquee { 
    overflow: hidden;
    white-space: nowrap;
  }
  
  .marquee-track {
    display: inline-flex;
    align-items: center;
    width: max-content;
    animation: scroll-left 36s linear infinite;
  }
  
  .marquee-track.reverse { 
    animation: scroll-right 42s linear infinite;
  }
  
  .marquee:hover .marquee-track { 
    animation-play-state: paused;
  }
  
  /* Reveal animation (fade in + slide up) */
  .reveal { 
    opacity: 0;
    transform: translateY(12px);
    transition: opacity 550ms ease, transform 550ms ease;
  }
  
  .reveal.in { 
    opacity: 1;
    transform: none;
  }
  
  /* Accessibility: Respect prefers-reduced-motion */
  @media (prefers-reduced-motion: reduce) {
    html { scroll-behavior: auto !important; }
    .marquee-track, .marquee-track.reverse { 
      animation: none !important;
    }
    .marquee { overflow-x: auto; }
    .reveal { 
      opacity: 1 !important;
      transform: none !important;
      transition: none !important;
    }
  }
  
  /* Accordion (collapsible sections) */
  .acc-body { 
    display: grid;
    grid-template-rows: 0fr;
    transition: grid-template-rows 260ms ease;
  }
  
  .acc-body > div { overflow: hidden; }
  .acc-body.open { grid-template-rows: 1fr; }
  
  .acc-chev { 
    transition: transform 200ms ease;
    display: inline-block;
  }
  
  .acc-btn[aria-expanded="true"] .acc-chev { 
    transform: rotate(90deg);
  }
  
  /* ===== ACCESSIBILITY ===== */
  
  /* Focus visible (keyboard navigation) */
  a:focus-visible, 
  button:focus-visible { 
    outline: 3px solid #6575DE;
    outline-offset: 3px;
    border-radius: 4px;
  }
  
  /* Skip to main content link */
  .skip-link { 
    position: absolute;
    left: -9999px;
  }
  
  .skip-link:focus { 
    left: 16px;
    top: 16px;
    z-index: 100;
    background: #1E1B16;
    color: #F6F2E7;
    padding: 10px 16px;
    border-radius: 4px;
  }
</style>
```

---

## 📈 **SNIPPET 5: Analytics Script**

**Location:** Inside `<head>` tag (before `</head>`)

**Purpose:** Lightweight pageview tracking (1.2KB)

```html
<!-- Plausible Analytics (lightweight, privacy-friendly) -->
<!-- Get your data-domain value from plausible.io dashboard -->
<script defer data-domain="my-portfolio.com" src="https://plausible.io/js/script.js"></script>

<!-- Alternative: Google Analytics (heavier, ~50KB) -->
<!-- <script async src="https://www.googletagmanager.com/gtag/js?id=GA_MEASUREMENT_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_MEASUREMENT_ID');
</script> -->

<!-- Alternative: Fathom Analytics (lightweight, privacy-friendly) -->
<!-- <script site="XXXX" defer src="https://cdn.usefathom.com/script.js"></script> -->
```

---

## 🎯 **SNIPPET 6: Custom Event Telemetry**

**Location:** Before closing `</body>` tag

**Purpose:** Track user interactions (button clicks, conversions)

```html
<!-- Custom Event Telemetry Tracker -->
<script>
  // ========== TELEMETRY CONFIGURATION ==========
  const ANALYTICS_CONFIG = {
    trackingEnabled: typeof window.plausible !== 'undefined',
    debug: true, // Set to false in production
    events: {
      RESUME_DOWNLOAD: 'resume-download',
      EMAIL_CLICK: 'email-click',
      LINKEDIN_CLICK: 'linkedin-click',
      GITHUB_CLICK: 'github-click',
      SECTION_VIEW: 'section-viewed',
      NAV_CLICK: 'navigation-click'
    }
  };

  // ========== TRACK EVENT FUNCTION ==========
  function trackEvent(eventName, data = {}) {
    if (ANALYTICS_CONFIG.trackingEnabled && window.plausible) {
      // Send to Plausible
      window.plausible(eventName, { props: data });
      
      // Console log for debugging
      if (ANALYTICS_CONFIG.debug) {
        console.log(`✓ [Telemetry] Event: ${eventName}`, data);
      }
    } else if (ANALYTICS_CONFIG.debug) {
      console.warn(`✗ [Telemetry] Analytics unavailable`);
    }
  }

  // ========== TRACK RESUME DOWNLOAD ==========
  document.querySelectorAll('a[href*="resume"]').forEach(link => {
    link.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.RESUME_DOWNLOAD, {
        referrer: document.referrer || 'direct',
        section: document.activeElement.closest('section')?.id || 'unknown',
        timestamp: new Date().toISOString()
      });
    });
  });

  // ========== TRACK EMAIL CLICK ==========
  const emailLink = document.querySelector('a[href^="mailto:"]');
  if (emailLink) {
    emailLink.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.EMAIL_CLICK, {
        action: 'contact-initiated',
        timestamp: new Date().toISOString()
      });
    });
  }

  // ========== TRACK SOCIAL LINK CLICKS ==========
  const socialLinks = {
    linkedin: document.querySelector('a[href*="linkedin"]'),
    github: document.querySelector('a[href*="github"]')
  };

  if (socialLinks.linkedin) {
    socialLinks.linkedin.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.LINKEDIN_CLICK, {
        platform: 'linkedin',
        timestamp: new Date().toISOString()
      });
    });
  }

  if (socialLinks.github) {
    socialLinks.github.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.GITHUB_CLICK, {
        platform: 'github',
        timestamp: new Date().toISOString()
      });
    });
  }

  // ========== TRACK NAVIGATION ==========
  document.querySelectorAll('.nav-link').forEach(link => {
    link.addEventListener('click', () => {
      const section = link.getAttribute('href').replace('#', '');
      trackEvent(ANALYTICS_CONFIG.events.NAV_CLICK, {
        section: section,
        timestamp: new Date().toISOString()
      });
    });
  });

  // ========== INITIALIZATION LOG ==========
  console.log(
    '%c[Telemetry] Portfolio analytics initialized',
    'color: #6575DE; font-weight: bold;'
  );
  console.log('Available events:', ANALYTICS_CONFIG.events);
  console.log('Tracking enabled:', ANALYTICS_CONFIG.trackingEnabled);
</script>
```

---

## 📐 **SNIPPET 7: Image Optimization (Add to Any Images)**

**Location:** Inside `<img>` tags throughout your HTML

**Purpose:** Prevent Cumulative Layout Shift (CLS)

```html
<!-- PATTERN: Profile Headshot (square) -->
<img 
  src="/assets/headshot.png" 
  alt="Swagatika Arukha headshot" 
  width="400" 
  height="400" 
  aspect-ratio="1 / 1"
  loading="lazy"
  decoding="async"
  class="rounded-2xl shadow-pop"
>

<!-- PATTERN: Landscape Screenshot (16:9) -->
<img 
  src="/assets/screenshot.png" 
  alt="New Relic MFE dashboard" 
  width="1200" 
  height="675" 
  aspect-ratio="16 / 9"
  loading="lazy"
  decoding="async"
  class="rounded-lg border-2 border-ink"
>

<!-- PATTERN: Company Logo (2:1) -->
<img 
  src="/assets/logo.svg" 
  alt="New Relic logo" 
  width="200" 
  height="100" 
  aspect-ratio="2 / 1"
  loading="lazy"
  decoding="async"
  class="h-12 w-auto object-contain"
>

<!-- PATTERN: Above-fold Hero Image (prioritize) -->
<img 
  src="/assets/hero.png" 
  alt="Portfolio hero" 
  width="1200" 
  height="400" 
  aspect-ratio="3 / 1"
  loading="eager"
  fetchpriority="high"
  decoding="async"
  class="w-full object-cover"
>
```

---

## 🆚 **SNIPPET 8: JSON-LD Structured Data**

**Location:** Inside `<head>` tag before `</head>`

**Purpose:** Help search engines understand your profile

```html
<!-- Structured Data (JSON-LD) for SEO -->
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "Person",
  "name": "Swagatika Arukha",
  "jobTitle": "Senior Technical Product Manager",
  "url": "https://my-portfolio.com",
  "image": "https://my-portfolio.com/assets/headshot.png",
  "description": "Senior Technical Product Manager specializing in platform engineering, DEM, and AI infrastructure.",
  "sameAs": [
    "https://linkedin.com/in/swagatikaarukha",
    "https://github.com/Sarukha2002",
    "https://substack.com/evolving-pm"
  ],
  "knowsAbout": [
    "Platform Engineering",
    "Digital Experience Monitoring",
    "Session Replay",
    "AI Infrastructure",
    "Telemetry",
    "Experimentation Platforms"
  ],
  "workLocation": {
    "@type": "Place",
    "name": "Chicago, Illinois",
    "address": {
      "@type": "PostalAddress",
      "addressLocality": "Chicago",
      "addressRegion": "Illinois",
      "addressCountry": "US"
    }
  }
}
</script>
```

---

## ✅ **Checklist: All Snippets Added**

- [ ] Favicon (SNIPPET 1)
- [ ] Meta tags (SNIPPET 2)
- [ ] Preconnect & fonts (SNIPPET 3)
- [ ] Inline CSS (SNIPPET 4)
- [ ] Analytics script (SNIPPET 5)
- [ ] Custom events (SNIPPET 6)
- [ ] Image optimization (SNIPPET 7 - if images added)
- [ ] Structured data (SNIPPET 8)

---

**Version:** July 2026  
**Portfolio:** Swagatika Arukha v6
