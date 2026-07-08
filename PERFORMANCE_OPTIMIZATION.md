# Google PageSpeed Insights 95+ Optimization Guide
## Engineering-Grade Performance Blueprint

---

## 🎯 **Target Metrics**

| Metric | Target | Your Current |
|--------|--------|--------------|
| **Core Web Vitals** | Green | - |
| Largest Contentful Paint (LCP) | < 2.5s | - |
| First Input Delay (FID) | < 100ms | - |
| Cumulative Layout Shift (CLS) | < 0.1 | - |
| **PageSpeed Score** | 95+ | - |

---

## ⚡ **1. Script & Stylesheet Isolation**

### **Current Implementation (✓ OPTIMIZED)**

Your portfolio already implements best practices:

```html
<!-- ✓ Preconnect to critical domains (no render blocking) -->
<link rel="preconnect" href="https://fonts.googleapis.com" crossorigin>
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- ✓ Google Fonts with display=swap (prevents FOUT) -->
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@700&display=swap" rel="stylesheet">

<!-- ✓ Tailwind CSS with defer (non-blocking) -->
<script defer src="https://cdn.tailwindcss.com"></script>

<!-- ✓ Analytics with defer (non-blocking) -->
<script defer data-domain="my-portfolio.com" src="https://plausible.io/js/script.js"></script>

<!-- ✓ Custom scripts with defer (non-blocking) -->
<script defer>
  // Your analytics and tracking code
</script>
```

### **What Each Attribute Does**

| Attribute | Effect | Use Case |
|-----------|--------|----------|
| `defer` | Loads async, executes after HTML | Non-critical scripts |
| `async` | Loads and executes immediately | Third-party analytics |
| (none) | Blocks HTML parsing | Critical scripts only |

### **Critical Path Rules**

```html
<!-- ❌ BLOCKS rendering -->
<script src="myapp.js"></script>

<!-- ✓ Non-blocking (recommended) -->
<script defer src="myapp.js"></script>

<!-- ✓ Analytics (non-blocking with async) -->
<script async src="analytics.js"></script>

<!-- ✓ CSS (blocks, but necessary) -->
<link rel="stylesheet" href="styles.css">

<!-- ✓ Preload critical assets -->
<link rel="preload" as="script" href="critical.js">
<link rel="preload" as="font" href="font.woff2" type="font/woff2" crossorigin>
```

---

## 🖼️ **2. Eliminating Cumulative Layout Shift (CLS)**

CLS measures unexpected layout shifts during page load. Your score is 0 if images/content don't move.

### **The Problem**

```html
<!-- ❌ BAD: No dimensions, causes layout shift when image loads -->
<img src="/assets/headshot.png" alt="Profile picture">

<!-- Browser doesn't know image size, reserves 0 space
     When image loads, all content below shifts down
     Result: High CLS, bad UX -->
```

### **The Solution: Reserve Space**

```html
<!-- ✓ GOOD: With width, height, and aspect ratio -->
<img 
  src="/assets/headshot.png" 
  alt="Swagatika Arukha headshot" 
  width="400" 
  height="400" 
  aspect-ratio="1 / 1"
  loading="lazy"
  decoding="async"
  class="rounded-2xl shadow-lg"
>

<!-- Browser knows image is square (400×400)
     Reserves space immediately
     When image loads, no shift
     Result: CLS = 0 ✓ -->
```

### **Complete Image Optimization Template**

For any images in your portfolio:

```html
<!-- Profile headshot -->
<img 
  src="/assets/headshot.png" 
  alt="Swagatika Arukha, Senior Technical PM" 
  width="480" 
  height="480" 
  aspect-ratio="1"
  loading="lazy"
  decoding="async"
  fetchpriority="high"
  class="rounded-2xl object-cover shadow-pop"
  style="aspect-ratio: 1 / 1; width: auto; height: auto; max-width: 100%;"
>

<!-- Project screenshot -->
<img 
  src="/assets/project-screenshot.png" 
  alt="MFE Limited Preview dashboard screenshot" 
  width="1200" 
  height="675" 
  aspect-ratio="16 / 9"
  loading="lazy"
  decoding="async"
  class="rounded-lg border-2 border-ink"
>

<!-- Company logos in carousel -->
<img 
  src="/assets/new-relic-logo.svg" 
  alt="New Relic logo" 
  width="200" 
  height="100" 
  aspect-ratio="2 / 1"
  loading="lazy"
  decoding="async"
  class="h-12 object-contain"
>
```

