---
name: content-triples-audit
description: Use when reviewing page content for semantic SEO quality - flags vague predicates like "helps" or "improves", unfalsifiable claims, disconnected entities, content that "feels fluffy"
---

# Content Triples Audit

## Overview

Analyze content for SPO (Subject-Predicate-Object) triple quality. Search engines and LLMs consume pages as graphs of factual statements, not paragraphs. Weak triples hurt machine comprehension and AI retrieval.

## When to Use

- Reviewing draft or published content for semantic clarity
- After writing a new service/product page
- When content "feels fluffy" but you can't pinpoint why
- Before structured data work (ensure copy expresses clean facts first)

## Input

Markdown content (pasted or from source files). Parse into sections using headings as delimiters.

## Output Format

### Part 1: Summary Table

| Section | Triples | Weak | Issues |
|---------|---------|------|--------|
| Hero | 3 | 1 | Vague predicate |
| Service Scope | 6 | 0 | — |

### Part 2: Section Breakdown (for sections with issues)

```
### Section Name (N issues)

**Strong triples:**
- Subject → Predicate → Object
- Subject → Predicate → Object

**Weak triples:**

1. VAGUE PREDICATE: "We help businesses recover data"
   - We → help → businesses
   - Problem: "help" is not falsifiable
   
2. UNFALSIFIABLE: "Trusted by enterprises worldwide"
   - Cannot be proven or disproven
```

## Detection Criteria

### Priority 1: Vague Predicates

**Flag:** helps, improves, enables, enhances, empowers, supports (abstract), provides (abstract), ensures, guarantees (non-contractual)

**Prefer:** requires, depends on, causes, prevents, contains, consists of, runs, executes, fails due to, is incompatible with, produces, generates

### Priority 2: Unfalsifiable Claims

- Cannot be proven/disproven ("trusted by...", "leading provider")
- Comparative without reference ("better than...", "faster...")
- Branding rather than facts ("Recovering the Unrecoverable")

### Priority 3: Missing Objects

Subject and predicate exist but object is vague or implied ("We handle complex cases")

### Priority 4: Disconnected Entities

Entity mentioned but never appears as subject or object in any triple. Key topic entities missing entirely.

## Workflow

1. Receive markdown content
2. Parse into sections (headings as delimiters)
3. Extract SPO patterns from natural language (interpretive, not mechanical)
4. Evaluate each triple against detection criteria
5. Present summary table + section breakdown
6. **STOP. Wait for user.**

## After Analysis

Do NOT automatically rewrite. Wait for explicit request:
- "Fix section 3"
- "Rewrite the hero"
- "Suggest stronger predicates for the FAQ"

Then propose specific rewrites converting weak triples to strong ones.
