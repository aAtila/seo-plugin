---
name: semantic-review
description: Use when a page implementation is complete and needs semantic HTML audit - comprehensive document-level analysis with severity classification, before making any fixes
---

# Semantic Review

## Overview

A comprehensive semantic HTML audit for completed pages. This is **analysis mode only** - identify and classify issues before implementing fixes.

## When to Use

- Page implementation is complete
- Before final QA sign-off
- After accessibility audit flags issues
- Periodic codebase health checks

**Not for:** Active development (use `semantic-html` skill instead)

## Execution Rules

**STOP. This is review-only mode.**

- Do NOT refactor code
- Do NOT rewrite markup
- Do NOT suggest exact replacement snippets
- Do NOT implement changes

Evaluate. Classify. Report. Wait for explicit approval.

## Review Framework

### Phase 1: Document-Level Assessment

Answer these questions first:

1. **Meaning vs Layout**: Does the HTML describe the *meaning* of the page, not just its visual layout?
2. **Machine Readability**: Could a non-visual agent (screen reader, crawler, AI) understand the page structure?
3. **Intent & Hierarchy**: Does the markup reflect intent, hierarchy, and relationships correctly?

### Phase 2: Systematic Review

Evaluate each lens. For every issue found, note:
- What the problem is
- Why it weakens semantic clarity
- Severity classification (see below)

#### 1. Landmark & Page Structure

- Is `<main>` used correctly and uniquely?
- Are `<header>`, `<footer>`, `<nav>`, `<aside>` used with intent?
- Do landmarks meaningfully divide the page?

#### 2. Sectioning & Content Grouping

- Are `<section>` and `<article>` used appropriately?
- Does each `<section>` have a clear thematic purpose?
- Are sections used for meaning, not spacing or styling?
- Are deeply nested sections justified?

#### 3. Heading Hierarchy

- Is heading order logical and uninterrupted?
- Do headings reflect semantic structure, not visual size?
- Are headings present where sectioning elements imply them?

#### 4. Content Semantics

- Are lists (`<ul>`, `<ol>`, `<dl>`) used correctly for their content type?
- Are `<dl>`, `<dt>`, `<dd>` used only for true term-definition relationships?
- Are `<figure>` and `<figcaption>` used where visual content conveys meaning?
- Is `<aside>` reserved for tangential or complementary content?

#### 5. Interactive Elements

- Are buttons vs links chosen based on action vs navigation?
- Are form elements labeled and grouped meaningfully?
- Are ARIA roles used only where native semantics are insufficient?

#### 6. Anti-Patterns

- Overuse of `<div>` where semantic elements exist
- Sections without headings
- Misuse of `<article>` for generic containers
- Decorative markup posing as semantic structure

## Severity Classification

For each finding, classify as:

| Classification | Meaning |
|----------------|---------|
| **Semantically sound** | Correct usage, no action needed |
| **Ambiguous / debatable** | Could go either way, document reasoning |
| **Semantically incorrect** | Clearly wrong, must fix |

And categorize impact:

| Impact | Examples |
|--------|----------|
| **Low-impact cleanup** | Minor improvements, nice-to-have |
| **Structural concern** | Affects page understanding, should fix |
| **Systemic pattern** | Recurring issue, needs codebase-wide guidance |

## Report Format

```markdown
## Semantic Review: [Page Name]

### Document-Level Assessment
[Answer the three Phase 1 questions]

### Findings

#### [Category]: [Specific Issue]
- **Location**: [file:line or component]
- **Problem**: [What's wrong]
- **Why it matters**: [Impact on a11y/SEO/maintainability]
- **Classification**: [sound/ambiguous/incorrect]
- **Impact**: [low/structural/systemic]
- **Correction type**: [conceptual description, NOT code]

### Summary
- **Overall quality**: [assessment]
- **HTML5 alignment**: [yes/partial/no]
- **Recurring patterns**: [list any systemic issues]

### Recommended Actions
[Prioritized list of what to address]
```

## Post-Review Actions

**STOP after analysis.**

Wait for explicit instruction:
- "Proceed with semantic fixes"
- "Apply agreed structural corrections"
- "Fix [specific issue]"

Until then, remain in **review-only mode**.
