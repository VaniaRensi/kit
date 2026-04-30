---
name: web-seo
category: development
description: >
  SEO applied page by page during BUILD. Load this skill every time you create a new route,
  add content, or insert images. Covers human-first content, URL/H1 alignment, metadata,
  image optimization, and internal linking. Launch-time SEO (sitemap, canonical, OG, schema)
  lives in web-deploy — that is a separate, one-time check at the end.
---

# SEO — Build It Right From The Start

SEO is not a phase you do at the end. It's a habit applied every time you create a page or add content. If you wait until launch to think about it, you are rewriting everything.

**This skill is loaded:**
- When creating a new route or page
- When writing page content
- When adding images
- When naming URLs

**Launch-time SEO** (sitemap, canonical URLs, OG tags, schema, robots.txt) is a separate checklist in `web-deploy`. That skill runs once before going live.

---

## 1. Human-First Content

Write for the person reading the page. Search engines are secondary.

**Rules:**
- One clear topic per page — don't try to rank for ten things at once
- Use the keyword naturally in the first paragraph — don't force it
- No keyword stuffing — if it sounds unnatural when read aloud, rewrite it
- Short paragraphs (3–4 lines max) — walls of text lose readers and rankings
- Use subheadings (H2, H3) to break up content — they help both readers and crawlers

```
❌ "Our AI refactoring tool is the best AI refactoring tool for AI-powered refactoring of AI code using AI."

✅ "AI Kit Base helps you refactor legacy code safely — without touching the original files."
```

---

## 2. URL + H1 Correspondence

Every page's URL slug and H1 must describe the same topic. Mismatches confuse both users and crawlers.

**Rules:**
- URL slug uses hyphens, lowercase, no special characters
- H1 contains the core concept of the URL — not a creative tagline
- One H1 per page — never two

```
❌ URL: /refactor   H1: "Transform Your Code Safely"
✅ URL: /refactor   H1: "Refactor Legacy Code Without Risk"

❌ URL: /pricing    H1: "Find Your Plan"
✅ URL: /pricing    H1: "Pricing — Simple Plans for Every Team"
```

**When creating a new route**, define the URL slug and H1 together — they are the same decision.

---

## 3. Heading Hierarchy

Structure each page like an outline. Crawlers build a document map from headings.

**Rules:**
- `H1` — one per page, the page topic
- `H2` — major sections
- `H3` — subsections within an H2
- Never skip levels (H1 → H3 with no H2)
- Never use headings for styling — use CSS classes instead

```
❌ <h1>AI Kit Base</h1>
   <h3>Why Use It</h3>    ← skipped H2

✅ <h1>AI Kit Base</h1>
   <h2>Why Use It</h2>
   <h3>For Solo Developers</h3>
   <h3>For Teams</h3>
```

---

## 4. Meta Title & Description (Per Page)

Write these when you create the page — not at launch. Every route needs its own, unique pair.

**Title rules:**
- Under 60 characters (Google truncates beyond this)
- Contains the primary keyword near the front
- Format: `[Page Topic] | [Brand Name]`
- Never use "Home", "Page", or the framework name

**Description rules:**
- 140–160 characters
- One sentence that explains the value of this specific page
- Ends with a subtle call to action if space allows
- No keyword stuffing — this is your ad copy in search results

```
❌ <title>Welcome to Our Website</title>
   <meta name="description" content="This is the home page of our product." />

✅ <title>AI Kit Base — Professional AI Coding Framework</title>
   <meta name="description" content="Structured skills and phases for building, auditing, and refactoring software with AI agents. Open source." />
```

**In Next.js**, use `generateMetadata()` for dynamic routes — never hardcode metadata in layout files for pages that need unique values.

---

## 5. Image Optimization

Every image you add has four decisions: format, size, filename, alt text. Make all four at the time of insertion — not at launch.

### Format
- Use **WebP** as default for photos and complex images
- Use **AVIF** if your build pipeline supports it (better compression than WebP)
- Use **SVG** for icons, logos, illustrations — never rasterize these
- Avoid PNG for photos and JPEG for anything new

### Size
- Target **under 150KB** for most images
- Hero/banner images: under 200KB
- Thumbnails and avatars: under 30KB
- Use [Squoosh](https://squoosh.app) or `sharp` in your build pipeline to compress

### Dimensions
- Serve images at the size they are displayed — never a 2000px image in a 400px card
- Always specify `width` and `height` attributes to prevent **Cumulative Layout Shift (CLS)**
- In Next.js: use the `<Image>` component — it handles WebP conversion, lazy loading, and CLS prevention automatically

### Lazy Loading
- All images **below the fold** → `loading="lazy"`
- Hero / above-the-fold images → `loading="eager"` or `<link rel="preload">`
- In Next.js `<Image>`: `priority={true}` for above-the-fold, default (lazy) for everything else

### Filename
- Descriptive, hyphen-separated: `audit-playbook-diagram.webp`, not `IMG_4921.jpg`
- Lowercase only — no spaces, no underscores
- The filename is indexed by Google Image Search

### Alt Text
- Describe what the image shows, not what you want to rank for
- For decorative images (dividers, backgrounds): `alt=""` — empty string, not missing
- For functional images (buttons with only an icon): describe the action, not the image

```
❌ <img src="/img/img1.png" alt="image" />
❌ <img src="/photo.jpg" />

✅ <img src="/audit-playbook-flow.webp" alt="Diagram showing how 6 audit reports are synthesized into a single AI Playbook" width="800" height="450" loading="lazy" />
```

---

## 6. Internal Linking

When you create a new page, link to it from at least one existing page. And link from it to at least one related page. Internal links distribute authority and help crawlers discover new content.

**Rules:**
- Anchor text must describe the destination — never "click here" or "read more"
- Link from high-traffic pages to new or important pages
- Don't orphan a page — every page must be reachable from at least one other page
- Navigation, footer, and sidebars count as internal links

```
❌ <a href="/refactor">Click here</a> to learn about refactoring.
✅ Learn more about <a href="/refactor">safe code refactoring with AI Kit</a>.
```

**When creating a new page**, ask: which existing pages should link here? Add those links before considering the page complete.

---

## 🏁 Skill Path & Next Step

1. **Current State**: PHASE 2: BUILD (Category: **DEVELOPMENT**).
2. **When to load**: Every new route, every content block, every image insertion.
3. **Recommended Next Step**:
   - Page content and metadata ready → continue building with `web-ux-ui`.
   - All pages built → `core-quality` checkpoint (Phase 3: CONTROL).
   - Ready to go live → `web-deploy` for the launch SEO checklist (sitemap, canonical, OG, schema).
4. **Flow**: `web-ux-ui` (build page) → `web-seo` (content + images + meta) → `core-quality` → `web-deploy` (launch)
