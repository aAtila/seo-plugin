---
name: semantic-html
description: Use when writing or reviewing HTML/JSX - catches divs-for-everything, skipped heading levels, onClick on non-interactive elements, cursor-pointer on divs, missing or incorrect alt text, a11y audit failures
---

# Semantic HTML

## Overview

Semantic HTML uses elements that convey meaning, not just appearance. Proper semantics improve accessibility (a11y), SEO, and maintainability. Screen readers, search engines, and future developers all benefit.

## When to Use

- Writing or reviewing any JSX/HTML
- Creating new UI components
- Responding to accessibility audit findings (WCAG, Lighthouse)
- Fixing "div soup" / "divitis" in existing code

## Review Checklist

### 1. Heading Hierarchy

- [ ] Single `<h1>` per page
- [ ] No skipped levels (h1 → h2 → h3, never h1 → h3)
- [ ] Headings reflect document outline, not visual styling

```tsx
// ❌ Using h3 for visual style
<h3 className="text-sm">Subtitle</h3>
// ✅ Correct level, styled smaller
<h2 className="text-sm">Subtitle</h2>
```

### 2. Landmark Elements

- [ ] Page has `<main>` (exactly one)
- [ ] Navigation uses `<nav>`
- [ ] Sections have headings or `aria-labelledby`

| Element | Use For |
|---------|---------|
| `<header>` | Page/section header |
| `<nav>` | Navigation links |
| `<main>` | Primary content (one per page) |
| `<section>` | Thematic grouping with heading |
| `<article>` | Self-contained content (post, card) |
| `<aside>` | Supplementary (sidebars, CTAs) |
| `<footer>` | Page/section footer |

When multiple sections exist:
```tsx
<section aria-labelledby="team-heading">
  <h2 id="team-heading">Our Team</h2>
</section>
```

### 3. Sectioning: Section vs Article

- [ ] `<section>` has a thematic purpose (not just for styling/spacing)
- [ ] `<article>` is self-contained (makes sense syndicated or standalone)
- [ ] Sections have an associated heading
- [ ] Not using `<article>` as a generic container

| Element | Use For | Test |
|---------|---------|------|
| `<section>` | Thematic grouping | "What is this section about?" has clear answer |
| `<article>` | Independent content | Would make sense in an RSS feed or reposted |

```tsx
// ❌ Article as generic wrapper
<article className="card-wrapper">...</article>

// ✅ Article for self-contained content
<article>
  <h2>How to Recover Data from SSD</h2>
  <p>Published: <time datetime="2026-01-02">Jan 2, 2026</time></p>
  <p>Content that stands alone...</p>
</article>

// ❌ Section for layout spacing
<section className="py-8">...</section>

// ✅ Section with thematic purpose
<section aria-labelledby="services-heading">
  <h2 id="services-heading">Our Services</h2>
  ...
</section>
```

### 4. Lists

- [ ] Collections use `<ul>` or `<ol>`, not div soup
- [ ] Navigation links wrapped in `<ul>` inside `<nav>`
- [ ] Definition lists for term-definition pairs

```tsx
// ❌ Divs for collection
<div className="cards"><div>Card 1</div></div>
// ✅ Semantic list
<ul className="cards"><li>Card 1</li></ul>
```

**Definition lists** for glossaries, FAQs, or key-value pairs:

```tsx
// ✅ Term-definition relationships
<dl>
  <dt>SSD</dt>
  <dd>Solid State Drive - storage using flash memory</dd>

  <dt>HDD</dt>
  <dd>Hard Disk Drive - storage using magnetic platters</dd>
</dl>

// ❌ Don't use dl for generic key-value that aren't definitions
// Use a table or simple list instead
```

### 5. Links vs Buttons

- [ ] Navigation uses `<Link>` or `<a href>`
- [ ] Actions use `<button>`
- [ ] No `onClick` on divs or spans
- [ ] No `<a href="#">` for actions

| Use | Element |
|-----|---------|
| Navigate to page | `<Link to>` or `<a href>` |
| Action (submit, toggle, open modal) | `<button>` |

```tsx
// ❌ Div with onClick for navigation
<div onClick={() => navigate('/about')}>About</div>
// ✅ Proper link
<Link to="/about">About</Link>

// ❌ Anchor for action
<a href="#" onClick={handleSubmit}>Submit</a>
// ✅ Button
<button onClick={handleSubmit}>Submit</button>
```

