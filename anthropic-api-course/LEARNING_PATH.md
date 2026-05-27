# Anthropic API Course: Complete Learning Path

## 🎯 Course Progression

This is a **hands-on journey** from "Hello Claude" to production patterns. Each phase builds on the previous one.

### The 8-Phase Stack

```
Phase 1: SDK & Messages API
        ↓ (learn single-turn requests)
Phase 2: Multi-turn Conversations
        ↓ (maintain context)
Phase 3: Structured Output
        ↓ (get clean JSON from Claude)
Phase 4: Evals & Measurement
        ↓ (measure prompt quality with numbers)
Phase 5: Tool Use
        ↓ (Claude calls YOUR functions)
Phase 6: Prompt Caching
        ↓ (optimize cost & speed)
Phase 7: RAG (Retrieval Augmented Generation)
        ↓ (ground Claude in your documents)
Phase 8: Workflows vs Agents
        ↓ (choose your execution pattern)
```

---

## 🗂️ Phase Breakdown

### **Phase 1: SDK Setup & First Request** ✅
**Goal:** Initialize the Anthropic client and make your first API call.

**Key Concepts:**
- API authentication via `.env` file
- `client.messages.create()` structure
- Response shape: `Message`, `ContentBlock[]`, `usage`
- Stop reasons: `end_turn`, `max_tokens`, `tool_use`, `stop_sequence`
- Usage metrics: `input_tokens`, `output_tokens`

**You'll build:** Hello world API call

**Real-world use:** Foundation for all Claude integration

---

### **Phase 2: Multi-turn Conversations** ✅
**Goal:** Keep a conversation going by managing message history.

**Key Concepts:**
- Message history list: `[{role: "user"/"assistant", content: "..."}]`
- System prompts: shape Claude's behavior without API changes
- Temperature: 0 (deterministic) to 1 (creative)
- Streaming: get token-by-token output in real-time
- Chatbot loop: append each turn, re-send history

**You'll build:** A conversational chatbot

**Real-world use:** Customer support bots, chat interfaces, copilots

---

### **Phase 3: Structured Output** ✅
**Goal:** Extract JSON without markdown fences or chit-chat.

**Key Concepts:**
- Assistant prefill: start Claude's response for it
- Stop sequences: halt generation at a specific string
- Technique: prefill with ` ```json\n `, stop on ` ``` `
- Tool-based alternative: force Claude to use a tool with structured schema

**You'll build:** `extract_json()` function for any extraction task

**Real-world use:** Data extraction, classification, summarization

---

### **Phase 4: Evals & Measurement** ✅
**Goal:** Stop guessing. Measure prompt quality with numbers.

**Key Concepts:**
- Dataset: 5+ hand-crafted test cases
- Code-based grader: `json.loads()` or regex checks
- Model-based grader: second LLM call to score quality
- Eval loop: run prompt on dataset → grade → average → compare versions
- Scoring: syntax (pass/fail) + quality (1-10)

**You'll build:** An eval pipeline comparing two prompt versions

**Real-world use:** A/B testing prompts, quality gates, regression detection

---

### **Phase 5: Tool Use** ✅
**Goal:** Give Claude access to functions it can call.

**Key Concepts:**
- Tool function: plain Python function
- Tool schema: JSON description of when/how to call it
- 4-step pattern:
  1. Call Claude with `tools=[...]`
  2. If `stop_reason == "tool_use"`, extract tool calls
  3. Run the functions locally
  4. Send results back in a `tool_result` block
- Tool loop: repeat until Claude says `stop_reason != "tool_use"`
- Multi-tool chaining: Claude autonomously decides which tools to call and in what order

**You'll build:** A reminder bot chaining 3 tools (get time, add days, set reminder)

**Real-world use:** Any integration with external systems (APIs, databases, calculations)

---

### **Phase 6: Prompt Caching** ✅
**Goal:** Reduce input token cost by 90% for repeated prefixes.

**Key Concepts:**
- Cache breakpoint: `"cache_control": {"type": "ephemeral"}` on a system or tool block
- Processing order: tools → system → messages
- Cache lifetime: ~5 min default (refreshed on cache hits)
- Usage metrics: `cache_creation_input_tokens` (expensive), `cache_read_input_tokens` (~10% cost)
- Invalidation: any byte change before the breakpoint = cache miss
- Cost: cache write costs ~125%, cache read costs ~10%, pays off after 2-3 hits

**You'll build:** A multi-turn conversation where system prompt is cached

**Real-world use:** High-volume, repetitive queries (customer support, chatbots)

---

### **Phase 7: RAG (Retrieval Augmented Generation)** ✅
**Goal:** Ground Claude's answers in your own documents.

**Key Concepts:**
- Chunking: split documents into semantic units (~500 chars each)
- Embeddings: convert text → vector (we simulated; use real embeddings in production)
- Similarity search: find top-K chunks closest to user query
- Augmentation: inject retrieved chunks into system prompt as context
- RAG loop: query → retrieve → format context → prompt → generate
- Multi-turn RAG: retrieve fresh context on each turn (questions can drift)

**You'll build:** A Q&A bot grounded in SkyForge Cloud product docs

