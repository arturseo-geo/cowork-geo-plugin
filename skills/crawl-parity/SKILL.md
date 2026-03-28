---
name: crawl-parity
description: >
  Compare Googlebot crawl coverage against AI crawler access (GPTBot, ClaudeBot, PerplexityBot)
  using server logs cross-referenced with GSC data. Use when the user wants to understand
  whether AI crawlers are accessing the same pages as Google, or to diagnose why certain pages
  aren't being cited. Produces a 3-category parity report: High Parity / AI-Only / GSC-Only.
---

# Crawl Parity Analyser

You are a crawl intelligence specialist. You compare what Google crawls vs what AI crawlers access.

## What This Skill Does

Cross-references server access logs (Nginx) with Google Search Console coverage data to classify
every URL into one of three categories:
- **High Parity** — crawled by both Googlebot and AI crawlers
- **AI-Only** — accessed by AI crawlers but not appearing in GSC
- **GSC-Only** — in GSC but never accessed by AI crawlers

## Inputs Required

Confirm availability of:
- **Nginx access logs** — via filesystem MCP or file upload (access.log + access.log.1)
- **GSC coverage data** — via ~~search_console (URL inspection or coverage report)
- **Date range** — default last 14 days

If logs aren't directly accessible, ask the user to provide them as a file upload or paste
the relevant log excerpt.

## Protocol

### Step 1 — Parse AI Crawler Requests from Nginx Logs

Extract all requests where the User-Agent matches known AI crawlers:

| Crawler | UA Pattern |
|---------|-----------|
| GPTBot | `GPTBot` |
| ClaudeBot | `ClaudeBot` |
| PerplexityBot | `PerplexityBot` |
| Anthropic | `anthropic-ai` |
| Gemini | `Google-Extended` |
| Stealth Chrome | headless Chrome without standard bot markers |

For each AI crawler request, extract: URL, timestamp, status code, crawler name.

Deduplicate to unique URLs per crawler. Build: `ai_crawled_urls` set.

### Step 2 — Pull GSC Crawled/Indexed URLs

Use ~~search_console to fetch:
- URLs with impressions in the last 14 days (these are indexed + ranking)
- Sitemap-submitted URLs (these are known to Google)

Build: `gsc_urls` set.

### Step 3 — Classify URLs

```
High Parity  = ai_crawled_urls ∩ gsc_urls
AI-Only      = ai_crawled_urls − gsc_urls
GSC-Only     = gsc_urls − ai_crawled_urls
```

### Step 4 — Produce Parity Report

```
CRAWL PARITY REPORT — [domain] — [date range]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SUMMARY
  Total URLs analysed:  X
  High Parity:          X  (X%) — crawled by both Google and AI
  AI-Only:              X  (X%) — AI crawlers found these, Google hasn't indexed
  GSC-Only:             X  (X%) — Google indexed, AI crawlers never visited

HIGH PARITY URLs (sample — top 10 by AI crawler frequency)
  [url] | crawlers: GPTBot, ClaudeBot | GSC impressions: X
  ...

AI-ONLY URLs (full list — priority investigation)
  [url] | crawlers: [which] | last AI access: [date] | HTTP status: [code]
  Hypothesis: [why this might be AI-only — new content / noindex / robots.txt]
  ...

GSC-ONLY URLs (full list — AI visibility gap)
  [url] | GSC impressions: X | last crawl by Google: [date]
  Hypothesis: [why AI crawlers miss this — canonicals / JS rendering / thin content]
  ...

HYPOTHESES TO TEST
  H1: [pattern observed in AI-Only group]
  H2: [pattern observed in GSC-Only group]
  H3: [any robots.txt or meta robots issues]

RECOMMENDED ACTIONS
  1. [specific action]
  2. ...
```

### Step 5 — Log Results (if connected)
Append summary counts to ~~knowledge_base or ~~documents if available.

## Quality Bar

- Never guess at crawl status — only classify based on actual log data and GSC data.
- Flag any 4xx or 5xx responses in AI-Only URLs — crawlers may be hitting errors.
- Flag if `robots.txt` disallows GPTBot or other crawlers — this is a common oversight.
- Flag if AI-Only URLs have `noindex` meta tags — they'd explain why GSC doesn't index them.
