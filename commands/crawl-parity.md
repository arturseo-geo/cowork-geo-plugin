---
description: Compare Googlebot vs AI crawler access patterns. Produces a 3-category parity report (High Parity / AI-Only / GSC-Only).
---

Use the crawl-parity skill to analyse crawler coverage.

Arguments: $ARGUMENTS

If a domain is provided, pull GSC data automatically.
If log files are referenced, read them from the filesystem.
If no arguments, ask the user to either provide a domain (for GSC pull) or upload/paste log data.

Return the full parity report with hypotheses and recommended actions.
