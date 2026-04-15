# Workflows

Human-readable Standard Operating Procedures (SOPs) that define **what** to do and **how** to handle edge cases. These are the instruction layer of the WAT framework — written in plain language, the same way you'd brief someone on your team.

## Available Workflows

| Workflow | Purpose |
|---|---|
| `scrape_youtube.md` | How to collect video and channel data from the YouTube Data API |
| `analyze_data.md` | How to process raw data into trending topics, benchmarks, and opportunities |
| `build_report.md` | How to generate the PDF, push to Sheets, and email the final report |

## How Workflows Are Used

An AI agent (Claude) reads these workflows to understand:
- **Objective** — What the workflow achieves
- **Required inputs** — What data or credentials are needed
- **Which tools to run** — Which scripts in `tools/` to execute
- **Expected outputs** — What gets produced
- **Edge cases** — How to handle failures, rate limits, and missing data

## Updating Workflows

Workflows should evolve as the system learns. When you discover:
- A better method or API endpoint
- A new rate limit or constraint
- A recurring issue and its fix

Update the relevant workflow so the knowledge is preserved for future runs.

## Creating New Workflows

Follow this structure:

```markdown
# Workflow Name

## Objective
What this workflow achieves.

## Required Inputs
- Input 1
- Input 2

## Steps
1. Run `tools/script_name.py`
2. Verify output at `.tmp/output_file.json`

## Error Handling
- Error scenario → How to recover

## Output
What gets produced and where it goes.
```
