---
name: ai-builds-daily
description: Short extra email with FT stories about AI builds (needs Chrome); the main digest is sent by a cloud routine
---

You send a SHORT add-on email of Financial Times stories about people or companies BUILDING or USING AI to make something. The main daily digest ("AI Builds Daily") is sent separately by a cloud routine at about 8 AM. Your job is only the FT stories that routine can't reach, because FT is behind the user's subscription.

## What counts
Keep only FT stories where someone built, deployed or discovered something with AI. Examples: "AI asked better questions than KPMG accountants in pilot audit", or an AI glasses startup for blind users. Bonus if it's in retail, energy, finance, asset management or audit/consulting.
HARD SKIP:
- Funding, valuations, IPOs, investor regrets, earnings, stock moves, exec drama, M&A, layoffs.
- Policy and regulation.
- Op-eds.
- Benchmarks.
- Non-AI news.
The test: does this story show someone building or using AI to make something? If not, drop it.
Freshness: last ~3 days.

## Avoid repeats
1. Read /Users/anishrajanand/ai-builds-digest/sent-log.md if it exists.
2. Use the Gmail tools to search subject:"AI Builds Daily" newer_than:3d, so you skip anything today's main digest already covered.
3. Skip anything already sent.

## Read FT via Claude in Chrome
The user is signed in to ft.com in their own Chrome.
1. Load the tools in ONE ToolSearch call: "select:mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__tabs_create_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__get_page_text,mcp__claude-in-chrome__javascript_tool,mcp__claude-in-chrome__tabs_close_mcp"
2. Call tabs_context_mcp with createIfEmpty true, and work only in tabs in that group.
3. Read https://www.ft.com/myft/following and https://www.ft.com/artificial-intelligence with get_page_text. FT may redirect once for its login check. If get_page_text errors about a domain change, call tabs_context_mcp again and retry.
4. Open the qualifying ft.com/content/... articles so you can summarise them accurately.
5. Only read pages. Never sign in or out, change settings, comment, or click anything but article links.
6. Close the tabs you created.
7. Summarise in your own words. Never paste FT text beyond a short phrase.

If Chrome isn't connected, or you find ZERO qualifying stories, send NOTHING. Just report that in one line.

## Email
Send ONE email with the Gmail send-message tool to [my own Gmail address]. That is the user's own address and the only recipient.
- Subject: 📰 FT AI Builds — {Weekday, D Mon YYYY} — {N}
- Send an htmlBody and a plain-text body. Use the same look as the main digest:
  - Clean HTML, inline styles, max-width ~640px, system font.
  - A small grey hint: "💡 Hover a headline for the summary · click to read the full story".
  - Then numbered rows. Each row is a small tag pill, then <a href="{FT URL}" title="{2-3 sentence summary: who built what, how AI was used, why it's cool; escape &quot; &amp;; under ~350 chars}">Headline naming the thing built</a>, then grey text "FT".
  - Headline links are #1a1a1a, bold, 16px, no underline. Thin dividers between rows.
- The plain-text body has, for each story, the headline, then the summary, then the URL.
- Usually 1-3 stories. Never invent anything.

After sending, append today's date and the stories (title — URL) to /Users/anishrajanand/ai-builds-digest/sent-log.md. Finish by reporting in one line how many stories were sent.