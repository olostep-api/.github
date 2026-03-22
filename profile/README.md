<div align="center">

<img src="https://www.olostep.com/images/olostep_logo.png" alt="Olostep Logo" width="120" />

# Olostep

### Extract clean, structured data from any website — in real time.

**The web scraping, crawling, and search API powering the world's leading AI agents and companies.**

[![Website](https://img.shields.io/badge/🌐_Website-olostep.com-orange?style=for-the-badge)](https://www.olostep.com/)
[![Docs](https://img.shields.io/badge/📚_Docs-docs.olostep.com-blue?style=for-the-badge)](https://docs.olostep.com/get-started/welcome)
[![Slack](https://img.shields.io/badge/💬_Slack-Join_Community-4A154B?style=for-the-badge&logo=slack)](https://olostep-users.slack.com/join/shared_invite/zt-2bfddyi8h-JzfjOgavg~98DJ1om1B5Lg#/shared-invite/email)
[![X / Twitter](https://img.shields.io/badge/𝕏_Twitter-@olostep-black?style=for-the-badge)](https://x.com/olostep)

</div>

---

## What is Olostep?

**Olostep is a web scraping, crawling, and search API** built for AI startups and companies that need real-time, clean, structured, and cost-effective web data — without the infrastructure headaches.

Whether you're building AI agents, LLM pipelines, data products, or automating research workflows, Olostep handles the hard parts: JavaScript rendering, anti-bot bypasses, structured extraction, and real-time crawling — so you can focus on what you're building.

> ⚡ Used by the top AI agents and companies to extract clean, structured web data at scale in the most reliable and cost-effective way on the market.

---

## Why Olostep?

**Scaling an AI product or company?** You need reliable, clean data from the web. Olostep handles the complexity of modern web scraping — bot detection, JavaScript-heavy pages, dynamic content, and schema-aligned extraction — so you don't have to.

- 🔍 **Web Search API** — Programmatic access to real-time web search results
- 🕷️ **Web Scraping API** — Extract clean, structured data from any URL, even JS-rendered pages
- 🌐 **Web Crawling API** — Recursively crawl entire websites and extract content at scale
- 🤖 **Built for AI Agents** — Clean markdown and structured JSON outputs, ready for LLMs
- ⚡ **Real-Time Extraction** — No caching, no stale data — live results every time
- 🛡️ **Anti-Bot Bypass** — Built-in handling for the toughest scraping challenges

The most cost-effective and reliable web data API on the market — trusted by top AI agents and leading companies. [See pricing →](https://www.olostep.com/pricing)


---
 
## Olostep Endpoints
 
| Endpoint | Description | Docs |
|---|---|---|
| **[Answers](https://www.olostep.com/answers-endpoint)** `POST /v1/answers` | Ask a question in natural language; get a source-backed answer and optional structured JSON — ideal for grounding LLMs on live web data | [→](https://docs.olostep.com/features/answers/answers) |
| **[Searches](https://www.olostep.com/searches-endpoint)** `POST /v1/searches` | Semantic web search from a plain-English query — deduplicated links with titles and descriptions | [→](https://docs.olostep.com/searches/searches) |
| **[Scrapes](https://www.olostep.com/scrapes-endpoint)** `POST /v1/scrapes` | Extract content from any URL — markdown, HTML, JSON, screenshots, and structured extraction | [→](https://docs.olostep.com/features/scrapes/scrapes) |
| **[Maps](https://www.olostep.com/maps-endpoint)** `POST /v1/maps` | Discover all URLs for a single domain with filters and cursor pagination | [→](https://docs.olostep.com/features/maps/maps) |
| **[Crawls](https://www.olostep.com/crawls-endpoint)** `POST /v1/crawls` | Walk an entire site from a start URL with depth and page limits; retrieve content per page | [→](https://docs.olostep.com/features/crawls/crawls) |
| **[Batches](https://www.olostep.com/batches-endpoint)** `POST /v1/batches` | Process large lists of arbitrary URLs in one job — with webhooks, parsers, and cursor pagination | [→](https://docs.olostep.com/features/batches/batches) |
 
→ [See all endpoints](https://www.olostep.com/endpoints)
 
---

## Core Repositories

| Repository | Description |
|---|---|
| **[olostep-js](https://github.com/olostep-api/olostep-js)** | Official JavaScript / TypeScript SDK |
| **[olostep-py](https://github.com/olostep-api/olostep-py)** | Official Python SDK |
| **[olostep-mcp-server](https://github.com/olostep/olostep-mcp-server)** | Olostep MCP Server |

---

## Quick Start

### JavaScript / TypeScript

```bash
npm install olostep
```

```javascript
import Olostep from 'olostep';

const client = new Olostep({apiKey: process.env.OLOSTEP_API_KEY});

// Minimal scrape example
const result = await client.scrapes.create('https://example.com');
console.log(result.id, result.html_content);
```

### Python

```bash
pip install olostep
```

```python
from olostep import Olostep

client = Olostep(api_key="your-api-key")

# Simple scraping
result = client.scrapes.create(url_to_scrape="https://example.com")
print(f"Scraped {len(result.markdown_content)} characters")

# Multiple formats
result = client.scrapes.create(
    url_to_scrape="https://example.com",
    formats=["html", "markdown"]
)
print(f"HTML: {len(result.html_content)} chars")
print(f"Markdown: {len(result.markdown_content)} chars")

# Crawl a website
crawl = client.crawls.create(
    start_url="https://www.olostep.com",
    max_pages=100,
    include_urls=["/integrations/**", "/blog/**"],
    exclude_urls=["/careers/**"]
)

for page in crawl.pages():
    content = page.retrieve(["html"])
    print(f"Crawled: {page.url}")
```

---

## Use Cases

- **AI Agent Data Pipelines** — Feed LLMs and AI agents with fresh, structured web data
- **Competitive Intelligence** — Monitor competitors, pricing, and market trends in real time
- **Lead Generation** — Extract contact data, company info, and signals at scale
- **Research Automation** — Automate web research workflows across thousands of pages
- **Price Tracking** — Monitor e-commerce prices and product availability
- **News & Content Aggregation** — Aggregate and structure content from across the web
- **SEO & SERP Analysis** — Analyze search results and track rankings programmatically

---

## Resources

- 📖 [Documentation](https://docs.olostep.com/get-started/welcome) — Full API reference and guides
- 🚀 [Get Started](https://www.olostep.com/) — Sign up and get your API key
- 💬 [Slack Community](https://olostep-users.slack.com/join/shared_invite/zt-2bfddyi8h-JzfjOgavg~98DJ1om1B5Lg#/shared-invite/email) — Get help and share what you're building
- 𝕏 [Twitter / X](https://x.com/olostep) — Follow for updates

---

<div align="center">

**[olostep.com](https://www.olostep.com/)** · The web scraping, crawling, and search API powering the world's leading AI agents and companies.

</div>
