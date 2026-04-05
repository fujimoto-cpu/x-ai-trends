# Daily AI Reports — Combined Instructions

Get today's date: `date '+%Y-%m-%d'` → DATE
Get day of week: `date '+%u'` → DOW (1=Mon...7=Sun)

GITHUB_REPO_IP=fujimoto-cpu/ip-report
GITHUB_REPO_TRENDS=fujimoto-cpu/x-ai-trends

---

## TASK 1: KONNEKT IP News Report

**Company:** KONNEKT INTERNATIONAL INC. Tokyo-based IP commercialization company.
**Brand names (exact):** Ange Charme, GOD ONLY KNOWS, LAVANDA, Armillary. (trailing period required)
**Licensed IP:** KISS, Aerosmith, AC/DC, One Piece, Sanrio characters

### Step 1-1: Collect IP News via WebSearch (last 7 days only)

Japan (3 articles):
- `character IP license latest 2026`
- `artist goods brand IP 2026`
- `anime IP license contract 2026`

Global (2 articles):
- `entertainment IP licensing news 2026`
- `celebrity influencer D2C fashion brand 2026`

For Japan articles: WebFetch og:image only (stop at `</head>`). Summary 200 chars from search snippet.
For Global articles: WebFetch og:image + full body. Write detailed Japanese translation 600+ chars covering: background, facts, industry impact, KONNEKT relevance.
If og:image unavailable: use `https://placehold.co/860x200/f0f4f8/1a1a2e?text=IP+News`

### Step 1-2: Check Backnumbers

For each of the last 10 days, check HTTP status of `https://fujimoto-cpu.github.io/ip-report/DATE.html`.
Keep only HTTP 200 URLs, max 5, for the backnumber section.

### Step 1-3: Generate HTML Report

Save to `/tmp/ip-DATE.html`

Design (white, clean):
- Background: #f8fafc
- Header: gradient #2980b9 to #6dd5fa
- Japan article cards: left border #e74c3c
- Global article cards: left border #2980b9
- Font: -apple-system, BlinkMacSystemFont, Hiragino Sans, Noto Sans JP
- Card layout with hover shadow

Sections:
1. Header (KONNEKT IP News Daily + date)
2. Summary banner (2-3 topic bullets)
3. Japan articles x3: title, image, source|date, 200-char summary, source link
4. Global articles x2: title (EN + JA), image, source|date, 600+ char Japanese translation, source link
5. KONNEKT INTERNATIONAL recommendations (4-grid layout, soft tone — avoid "should", use "recommend", "consider", "could work well")
   - Reference brand names exactly: Ange Charme, GOD ONLY KNOWS, LAVANDA, Armillary.
6. Backnumbers (confirmed HTTP 200 URLs only, max 5)

### Step 1-4: Upload to GitHub Pages

```bash
DATE=$(date '+%Y-%m-%d')
CONTENT=$(base64 -i /tmp/ip-${DATE}.html | tr -d '\n')
curl -s -X PUT \
  -H "Authorization: token GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  https://api.github.com/repos/fujimoto-cpu/ip-report/contents/${DATE}.html \
  -d "{\"message\": \"Add IP Report ${DATE}\", \"content\": \"${CONTENT}\"}"
```

If HTTP 201: proceed. Public URL: `https://fujimoto-cpu.github.io/ip-report/DATE.html`

### Step 1-5: Slack Notifications

**Personal DM (every day, any DOW):** Send to user ID `U034EFSD81G` via slack_send_message:
```
📊 *IP News Report* (DATE)

🇯🇵 [article 1 title, max 40 chars]
🇯🇵 [article 2 title, max 40 chars]
🇯🇵 [article 3 title, max 40 chars]
🌍 [article 4 title, max 40 chars]
🌍 [article 5 title, max 40 chars]

🌐 HTMLで読む → https://fujimoto-cpu.github.io/ip-report/DATE.html
（※1〜2分で公開されます）
```

**#general channel (weekdays only, DOW 1-5):** Same format, send to #general channel.
Skip #general on weekends (DOW 6-7).

---

## TASK 2: X AI Trends Report

### Step 2-1: Collect 10 Real X Posts (last 24-48 hours)

Search queries (run in parallel):
- `AI viral tweet trending 2026 site:x.com`
- `LLM Claude GPT trending discussion 2026`
- `AI tool viral tweet 2026 site:x.com`
- `AI news buzz Twitter 2026`
- `人工知能 バズ X Twitter 2026 site:x.com`
- `AIツール 使ってみた バズ 2026`

**Important:** Only use REAL tweets from REAL X accounts. No fictional content.

Select 5 global (English) + 5 Japanese posts.

For each post:
- Title: 30 chars max
- @handle: required (real account)
- Content: 100 chars (original or summary)
- Explanation: 200+ chars covering why it's viral, technical background, business/life implications
- URL: if available
- Category: one of #新技術, #ツール, #議論, #事例, #速報

