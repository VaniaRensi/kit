---
name: web-deploy
category: development
description: Final checklist to run before going live with a project. Activate this skill when the user says "we're ready to deploy", "let's go live", "loading to production", "let's publish". Covers production configuration, basic SEO, errors and crashes, performance, mobile, accessibility, final security. Run once only, after all development checkpoints have been passed.
---

# Pre-Launch — Checklist Before Going Live

This checklist runs once only, when development is complete and you're ready to deploy to production. It's not a development checkpoint — it's the final verification before real users see the product.

Run sections in order. If you find problems, fix them before moving to the next section.

---

## 1. Production Configuration

**Environment Variables**
- All required `.env` variables are configured on the deploy platform (Vercel, Netlify, etc.)
- No variable still uses development/test values (localhost URLs, Stripe test keys, etc.)
- Production API keys are the correct ones (not the same as dev if separate environments exist)
- The `.env` file is not in the repository — confirmed in `.gitignore`

**Database and External Services**
- Database points to the production instance, not development
- Access policies (e.g., Supabase Row Level Security) are active in production
- Webhooks and external integrations point to production URLs
- Rate limits and quotas of external services are adequate for expected traffic

**Build and Deploy**
- Production build compiles without errors and without critical warnings
- Deploy goes to the correct URL (not a test subdomain)
- www → non-www redirects (or vice versa) are configured
- HTTPS is active and the SSL certificate is valid

---

## 2. Errors and Crashes

**Console**
- No JavaScript console errors in the production version
- No critical warnings (prop types, missing keys in React, API deprecation)
- API calls don't fail silently

**User Error Handling**
- A custom 404 page exists (not the framework's default)
- A 500 / error boundary page exists for unexpected errors
- Forms show clear error messages, not stack traces or technical messages
- If an external API doesn't respond, the app shows a useful message — it doesn't crash

**Critical Flows Tested Manually**
- Registration / login / logout work end-to-end
- The product's main flow works from start to finish
- Payment (if present) works in production mode with a real test transaction
- Confirmation / notification email actually arrives (not just locally)

---

## 3. Performance

**Loading**
- Lighthouse score ≥ 80 on Performance (test on mobile, not just desktop)
- Hero and above-the-fold images are optimized (WebP/AVIF, correct dimensions)
- No image exceeds 200KB without a valid reason
- Fonts are preloaded and don't cause FOIT (invisible text during loading)

**JavaScript**
- Main bundle doesn't exceed 200KB gzip without a specific reason
- Secondary routes are in lazy loading (not everything loaded at startup)
- No huge libraries imported entirely when only small parts are needed

**Runtime**
- Long lists use virtualization or pagination — don't render 500 elements in DOM
- API calls don't repeat unnecessarily (caching where it makes sense)

---

## 4. Mobile

- The site/app is tested on a real physical device, not just the browser simulator
- No content overflows the viewport horizontally
- Touch targets (buttons, links) are clickable without needing pixel precision
- The mobile keyboard doesn't cover important inputs without scroll
- The viewport meta tag is present and doesn't disable zoom: `width=device-width, initial-scale=1`
- Tested in portrait and landscape mode

---

## 5. SEO — Launch Verification

> The per-page SEO work (content, metadata, image optimization, internal linking) should have been done during BUILD using `web-seo`. This section verifies the launch-critical items that only make sense once the full site exists.

**Indexability**
- `robots.txt` exists and is correctly configured — not blocking pages that should be indexed
- Admin, dashboard, and private routes have `<meta name="robots" content="noindex">` 
- `sitemap.xml` exists, includes all public indexable routes, and is submitted to Google Search Console

**Canonical URLs**
- Every page with duplicatable content has a canonical URL defined
- Paginated content (e.g., `/blog?page=2`) has canonical pointing to the base URL or uses `rel="next"` / `rel="prev"`
- www and non-www versions redirect to one canonical domain (verified in Production Configuration above)

**Social & Rich Visibility**
- Every public page has OpenGraph tags: `og:title`, `og:description`, `og:image`, `og:url`
- Twitter/X cards are configured: `twitter:card`, `twitter:title`, `twitter:description`, `twitter:image`
- OG images exist and are the correct dimensions (1200×630px)
- JSON-LD structured data is present for the content type (Article, Product, BreadcrumbList, etc.)
- If multilingual: `hreflang` attributes are set for each language/region pair

**Core Web Vitals**
- LCP (Largest Contentful Paint) < 2.5s on mobile
- CLS (Cumulative Layout Shift) < 0.1 — all images have `width` and `height` set
- INP (Interaction to Next Paint) < 200ms
- Run: `npx lighthouse [url] --emulated-form-factor=mobile` and verify all three pass

**Content Verification**
- All pages have unique `<title>` and `<meta description>` — no two pages share the same values
- No placeholder text ("Lorem ipsum", "TODO", "Coming soon") on indexed pages
- Internal links verified — no broken links on public pages

---

## 6. Basic Accessibility

- Text/background contrast meets WCAG AA minimum (4.5:1 for normal text)
- All buttons and links have readable text or `aria-label`
- Forms have labels associated with every field (not just placeholder)
- Keyboard navigation works: Tab traverses elements in the correct visual order
- No focus traps (modal that won't close with Escape, etc.)

---

## 7. Final Security

- HTTP security headers are configured: `X-Frame-Options`, `Content-Security-Policy` (even basic), `X-Content-Type-Options`
- npm dependencies have no known critical vulnerabilities: `npm audit`
- No sensitive API route is reachable without authentication
- Production logs don't print users' personal data or tokens

---

## 8. Communication and Content

- All placeholder text ("Lorem ipsum", "Coming soon", "TODO") is replaced
- Links to social, privacy policy, terms of service exist and work
- Privacy policy is present if the site collects personal data (legally required)
- Cookie banner is present if using third-party cookies or analytics
- Transactional emails (confirmation, password reset) use the correct domain in the sender

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD / PHASE 3: CONTROL (Category: **DEVELOPMENT**).
2. **Objective**: Verify that the project is technically ready for production.
3. **Recommended Next Step**:
   - If deploy is complete → Load `core-documentation` (Phase 4: LAUNCH).
   - If SEO per-page work is incomplete → Load `web-seo` and complete it before deploying.
   - If structural changes are needed before launch → Load `web-ux-ui`.
4. **Tool Tip**: A code-specialized agent ("Builder") is necessary here to handle server configurations and environment variables.
