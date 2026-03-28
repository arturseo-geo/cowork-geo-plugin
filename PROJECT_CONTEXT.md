# Project Context — cowork-geo-plugin

## Purpose
GEO / AI Visibility Cowork Plugin for Claude Cowork. Packages domain-specific skills, commands, and an autonomous agent into a single installable plugin.

## Architecture
- **Skills (5):** citation-monitor, crawl-parity, geo-scoring, schema-optimization, ai-content-strategy
- **Commands (5):** /geo:citation-check, /geo:crawl-parity, /geo:geo-score, /geo:schema-check, /geo:brief
- **Agent:** weekly-geo-monitor

## Design Decisions
- Skills contain the domain knowledge and step-by-step instructions
- Commands are lightweight entry points that invoke the right skill
- The agent chains multiple skills into an autonomous workflow
- MCP connectors declared in .mcp.json (user configures credentials)

## Installation
Cowork → Customize → Browse Plugins → Upload → select ZIP.

## Author
Artur Ferreira / The GEO Lab (thegeolab.net)
