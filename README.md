# SEO Plugin for Claude Code

SEO best practices for web development - semantic HTML, meta tags, structured data, and more.

## Installation

```bash
/plugin marketplace add aAtila/seo-plugin
/plugin install seo@aAtila
```

Then restart Claude Code.

## Skills

### semantic-html

**Use during:** Writing or reviewing HTML/JSX

Checklist-based skill that catches common issues:

- Div soup / divitis
- Skipped heading levels
- `onClick` on non-interactive elements
- Missing or incorrect alt text
- Improper landmark usage
- Section vs article misuse
- Form labeling issues
- Redundant ARIA

Triggers automatically when writing or reviewing HTML/JSX.

### semantic-review

**Use after:** Page implementation is complete

Comprehensive semantic audit methodology:

- Document-level assessment (meaning vs layout)
- Systematic review across 6 lenses
- Severity classification (sound/ambiguous/incorrect)
- Impact categorization (low/structural/systemic)
- Analysis-only mode (no auto-fixing)

Run explicitly when you want a thorough review before final QA.

### content-triples-audit

**Use when:** Reviewing content for semantic SEO quality

Analyzes page content for SPO (Subject-Predicate-Object) triple quality:

- Flags vague predicates ("helps", "improves", "enables")
- Identifies unfalsifiable claims ("trusted by...", "leading provider")
- Catches missing objects and disconnected entities
- Produces summary table + section-by-section breakdown

Analysis only - waits for explicit approval before suggesting rewrites.

## License

MIT
