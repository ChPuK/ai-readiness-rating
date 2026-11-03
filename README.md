# AI Readiness Rating — open data

How 100 well-known online services look to AI crawlers and assistants (ChatGPT, Claude, Perplexity and others): can a bot open the site, does robots.txt let AI search bots in, is the main text there without JavaScript, is there llms.txt and Organization markup.

Collected by [aiseen.cloud](https://aiseen.cloud/?utm_source=github&utm_medium=dataset) — a checker of website visibility for AI. Live rating: [aiseen.cloud/en/rating/](https://aiseen.cloud/en/rating/?utm_source=github&utm_medium=dataset).

## Files

| File | What |
|---|---|
| [`data/ai-readiness-rating-2026-10.csv`](data/ai-readiness-rating-2026-10.csv) | 100 sites, 10 niches × 10, checked on 27 Oct 2026 |

New snapshots are added as new files (`ai-readiness-rating-YYYY-MM.csv`); old ones are not changed.

## Key findings (October 2026)

- **14 of 100 sites returned no readable page to our crawler** — with AI-bot User-Agents and with a regular browser User-Agent alike: 10 Cloudflare bot challenges or captchas (HTTP 403), 2 pages without readable text (HTTP 200), 2 timeouts. Among them: openai.com, perplexity.ai, udemy.com, pipedrive.com, revolut.com.
- **12 of those 14 do not disallow major AI bots in robots.txt.** openai.com serves `User-agent: * / Allow: /` and a 403 challenge.
- Of the 86 sites that opened: median readiness score 76 (75.5); 26 (30 %) block at least one AI search or user-triggered bot; 48 (56 %) have llms.txt; 43 (50 %) serve the whole main text without JavaScript; only 11 (13 %) have complete Organization markup.

Write-up: [robots.txt says yes, the firewall says no](https://aiseen.cloud/en/blog/robots-txt-vs-firewall-ai-crawlers/?utm_source=github&utm_medium=dataset).

## Columns

| Column | Meaning |
|---|---|
| `checked_at` | date of the check, YYYY-MM-DD |
| `category` | niche (10 niches, 10 services each) |
| `service`, `domain` | the service and the domain that was checked |
| `opened_for_check` | `yes` — the site returned a readable page; `no` — it did not, see next column |
| `not_opened_reason` | what the server returned instead: bot challenge, captcha, page without text, timeout |
| `ai_readiness_score` | 0–100, sum of open rules ([methodology](https://aiseen.cloud/en/methodology/)); empty if the site did not open |
| `grade` | A ≥ 85, B ≥ 65, C ≥ 45, D ≥ 25, E < 25 |
| `ai_search_bots_blocked` | how many AI search and user-triggered bots (OAI-SearchBot, ChatGPT-User, PerplexityBot, Claude-User and others) are blocked by robots.txt or by server responses |
| `llms_txt` | `yes` / `no` — /llms.txt is present and valid |
| `main_text_without_js` | `yes` — the whole main text is in the HTML; `partly` — part appears only after JavaScript; `no` — almost none |
| `organization_schema` | `yes` — complete Organization markup (name, logo, contacts, profiles); `partly` — some fields; `no` — none |

## Method

- One check per site on 27 Oct 2026, from our server (not from AI vendors' IP ranges).
- The home page and up to 10 internal pages, fetched with a regular browser User-Agent and with AI-bot User-Agents (GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, Claude-User, PerplexityBot and others); robots.txt groups parsed; llms.txt, Organization markup, page text with and without JavaScript compared.
- The score is computed by fixed rules, not by a language model. Full methodology: [aiseen.cloud/en/methodology/](https://aiseen.cloud/en/methodology/).

## Caveats

- **Verified crawlers may pass.** Firewalls can allow official crawlers by IP range or signature. We checked as an ordinary third-party AI service; the long tail of AI agents, new assistants and browser tools is in the same position.
- One check, one moment. Sites change; a timeout may be temporary.
- A score is not a verdict on the product — only on how readable the site is for AI.
- Blocking AI *training* bots is a normal choice and is not counted as a problem; blocking *search* and *user-triggered* bots removes the site from AI answers with links.

## License and citation

Data — [CC BY 4.0](LICENSE). You can use, share and adapt it, including commercially, with attribution:

> AI Readiness Rating, aiseen.cloud, October 2026 — https://aiseen.cloud/en/rating/

Questions about the data: info@aiseen.cloud.