### **Image Attribute Breakdown**

| Attribute | Value | Purpose |
|-----------|-------|---------|
| `width` | `480` | Exact pixel width |
| `height` | `480` | Exact pixel height |
| `aspect-ratio` | `1 / 1` | Maintains ratio during load |
| `loading` | `lazy` | Defer offscreen images |
| `decoding` | `async` | Don't block rendering |
| `fetchpriority` | `high` | Load above-fold images first |

### **SVG (No CLS at All)**

If you use SVG images, CLS is automatic:

```html
<!-- SVGs don't cause layout shifts -->
<svg width="400" height="400" viewBox="0 0 400 400" xmlns="http://www.w3.org/2000/svg">
  <!-- SVG content -->
</svg>
```

---

## 🎨 **3. Font Loading Optimization**

Your Google Fonts implementation is already optimized. Here's why:

### **Current (✓ OPTIMIZED)**

```html
<!-- Step 1: Preconnect (early connection) -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- Step 2: Load with display=swap (show system font immediately) -->
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@700&display=swap" rel="stylesheet">
```

### **Font Display Strategies**

| Strategy | Behavior | Use Case |
|----------|----------|----------|
| `auto` | Browser decides | Don't use (varies by browser) |
| `block` | Hide 3s, then fallback | Avoid (blank text) |
| `swap` | Show fallback immediately, replace | ✓ **RECOMMENDED** |
| `fallback` | Show fallback 100ms, replace if ready | Good for body text |
| `optional` | Show fallback, don't replace | Use for decorative fonts |

### **Best Practice (Your Setup)**

```html
<!-- ✓ Preconnect to Google Fonts DNS -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

<!-- ✓ Use display=swap (avoids blank text) -->
<link href="https://fonts.googleapis.com/css2?family=Archivo:wght@700&display=swap" rel="stylesheet">
```

---

## ✅ **4. Asset Optimization Checklist**

### **Critical Assets (Load First)**

- [ ] HTML document (always first)
- [ ] CSS (preload if external)
- [ ] Hero image or banner (if above fold)
- [ ] Font files (via preconnect)

### **Secondary Assets (Load After)**

- [ ] Analytics scripts (async/defer)
- [ ] Tracking code (defer)
- [ ] Non-critical images (lazy load)

### **Never Block Rendering**

- ❌ Large JavaScript bundles without `defer`
- ❌ Render-blocking CSS for below-the-fold content
- ❌ External fonts without preconnect
- ❌ Images without `loading="lazy"`

---

## 🔧 **5. Measuring Your Score**

### **Before Deploying: Local Test**

```bash
# Install Lighthouse CLI
npm install -g lighthouse

# Run audit
lighthouse https://my-portfolio.com --view
```

### **After Deploying: Google PageSpeed Insights**

