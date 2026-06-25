[HTML To Markdown](https://apify.com/web.harvester/html-to-markdown?fpr=data)

> 🔄 Convert HTML to clean Markdown. Supports GFM tables, code blocks, and custom formatting. Perfect for content migration.

[![Apify Actor](https://img.shields.io/badge/Apify-Actor-blue)](https://apify.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 🎯 What This Actor Does

Convert HTML to Markdown:

- **GFM Tables** - HTML tables → Markdown tables
- **Code Blocks** - Fenced or indented
- **Headings** - ATX (#) or Setext (underlined)
- **Lists** - Customizable bullet markers
- **Clean Output** - Readable Markdown

## 🚀 Use Cases

| Use Case | Description |
| --- | --- |
| **Content Migration** | Move HTML to Markdown-based CMS |
| **Documentation** | Convert HTML docs to MD |
| **Web Scraping** | Extract content as Markdown |
| **Blog Import** | Import HTML posts |
| **Archive** | Store web content as MD |
| **Git Wikis** | Convert HTML wikis |

## 📥 Input Examples

### Basic Conversion

```
{
    "html": "<h1>Title</h1><p>Content</p>",
    "headingStyle": "atx"
}
```

### From URL

```
{
    "htmlUrl": "https://example.com/page.html",
    "gfmTables": true
}
```

### Custom Formatting

```
{
    "html": "<ul><li>Item</li></ul>",
    "bulletListMarker": "*",
    "codeBlockStyle": "fenced"
}
```

## ⚙️ Configuration

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `html` | string | - | HTML content |
| `htmlUrl` | string | - | URL to HTML page |
| `headingStyle` | string | `atx` | atx (#) or setext (underlined) |
| `codeBlockStyle` | string | `fenced` | fenced (```) or indented |
| `bulletListMarker` | string | `-` | -, *, or + |
| `gfmTables` | boolean | `true` | Convert tables to GFM |
| `keepImages` | boolean | `true` | Convert img tags |
| `keepLinks` | boolean | `true` | Convert a tags |

## 📤 Output

```
{
    "inputLength": 200,
    "outputLength": 150,
    "headingStyle": "atx",
    "markdown": "# Title\n\nContent here...",
    "markdownUrl": "https://api.apify.com/v2/..."
}
```

## 📝 Conversion Examples

### Headers

```
<h1>Title</h1>  →  # Title
<h2>Subtitle</h2>  →  ## Subtitle
```

### Text Formatting

```
<strong>bold</strong>  →  **bold**
<em>italic</em>  →  *italic*
<code>code</code>  →  `code`
```

### Lists

```
<ul><li>Item</li></ul>  →  - Item
<ol><li>First</li></ol>  →  1. First
```

## 💰 Cost Estimation

| Size | Approx. Time | Compute Units |
| --- | --- | --- |
| 10 KB | ~1 second | ~0.001 |
| 100 KB | ~2 seconds | ~0.003 |

## 🔧 Technical Details

- **Language:** TypeScript / Node.js 22
- **Library:** Turndown 7.x
- **Memory:** 128MB-256MB

## 📄 License

MIT License - see LICENSE for details.

---

## 🏪 Apify Store Listing

 

---

**Keywords:** html to markdown, html to md, turndown, html converter, markdown converter, content migration, gfm