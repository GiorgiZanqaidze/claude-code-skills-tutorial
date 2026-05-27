# Anthropic API Course — Hands-on Companion

A step-by-step coding companion for the [Skilljar "Claude with the Anthropic API"](https://anthropic.skilljar.com/claude-with-the-anthropic-api) course.

Each notebook is one focused phase. Work through them **in order**. By the end, you'll understand the entire stack: single-turn requests → multi-turn conversations → structured output → evals → tools → caching → RAG → agents.

**[Start here: LEARNING_PATH.md](LEARNING_PATH.md)** — complete guide to the course structure and decision trees for real-world use.

## Phases

| # | Notebook | Concepts |
|---|----------|----------|
| 1 | `notebooks/01_first_request.ipynb` ✅ | SDK setup, first `messages.create`, response shape |
| 2 | `notebooks/02_chatbot.ipynb` ✅ | Multi-turn conversations, system prompts, temperature, streaming |
| 3 | `notebooks/03_structured_output.ipynb` ✅ | Prefill, stop sequences, structured JSON output |
| 4 | `notebooks/04_evals.ipynb` ✅ | Eval pipeline: dataset → grader → score |
| 5 | `notebooks/05_tool_use.ipynb` ✅ | Tool use: schema, run loop, multiple tools |
| 6 | `notebooks/06_prompt_caching.ipynb` ✅ | Prompt caching: cache_control breakpoints |
| 7 | `notebooks/07_rag.ipynb` ✅ | RAG: chunk, embed, retrieve, augment, generate |
| 8 | `notebooks/08_workflows_vs_agents.ipynb` ✅ | Workflows vs agents: state, loops, autonomy, research agent |

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
