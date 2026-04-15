<p align="center">
  <img src="https://img.shields.io/badge/Python-3.13-BED754?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/YouTube_API-v3-E8293A?style=for-the-badge&logo=youtube&logoColor=white" alt="YouTube API">
  <img src="https://img.shields.io/badge/Google_Sheets-API-8A9E3A?style=for-the-badge&logo=googlesheets&logoColor=white" alt="Sheets">
  <img src="https://img.shields.io/badge/Gmail-API-BED754?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail">
  <img src="https://img.shields.io/badge/Scheduled-Daily_7AM-2A2A2A?style=for-the-badge&logo=clockify&logoColor=BED754" alt="Scheduled">
</p>

<h1 align="center">YouTube AI Niche Analyzer</h1>

<p align="center">
  <strong>Automated intelligence pipeline that scrapes, analyzes, and delivers daily reports on the AI/automation YouTube niche.</strong>
</p>

<p align="center">
  Built on the <strong>WAT Framework</strong> (Workflows → Agents → Tools) — where AI handles reasoning and deterministic scripts handle execution.
</p>

---

## What It Does

Every day at 7:00 AM, this pipeline automatically:

1. **Scrapes** 500+ videos across 7 AI keywords from the YouTube Data API
2. **Analyzes** trending topics, engagement benchmarks, content gaps, and optimal posting strategies
3. **Generates** a branded 10-page PDF report with charts and dynamic insights
4. **Pushes** structured data to Google Sheets for further exploration
5. **Emails** the finished PDF report to your inbox via Gmail

All five steps run end-to-end in under 2 minutes with zero manual intervention.

---

## Pipeline Overview

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   SCRAPE        │────▶│   ANALYZE       │────▶│   REPORT        │
│                 │     │                 │     │                 │
│ 7 keywords      │     │ Trending topics │     │ 10-page PDF     │
│ 14 API searches │     │ Top channels    │     │ Google Sheets   │
│ 500+ videos     │     │ Benchmarks      │     │ Gmail delivery  │
│ 450+ channels   │     │ Opportunities   │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

---

## Report Insights

| Analysis | What You Get |
|---|---|
| **Trending Topics** | Top 15 rising topics ranked by view velocity and volume |
| **Top Videos** | 10 highest-performing videos with engagement breakdowns |
| **Top Channels** | 10 channels ranked by engagement rate (likes + comments / views) |
| **Duration Sweet Spot** | Which video length gets the most views |
| **Best Publish Day** | Day-of-week breakdown by average views |
| **Best Publish Hour** | Optimal upload time (UTC) |
| **Title Patterns** | Performance by format: how-to, listicle, question, comparison, news, tutorial |
| **Content Opportunities** | Rising topics with low competition — your next video ideas |

---

## Quick Start

### Prerequisites

- Python 3.10+
- YouTube Data API key or Google OAuth credentials
- Google Cloud project with YouTube, Sheets, and Gmail APIs enabled

### 1. Clone & Install

```bash
git clone https://github.com/CodeWithArhum/Youtube-Analysis.git
cd Youtube-Analysis
pip install -r requirements.txt
```

### 2. Configure Environment

Create a `.env` file in the project root:

```env
YOUTUBE_API_KEY=your_youtube_api_key_here
GOOGLE_SHEETS_ID=your_google_sheets_id_here
```

Place your Google OAuth `client_secret*.json` file in the project root for Sheets and Gmail access.

### 3. Run the Pipeline

```bash
# Full pipeline (scrape → analyze → PDF → sheets → email)
python tools/run_pipeline.py

# Or run individual steps
python tools/youtube_scraper.py
python tools/analyze_data.py
python tools/build_pdf.py
python tools/push_to_sheets.py
python tools/send_email.py
```

### 4. Schedule Daily Runs (Windows)

```bash
# Creates a Windows Task Scheduler job for 7:00 AM daily
setup_schedule.bat
```

---

## Project Structure

```
Youtube-Analysis/
│
├── tools/                  # Deterministic Python scripts (execution layer)
│   ├── youtube_scraper.py  # YouTube Data API collector
│   ├── analyze_data.py     # Data processor & trend analyzer
│   ├── build_pdf.py        # Branded PDF report generator
│   ├── build_slides.py     # Google Slides report builder
│   ├── push_to_sheets.py   # Google Sheets uploader
│   ├── send_email.py       # Gmail sender with PDF attachment
│   └── run_pipeline.py     # Full pipeline orchestrator
│
├── workflows/              # Markdown SOPs (instruction layer)
│   ├── scrape_youtube.md   # Scraping procedure & error handling
│   ├── analyze_data.md     # Analysis methodology & computations
│   └── build_report.md     # Report generation & delivery steps
│
├── .tmp/                   # Intermediate files (gitignored)
│   ├── raw_youtube_data.json
│   ├── analysis_results.json
│   └── ai_youtube_report.pdf
│
├── setup_schedule.bat      # Windows Task Scheduler setup
├── requirements.txt        # Python dependencies
├── .env                    # API keys (gitignored)
└── CLAUDE.md               # AI agent operating instructions
```

---

## The WAT Framework

This project is built on the **Workflows, Agents, Tools** architecture:

| Layer | Role | Location |
|---|---|---|
| **Workflows** | Human-readable SOPs that define *what* to do | `workflows/` |
| **Agents** | AI reasoning layer that orchestrates execution | Claude / LLM |
| **Tools** | Deterministic scripts that *do* the work | `tools/` |

**Why?** When AI handles every step directly, accuracy compounds downward — 90% per step means 59% after five. By offloading execution to deterministic scripts, the AI focuses on orchestration where it excels, and the scripts deliver consistent, testable results.

---

## API Usage

| API | Units Per Run | Daily Limit |
|---|---|---|
| YouTube Data API v3 | ~1,430 | 10,000 |
| Google Sheets API | ~20 requests | 300/min |
| Gmail API | 1 email | 100/min |

Safe to run 5-7x per day with overhead for other usage.

---

## License

This project is for personal and educational use.

---

<p align="center">
  Built by <a href="https://github.com/CodeWithArhum"><strong>@CodeWithArhum</strong></a>
</p>