### Step 2-2: Collect 5 Coding AI Use Cases

Real viral X posts about Cursor, Claude Code, or other coding AI tools:
- `Cursor AI use case viral 2026 site:x.com`
- `Claude code vibe coding result 2026`
- `AI coding productivity viral 2026 site:x.com`
- `コーディングAI 活用事例 バズ 2026`

For each:
- Title: 30 chars max
- @handle: required
- Summary: 100 chars (what was built or solved)
- Explanation: 150+ chars (why it's groundbreaking, how to apply it)
- URL: if available

### Step 2-3: Check X AI Trends Backnumbers

For each of the last 10 days, check HTTP status of `https://fujimoto-cpu.github.io/x-ai-trends/DATE.html`.
Keep only HTTP 200 URLs, max 5.

### Step 2-4: Generate HTML Report

Save to `/tmp/x-ai-trends-DATE.html`

Design (white, morning-friendly):
- Background: #f7f7f5
- Card background: #ffffff
- Header: white + top gradient #4f46e5 to #7c3aed
- Global cards: left border #4f46e5 (indigo)
- Japan cards: left border #7c3aed (purple)
- Use cases cards: left border #ff6b35 (orange)
- Text: #1a1a2e, subtext: #6b7280
- Card layout with hover shadow effect
- Font: -apple-system, BlinkMacSystemFont, Hiragino Sans, Noto Sans JP

Category tag colors:
- #新技術 → #7c3aed
- #ツール → #059669
- #議論 → #d97706
- #事例 → #4f46e5
- #速報 → #dc2626

Sections:
1. Header (𝕏 AI Trends Daily + date)
2. Summary banner (top 3 highlights)
3. Global AI Trends (5 posts): category badge, title, @handle, blockquote content, 📖 explanation (200+ chars), source link button
4. Japan AI Trends (5 posts): same format
5. Coding AI Use Cases (5 posts): title, @handle, blockquote summary, 📖 explanation, source link button
6. KONNEKT × Yuriko Application (2-column grid, 4-6 items):
   - Apply today's trends to KONNEKT brand work: Armillary., GOD ONLY KNOWS, Ange Charme, LAVANDA
   - Internal AI promotion at KONNEKT
   - Planning and design workflow improvements
   - Specific action items Yuriko can try this week
7. Backnumbers (confirmed HTTP 200 URLs only, max 5)

### Step 2-5: Upload to GitHub Pages

```bash
DATE=$(date '+%Y-%m-%d')
CONTENT=$(base64 -i /tmp/x-ai-trends-${DATE}.html | tr -d '\n')
curl -s -X PUT \
  -H "Authorization: token GITHUB_TOKEN" \
  -H "Content-Type: application/json" \
  https://api.github.com/repos/fujimoto-cpu/x-ai-trends/contents/${DATE}.html \
  -d "{\"message\": \"Add X AI Trends ${DATE}\", \"content\": \"${CONTENT}\"}"
```

If HTTP 201: proceed. Public URL: `https://fujimoto-cpu.github.io/x-ai-trends/DATE.html`

### Step 2-6: Save to Notion Log DB

Database: `collection://180ec59f-a90f-810e-99e9-000be5cdd6b3`
Title: `DATE X AIトレンド10選＋活用事例5選`

Body must include:
- Table of Global AI Trends (5 rows): title, @handle, category, key point
- Table of Japan AI Trends (5 rows): same
- Table of Coding AI Use Cases (5 rows): title, @handle, summary
- HTML report URL

### Step 2-7: Slack Personal DM only (every day, any DOW — do NOT send to #general)

Send to user ID `U034EFSD81G` via slack_send_message. Do not send to any channel.

```
𝕏 *X AI Trends Report* (DATE)

━━━━━━━━━━━━━━━━
🌍 グローバルAIトレンド TOP3
━━━━━━━━━━━━━━━━
1. [title 40 chars] — @handle
2. [title 40 chars] — @handle
3. [title 40 chars] — @handle

━━━━━━━━━━━━━━━━
🇯🇵 日本語AIトレンド TOP3
━━━━━━━━━━━━━━━━
1. [title 40 chars] — @handle
2. [title 40 chars] — @handle
3. [title 40 chars] — @handle

━━━━━━━━━━━━━━━━
💻 コーディングAI活用事例 TOP3
━━━━━━━━━━━━━━━━
1. [title 40 chars] — @handle
2. [title 40 chars] — @handle
3. [title 40 chars] — @handle

━━━━━━━━━━━━━━━━
💡 コネクト × ゆりこに当てはめると
━━━━━━━━━━━━━━━━
• [3-4 lines of practical suggestions for KONNEKT brand work and AI promotion]

🌐 全件を読む → https://fujimoto-cpu.github.io/x-ai-trends/DATE.html
📝 Notionにも保存済み
（※ページ公開まで1〜2分かかる場合があります）
```
