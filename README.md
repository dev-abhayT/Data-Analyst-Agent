# Data Analyst Agent

Upload a spreadsheet, ask questions about it in plain English, and get real answers back — no coding, no formulas, no pivot tables.

This is a chat-style web app. You drop in a CSV or Excel file, and the agent reads it, understands what's in it, and lets you ask questions like you're talking to a data analyst. It runs the actual calculations behind the scenes (using pandas) and replies in plain language, sometimes with a small table to back up the answer.

---

## What It Does (Features)

- **Upload a file** — drag and drop a CSV or Excel file (up to 100 MB).
- **Instant data profile** — as soon as you upload, it shows you the row count, column names, data types, missing values, and a few sample rows, so you know what you're working with.
- **Suggested questions** — the agent looks at your actual columns and suggests 3 relevant questions to get you started.
- **Ask anything in plain English** — type a question like "What's the average sales by region?" or "Which product had the most returns?" and get a written answer, streamed in real time as it's generated.
- **Answer tables** — when it makes sense, the answer comes with a small results table underneath it.
- **Follow-up suggestions** — after each answer, it suggests natural next questions based on the conversation.
- **Charts** — the agent automatically draws a bar, line, or pie chart when the data calls for one.
- **Multiple datasets** — upload more than one file and pick which ones a question should look at.
- **"What is this data about?"** — ask general/descriptive questions and get a plain-language summary instead of raw numbers.
- **Download your results** — export any answer's data as a CSV.
- **See the work** — every answer has a "Show code" option so you can see exactly what calculation produced it.
- **Cost tracking** — see how many tokens each answer used and its estimated cost.
- **Session memory** — close the tab and come back later; your upload and conversation history are still there.
- **Full audit trail** — every question, the code that ran, and the result are saved, so nothing is a black box.

---

## Tech Stack

**Backend**
- Python + FastAPI — the web server
- LangGraph — orchestrates the multi-step "understand → write code → run it → answer" process
- Google Gemini — the AI model that reads your question and writes the analysis
- pandas / NumPy — does the actual number-crunching on your spreadsheet
- SQLite — stores sessions, questions, and results for the audit trail
- Server-Sent Events (SSE) — streams the answer to you word-by-word as it's written

**Frontend**
- Next.js + TypeScript — the web interface
- Tailwind CSS — styling

**Hosting**
- Deployed on Render (free tier)

---

## How to Use It

### Online
Just open the app in your browser — works on desktop or mobile, no install needed:

**https://data-analyst-agent-xbxv.onrender.com/app/**

(If it's been idle a while, the first load can take 30–60 seconds to wake up — that's normal on the free hosting tier.)

1. Drag and drop a CSV or Excel file onto the page.
2. Wait a couple seconds — you'll see a profile card showing what's in your data.
3. Click one of the suggested questions, or type your own.
4. Read the answer as it streams in. If there's a relevant chart or table, it'll show up underneath.
5. Ask a follow-up, download the data, or check "Show code" to see how the answer was calculated.

### Running it yourself (for developers)

```bash
git clone https://github.com/dev-abhayT/Data-Analyst-Agent.git
cd Data-Analyst-Agent

cp .env.example .env
# edit .env and add your Gemini API key:
#   AGENT_GEMINI_API_KEY=<your key>

uv sync
uv run alembic upgrade head
uv run python -m src
```

Then open `http://localhost:8001/app/` in your browser.

To run the test suite:

```bash
uv run pytest tests/ -v
```
