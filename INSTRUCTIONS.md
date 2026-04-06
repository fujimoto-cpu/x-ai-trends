# Daily X AI Trends Report — Instructions

## TASK: X AI Trends Report

**Step 1: Get today's date**
```bash
DATE=$(date '+%Y-%m-%d')
DOW=$(date '+%u')
```

**Step 2-1: Collect 10 X (Twitter) AI posts (past 24–48 hours)**
- Global 5 posts (English) + Japan 5 posts (Japanese)
- For each post: title (30 chars), @handle, content (100 chars), explanation (200+ chars), category (#新技術/#ツール/#議論/#事例/#速報)

**Step 2-2: Collect 5 coding AI use cases**
- Buzzworthy posts about Cursor / Claude Code / other coding AI tools

**Step 2-3: Check backnumber links**
- Check past 10 days: `https://fujimoto-cpu.github.io/x-ai-trends/DATE.html`
- Only use HTTP 200 responses (max 5 links)

**Step 2-4: Generate HTML report** → `/tmp/x-ai-trends-${DATE}.html`
Design:
- Background: white
- Header gradient: #4f46e5 → #7c3aed
- Global posts border: #4f46e5 (indigo)
- Japan posts border: #7c3aed (purple)
- Use cases border: #ff6b35 (orange)
- Mobile responsive

**Step 2-5: Upload to GitHub Pages**
Token: GITHUB_TOKEN
Repo: fujimoto-cpu/x-ai-trends
URL: `https://fujimoto-cpu.github.io/x-ai-trends/${DATE}.html`

**Step 2-6: Save to Notion Log DB**
- DB: `collection://180ec59f-a90f-810e-99e9-000be5cdd6b3`
- Title: `${DATE} X AIトレンド10選＋活用事例5選`
- Tables: Global 5 / Japan 5 / Use cases 5 + HTML report URL

**Step 2-7: Slack personal DM only**
- Send to `U034EFSD81G` only (do NOT send to #general)

**Step 3: Done**
Report: ✅ X AI Trends Report ${DATE} を作成しました！ + GitHub Pages URL + Notion URL

