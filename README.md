# Building Agents

A collection of small, self-contained agentic AI projects, each exploring a different agent pattern and SDK.

## Modules

### `foundations/`

A personal-assistant chatbot that answers questions as "you" on a website (e.g. for recruiters or clients).

- Uses the OpenAI Chat Completions API with function calling.
- Builds its persona from `me/summary.txt` and `me/linkedin.pdf`.
- Exposes two tools: `record_user_details` (captures a visitor's email/notes) and `record_unknown_question` (logs questions it couldn't answer), both delivered via Pushover push notifications.
- Served through a Gradio chat UI.

Run it with:

```bash
cd foundations
python app.py
```

Requires `PUSHOVER_TOKEN` and `PUSHOVER_USER` env vars, and an `OPENAI_API_KEY`.

### `deep_research/`

A multi-agent research pipeline built on the OpenAI Agents SDK. Given a topic, it plans web searches, executes them, synthesizes a report, and emails it out.

- `planner_agent.py` — plans a set of web searches for the query (`WebSearchPlan`).
- `search_agent.py` — runs each search with `WebSearchTool` and returns a concise summary.
- `writer_agent.py` — synthesizes all search summaries into a long-form markdown report (`ReportData`).
- `email_agent.py` — converts the report to HTML and sends it via SendGrid.
- `research_manager.py` — orchestrates the agents end-to-end (plan → search → write → email) and streams progress updates.
- `deep_research.py` — Gradio UI entry point.

Run it with:

```bash
cd deep_research
python deep_research.py
```

Requires `OPENAI_API_KEY` and `SENDGRID_API_KEY` env vars.

## Setup

This project uses [uv](https://github.com/astral-sh/uv) for dependency management.

```bash
uv sync
```

Create a `.env` file in the project root with the API keys referenced above.