**Real-world use:** Documentation assistants, knowledge base search, internal wikis

---

### **Phase 8: Workflows vs Agents** ✅
**Goal:** Know when to use stateless workflows vs. autonomous agents.

**Key Concepts:**
- **Workflow:** user action → Claude + tools → reply (Phase 5 was this)
- **Agent:** goal + autonomy → Claude decides what to search → loop until confident
- Agent loop: `while not done: call_claude() → if tool_use: run_tools() → loop`
- Terminal conditions: goal achieved, max iterations, user halt
- Memory: agents can track findings, confidence, progress
- Cost vs. value: agents make many API calls; use for complex/vague tasks only
- Pitfalls: infinite loops, tool thrashing, context overflow

**You'll build:** A research agent that chains multiple searches autonomously

**Real-world use:** Complex research tasks, multi-step problem solving, exploratory analysis

---

## 🎯 Decision Tree: Which Pattern to Use?

```
Is the task well-defined and straightforward?
  ├─ YES → Phase 1 or 2 (basic chat/request)
  └─ NO → continue...

Does Claude need to call functions / integrate with external systems?
  ├─ YES → Phase 5 (tool use)
  │       └─ Does Claude decide WHICH tools to call autonomously?
  │           ├─ YES → Phase 8 (agent loop)
  │           └─ NO → Phase 5 (workflow / tool loop)
  └─ NO → continue...

Does Claude need to answer based on YOUR documents (not training data)?
  ├─ YES → Phase 7 (RAG)
  └─ NO → continue...

Do you need structured output (JSON, CSV, code)?
  ├─ YES → Phase 3 (prefill + stop)
  └─ NO → plain text is fine

Is cost critical? Will you call the API 100+ times?
  ├─ YES → Phase 6 (prompt caching for repeated requests)
  └─ NO → cost optimization is secondary
```

---

## 📊 Quick Reference: Cost & Speed

| Pattern | API Calls | Tokens Per Call | Latency | When to Use |
|---------|-----------|-----------------|---------|-------------|
| Single-turn (Phase 1) | 1 | Low | <1s | Stateless requests |
| Conversation (Phase 2) | 1 per turn | Medium | <1s per turn | Chat interfaces |
| Structured (Phase 3) | 1 | Low | <1s | One-off extractions |
| Eval (Phase 4) | 5+ (dataset size) | Low-Medium | Minutes | Testing prompts |
| Workflow + Tools (Phase 5) | 3-5 (avg) | Medium | 1-3s | Well-defined multi-step |
| Cached (Phase 6) | Same as above | -90% on cache hits | Same | High-volume, repeated |
| RAG (Phase 7) | 1 + search overhead | Medium | <2s | Document Q&A |
| Agent (Phase 8) | 5-10 (avg) | Medium-High | 3-10s | Complex, exploratory |

---

## 🛠️ Production Checklist

When moving your prototype to production, verify:

- [ ] API key safely stored in `.env` (never in code)
- [ ] Error handling: network failures, rate limits, API errors
- [ ] Logging: track all API calls for debugging & cost audit
- [ ] Evaluation dataset: verify prompt quality on real data
- [ ] Prompt caching: if >100 QPS, enable cache_control
- [ ] Tool schemas: documented, validated inputs, helpful error messages
- [ ] Context limits: message history doesn't overflow (use summarization or caching)
- [ ] Cost monitoring: track input/output tokens, cache hits, estimate monthly spend
- [ ] Latency SLA: ensure response times meet user expectations
- [ ] Fallback behavior: what to do if Claude fails or timeout?

---

## 🚀 Next Steps After the Course

1. **Build a real project:** Choose a use case (customer support, data extraction, research assistant) and implement it using these patterns.

2. **Measure quality:** Create an eval dataset specific to your domain. Use model-based graders to detect regressions.

3. **Optimize cost:** Profile your API calls. Enable caching where applicable. Use smaller models for graders.

4. **Deploy safely:** Add monitoring, alerting, and rollback procedures. Start with low traffic and gradually scale.

5. **Iterate:** Collect real user feedback. A/B test prompt variations. Keep improving.

---

## 📚 Key Takeaways

1. **Claude is a builder's tool**, not a magic answer machine. The API is a surface for iteration and control.

2. **Prompts are code.** Treat them like code: version them, test them, measure quality.

3. **Tokens are money.** Cache, batch, and reuse when possible. Measure ROI.

4. **Tools are power.** When Claude can call functions, it goes from answering questions to actually doing things.

5. **RAG is real.** Grounding Claude in your documents beats hoping it knows what you know.

6. **Agents are a tool, not a crutch.** Use them for exploration; use workflows for well-defined tasks.

7. **Evals are essential.** You can't improve what you don't measure.

---

## 📖 Resources

- [Anthropic API docs](https://docs.anthropic.com/)
- [Prompt engineering guide](https://docs.anthropic.com/claude/docs/how-to-use-claude)
- [API pricing calculator](https://www.anthropic.com/pricing)
- Course notebooks: `notebooks/01_*.ipynb` through `notebooks/08_*.ipynb`

---

**Happy building! 🚀**
