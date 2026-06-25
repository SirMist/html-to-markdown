[HTML To Markdown](https://apify.com/santamaria-automations/html-to-markdown?fpr=data)

**Convert any website to clean Markdown — perfect for LLM training, AI pipelines, and documentation.**

Give the actor a list of URLs and get back clean, well-formatted Markdown for every page. Tables, code blocks, images, and nested lists are preserved. Navigation bars, footers, cookie banners, sidebars, and ads are stripped out automatically via readability-style main content extraction.

## Features

- **Readability-style extraction** — returns the article body, not the whole page
- **Tables preserved** — HTML tables become proper Markdown tables with pipes and separators
- **Code blocks preserved** — `<pre>` and `<code>` blocks kept intact, fenced and ready for LLMs
- **Images preserved** — alt text, titles, and absolute URLs
- **Nested structures** — lists inside lists, blockquotes, headings all handled correctly
- **Strikethrough** — `<s>`, `<strike>`, `<del>` converted to `~~text~~`
- **Outbound link discovery** — every external link the page points to, with anchor text
- **Smart metadata** — page title, meta description, Open Graph, content type classification
- **Parallel processing** — 6 URLs at a time for fast bulk conversion
- **Tiny footprint** — minimal compute usage keeps your bill low

## Use with AI Agents (MCP)

Connect this actor to any MCP-compatible AI client — Claude Desktop, Claude.ai, Cursor, VS Code, LangChain, LlamaIndex, or custom agents.

**Apify MCP server URL:**

```
https://mcp.apify.com?tools=santamaria-automations/html-to-markdown
```

**Example prompt once connected:**

> "Use `html-to-markdown` to process data with html to markdown. Return results as a table."

Clients that support dynamic tool discovery (Claude.ai, VS Code) will receive the full input schema automatically via `add-actor`.

## Example Output

Input URL: `https://en.wikipedia.org/wiki/Markdown`

```
# Markdown

**Markdown** is a lightweight [markup language](/wiki/Markup_language) for
creating [formatted text](/wiki/Formatting_(word_processing)) using a
[plain-text editor](/wiki/Text_editor). [John Gruber](/wiki/John_Gruber)
created Markdown in 2004 as an easy-to-read markup language.

## Examples

Text using Markdown syntax:

​```
# Heading

Paragraphs are separated
by a blank line.

**bold**, *italic*, `monospace`
​```

Bullet lists nested within numbered list:

1. fruits
   - apple
   - banana
2. vegetables
   - carrot
   - broccoli

## See also

- [CommonMark](/wiki/CommonMark)
- [reStructuredText](/wiki/ReStructuredText)
- [AsciiDoc](/wiki/AsciiDoc)
```

Clean, readable, LLM-ready. No navigation menus, no "Toggle sidebar", no language switcher.

## Input

```
{
  "urls": [
    "https://en.wikipedia.org/wiki/Markdown",
    "https://blog.apify.com/"
  ],
  "extractMainContent": true,
  "includeImages": true,
  "includeTables": true,
  "includeStrikethrough": true,
  "followRedirects": true,
  "maxContentLengthKB": 500,
  "timeoutSeconds": 30
}
```

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| `urls` | array of strings | **required** | URLs to fetch and convert |
| `extractMainContent` | boolean | `true` | Strip navigation, ads, footers — return only article body |
| `includeImages` | boolean | `true` | Keep image links in output |
| `includeTables` | boolean | `true` | Enable table conversion plugin |
| `includeStrikethrough` | boolean | `true` | Enable `~~strikethrough~~` plugin |
| `followRedirects` | boolean | `true` | Follow HTTP 3xx redirects |
| `maxContentLengthKB` | integer | `500` | Per-URL HTML size cap |
| `timeoutSeconds` | integer | `30` | Per-URL download + parse timeout |

## Output

One record per input URL:

```
{
  "url": "https://en.wikipedia.org/wiki/Markdown",
  "final_url": "https://en.wikipedia.org/wiki/Markdown",
  "success": true,
  "error": "",
  "page_title": "Markdown - Wikipedia",
  "page_description": "Markdown is a lightweight markup language...",
  "markdown": "# Markdown\n\n**Markdown** is a lightweight...",
  "markdown_length": 36278,
  "word_count": 2907,
  "html_length": 195413,
  "content_type": "article",
  "images": [
    "https://upload.wikimedia.org/wikipedia/commons/..."
  ],
  "links": [
    { "text": "John Gruber", "url": "https://daringfireball.net/" }
  ],
  "main_content_only": true,
  "scraped_at": "2026-04-07T12:34:56Z"
}
```

`content_type` is one of: `article`, `blog`, `documentation`, `generic` — detected from JSON-LD schema, `<article>` tags, and code block density.

## Main Content Extraction

When `extractMainContent` is enabled, the actor tries these strategies in order:

1. **JSON-LD `articleBody`** — Schema.org `Article`, `BlogPosting`, or `NewsArticle`
2. **CSS selectors** — `.mw-parser-output`, `.article-content`, `.post-content`, `.entry-content`, `.article-body`, `.post-body`, `#mw-content-text`, `#content`, `#main`
3. **Semantic tags** — `<article>`, `<main>`, `[role=main]`
4. **Body fallback** — `<body>` with navigation, footer, aside, script, style, forms, and common noise classes removed

This gives much cleaner Markdown output for articles and blog posts than a naive conversion of the entire page.

## Use Cases

- **LLM training data** — build high-quality datasets from web content for fine-tuning
- **AI RAG pipelines** — ingest web content into vector DBs (Pinecone, Weaviate, Qdrant) as clean chunks
- **Content archiving** — save articles, blog posts, and documentation as portable Markdown files
- **Documentation conversion** — migrate legacy HTML docs to Markdown-based static site generators
- **Newsletter generation** — extract clean article text for email newsletters without HTML clutter
- **Note-taking workflows** — save web articles directly to Obsidian, Notion, Logseq, or any Markdown tool
- **Research and summarization** — feed AI summarizers with the actual content, not navigation menus
- **Knowledge base construction** — build searchable knowledge bases from public web content
- **Competitor content analysis** — bulk-convert competitor blogs for analysis

## Pricing

Pay-per-event — you only pay for URLs you actually convert:

| Event | Price |
| --- | --- |
| Actor start | $0.001 |
| URL converted | $0.003 |

**1,000 URLs ≈ $3.00**

No hidden platform fees, no surprise compute charges.

## Related Actors

- [RSS Feed Reader](https://apify.com/santamaria-automations/rss-feed-reader) — pull article URLs from RSS feeds, then pipe into this actor
- [PDF Text Extractor](https://apify.com/santamaria-automations/pdf-extractor) — convert PDFs to plain text instead of HTML
- [Website Content Crawler](https://apify.com/apify/website-content-crawler) — crawl entire sites, not just a URL list
- [Website Tech Stack Detector](https://apify.com/santamaria-automations/website-tech-detector) — identify the CMS and tech behind any site

---

Built by [santamaria-automations](https://apify.com/santamaria-automations).