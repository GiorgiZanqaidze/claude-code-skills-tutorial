# 📚 Anthropic API Course — Complete Index

## 🎓 Course Materials (8 Phases)

### Getting Started
1. **[QUICK_START.md](QUICK_START.md)** — 5-minute setup (start here!)
2. **[README.md](README.md)** — Course overview and phase structure
3. **[LEARNING_PATH.md](LEARNING_PATH.md)** — Complete learning guide with decision trees
4. **[COURSE_SUMMARY.md](COURSE_SUMMARY.md)** — What you learned and cheat sheets

---

## 📖 Notebooks (8 Phases — Run in Order)

### Phase 1: SDK Setup & First Request ✅
**File:** `notebooks/01_first_request.ipynb`
- Initialize Anthropic client
- Make your first API call
- Understand response shape and tokens
- Learn about stop reasons

**What you'll build:** Hello world Claude request

**Estimated time:** 10 minutes

---

### Phase 2: Multi-Turn Conversations ✅
**File:** `notebooks/02_chatbot.ipynb`
- Maintain message history
- Use system prompts
- Control temperature (creative vs deterministic)
- Implement streaming output

**What you'll build:** A conversational chatbot

**Estimated time:** 20 minutes

---

### Phase 3: Structured Output ✅
**File:** `notebooks/03_structured_output.ipynb`
- Extract clean JSON without markdown
- Use prefill technique (start Claude's response)
- Use stop sequences (halt at specific string)
- Tool-based alternative for reliability

**What you'll build:** `extract_json()` helper function

**Estimated time:** 15 minutes

---

### Phase 4: Evals & Measurement ✅
**File:** `notebooks/04_evals.ipynb`
- Create test datasets
- Build code-based graders (syntax checks)
- Build model-based graders (LLM quality scoring)
- Compare prompt versions with numbers

**What you'll build:** Eval pipeline showing prompt improvement

**Estimated time:** 20 minutes

---

### Phase 5: Tool Use ✅
**File:** `notebooks/05_tool_use.ipynb`
- Define tool functions
- Write tool schemas
- Implement the 4-step tool loop
- Chain multiple tools automatically

**What you'll build:** Reminder bot (get time → add days → set reminder)

**Estimated time:** 30 minutes

---

### Phase 6: Prompt Caching ✅
**File:** `notebooks/06_prompt_caching.ipynb`
- Enable caching with `cache_control`
- Understand cache lifecycle and costs
- Optimize high-volume workloads
- Measure cache hits vs writes

**What you'll build:** Cached chatbot saving 90% on repeated context

**Estimated time:** 20 minutes

---

### Phase 7: RAG (Retrieval Augmented Generation) ✅
**File:** `notebooks/07_rag.ipynb`
- Chunk documents into semantic units
- Create embeddings (simulated for tutorial)
- Implement similarity search
- Build Q&A system grounded in documents

**What you'll build:** Product documentation Q&A bot

**Estimated time:** 30 minutes

---

### Phase 8: Workflows vs Agents ✅
**File:** `notebooks/08_workflows_vs_agents.ipynb`
- Compare stateless workflows vs autonomous agents
- Implement agent loop (planning + execution)
- Handle terminal conditions
- Build research agent

**What you'll build:** Autonomous research assistant

**Estimated time:** 30 minutes

---

## 🚀 Quick Navigation

### By Use Case

**"I want to..."**

- **Chat with Claude** → Phase 2 (02_chatbot.ipynb)
- **Extract structured data** → Phase 3 (03_structured_output.ipynb)
- **Improve my prompt** → Phase 4 (04_evals.ipynb)
- **Let Claude call my APIs** → Phase 5 (05_tool_use.ipynb)
- **Reduce API costs** → Phase 6 (06_prompt_caching.ipynb)
- **Answer questions over my documents** → Phase 7 (07_rag.ipynb)
- **Solve complex problems autonomously** → Phase 8 (08_workflows_vs_agents.ipynb)

### By Topic

**API Basics:**
- Client initialization → Phase 1
- Messages, roles, content → Phase 1, 2
- Stop reasons → Phase 1, 3
- Usage tokens → Phase 1, 6

**Behavior Control:**
- System prompts → Phase 2
- Temperature → Phase 2
- Streaming → Phase 2

**Output Handling:**
- Structured JSON → Phase 3
- Stop sequences → Phase 3
- Prefill technique → Phase 3

**Quality Metrics:**
- Datasets → Phase 4
- Graders (code + model) → Phase 4
- Scoring → Phase 4

**Integration:**
- Tool functions → Phase 5
- Tool schemas → Phase 5
- Tool loop → Phase 5
- Multi-tool chaining → Phase 5

**Optimization:**
- Caching → Phase 6
- Cache_control → Phase 6
- Cost savings → Phase 6

**Knowledge:**
- Chunking → Phase 7
- Embeddings → Phase 7
- Retrieval → Phase 7
- Augmentation → Phase 7

**Autonomy:**
- Agent loop → Phase 8
- Planning → Phase 8
- State management → Phase 8
- Workflows vs agents → Phase 8

---

## 📊 Learning Progression

```
Phase 1: Stateless → Phase 2: Stateful (conversation)
                 ↓
Phase 3: Structured Output → Phase 4: Measured Quality
                 ↓
Phase 5: Tool Integration → Phase 6: Cost Optimization
                 ↓
Phase 7: Knowledge Grounding (RAG) → Phase 8: Autonomous Systems
```

---

## 🎯 Recommended Learning Path

### Fast Track (2-3 hours)
1. QUICK_START.md
2. 01_first_request.ipynb
3. 02_chatbot.ipynb
4. 05_tool_use.ipynb
5. 08_workflows_vs_agents.ipynb (read, don't run)

### Comprehensive (4-5 hours)
1. QUICK_START.md
2. Run all 8 notebooks in order
3. Do mini-exercises at end of each phase
4. Read LEARNING_PATH.md for decision trees

### Deep Dive (6+ hours)
1. Run all 8 notebooks with extensive experimentation
2. Modify code, break things, fix them
3. Do all mini-exercises
4. Build a small real-world project using patterns from the course

---

## 💻 Prerequisites

- Python 3.8+
- `pip` (Python package manager)
- Anthropic API key (free trial available)
- ~30 minutes to 2+ hours depending on learning path

## 🏃 Quick Setup

```bash
# 1. Get your API key from console.anthropic.com

# 2. Clone and setup
cd anthropic-api-course
cp .env.example .env
# Edit .env and paste your API key

# 3. Install dependencies
pip install -r requirements.txt

# 4. Start Jupyter
jupyter notebook

# 5. Open notebooks/01_first_request.ipynb and run!
```

---

## 📞 Questions?

- **Setup issues?** → See QUICK_START.md Troubleshooting
- **Lost in course?** → Check LEARNING_PATH.md for navigation
- **What can I build?** → See COURSE_SUMMARY.md examples
- **Which pattern to use?** → LEARNING_PATH.md has decision trees

---

## ✅ What You'll Know After This Course

✅ How the Anthropic API works (messages, roles, tokens)
✅ Multi-turn conversations with memory
✅ Structured output extraction (JSON, CSV, etc.)
✅ How to measure and improve prompts
✅ Tool use and function calling
✅ Cost optimization with caching
✅ RAG (document grounding)
✅ Agent loops and autonomous systems

**You'll be ready to build production systems with Claude.**

---

**[Start with QUICK_START.md →](QUICK_START.md)**

Last updated: 2026-05-27
