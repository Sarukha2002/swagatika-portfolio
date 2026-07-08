# Analytics & Telemetry Setup Guide
## Lightweight Tracking for Your Portfolio

---

## 📊 **Analytics Overview**

This implementation uses **Plausible Analytics** — a lightweight, privacy-focused alternative to Google Analytics.

**Why Plausible?**
- ✅ 1.2KB script (vs 50KB+ for Google Analytics)
- ✅ No cookie banner required (GDPR compliant)
- ✅ No third-party tracking
- ✅ Real-time dashboard
- ✅ Affordable ($9–20/month)

---

## 🔧 **Setup Instructions**

### **Step 1: Create Plausible Account**

1. Go to [plausible.io](https://plausible.io)
2. Click "Start free trial"
3. Sign up with email
4. Create account → Free tier (up to 10K pageviews/month)

### **Step 2: Add Your Domain**

1. Log in to Plausible dashboard
2. Click "Add website"
3. Enter domain: `my-portfolio.com`
4. Copy your tracking script (looks like below)

### **Step 3: Implement Tracking Script**

Replace this line in your `index.html` `<head>`:

```html
<!-- Old (if you had any) -->
<!-- <script async src="..." ></script> -->

<!-- New Plausible tracking -->
<script defer data-domain="my-portfolio.com" src="https://plausible.io/js/script.js"></script>
```

**Key attributes:**
- `defer`: Prevents blocking page render
- `data-domain`: Your actual domain name
- `src`: Points to Plausible CDN

---

## 📈 **Custom Event Tracking**

This is the JavaScript snippet that tracks button clicks and user interactions.

### **Add This Before Closing `</body>` Tag:**

```html
<!-- Custom Event Telemetry Tracker -->
<script>
  // ========== TELEMETRY CONFIGURATION ==========
  const ANALYTICS_CONFIG = {
    trackingEnabled: typeof window.plausible !== 'undefined',
    events: {
      RESUME_DOWNLOAD: 'resume-download',
      EMAIL_CLICK: 'email-click',
      LINKEDIN_CLICK: 'linkedin-click',
      GITHUB_CLICK: 'github-click',
      SECTION_VIEW: 'section-viewed',
      NAV_CLICK: 'navigation-click'
    }
  };

  // ========== SEND EVENT TO PLAUSIBLE ==========
  function trackEvent(eventName, data = {}) {
    if (ANALYTICS_CONFIG.trackingEnabled && window.plausible) {
      // Send to Plausible
      window.plausible(eventName, { props: data });
      
      // Log for debugging
      console.log(`✓ [Telemetry] Event tracked: ${eventName}`, data);
    } else {
      console.warn(`✗ [Telemetry] Analytics disabled or unavailable. Event: ${eventName}`);
    }
  }

  // ========== TRACK RESUME DOWNLOAD ==========
  const resumeLinks = document.querySelectorAll('a[href*="resume"]');
  resumeLinks.forEach(link => {
    link.addEventListener('click', (e) => {
      trackEvent(ANALYTICS_CONFIG.events.RESUME_DOWNLOAD, {
        referrer: document.referrer || 'direct',
        timestamp: new Date().toISOString(),
        from_section: document.activeElement.closest('section')?.id || 'unknown'
      });
    });
  });

  // ========== TRACK EMAIL CLICK ==========
  const emailLink = document.querySelector('a[href^="mailto:"]');
  if (emailLink) {
    emailLink.addEventListener('click', () => {
      trackEvent(ANALYTICS_CONFIG.events.EMAIL_CLICK, {
        action: 'email-initiated',
        email: emailLink.getAttribute('href').replace('mailto:', ''),
        timestamp: new Date().toISOString()
      });
    });
  }

  // ========== TRACK SOCIAL LINKS ==========
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

  // ========== TRACK NAVIGATION CLICKS ==========
  const navLinks = document.querySelectorAll('.nav-link');
  navLinks.forEach(link => {
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
    `%c[Telemetry] Portfolio analytics initialized`,
    'color: #6575DE; font-weight: bold;'
  );
  console.log('Events available:', ANALYTICS_CONFIG.events);
  console.log('Tracking enabled:', ANALYTICS_CONFIG.trackingEnabled);
</script>
```

---

## 🎯 **Events You're Tracking**

| Event | Trigger | Data Sent |
|-------|---------|-----------|
| `resume-download` | "Download Resume" button clicked | referrer, timestamp, section |
| `email-click` | "Email Me" button clicked | email address, timestamp |
| `linkedin-click` | LinkedIn link clicked | platform, timestamp |
| `github-click` | GitHub link clicked | platform, timestamp |
| `navigation-click` | Navigation menu item clicked | section name, timestamp |

---

## 📊 **Viewing Analytics**

### **Plausible Dashboard**

After deploying, visit [plausible.io/my-portfolio.com](https://plausible.io) to see:

1. **Top Pages** — Which sections get most traffic
2. **Entry Pages** — How visitors first arrive
3. **Exit Pages** — Where they leave
4. **Custom Events** — Your tracked button clicks
5. **Referrers** — Where traffic comes from
6. **Devices** — Mobile vs desktop breakdown

### **Custom Events Report**

1. In Plausible dashboard, select "Custom Events"
2. Click on any event (e.g., "resume-download")
3. See properties breakdown:
   - From which section?
   - From which referrer?
   - How many this week?

---

## 🔍 **Testing & Debugging**

### **Test Locally**

Before deploying, test tracking in browser console:

1. Open your `index.html` in Chrome
2. Press `F12` to open Developer Tools
3. Go to **Console** tab
4. Should see: `✓ [Telemetry] Portfolio analytics initialized`
5. Click "Email Me" button
6. Should log: `✓ [Telemetry] Event tracked: email-click`

### **Test After Deployment**

1. Deploy to Vercel/Netlify
2. Visit your deployed site
3. Open Console (F12)
4. Click any tracked button
5. Should see success log in console
6. Go to Plausible dashboard (may take 30 seconds)
7. Check "Custom Events" for your clicks

### **Verify Script is Loading**

1. Open Network tab (F12 → Network)
2. Search for "plausible"
3. Should see `script.js` with status `200`
4. If you see `blocked` or `ad-blocker`, the script is being blocked

---

## ⚙️ **Advanced Configuration**

### **Disable Tracking for Yourself**

If you don't want your own visits tracked:

```javascript
// Add to index.html head
<script>
  window.plausible = window.plausible || function() { (window.plausibleQueue = window.plausibleQueue || []).push(arguments) }
  // Exclude this device
  if (navigator.doNotTrack == "1") {
    console.log("Do Not Track enabled - analytics disabled");
  }
</script>
```

### **Custom Event with Extra Data**

Track any event with custom properties:

```javascript
// Example: Track time spent on section
function trackSectionTime(sectionId, timeSpent) {
  trackEvent('section-time-on-page', {
    section: sectionId,
    time_seconds: Math.round(timeSpent / 1000),
    timestamp: new Date().toISOString()
  });
}
```

### **Outbound Link Tracking**

Track when visitors click external links:

```javascript
// Track all external link clicks
document.querySelectorAll('a[target="_blank"]').forEach(link => {
  link.addEventListener('click', () => {
    trackEvent('outbound-link', {
      url: link.getAttribute('href'),
      text: link.textContent,
      timestamp: new Date().toISOString()
    });
  });
});
```

---

## 🛡️ **Privacy & Compliance**

### **GDPR Compliant?**

✅ Yes! Plausible automatically:
- Does NOT use cookies
- Does NOT store personal data
- Does NOT require cookie consent
- Complies with GDPR, CCPA, PECR

### **Privacy Policy Update**

Add this to your site's privacy policy (if you have one):

> "We use Plausible Analytics to understand visitor patterns. Plausible does not use cookies or collect personally identifiable information. For more details, see [Plausible's privacy policy](https://plausible.io/privacy)."

---

## 💰 **Pricing & Limits**

| Plan | Price | Pageviews | Features |
|------|-------|-----------|----------|
| **Free Trial** | $0 | 10,000/month | Full dashboard, 30 days |
| **Starter** | $9/month | 10,000/month | All features |
| **Growth** | $20/month | 100,000/month | All features |
| **Business** | $200/month | Unlimited | Priority support |

For a portfolio with typical traffic, **Starter ($9)** is more than sufficient.

---

## 🚀 **Next Steps**

1. ✅ Sign up for Plausible
2. ✅ Add domain to Plausible
3. ✅ Copy tracking script to `<head>`
4. ✅ Add custom event script before `</body>`
5. ✅ Deploy to Vercel/Netlify
6. ✅ Test in Console
7. ✅ Monitor Plausible dashboard

---

## 📚 **Resources**

- **Plausible Docs:** https://plausible.io/docs
- **Privacy Policy:** https://plausible.io/privacy
- **Event Tracking Guide:** https://plausible.io/docs/custom-event-goals
- **API Reference:** https://plausible.io/docs/events-api

---

**Last Updated:** July 2026
