# 🪸 CoralMind — Personal Knowledge Dashboard

## ✨ What it does

CoralMind simulates what a **Coral-powered** personal knowledge dashboard would look like. You connect multiple data sources (Notion notes, PDFs, CSV files, GitHub repos, Markdown), then:

- **Ask questions in natural language** — the AI answers by synthesizing across all your sources and citing each one
- **Run SQL queries** — cross-source joins just like Coral's SQL interface, with a live editor and example queries
- **Add new sources on the fly** — paste any content to index it immediately
- **Track query history** — every search saved and replayable

### 🎯 Judging criteria addressed

| Criterion | How |
|---|---|
| 🏴‍☠️ Potential Impact | Solves the "scattered knowledge" problem — query all your docs from one place |
| ⚓ Creativity | Cross-source natural language + SQL on heterogeneous data (notes + PDFs + CSVs) |
| 🗺️ Learning & Growth | First-time Coral user learning SQL joins, caching, and multi-source retrieval |
| ⚔️ Technical Implementation | Groq streaming API, simulated Coral SQL engine, live source indexing |
| 🎨 Aesthetics & UX | Dark dashboard UI with streaming responses, source chips, SQL highlighting |
| 🪸 Best Use of Coral | Cross-source joins, SQL explorer, caching simulation, multi-source citations |

---

## 🚀 Quick start (60 seconds)

This is a **single HTML file** — no build step, no npm install, no server needed.

### Step 1 — Get a Groq API key

1. Go to [console.groq.com/keys](https://console.groq.com/keys)
2. Sign up (free) and click **Create API Key**
3. Copy your key — it looks like `gsk_...`

### Step 2 — Open the dashboard

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/coralmind.git
cd coralmind

# Just open the file in your browser
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

Or simply **double-click** `index.html` in your file explorer.

### Step 3 — Enter your API key

In the top-right corner of the dashboard, paste your Groq API key into the **GROQ API KEY** field. The dot turns green when it's ready.

> ⚠️ Your API key is never stored or sent anywhere except directly to Groq's API from your browser. It lives only in memory for your session.

### Step 4 — Start querying

Click any suggestion or type a question like:

```
What did I write about machine learning last month?
Which papers have I rated 5 stars?
Find connections between my notes and PDFs
```

Hit **⌘ + Enter** (Mac) or **Ctrl + Enter** (Windows) to send.

---

## 📁 Project structure

```
coralmind/
├── index.html          ← entire app (HTML + CSS + JS, single file)
├── README.md           ← you are here
├── LICENSE             ← MIT
└── .gitignore          ← keeps secrets out of git
```

---

## 🔑 Where to put your API key

The API key goes in the **browser UI** — there is no config file or `.env` to edit.

```
[Top bar] → GROQ API KEY field → paste gsk_xxxxxxxxxxxxxxxxxxxx
```

If you want to hardcode it for local dev only (never commit this):

1. Open `index.html` in a text editor
2. Find this line near the bottom of the `<script>` section:
   ```js
   const apiKey = document.getElementById('api-key').value.trim();
   ```
3. Replace it with:
   ```js
   const apiKey = 'gsk_YOUR_KEY_HERE'; // ← local dev only, never commit
   ```

> 🚨 Never commit your API key to GitHub. The `.gitignore` and `.env.example` are there to help.

---

## 🧠 How it works

```
Your query
    │
    ▼
Source chips (select which sources to query)
    │
    ▼
All selected source content → bundled into a context prompt
    │
    ▼
Groq API (llama-3.3-70b-versatile) — streamed response
    │
    ▼
Answer with source citations + generated Coral SQL query
```

### Simulated Coral features

| Coral feature | How it's simulated in this app |
|---|---|
| SQL interface | Live SQL editor with syntax highlighting + example cross-source queries |
| Cross-source joins | Multiple sources bundled into one context; AI synthesizes and cites each |
| Caching | Cache hit counter in sidebar stats (simulated ~40% cache rate) |
| Data indexing | Paste any content into "Add source" modal → immediately queryable |

---

## 🤖 Supported AI models (via Groq)

Select from the dropdown in the top bar:

| Model | Speed | Best for |
|---|---|---|
| `llama-3.3-70b-versatile` | Fast | Default — great balance |
| `llama-3.1-70b-versatile` | Fast | Alternative 70B |
| `mixtral-8x7b-32768` | Very fast | Long context queries |
| `gemma2-9b-it` | Fastest | Quick lookups |

---

## 📚 Adding your own data

Click **+ Add source** in the left sidebar:

1. **Pick a type** — Notion, PDF, CSV, GitHub, Markdown, or Custom
2. **Name it** — e.g. "My Research Notes"
3. **Paste content** — copy-paste from your actual notes, a CSV export, a PDF's text, anything
4. Click **Connect source** — it's immediately queryable

**Demo tip:** Add a source mid-demo, then ask a question that spans the new source and an existing one. The AI will cite both — that's the Coral cross-source join story in action.

---

## 🛠️ Local development

No build tools needed. Edit `index.html` and refresh your browser.

If you want a local dev server (for proper CORS handling):

```bash
# Python 3
python3 -m http.server 3000

# Node.js
npx serve .

# Then open http://localhost:3000
```

---

## 🔒 Privacy & security

- Your API key is **never stored** (not in localStorage, not sent to any server)
- All source content stays **in-browser memory only**
- The only external calls are to `api.groq.com` and Google Fonts
- Closing the tab clears everything

---

## 🪸 About Coral

[Coral](https://coraldata.io) is a data retrieval layer that lets you query multiple heterogeneous data sources — databases, APIs, files, and SaaS tools — through a unified SQL interface with caching and cross-source joins.

This project demonstrates what a personal knowledge tool powered by Coral could look like.

---

## 📄 License

MIT — use it, fork it, build on it.

---

*Built with ❤️ for the Coral Hackathon*
