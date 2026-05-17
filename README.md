# Sitemap.xml Monitor

A stateful, diff-based `sitemap.xml` tracking and coverage monitoring Actor designed for autonomous data engines, continuous SEO guardrails, and enterprise RAG pipelines.

Unlike stateless index parsers that dump large volumes of noisy data or trigger false positives over minor spacing updates, this tool utilizes a **versioned stable snapshot contract (v1)**. It tracks structural metadata shifts and page availability over time, filtering out superficial noise so downstream AI agents or webhooks only ingest actionable changes.

## Key Features

- **Stateful Baseline Architecture:** Stores a normalized snapshot on the first execution and computes explicit deltas from the second run onward.
- **Mass-Deletion Protection:** Automatically triggers high-priority alerts if a major structural drop occurs (e.g., ≥30% of URLs or ≥50% of index paths vanish).
- **Strict Severity Contract:** Divides operational signals into distinct tiers (`critical`, `warning`, `info`) to eliminate developer alert fatigue.
- **Formatting-Only Insulation:** Standardizes and normalizes attribute order, tag arrangements, white-space variances, and XML namespace prefixes.

## Usage & Integration

This tool runs as a managed Actor on the Apify platform. 
**[Run on Apify Store →](https://apify.com/datawinder/sitemap-xml-monitor)**

### Network & Fetch Failure Semantics
To prevent down-line execution pipelines from crashing, network timeouts or fetch blocks are assigned an `httpStatus = 0` failure profile. The Actor will still output data objects during reachability failures to maintain continuity logs.

---

## Alert Semantics (Severity Contract)

This Actor follows a rigorous operational runtime design, making it safe to link straight to notifications, alert queues, or autonomous script execution:

| Severity Tier | System Trigger Parameters | Downstream System Target |
| :--- | :--- | :--- |
| **🔴 Critical** | File unreachable; Sitemap type changes; Mass URL purge (≥30%). | **Page On-Call / Halt Pipeline** |
| **🟠 Warning** | Individual URL drops; `lastmod` moving backward; Corrupted formatting. | **Notify Slack/DevOps Logs** |
| **🔵 Info** | New URL nodes discovered; `priority`/`changefreq` updates; Formatting edits. | **Silent Audit Append** |

---

## Output Contract Example

Subsequent runs output an optimized JSON delta object engineered for instant automated consumption:

```json
{
  "baseline": false,
  "unchanged": false,
  "summary": {
    "critical": 0,
    "warning": 1,
    "info": 2
  },
  "changes": [
    {
      "type": "lastmod_regression",
      "severity": "warning",
      "url": "[https://example.com/docs/intro](https://example.com/docs/intro)",
      "description": "Timestamp moved backward"
    }
  ],
  "unchangedCount": 1420
}
```
## Recommended Ingestion Setup
Frequency: Automate via Apify scheduling structures to loop hourly or daily.

Data Supply Signal: Use this as a discovery roadmap upstream from your web crawlers or vector embed pipelines. Treat your sitemap.xml as a real-time index coverage tracker rather than a static document.
