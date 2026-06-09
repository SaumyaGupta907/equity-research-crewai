# equity-research-crewai
# Equity Research CrewAI Agent

A multi-agent equity research system that automates company discovery, financial research, comparative analysis, and final stock selection using CrewAI.

The project uses specialized AI agents to research trending companies in a selected sector, evaluate market signals and business risks, and generate structured investment research outputs.

## Overview

Equity research usually requires gathering market news, identifying relevant companies, comparing financial and business signals, and writing a final recommendation. This project automates that workflow using a multi-agent architecture.

Each agent has a specific responsibility, and the workflow is coordinated through CrewAI. The system produces structured JSON reports and a final decision summary.

## Features

* Multi-agent research workflow using CrewAI
* Sector-based company discovery
* Web research using Serper API
* Structured company research reports
* Final stock-pick decision report
* Push notification support using Pushover
* Long-term memory using SQLite
* YAML-based agent and task configuration
* Reproducible dependency setup using `uv`

## Tech Stack

* Python
* CrewAI
* OpenAI
* Serper API
* Pushover API
* SQLite
* YAML
* uv

## Project Architecture

The system is organized into four main agents:

### Trending Company Finder

Identifies companies that are currently trending in a given sector based on recent market activity and news signals.

### Financial Researcher

Researches the shortlisted companies and generates structured analysis covering business context, growth signals, risks, and market relevance.

### Equity Picker

Compares the researched companies and selects the strongest candidate. It generates the final decision report and sends a push notification with the selected company.

### Manager Agent

Coordinates the workflow and delegates tasks between agents in the correct order.

## Workflow

```text
Sector Input
    ↓
Trending Company Finder
    ↓
Financial Researcher
    ↓
Equity Picker
    ↓
Final Decision Report + Push Notification
```

## Project Structure

```text
equity_researcher/
├── knowledge/
│   └── user_preference.txt
├── src/
│   └── equity_researcher/
│       ├── config/
│       │   ├── agents.yaml
│       │   └── tasks.yaml
│       ├── tools/
│       │   └── push_tool.py
│       ├── crew.py
│       └── main.py
├── pyproject.toml
├── uv.lock
└── README.md
```

Generated files are stored locally in:

```text
output/
memory/
```

These folders are ignored from Git because they are created during runtime.

## Output

A successful run generates structured research artifacts:

```text
output/trending_companies.json
output/research_report.json
output/decision.md
```

### Example Outputs

* `trending_companies.json`: list of companies identified for the selected sector
* `research_report.json`: detailed research for shortlisted companies
* `decision.md`: final recommendation with reasoning

## Environment Variables

Create a `.env` file in the project root:

```env
OPENAI_API_KEY=your_openai_key
CHROMA_OPENAI_API_KEY=your_openai_key
SERPER_API_KEY=your_serper_key
PUSHOVER_USER=your_pushover_user
PUSHOVER_TOKEN=your_pushover_token
```

`CHROMA_OPENAI_API_KEY` is used by Chroma for CrewAI memory.

## Installation

Install dependencies using `uv`:

```bash
uv lock
```

## Run

```bash
uv run crewai run
```

## Memory

The project uses CrewAI memory to persist agent context across runs.

Long-term memory is stored locally using SQLite:

```text
memory/long_term_memory_storage.db
```

Memory files are not committed to Git.

## Git Ignore

The following files and folders are ignored:

```text
.env
.venv/
memory/
output/
__pycache__/
*.pyc
```

## Use Case

This project demonstrates how multi-agent AI systems can automate research-heavy workflows. Instead of relying on a single prompt, the work is divided across agents with clear responsibilities, tool access, memory, and structured outputs.

## Disclaimer

This project is for technical demonstration and research automation purposes only. It is not financial advice.