Clickable cards: wrap entire content in `<Link>`, not `onClick` on div.

### 6. Images & Figures

- [ ] Informative images have descriptive `alt`
- [ ] Decorative images have `alt=""`
- [ ] Images inside links with visible text have `alt=""`
- [ ] Referenced images/diagrams use `<figure>` with `<figcaption>`

```tsx
// Informative - describe what's shown
<img src="/team.jpg" alt="Team working in the lab" />

// Decorative - empty alt
<img src="/pattern.svg" alt="" />

// Inside link with text - empty alt (link text provides context)
<Link to="/ssd">
  <img src="/ssd.jpg" alt="" />
  <h3>SSD Recovery</h3>
</Link>
```

**Figures** for images/diagrams referenced in content:

```tsx
// ✅ Image that's referenced or explained
<figure>
  <img src="/data-flow.png" alt="Diagram showing data flow from client to server" />
  <figcaption>Figure 1: Request lifecycle in the application</figcaption>
</figure>

// ❌ Don't use figure for purely decorative images
// ❌ Don't use figure without figcaption
```

### 7. Text Elements

- [ ] Paragraphs use `<p>`, not `<div>`
- [ ] Important text uses `<strong>`, not styled `<span>`
- [ ] Emphasized text uses `<em>`, not styled `<span>`
- [ ] Dates/times use `<time datetime="...">`
- [ ] Contact info uses `<address>`

| Element | Use For |
|---------|---------|
| `<p>` | Paragraphs of text |
| `<strong>` | Important text (not just bold) |
| `<em>` | Emphasized text (not just italic) |
| `<time>` | Dates and times |
| `<address>` | Contact information |

### 8. Forms

- [ ] Inputs have associated `<label>` elements
- [ ] Related inputs grouped with `<fieldset>` and `<legend>`
- [ ] Required fields indicated accessibly (not just color)
- [ ] Error messages linked to inputs via `aria-describedby`

```tsx
// ❌ Placeholder as label
<input placeholder="Email" />

// ✅ Proper label association
<label htmlFor="email">Email</label>
<input id="email" type="email" />

// ✅ Grouped related fields
<fieldset>
  <legend>Shipping Address</legend>
  <label htmlFor="street">Street</label>
  <input id="street" />
  ...
</fieldset>

// ✅ Error message linked to input
<label htmlFor="email">Email</label>
<input id="email" aria-describedby="email-error" aria-invalid="true" />
<span id="email-error">Please enter a valid email</span>
```

### 9. ARIA: Use Sparingly

- [ ] Native HTML used before ARIA (first rule of ARIA)
- [ ] ARIA only when no native element exists
- [ ] No redundant ARIA (e.g., `role="button"` on `<button>`)

```tsx
// ❌ Redundant ARIA
<button role="button">Click</button>
<nav role="navigation">...</nav>

// ❌ ARIA to fix bad HTML
<div role="button" tabindex="0" onClick={...}>Click</div>

// ✅ Just use the native element
<button onClick={...}>Click</button>

// ✅ ARIA when needed (custom widget with no native equivalent)
<div role="tablist">
  <button role="tab" aria-selected="true">Tab 1</button>
  <button role="tab" aria-selected="false">Tab 2</button>
</div>
```

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| `<div>` with heading styles | Use `<h1>`-`<h6>` |
| Skipped heading levels | Correct hierarchy, style with CSS |
| `<a href="#">` for actions | Use `<button>` |
| Missing `alt` attribute | Add descriptive text or `alt=""` |
| `onClick` on divs/spans | Use `<Link>` or `<button>` |
| `cursor-pointer` on div | Make it a real interactive element |
| `<div>` for paragraphs | Use `<p>` |
| `<b>` / `<i>` for semantics | Use `<strong>` / `<em>` |
| `<article>` as generic wrapper | Use `<div>` or `<section>` |
| `<section>` for spacing | Use `<div>` with classes |
| `<figure>` without `<figcaption>` | Add caption or use plain `<img>` |
| `<dl>` for non-definitions | Use `<ul>` or `<table>` |
| Placeholder as only label | Add visible `<label>` |
| `role="button"` on `<button>` | Remove redundant ARIA |
