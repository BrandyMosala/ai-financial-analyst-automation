
# AI Financial Analyst Automation

A no-code automation pipeline that watches a live Google Sheet for new sales data 
and automatically generates a structured executive report using AI.

## What it does

When a new row is added to a Google Sheet, this system:
1. Captures the new sales data (date, product, region, sales, profit)
2. Sends it to an LLM with a structured prompt for financial analysis
3. Generates a formatted executive report and saves it as a Google Doc

## Architecture

Google Sheets (trigger) → Gemini 2.5 Flash (analysis) → Google Docs (output)

Built on Make.com (formerly Integromat).

## Why this matters

Manual reporting from spreadsheets is slow and inconsistent — different people 
summarize the same data differently. This pipeline enforces a consistent report 
structure every time, regardless of who adds the data.

## Prompt engineering decisions

- **Fixed output structure**: the prompt enforces exact headers (Executive Summary, 
  Total Sales, Best/Worst Product, Regional Insights, Trends, Recommendations) so 
  every report is consistent and easy to scan.
- **Edge case handling**: the prompt explicitly instructs the model to acknowledge 
  when data is too limited for trend analysis (e.g., a single row) rather than 
  fabricating insights. See `prompts/system-prompt.md`.
- **Anti-hallucination guardrail**: explicit instruction not to invent numbers not 
  present in the source data.

## Files

- `scenario-blueprint.json` — exportable Make.com scenario
- `prompts/system-prompt.md` — the full prompt used for report generation
- `screenshots/` — scenario overview, sample generated report

## Example output

See `screenshots/sample-report.png` for a real generated report from test data.

## Stack

- Make.com (automation/orchestration)
- Google Sheets (data source)
- Google Gemini 2.5 Flash (analysis/generation)
- Google Docs (output delivery)
