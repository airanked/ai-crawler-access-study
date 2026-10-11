# AI Crawler Access Study (October 2026)

Open dataset: the robots.txt and llms.txt of 285 major websites in 10 categories, checked against 14 AI user agents plus Googlebot as a control. Published by [AI Ranked](https://airanked.ai).

**Full analysis:** [Which AI crawlers do top websites block?](https://airanked.ai/research/ai-crawler-access-report)
**Dataset page:** https://airanked.github.io/ai-crawler-access-study/

## Key numbers

- 261 of 285 robots.txt files could be read.
- 35% (91 sites) block at least one AI training crawler; 21% (56 sites) block at least one AI search crawler.
- 65% (170 sites) block none of the 14 AI agents; 12 (4.6%) block all 14.
- CCBot and Bytespider are blocked most (28.7% each); OAI-SearchBot least (11.5%).
- 31 of the 59 sites that block GPTBot still allow OAI-SearchBot.
- 88% of news sites block a training bot, against 12% of B2B SaaS sites.
- 81 of 241 sites (34%) serve a valid llms.txt; B2B SaaS leads at 64%.

## File

`ai-crawler-access-data.csv`: 285 rows, one per domain, 20 columns.

| Column | Values | Description |
|---|---|---|
| `domain` | text | Domain checked |
| `category` | text | One of 10 site categories |
| `fetched_ok` | yes / no | Whether robots.txt could be read (a 404 counts as read) |
| `robots_status` | text | `ok`, `no robots.txt (404)` or `failed (reason)` |
| `GPTBot` | allowed / blocked | OpenAI training crawler |
| `OAI-SearchBot` | allowed / blocked | OpenAI search indexing agent |
| `ChatGPT-User` | allowed / blocked | OpenAI user-requested fetch |
| `ClaudeBot` | allowed / blocked | Anthropic training crawler |
| `Claude-SearchBot` | allowed / blocked | Anthropic search indexing agent |
| `Claude-User` | allowed / blocked | Anthropic user-requested fetch |
| `PerplexityBot` | allowed / blocked | Perplexity search indexing agent |
| `Perplexity-User` | allowed / blocked | Perplexity user-requested fetch |
| `Google-Extended` | allowed / blocked | Google AI training control token |
| `Applebot-Extended` | allowed / blocked | Apple AI training control token |
| `meta-externalagent` | allowed / blocked | Meta AI training crawler |
| `CCBot` | allowed / blocked | Common Crawl crawler |
| `Bytespider` | allowed / blocked | ByteDance training crawler |
| `Amazonbot` | allowed / blocked | Amazon crawler |
| `Googlebot` | allowed / blocked | Control: Google Search crawler |
| `llms_txt` | yes / no / unknown | Valid llms.txt at the site root |

Agent columns are empty for the 24 domains whose robots.txt could not be read.

## Method

- **Sample:** 285 hand-picked domains in 10 categories, including 102 B2B SaaS companies and 53 news and media publishers.
- **Collection:** October 2026; `/robots.txt` and `/llms.txt` requested per domain with a 10-second timeout, redirects followed, one retry (including the www host).
- **Base:** 24 domains that refused, timed out or returned an HTML page are excluded from percentages (n = 261).
- **Parser:** RFC 9309 rules evaluated at the path `/`: merged groups, fallback to `*`, longest match wins, Allow wins a tie, `*` and `$` wildcards, case-insensitive agent names.
- **llms.txt:** counted only on HTTP 200 with a text content type and a Markdown H1 first line; adoption base is the 241 domains that returned 200, 404 or 410.

## Also available

- Zenodo (DOI): https://doi.org/10.5281/zenodo.23303786
- Hugging Face: https://huggingface.co/datasets/airanked/ai-crawler-access-2026

## License

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Share and adapt for any purpose with credit to AI Ranked.

## How to cite

AI Ranked Editorial (2026). AI Crawler Access Study. https://doi.org/10.5281/zenodo.23303786
