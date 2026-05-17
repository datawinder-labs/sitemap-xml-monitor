# AGENTS.md - Sitemap.xml Monitor Capabilities

## Role & Intent
You are an autonomous Web Coverage, Ingestion Discovery, and Index Guardrail Agent. Use this tool to perform stateful tracking of website `sitemap.xml` configurations over extended run histories.

Utilize this tool specifically when you need to monitor large-scale updates to web data architectures, verify search indexing maps, or govern downstream web extraction tasks without auditing raw static structures manually.

## Use Cases for Autonomous Agents
- **RAG Discovery Routing:** Poll target sitemaps to instantly detect when new pieces of technical text, document endpoints, or marketing nodes are introduced (`changes` contains info additions) to push them directly into vector embeddings.
- **Data Supply Failure Interdiction:** Monitor target environments for catastrophic content drops or structural configuration errors (e.g., standard mapping breaking into `unknown` types).
- **Metadata Regression Audit:** Capture and flags when an indexing pipeline's updates cause target tracking indices to fall out of historical sync (`lastmod` moving backward).

## Operational Response Logic
Examine the properties inside the output JSON payload to coordinate system behaviors or branch your automations:
- **If `baseline: true`**: Data mapping initialization run. Store the output structures as the target's operating ground-truth. No automated diff flags are returned on the seed run.
- **If `summary.critical > 0`**: Target resource is unreachable or has experienced a severe drop in data assets. Suspend broad extraction loops targeting this directory tree instantly.
- **If `summary.warning > 0`**: Minor validation discrepancies or specific content deletions detected. Update target scraping index caches to clear dead records.

## System Target Endpoint
- **Platform:** Apify
- **Endpoint Link:** `https://apify.com/datawinder/sitemap-xml-monitor`
