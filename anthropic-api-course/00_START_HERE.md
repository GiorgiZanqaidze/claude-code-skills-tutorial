# 🚀 START HERE — Anthropic API Course

Welcome! This is a **complete, hands-on course** teaching you to build production systems with the Anthropic Claude API.

## ⏱️ How Long?
- **Fast track:** 2-3 hours (key phases only)
- **Full course:** 5-6 hours (all 8 phases + exercises)
- **Deep dive:** 8+ hours (experimentation and real project)

## 📍 You Are Here

```
START_HERE.md (this file)
    ↓
Read one of the guides below, then start coding
```

---

## 📖 Choose Your Path

### 🏃 **I want to start coding RIGHT NOW**
1. Read: **[QUICK_START.md](QUICK_START.md)** (5 minutes)
2. Run: `notebooks/01_first_request.ipynb`
3. Continue through Phase 2, then jump to Phase 5

### 🎓 **I want the full experience**
1. Read: **[QUICK_START.md](QUICK_START.md)** (5 minutes)
2. Read: **[LEARNING_PATH.md](LEARNING_PATH.md)** (10 minutes)
3. Run all 8 notebooks in order
4. Do the mini-exercises

### 🔍 **I'm looking for something specific**
- Check **[INDEX.md](INDEX.md)** for quick navigation by topic
- Use the decision trees in **[LEARNING_PATH.md](LEARNING_PATH.md)**

### 💡 **I want to understand the big picture first**
1. Read: **[README.md](README.md)** (overview)
2. Read: **[COURSE_SUMMARY.md](COURSE_SUMMARY.md)** (what you'll learn)
3. Then pick a learning path above

---

## 📚 File Guide

### Setup & Getting Started
- **[QUICK_START.md](QUICK_START.md)** — 5-minute setup
- **[README.md](README.md)** — Course overview
- **[requirements.txt](requirements.txt)** — Dependencies to install
- **.env.example** → **.env** — Where to put your API key

### Learning Materials
- **[LEARNING_PATH.md](LEARNING_PATH.md)** ⭐ **Most useful** — Complete curriculum with decision trees
- **[COURSE_SUMMARY.md](COURSE_SUMMARY.md)** — Cheat sheets and reference
- **[INDEX.md](INDEX.md)** — Navigation by topic

### Code Notebooks (Run these!)
1. `notebooks/01_first_request.ipynb` — SDK basics
2. `notebooks/02_chatbot.ipynb` — Multi-turn conversations
3. `notebooks/03_structured_output.ipynb` — JSON extraction
4. `notebooks/04_evals.ipynb` — Measuring prompt quality
5. `notebooks/05_tool_use.ipynb` — Tool calling (reminder bot)
6. `notebooks/06_prompt_caching.ipynb` — Cost optimization
7. `notebooks/07_rag.ipynb` — Document Q&A
8. `notebooks/08_workflows_vs_agents.ipynb` — Autonomous systems

---

## ✅ Quick Setup (copy-paste ready)

### Step 1: Install Python dependencies
```bash
cd anthropic-api-course
pip install -r requirements.txt
```

### Step 2: Set up your API key
```bash
cp .env.example .env
# Edit .env and paste your API key from https://console.anthropic.com/
```

Your `.env` should contain:
```
ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxxxxx
```

### Step 3: Start Jupyter
```bash
jupyter notebook
```

### Step 4: Open Phase 1
Click `notebooks/01_first_request.ipynb` and run the first cell.

---

## 🎯 What You'll Learn

| Phase | Topic | Example |
|-------|-------|---------|
| 1 | API basics | "Hello Claude!" |
| 2 | Conversations | Chatbot that remembers context |
| 3 | Structured data | Extract JSON reliably |
| 4 | Measurement | Score your prompts |
| 5 | Tool use | Reminder bot with 3 tools |
| 6 | Optimization | 90% cheaper API calls |
| 7 | RAG | Q&A over your documents |
| 8 | Agents | Autonomous research assistant |

---

## 🔑 Key Concepts You'll Master

✅ Authentication and initialization
✅ Single-turn and multi-turn conversations
✅ System prompts and temperature control
✅ Structured output extraction
✅ Prompt evaluation and measurement
✅ Tool calling and function integration
✅ Multi-tool chaining
✅ API cost optimization
✅ Document grounding (RAG)
✅ Autonomous agents and planning

---

## ⚡ Common Questions

**Q: Do I need to know Python?**
A: Yes, basics like functions, loops, and dictionaries. This course isn't a Python intro.

**Q: Do I need a paid API key?**
A: No, Anthropic offers a free trial. Sign up at https://console.anthropic.com/

**Q: How much will this cost?**
A: The free tier is usually enough. Each phase uses ~$0.01-0.10. Production systems scale from there.

**Q: Can I skip phases?**
A: Not recommended. Each builds on the previous. Minimum: 1 → 2 → 5 → 8.

**Q: Where do I ask questions?**
A: Check the Troubleshooting section in QUICK_START.md or LEARNING_PATH.md.

---

## 📊 Course Structure at a Glance

```
Foundation (Phase 1-2)
    ↓
Output Control (Phase 3-4)
    ↓
Integration (Phase 5-6)
    ↓
Knowledge & Autonomy (Phase 7-8)
```

---

## 🏁 Next Step

**Pick your path above, then:**

👉 **New to Claude?** → [QUICK_START.md](QUICK_START.md)

👉 **Want guidance?** → [LEARNING_PATH.md](LEARNING_PATH.md)

👉 **Ready to code?** → Run `jupyter notebook` and open `notebooks/01_first_request.ipynb`

---

## 📞 Help & Support

| Need | Go To |
|------|-------|
| Setup help | [QUICK_START.md](QUICK_START.md) Troubleshooting |
| Lost in course | [INDEX.md](INDEX.md) Navigation |
| How to choose pattern | [LEARNING_PATH.md](LEARNING_PATH.md) Decision Trees |
| Quick reference | [COURSE_SUMMARY.md](COURSE_SUMMARY.md) Cheat Sheets |
| Course overview | [README.md](README.md) |

---

## 🎓 By the End of This Course

You'll know how to:
- Build production Claude integrations
- Write measurable, testable prompts
- Optimize costs with caching
- Ground Claude in your documents
- Build autonomous AI systems
- Make architectural decisions (workflows vs agents)

**Ready?** → [QUICK_START.md](QUICK_START.md) (5 minutes) → Code!

---

**Course by:** Anthropic API Documentation
**Your learning journey starts now.** 🚀
