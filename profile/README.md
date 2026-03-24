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

# **Olostep**

**Extract clean, structured data from any website — in real time.**

[**Olostep**](https://www.olostep.com/) is an API that scrapes, crawls, searches, and answers questions from the web — powering AI agents and apps with real-time, structured data.

---

## Why Olostep?

- **LLM-ready output**: Clean markdown, structured JSON, screenshots, HTML, and more
- **Real-time extraction**: No caching, no stale data — live results every time
- **Handles the hard stuff**: JavaScript rendering, anti-bot bypasses, and dynamic content
- **Built for AI agents**: Schema-aligned extraction and natural language answers grounded on live web data
- **Cost-effective at scale**: The most reliable and affordable web data API on the market

---

## Quick Start

Sign up at [olostep.com](https://www.olostep.com/) to get your API key and start extracting data in seconds. Try the [playground](https://www.olostep.com/playground) to test it out.

### Make Your First API Request
```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"url_to_scrape": "https://example.com", "formats": ["markdown"]}'
```

Response:
```json
{
  "id": "scrape_bgfa9f9wim",
  "object": "scrape",
  "created": 1774350584,
  "url": "https://example.com",
  "retrieve_id": "bgfa9f9wim",
  "result": {
    "markdown_content": "Example Domain\n\nExample Domain\n==============\n\nThis domain is for use in documentation examples without needing permission. Avoid use in operations.\n\n[Learn more](https://iana.org/domains/example)",
    "html_content": null,
    "text_content": null,
    "json_content": null,
    "screenshot_hosted_url": null,
    "links_on_page": [],
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 1
}
```

<!-- ### Install the SDK

**JavaScript / TypeScript**
```bash
npm install olostep
```

**Python**
```bash
pip install olostep
```

Set your API key:
```bash
export OLOSTEP_API_KEY=your_api_key_here
``` -->

---

## Feature Overview

| Feature | Description | Docs |
|---------|-------------|------|
| [**Scrapes**](#scrapes) | Convert any URL to markdown, HTML, screenshots, or structured JSON | [→](https://docs.olostep.com/features/scrapes/scrapes) |
| [**Crawls**](#crawls) | Scrape all pages of a website with a single request | [→](https://docs.olostep.com/features/crawls/crawls) |
| [**Maps**](#maps) | Discover all URLs on a website instantly | [→](https://docs.olostep.com/features/maps/maps) |
| [**Batches**](#batches) | Process up to 10,000 URLs in one async job | [→](https://docs.olostep.com/features/batches/batches) |
| [**Answers**](#answers) | Ask a question in natural language; get a source-backed, structured answer from live web data | [→](https://docs.olostep.com/features/answers/answers) |
| [**Searches**](#searches) | Search the web with a plain-English query — deduplicated links with titles and descriptions | [→](https://docs.olostep.com/searches/searches) |
| [**Agents**](#agents) | Autonomous research agents that automate data pipelines and deliver structured results on a schedule | [→](https://docs.olostep.com/features/agents/agents) |

---

## Scrapes

Convert any URL to clean markdown, HTML, plain text, structured JSON, or a screenshot. Handles JavaScript-rendered pages, anti-bot challenges, and dynamic content automatically.

```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url_to_scrape": "https://docs.olostep.com/get-started/welcome",
    "formats": ["markdown", "html"]
  }'
```

Response:
```json
{
  "id": "scrape_309i70dx3x",
  "object": "scrape",
  "created": 1774366419,
  "url": "https://docs.olostep.com/get-started/welcome",
  "retrieve_id": "309i70dx3x",
  "result": {
    "markdown_content": "Welcome to Olostep - Olostep Docs\n\nOlostep is a web scraping, crawling, and search API...",
    "html_content": "<html lang=\"en\" class=\"__variable_47c970 ...\">...",
    "text_content": null,
    "json_content": null,
    "screenshot_hosted_url": null,
    "html_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/text_309i70dx3x.txt",
    "markdown_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/markDown_309i70dx3x.txt",
    "links_on_page": [],
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 1,
  "metadata": {}
}
```

### Extract Structured Data

You can extract structured JSON in two ways: **using Parsers** or **LLM extraction**.

#### Using a Parser (recommended for scale)

Parsers turn unstructured web data into structured JSON. They are ideal when you need data at scale in a recurrent way from the same websites — significantly more cost-efficient (1–5 credits) than LLM extraction (20 credits). Olostep offers [pre-built parsers](https://www.olostep.com/store) for popular websites, and you can also create your own through the [dashboard](https://www.olostep.com/dashboard/parsers).

Define `formats: ["json"]` and provide a `parser` `id`:

```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url_to_scrape": "https://www.google.com/search?q=olostep+web+scraping+api&gl=us&hl=en",
    "formats": ["json"],
    "parser": {
      "id": "@olostep/google-search"
    }
  }'
```

Response:
```json
{
  "id": "scrape_yxhfnrlfuh",
  "object": "scrape",
  "created": 1774369250,
  "url": "https://www.google.com/search?q=olostep+web+scraping+api&gl=us&hl=en",
  "retrieve_id": "yxhfnrlfuh",
  "result": {
    "html_content": null,
    "markdown_content": null,
    "text_content": null,
    "json_content": "{\"searchParameters\":{\"q\":\"olostep web scraping api\",\"gl\":\"us\",\"hl\":\"en\",\"type\":\"search\",\"engine\":\"google\"},\"organic\":[{\"title\":\"Olostep - Web Data API for AI, Crawling & Data Extraction\",\"link\":\"https://www.olostep.com/\",\"snippet\":\"Olostep is a Web Data API that helps AI teams search, crawl, scrape and structure web data through a single, developer-friendly platform. Built for modern AI ...\",\"position\":1},{\"title\":\"Olostep Docs: Welcome to Olostep\",\"link\":\"https://docs.olostep.com/get-started/welcome\",\"snippet\":\"The Olostep API is the best web search, scraping and crawling API for AI used by some of the leading startups in the world.\",\"position\":2},{\"title\":\"Scrape - Olostep Docs\",\"link\":\"https://docs.olostep.com/features/scrapes/scrapes\",\"snippet\":\"Through the Olostep /v1/scrapes endpoint you can extract LLM-friendly Markdown, HTML, text, screenshots, or structured JSON from any URL in real time.\",\"position\":3}],\"relatedSearches\":[{\"query\":\"Olostep web scraping api tutorial\"},{\"query\":\"Olostep pricing\"}]}",
    "screenshot_hosted_url": null,
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/json_yxhfnrlfuh.json",
    "links_on_page": [],
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 2,
  "metadata": {}
}
```

Available pre-built parsers include `@olostep/google-search`, `@olostep/amazon-it-product`, `@olostep/extract-emails`, `@olostep/extract-calendars`, and `@olostep/extract-socials`. Parsers are self-healing and update automatically when websites change. Need a custom parser? Contact [info@olostep.com](mailto:info@olostep.com).

#### Using LLM Extraction (schema and/or prompt)

For websites with changing structures or one-off extraction needs, provide `llm_extract` with a JSON Schema (`schema`) and/or a natural language instruction (`prompt`). You can pass both parameters, but if both are provided, `schema` takes precedence.

**With a schema:**

```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url_to_scrape": "https://en.wikipedia.org/wiki/Web_scraping",
    "formats": ["markdown", "json"],
    "llm_extract": {
      "schema": {
        "type": "object",
        "properties": {
          "title": {"type": "string"},
          "summary": {"type": "string"}
        }
      }
    }
  }'
```

Response:
```json
{
  "id": "scrape_afuw1y7lm0",
  "object": "scrape",
  "created": 1774369369,
  "url": "https://en.wikipedia.org/wiki/Web_scraping",
  "retrieve_id": "afuw1y7lm0",
  "result": {
    "markdown_content": "Web scraping - Wikipedia\n\nWeb scraping\n============\n\n...",
    "json_content": "{\"summary\":\"Web scraping, web harvesting, or web data extraction is data scraping used for extracting data from websites. Web scraping software may directly access the World Wide Web using the Hypertext Transfer Protocol or a web browser. While web scraping can be done manually by a software user, the term typically refers to automated processes implemented using a bot or web crawler.\",\"title\":\"Web scraping\"}",
    "html_content": null,
    "text_content": null,
    "screenshot_hosted_url": null,
    "markdown_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/markDown_afuw1y7lm0.txt",
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/json_afuw1y7lm0.json",
    "links_on_page": [],
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 20,
  "metadata": {}
}
```

> **Note:** `result.json_content` returns a stringified JSON. Parse it in your code to access the structured data.

**With a prompt (no schema):**

If you just pass a `prompt`, the LLM will extract the data based on the prompt and decide the data structure on its own:

```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url_to_scrape": "https://docs.olostep.com/get-started/welcome",
    "formats": ["json"],
    "llm_extract": {
      "prompt": "Extract the product name and a list of all API endpoint names mentioned on this page."
    }
  }'
```

Response:
```json
{
  "id": "scrape_ub9d81eqsw",
  "object": "scrape",
  "created": 1774369391,
  "url": "https://docs.olostep.com/get-started/welcome",
  "retrieve_id": "ub9d81eqsw",
  "result": {
    "html_content": null,
    "markdown_content": null,
    "text_content": null,
    "json_content": "{\"productName\":\"Olostep\",\"endpoints\":[\"/scrapes\",\"/crawls\",\"/maps\",\"/batches\",\"/answers\",\"/parsers\",\"/agents\",\"/files\",\"/sandboxes\"]}",
    "screenshot_hosted_url": null,
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/json_ub9d81eqsw.json",
    "links_on_page": [],
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 20,
  "metadata": {}
}
```

### Screenshot

```bash
curl -X POST 'https://api.olostep.com/v1/scrapes' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "url_to_scrape": "https://www.olostep.com",
    "formats": ["screenshot"]
  }'
```

Response:
```json
{
  "id": "scrape_bj3tz6vang",
  "object": "scrape",
  "created": 1774366431,
  "url": "https://www.olostep.com",
  "retrieve_id": "bj3tz6vang",
  "result": {
    "screenshot_hosted_url": "https://olostep-screenshots.s3.us-east-1.amazonaws.com/image_bj3tz6vang.png",
    "markdown_content": null,
    "html_content": null,
    "page_metadata": {
      "status_code": 200
    }
  },
  "credits_consumed": 1,
  "metadata": {}
}
```

### Actions (Interact Before Scraping)

Click, type, scroll, and wait before extracting — for login-gated pages and JS-heavy SPAs:

```python
import os
from olostep import Olostep

client = Olostep(api_key=os.environ["OLOSTEP_API_KEY"])

result = client.scrapes.create(
    url_to_scrape="https://example.com/dashboard",
    formats=["markdown"],
    actions=[
        {"type": "click",      "selector": "#login-button"},
        {"type": "fill_input", "selector": "#email",    "value": "user@example.com"},
        {"type": "fill_input", "selector": "#password", "value": "password"},
        {"type": "click",      "selector": "button[type='submit']"},
        {"type": "wait",       "milliseconds": 2000}
    ]
)
print(result.result.markdown_content)
```

### Scrape Formats

Available formats: `markdown`, `html`, `text`, `json`, `screenshot`, `raw_pdf`

| Format | Response Field | Description |
|--------|----------------|-------------|
| `markdown` | `markdown_content` | Clean markdown — ideal for LLM context |
| `html` | `html_content` | Full rendered HTML |
| `text` | `text_content` | Plain text, no markup |
| `json` | `json_content` | Structured JSON (requires `llm_extract` or `parser`) |
| `screenshot` | `screenshot_hosted_url` | Full-page screenshot URL (PNG) |
| `raw_pdf` | `file_hosted_url` | Raw PDF text extraction |

---

## Crawls

Crawl an entire website and get content from all pages.

```bash
curl -X POST 'https://api.olostep.com/v1/crawls' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "start_url": "https://docs.olostep.com",
    "max_pages": 5,
    "include_urls": ["/features/**", "/get-started/**"],
    "exclude_urls": ["/changelog/**"],
    "max_depth": 2
  }'
```

Returns a job ID:
```json
{
  "id": "crawl_pznr94twat",
  "object": "crawl",
  "status": "in_progress",
  "created": 1774366526357,
  "start_date": "2026-03-24",
  "start_url": "https://docs.olostep.com",
  "max_pages": 5,
  "max_depth": 2,
  "exclude_urls": ["/changelog/**"],
  "include_urls": ["/features/**", "/get-started/**"],
  "include_external": false,
  "current_depth": 0,
  "pages_count": 0
}
```

### Check Crawl Pages

```bash
curl -X GET 'https://api.olostep.com/v1/crawls/crawl_pznr94twat/pages' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY'
```

```json
{
  "id": "crawl_pznr94twat",
  "object": "crawl",
  "status": "completed",
  "pages_count": 5,
  "pages": [
    {
      "id": "urlId_1782f5bad2",
      "retrieve_id": "x9pkauadjv",
      "url": "https://docs.olostep.com/",
      "is_external": false
    },
    {
      "id": "urlId_c0233df380",
      "retrieve_id": "xpqm6uul08",
      "url": "https://docs.olostep.com/get-started/authentication",
      "is_external": false
    },
    {
      "id": "urlId_a2f0d23899",
      "retrieve_id": "lltjltz9hn",
      "url": "https://docs.olostep.com/features/answers/answers",
      "is_external": false
    },
    {
      "id": "urlId_36035aafd9",
      "retrieve_id": "hkaxd1zlng",
      "url": "https://docs.olostep.com/features/maps/maps",
      "is_external": false
    },
    {
      "id": "urlId_c0a2f0feb1",
      "retrieve_id": "owliom9ldx",
      "url": "https://docs.olostep.com/features/crawls/crawls",
      "is_external": false
    }
  ],
  "metadata": {
    "external_urls": [],
    "failed_urls": []
  }
}
```

### Retrieve Page Content

```bash
curl -X GET 'https://api.olostep.com/v1/retrieve?retrieve_id=x9pkauadjv&formats=markdown' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY'
```

```json
{
  "markdown_content": "Welcome to Olostep - Olostep Docs\n\nOlostep is a web scraping, crawling, and search API...",
  "html_content": null,
  "json_content": null,
  "screenshot_hosted_url": null,
  "markdown_hosted_url": "https://olostep-storage.s3.amazonaws.com/markDown_x9pkauadjv.txt",
  "success": true
}
```

**Note:** The SDKs handle polling automatically for a better developer experience.

---

## Maps

Discover all URLs on a website instantly.

```bash
curl -X POST 'https://api.olostep.com/v1/maps' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"url": "https://docs.olostep.com", "top_n": 10}'
```

Response:
```json
{
  "id": "map_6ahdf6sf5o",
  "urls_count": 10,
  "urls": [
    "https://docs.olostep.com/sdks/python",
    "https://docs.olostep.com/examples/batch",
    "https://docs.olostep.com/integrations/relay",
    "https://docs.olostep.com/integrations/mastra",
    "https://docs.olostep.com/integrations/n8n",
    "https://docs.olostep.com/concepts/latency",
    "https://docs.olostep.com/get-started/welcome",
    "https://docs.olostep.com/integrations/mcp-server",
    "https://docs.olostep.com/features/maps/maps",
    "https://docs.olostep.com/de/integrations/mastra"
  ]
}
```

### Map with URL Filters

Find specific URLs within a site using glob patterns:

```python
import os
from olostep import Olostep

client = Olostep(api_key=os.environ["OLOSTEP_API_KEY"])

result = client.maps.create(
    url="https://docs.olostep.com",
    include_urls=["/features/**"],
    exclude_urls=["/changelog/**"],
    top_n=50
)

for url in result.urls:
    print(url)

# Paginate for large sites
if result.cursor:
    next_page = client.maps.create(
        url="https://docs.olostep.com",
        cursor=result.cursor
    )
```

---

## Batches

Scrape multiple URLs at once — up to 10,000 URLs in a single job, completing in 5–8 minutes.

```bash
curl -X POST 'https://api.olostep.com/v1/batches' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "items": [
      {"custom_id": "item-001", "url": "https://docs.olostep.com/features/scrapes/scrapes"},
      {"custom_id": "item-002", "url": "https://docs.olostep.com/features/crawls/crawls"},
      {"custom_id": "item-003", "url": "https://docs.olostep.com/features/answers/answers"}
    ],
    "country": "us"
  }'
```

Returns a job ID:
```json
{
  "id": "batch_uc2q18nijo",
  "object": "batch",
  "status": "in_progress",
  "created": 1774366558223,
  "total_urls": 3,
  "completed_urls": 0,
  "batch_country": "us",
  "country": "us",
  "start_date": "2026-03-24",
  "metadata": {}
}
```

### Check Batch Status

```bash
curl -X GET 'https://api.olostep.com/v1/batches/batch_uc2q18nijo/items' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY'
```

```json
{
  "id": "batch_uc2q18nijo",
  "object": "batch",
  "status": "completed",
  "items": [
    {
      "custom_id": "item-002",
      "retrieve_id": "uc2q18nijo_item-002",
      "url": "https://docs.olostep.com/features/crawls/crawls"
    },
    {
      "custom_id": "item-003",
      "retrieve_id": "uc2q18nijo_item-003",
      "url": "https://docs.olostep.com/features/answers/answers"
    },
    {
      "custom_id": "item-001",
      "retrieve_id": "uc2q18nijo_item-001",
      "url": "https://docs.olostep.com/features/scrapes/scrapes"
    }
  ],
  "items_count": 3
}
```

### Retrieve Item Content

```bash
curl -X GET 'https://api.olostep.com/v1/retrieve?retrieve_id=uc2q18nijo_item-002&formats=markdown' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY'
```

```json
{
  "markdown_content": "Crawl - Olostep Docs\n\nCrawl\n\nCrawl an entire website and get content from all pages...",
  "html_content": null,
  "json_content": null,
  "screenshot_hosted_url": null,
  "success": true,
  "markdown_hosted_url": "https://olostep-storage.s3.amazonaws.com/markDown_uc2q18nijo_item-002.txt"
}
```

**Note:** The SDKs handle polling automatically for a better developer experience.

---

## Answers

> **Olostep's unique differentiator.** Ask a question in natural language and get a source-backed answer synthesized from live web data. No other web data API exposes this — ideal for grounding LLM agents on real-time information without managing search and scrape pipelines yourself.

```bash
curl -X POST 'https://api.olostep.com/v1/answers' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"task": "What is Olostep and what are its main features?"}'
```

Response:
```json
{
  "id": "answer_jg4inrka6b",
  "object": "answer",
  "created": 1774366472,
  "metadata": {},
  "task": "What is Olostep and what are its main features?",
  "result": {
    "json_content": "{\"result\":\"Olostep is a Web Data API that lets AI teams search, crawl, scrape and structure real-time web data through a single developer-friendly platform.\\n\\nMain features:\\n- Scrape any URL for Markdown, HTML, text or structured JSON\\n- Crawl all subpages of a site without needing a sitemap\\n- Batch process up to 10,000 URLs concurrently\\n- Ask natural-language questions and get AI answers with sources via /answers\\n- Create custom parsers to turn unstructured data into clean JSON\\n- Build, schedule and run research agents with no-code prompts\\n- Full JavaScript rendering and premium residential proxies on every request\\n- Multi-format outputs (JSON, Markdown, HTML, PDF) and automated form-fill actions\"}",
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/answer_jg4inrka6b.json",
    "sources": [
      "https://github.com/olostep",
      "https://docs.olostep.com/get-started/welcome",
      "https://www.olostep.com/"
    ]
  }
}
```

### Structured JSON Extraction with Schema

Provide a `json` parameter with empty values as a schema to guide the output. The API will return structured data matching your schema, sourced from the live web. If the agent isn't confident about a field, it returns `NOT_FOUND` for that value.

```bash
curl -X POST 'https://api.olostep.com/v1/answers' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{
    "task": "What is Olostep and what does it do?",
    "json": {
      "company_name": "",
      "description": "",
      "main_use_case": "",
      "website": ""
    }
  }'
```

Response:
```json
{
  "id": "answer_y0s1evxe8f",
  "object": "answer",
  "created": 1774369398,
  "metadata": {},
  "task": "What is Olostep and what does it do?",
  "result": {
    "json_content": "{\"company_name\":\"Olostep\",\"description\":\"Olostep is a Web Data API that helps AI teams search, crawl, scrape and structure web data through a single, developer-friendly platform\",\"main_use_case\":\"Real-time extraction and structuring of web data for AI teams, data pipelines and automation\",\"website\":\"https://www.olostep.com/\"}",
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/answer_y0s1evxe8f.json",
    "sources": [
      "https://www.facebook.com/StartupPakistanSP/posts/olostep-launches-today-to-the-public-what-started-as-an-idea-in-italy-has-now-gr/1182671233896851/",
      "https://docs.olostep.com/get-started/welcome",
      "https://github.com/olostep",
      "https://medium.com/red-buffer/olostep-web-data-api-for-ai-and-research-automation-be8c93c28ef1",
      "https://www.olostep.com/pricing",
      "https://www.linkedin.com/company/olostep",
      "https://www.olostep.com/blog/about-olostep",
      "https://www.olostep.com/"
    ]
  }
}
```

Your requested answer, formatted according to the `json` parameter, is in `result.json_content`:
```json
{
  "company_name": "Olostep",
  "description": "Olostep is a Web Data API that helps AI teams search, crawl, scrape and structure web data through a single, developer-friendly platform",
  "main_use_case": "Real-time extraction and structuring of web data for AI teams, data pipelines and automation",
  "website": "https://www.olostep.com/"
}
```

> When you don't pass the `json` parameter, the API returns a JSON object with the answer text inside a `result` field. You can also pass a string describing the data you want instead of a JSON object.

---

## Searches

Search the web with a plain-English query and get deduplicated results with URLs, titles, and descriptions.

```bash
curl -X POST 'https://api.olostep.com/v1/searches' \
  -H 'Authorization: Bearer $OLOSTEP_API_KEY' \
  -H 'Content-Type: application/json' \
  -d '{"query": "Olostep web scraping API for AI agents"}'
```

Response:
```json
{
  "id": "search_3v8hfo3yys",
  "object": "search",
  "created": 1774366508,
  "metadata": {},
  "query": "Olostep web scraping API for AI agents",
  "result": {
    "json_hosted_url": "https://olostep-storage.s3.us-east-1.amazonaws.com/search_3v8hfo3yys.json",
    "links": [
      {
        "url": "https://www.olostep.com/",
        "title": "Olostep - Web Data API for AI, Crawling & Data Extraction",
        "description": "Olostep is a Web Data API that helps AI teams search, crawl, scrape and structure web data through a single, developer-friendly platform. Built for modern AI ..."
      },
      {
        "url": "https://docs.olostep.com/get-started/welcome",
        "title": "Olostep Docs: Welcome to Olostep",
        "description": "Introduction. The Olostep API is the best web search, scraping and crawling API for AI used by some of the leading startups in the world."
      },
      {
        "url": "https://www.olostep.com/blog/best-web-scraping-tools",
        "title": "Best Web Scraping Tools: 11 Picks That Actually Scale | Olostep Blog",
        "description": "Best web scraping API for scalable, structured extraction. Olostep: Best for structured JSON, recurring batch workloads, and parser-driven ..."
      }
    ]
  }
}
```

### Search with Content Scraping

Chain Searches with Scrapes for a full AI research pipeline — search for relevant URLs, then pass each into `/v1/scrapes` to retrieve full page content.

```python
import os
from olostep import Olostep

client = Olostep(api_key=os.environ["OLOSTEP_API_KEY"])

# Step 1: search
search = client.searches.create(query="Olostep web scraping API for AI agents")

# Step 2: scrape each result for full content
for link in search.result.links[:3]:
    scrape = client.scrapes.create(
        url_to_scrape=link.url,
        formats=["markdown"]
    )
    print(f"\n--- {link.title} ---")
    print(scrape.result.markdown_content[:300])
```

---

## SDKs

Our SDKs provide a convenient way to interact with all Olostep features and automatically handle polling for async operations like crawls and batches.

### Python

```bash
pip install olostep
```

```python
import os
from olostep import Olostep

client = Olostep(api_key=os.environ["OLOSTEP_API_KEY"])

# Scrape a URL
result = client.scrapes.create(
    url_to_scrape="https://example.com",
    formats=["markdown"]
)
print(result.result.markdown_content)

# Search the web
search = client.searches.create(query="best LLM frameworks 2025")
for link in search.result.links:
    print(f"{link.title}: {link.url}")

# Ask a question grounded on live web data
answer = client.answers.create(
    task="What is the latest version of Python?"
)
print(answer.result.json_content)

# Crawl a website (automatically polls for completion)
crawl = client.crawls.create(
    start_url="https://docs.olostep.com",
    max_pages=50,
    include_urls=["/features/**"]
)
for page in crawl.pages():
    content = client.retrieve(retrieve_id=page.retrieve_id, formats=["markdown"])
    print(f"Crawled: {page.url}")
```

### JavaScript / TypeScript

```bash
npm install olostep
```

```javascript
import Olostep from 'olostep';

const client = new Olostep({ apiKey: process.env.OLOSTEP_API_KEY });

// Scrape a URL
const result = await client.scrapes.create({
  url_to_scrape: 'https://example.com',
  formats: ['markdown']
});
console.log(result.result.markdown_content);

// Search the web
const search = await client.searches.create({
  query: 'best LLM frameworks 2025'
});
search.result.links.forEach(link => console.log(`${link.title}: ${link.url}`));

// Ask a question grounded on live web data
const answer = await client.answers.create({
  task: 'What is the latest version of Python?'
});
console.log(answer.result.json_content);

// Crawl a website (automatically polls for completion)
const crawl = await client.crawls.create({
  start_url: 'https://docs.olostep.com',
  max_pages: 50,
  include_urls: ['/features/**']
});
for (const page of crawl.pages) {
  const content = await client.retrieve({ retrieve_id: page.retrieve_id, formats: ['markdown'] });
  console.log(`Crawled: ${page.url}`);
}
```

---

## Core Repositories

| Repository | Description |
|---|---|
| **[olostep-js](https://github.com/olostep-api/olostep-js)** | Official JavaScript / TypeScript SDK |
| **[olostep-py](https://github.com/olostep-api/olostep-py)** | Official Python SDK |
| **[olostep-mcp-server](https://github.com/olostep/olostep-mcp-server)** | Olostep MCP Server |
| **[CLI](https://github.com/olostep-api/CLI)** | Olostep CLI |

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

## Integrations

**Agents & AI Tools**

- 🔨 [MCP Server](https://www.olostep.com/integrations/mcp-server) — Connect any MCP-compatible AI (Cursor, Claude, Windsurf) to live web data
- 🦜 [LangChain](https://www.olostep.com/integrations/langchain) — Add web scraping, search, and crawling to LangChain and LangGraph agents
- 🟣 [Apify](https://www.olostep.com/integrations/apify) — Deploy Olostep as a managed Apify Actor with scheduled runs and dataset exports
- ⚡ [Mastra](https://www.olostep.com/integrations/mastra) — Integrate web scraping and search into Mastra AI agents and workflows

**Workflow Automation**

- 🔗 [Zapier](https://www.olostep.com/integrations/zapier) — Connect web data to 8,000+ apps without writing code
- 🔁 [n8n](https://www.olostep.com/integrations/n8n) — Use Olostep as native nodes in your self-hosted n8n workflows
- 🔀 [Relay](https://www.olostep.com/integrations/relay) — Add web scraping and search to Relay's workflow builder with human-in-the-loop support

[View all integrations →](https://www.olostep.com/integrations)

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