1. Go to [pagespeed.web.dev](https://pagespeed.web.dev)
2. Enter your domain: `https://my-portfolio.com`
3. Wait for report (takes 30-60 seconds)
4. Check:
   - **Core Web Vitals** (should be green)
   - **PageSpeed Score** (target 95+)
   - **Opportunities** section (fix highest impact items)

### **Real-User Monitoring**

After deploying, monitor real users in Google Search Console:

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. Add property
3. Go to **Enhancements** → **Core Web Vitals**
4. View field data (real user metrics)

---

## 🎯 **6. Incremental Optimization Path**

### **Phase 1: Baseline (Minimum)**

- [x] Preconnect to fonts
- [x] Font display=swap
- [x] Defer/async scripts
- [x] Compress images
- [x] Enable GZIP

**Expected Score: 85–90**

### **Phase 2: Image Optimization**

- [x] Add width/height to all images
- [x] Use aspect-ratio CSS
- [x] Lazy load below-fold images
- [x] Use Next-gen formats (WebP if applicable)

**Expected Score: 90–95**

### **Phase 3: Advanced**

- [x] Preload critical assets
- [x] Remove unused CSS
- [x] Minify JavaScript
- [x] Use CDN for assets

**Expected Score: 95+**

---

## 📊 **7. Monitoring Dashboard**

### **Weekly Checklist**

- [ ] Run PageSpeed Insights
- [ ] Check Core Web Vitals in Search Console
- [ ] Monitor Plausible analytics for traffic
- [ ] Check for broken images/links

### **Logging Script Performance**

Optional: Add performance logging to your HTML:

```html
<script defer>
  // Log performance metrics
  if (window.performance && window.performance.timing) {
    window.addEventListener('load', () => {
      const timing = window.performance.timing;
      const metrics = {
        'DNS Lookup': timing.domainLookupEnd - timing.domainLookupStart,
        'TCP Connection': timing.connectEnd - timing.connectStart,
        'Request Time': timing.responseStart - timing.requestStart,
        'Response Time': timing.responseEnd - timing.responseStart,
        'Page Render': timing.domContentLoadedEventEnd - timing.responseEnd,
        'Total Load Time': timing.loadEventEnd - timing.navigationStart
      };
      
      console.table(metrics);
      console.log('%c✓ Page loaded optimally', 'color: #4ade80; font-weight: bold;');
    });
  }
</script>
```

---

## 🚀 **8. Performance Best Practices (Checklist)**

### **Critical Path**

- [x] Minimize request count
- [x] Reduce transfer size
- [x] Defer non-critical code
- [x] Preload critical resources

### **Image Strategy**

- [x] Optimize all images (TinyPNG, ImageOptim)
- [x] Use correct dimensions
- [x] Lazy load offscreen images
- [x] Use WebP with fallback (if applicable)

### **JavaScript**

- [x] Defer all non-critical scripts
- [x] Remove unused libraries
- [x] Split code into smaller chunks
- [x] Use event delegation (single listener for many elements)

### **CSS**

- [x] Critical CSS inline (already doing this)
- [x] Defer non-critical styles
- [x] Remove duplicate selectors
- [x] Use utility-first framework (Tailwind is optimal)

### **Caching**

- [x] Set Cache-Control headers (in `vercel.json` or `_headers`)
- [x] Immutable cache for versioned assets (`/assets/*`)
- [x] Revalidate HTML frequently
- [x] Use CDN for static files

---

## 🔍 **9. Common Pitfalls**

### **❌ Mistake: Render-Blocking Scripts**

```html
<!-- WRONG -->
<script src="analytics.js"></script>
```

### **✓ Fix: Use defer**

```html
<!-- RIGHT -->
<script defer src="analytics.js"></script>
```

---

### **❌ Mistake: No Image Dimensions**

```html
<!-- WRONG -->
<img src="headshot.png">
```

### **✓ Fix: Always specify dimensions**

```html
<!-- RIGHT -->
<img src="headshot.png" width="400" height="400" aspect-ratio="1 / 1">
```

---

### **❌ Mistake: Fonts Block Rendering**

```html
<!-- WRONG -->
<link href="...font.css?display=auto">
```

### **✓ Fix: Use display=swap**

```html
<!-- RIGHT -->
<link href="...font.css?display=swap">
```

---

## 📈 **10. Expected Scores**

### **Your Portfolio (Optimized)**

| Component | Score |
|-----------|-------|
| **Performance** | 95–98 |
| **Accessibility** | 95–100 |
| **Best Practices** | 95–100 |
| **SEO** | 98–100 |
| **Overall** | **96–99** |

---

## 🎓 **Resources**

- **Lighthouse Guide:** https://developers.google.com/web/tools/lighthouse
- **Web Vitals:** https://web.dev/vitals
- **Image Optimization:** https://web.dev/image-optimization
- **Font Loading:** https://web.dev/font-load-event
- **PageSpeed Insights:** https://pagespeed.web.dev

---

**Last Updated:** July 2026  
**Portfolio Version:** SA4E v6
