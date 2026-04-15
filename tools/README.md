# Tools

Deterministic Python scripts that form the **execution layer** of the WAT framework. Each script handles one specific job — no AI reasoning, just reliable, testable code.

## Scripts

| Script | Purpose | Input | Output |
|---|---|---|---|
| `youtube_scraper.py` | Searches YouTube Data API v3 for AI niche videos and fetches detailed stats | API credentials | `.tmp/raw_youtube_data.json` |
| `analyze_data.py` | Extracts trending topics, ranks channels, computes engagement benchmarks | `raw_youtube_data.json` | `.tmp/analysis_results.json` |
| `build_pdf.py` | Generates a branded 10-page PDF report with charts and insights | `analysis_results.json` | `.tmp/ai_youtube_report.pdf` |
| `build_slides.py` | Creates a Google Slides presentation from analysis data | `analysis_results.json` | Google Slides |
| `push_to_sheets.py` | Writes analysis data to 6 tabs in Google Sheets | `analysis_results.json` | Google Sheets |
| `send_email.py` | Sends the PDF report as a Gmail attachment | `ai_youtube_report.pdf` | Email delivered |
| `run_pipeline.py` | Orchestrates all 5 steps sequentially with error handling | All of the above | Full pipeline |

## Data Flow

```
youtube_scraper.py ──▶ analyze_data.py ──▶ build_pdf.py ──────▶ send_email.py
                                       ├──▶ push_to_sheets.py
                                       └──▶ build_slides.py
```

## Running Individual Tools

```bash
# From the project root
python tools/youtube_scraper.py    # Step 1: Scrape
python tools/analyze_data.py       # Step 2: Analyze
python tools/build_pdf.py          # Step 3: PDF
python tools/push_to_sheets.py     # Step 4: Sheets
python tools/send_email.py         # Step 5: Email

# Or run everything at once
python tools/run_pipeline.py
```

## Error Handling

Each script handles failures gracefully:

- **403 Quota Exceeded** — Saves partial data, exits cleanly. Re-run next day.
- **429 Rate Limited** — Exponential backoff retry (3 attempts).
- **Missing Input File** — Prints which step to run first.
- **Expired OAuth Token** — Auto-refreshes; opens browser if refresh fails.

## Adding New Tools

1. Create a new `.py` file in this directory
2. Follow the pattern: read input from `.tmp/`, write output to `.tmp/` or a cloud service
3. Add a corresponding workflow in `workflows/` documenting its usage
4. If it should run in the daily pipeline, add it to `run_pipeline.py`
