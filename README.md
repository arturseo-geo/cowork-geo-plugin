# GEO Plugin for Claude Cowork

**Generative Engine Optimisation (GEO) — the first Cowork plugin built specifically for AI search visibility.**

Built by [Artur Ferreira](https://thegeolab.net) | The GEO Lab

---

## What This Plugin Does

GEO is the practice of optimising content to be cited by AI search engines — ChatGPT, Perplexity,
and Google AI Overviews. This plugin gives you the tools to measure, diagnose, and improve your
AI search visibility directly inside Claude Cowork.

No other plugin in the directory covers this. GEO is a new discipline, and this is its native Cowork tool.

---

## Skills (auto-activate when relevant)

| Skill | Activates When |
|-------|---------------|
| `citation-monitor` | You ask about citations, AI search visibility, or whether your content is being cited |
| `crawl-parity` | You ask about AI crawlers, log analysis, or why pages aren't cited |
| `geo-scoring` | You share a URL or ask how well content performs in AI search |
| `schema-optimization` | You share JSON-LD, ask about structured data, or schema validation |
| `ai-content-strategy` | You ask for a content brief, topic ideas, or GEO-optimised planning |

---

## Commands

| Command | What It Does |
|---------|-------------|
| `/geo:citation-check [domain]` | Run the 30-check citation protocol across all 3 AI platforms |
| `/geo:crawl-parity [domain]` | Compare Googlebot vs AI crawler access — 3-category parity report |
| `/geo:geo-score [url]` | Score a page against the 5-layer GEO Stack (0–100) |
| `/geo:schema-check [url]` | Audit and fix JSON-LD structured data |
| `/geo:brief [keyword]` | Generate a GEO-optimised content brief with entity targets |

---

## Agent

`weekly-geo-monitor` — Run all monitoring jobs in one pass: citation check, crawl parity,
GEO score delta, and consolidated weekly report logged to Notion/Sheets.

Invoke: *"Run the weekly GEO report"* or *"Run all GEO monitoring jobs"*

---

## Required Connectors

| Connector | Used For |
|-----------|---------|
| DataForSEO | AIO detection, SERP features, keyword data |
| Google Search Console | URL coverage, impressions, crawl data |
| Firecrawl | Page extraction and content analysis |
| Notion *(optional)* | Experiment tracking, score history |
| Google Drive *(optional)* | Citation rate logs, brief storage |
| Google Analytics 4 *(optional)* | Traffic correlation with GEO score |

---

## The 5-Layer GEO Stack

This plugin scores every page against five layers:

1. **Extractability** — Can AI crawlers cleanly parse the content?
2. **Entity Density** — Are real-world entities named and attributed?
3. **Declarative Structure** — Are claims stated directly and citably?
4. **Schema Coverage** — Does structured data match and enrich the content?
5. **Citation Signals** — Are external sources named and linked?

Each layer scores 0–10. Combined GEO Score = sum × 2 (max 100).

---

## Install

```bash
# Add the marketplace
claude plugin marketplace add arturseo-geo/geo-plugin

# Install the plugin
claude plugin install geo@geo-plugin
```

Or install directly from Cowork → Customize → Browse Plugins.

---

## About

This plugin packages research and methodology from [The GEO Lab](https://thegeolab.net),
where 20+ controlled GEO experiments are actively running. The 30-check citation protocol,
5-layer scoring system, and crawl parity framework are all derived from real measurement work.

**Current experiment results:**
- E001: Declarative vs narrative content → +24pp citation rate on Perplexity
- E002: Entity density baseline → 3% combined citation rate at 3% entity density
- E014: System memory signals → 6.7% combined, 20% on Perplexity alone

---

From the [GEO Lab experiment series](https://thegeolab.net/geo-experiments/) by [Artur Ferreira](https://thegeolab.net/about/)
