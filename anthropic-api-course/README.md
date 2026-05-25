# Anthropic API Course — Hands-on Companion

A step-by-step coding companion for the [Skilljar "Claude with the Anthropic API"](https://anthropic.skilljar.com/claude-with-the-anthropic-api) course.

Each notebook is one focused phase. Work through them in order.

## Phases

| # | Notebook | Concepts |
|---|----------|----------|
| 1 | `notebooks/01_first_request.ipynb` ✅ | SDK setup, first `messages.create`, response shape |
| 2 | `notebooks/02_chatbot.ipynb` | Multi-turn conversations, system prompts, temperature, streaming |
| 3 | _(next)_ | Prefill, stop sequences, structured JSON output |
| 4 | _(next)_ | Eval pipeline: dataset → grader → score |
| 5 | _(next)_ | Tool use: schema, run loop, multiple tools |
| 6 | _(next)_ | Prompt caching: cache_control breakpoints |
| 7 | _(next)_ | RAG: chunk, embed, search |
| 8 | _(next)_ | Workflows vs agents |

## Setup (one time)

```bash
cd anthropic-api-course
cp .env.example .env          # then paste your real key into .env
pip install -r requirements.txt
jupyter notebook
```

Open `notebooks/01_first_request.ipynb` and run the cells top to bottom.

## Getting your API key

1. Go to https://console.anthropic.com/
2. Settings → API Keys → Create Key
3. Paste it into `.env` as `ANTHROPIC_API_KEY="sk-ant-..."`

The `.env` file is gitignored — never commit it.
