# Anthropic API Course — Complete Summary

## 🎓 What You've Learned

This 8-phase course teaches you to build production systems with Claude. You've learned:

| Phase | Topic | Core Skill | Example Output |
|-------|-------|-----------|-----------------|
| 1 | API Basics | Initialize client, make requests | "Hello Claude!" |
| 2 | Conversations | Maintain state across turns | Chatbot loop |
| 3 | Structured Output | Extract clean JSON | `{"name": "...", "age": ...}` |
| 4 | Evals | Measure prompt quality | "Prompt v2 scores 8.5/10" |
| 5 | Tool Use | Claude calls your functions | Reminder bot (3 tools chained) |
| 6 | Caching | Reduce costs by 90% | Cached system prompt saves 10¢/call |
| 7 | RAG | Ground in your documents | Q&A bot over product docs |
| 8 | Agents | Autonomous problem solving | Research agent loops until confident |

---

## 🚀 You Can Now Build

✅ **Stateless services:** One-shot requests, translations, classifications
✅ **Chatbots:** Multi-turn conversations with memory
✅ **Data pipelines:** Extract structured data from text
✅ **Integrations:** Claude calling your APIs, databases, external tools
✅ **Document Q&A:** Search your own knowledge bases
✅ **Agentic systems:** Complex problem solving with tool chains
✅ **Cost-optimized systems:** Intelligent caching for high-volume workloads
✅ **Measurable systems:** Data-driven prompt optimization

---

## 📂 Files You've Created

```
anthropic-api-course/
├── README.md                    # Course overview
├── QUICK_START.md               # 5-minute setup
├── LEARNING_PATH.md             # Complete learning guide + decision trees
├── COURSE_SUMMARY.md            # This file
├── requirements.txt             # Python dependencies
├── .env.example                 # Template for API key storage
└── notebooks/
    ├── 01_first_request.ipynb   # SDK setup, basic API call
    ├── 02_chatbot.ipynb          # Multi-turn conversations
    ├── 03_structured_output.ipynb # Prefill, stop sequences, JSON extraction
    ├── 04_evals.ipynb            # Eval pipelines, prompt testing
    ├── 05_tool_use.ipynb         # Reminder bot, tool schemas, tool chaining
    ├── 06_prompt_caching.ipynb   # Cost optimization, cache_control
    ├── 07_rag.ipynb              # Chunking, embedding, retrieval, Q&A
    └── 08_workflows_vs_agents.ipynb # Research agent, autonomous loops
```

---

## 🎯 Key Patterns (Cheat Sheet)

### Single-Turn Request
```python
response = client.messages.create(
    model="claude-sonnet-4-5",
    max_tokens=1000,
    messages=[{"role": "user", "content": "..."}]
)
print(response.content[0].text)
```

### Multi-Turn Conversation
```python
messages = [{"role": "user", "content": "First question"}]
# Add system prompt to guide behavior
response = client.messages.create(
    model=model,
    max_tokens=1000,
    system="You are a helpful assistant.",
    messages=messages
)
messages.append({"role": "assistant", "content": response.content[0].text})
# Continue looping, appending each turn
```

### Structured JSON Output
```python
response = client.messages.create(
    model=model,
    max_tokens=500,
    messages=[
        {"role": "user", "content": "Extract name, age as JSON"},
        {"role": "assistant", "content": "```json\n"}  # Prefill
    ],
    stop_sequences=["```"]  # Stop at closing fence
)
data = json.loads(response.content[0].text)
```

### Tool Use Loop
```python
messages = [{"role": "user", "content": "Set a reminder..."}]
while True:
    response = client.messages.create(
        model=model, tools=tools, messages=messages
    )
    if response.stop_reason != "tool_use":
        break  # Done
    
    messages.append({"role": "assistant", "content": response.content})
    tool_results = run_tools(response)
    messages.append({"role": "user", "content": tool_results})
```

### Prompt Caching
```python
response = client.messages.create(
    model=model,
    system=[{
        "type": "text",
        "text": BIG_SYSTEM_PROMPT,
        "cache_control": {"type": "ephemeral"}  # Cache this
    }],
    messages=messages
)
# First call: expensive (cache write)
# Second+ calls: cheap (cache read ~10% cost)
```

### RAG (Document Q&A)
```python
# 1. Chunk documents
chunks = chunk_documents(my_documents)

# 2. Embed (use real embeddings in production)
for chunk in chunks:
    chunk["embedding"] = embed(chunk["text"])

# 3. Retrieve on user query
relevant = retrieve(user_query, chunks, top_k=3)

# 4. Augment prompt
context = format_context(relevant)
system_prompt = f"Use this context:\n{context}"

# 5. Generate answer
response = client.messages.create(
    model=model,
    system=system_prompt,
    messages=[{"role": "user", "content": user_query}]
)
```

### Agent Loop
```python
messages = [{"role": "user", "content": goal}]
for iteration in range(max_iterations):
    response = client.messages.create(
        model=model,
        tools=tools,
        messages=messages
    )
    
    messages.append({"role": "assistant", "content": response.content})
    
    # Check for termination
    if "DONE" in response.content[0].text:
        break
    
    if response.stop_reason != "tool_use":
        break
    
    # Run tools and loop
    tool_results = run_tools(response)
    messages.append({"role": "user", "content": tool_results})
```

---

## 💡 Pro Tips

1. **Always use `.env`** — never hardcode API keys
2. **Log API usage** — track token consumption and cost
3. **Set reasonable `max_tokens`** — prevent runaway responses
4. **Use `temperature=0`** — for deterministic tasks (analysis, extraction)
5. **Use `temperature=0.7-1.0`** — for creative tasks (brainstorming, writing)
6. **Version your prompts** — treat them like code
7. **Measure quality** — use evals to compare prompt versions
8. **Cache aggressively** — if the same context repeats, cache it
9. **Handle errors gracefully** — network failures, rate limits, API changes
10. **Start small** — build on localhost, test thoroughly, then scale

---

## 📊 Token Economy (Reference)

| Task | Typical Tokens | Cost at $3/$15 per 1M |
|------|----------------|----------------------|
| Simple question | 50-200 input, 50-100 output | ~$0.0003 |
| Data extraction | 200-500 input, 100-300 output | ~$0.001 |
| Multi-turn (10 turns) | 500-2000 input, 200-500 output | ~$0.005 |
| RAG query | 300-1500 input (context), 100-200 output | ~$0.002 |
| Eval (100 test cases) | 10,000+ input, 2000+ output | ~$0.05 |

*Numbers are rough estimates. Use the API pricing calculator for accuracy.*

---

## 🔄 When to Use Each Pattern

```
┌─ Need to call functions?
│  ├─ YES → Phase 5 (Tool Use)
│  │       └─ Claude decides which? → Phase 8 (Agent)
│  └─ NO → continue...
│
├─ Need to maintain conversation state?
│  ├─ YES → Phase 2 (Multi-turn)
│  └─ NO → Phase 1 (Single-turn)
│
├─ Need structured output?
│  ├─ YES → Phase 3 (Prefill + Stop)
│  └─ NO → continue...
│
├─ Grounding in your documents?
│  ├─ YES → Phase 7 (RAG)
│  └─ NO → continue...
│
└─ High API volume (>100 QPS)?
   ├─ YES → Phase 6 (Caching)
   └─ NO → done
```

---

## 🎬 Next Steps

1. **Run all 8 notebooks** — follow along, modify code, experiment
2. **Do the mini-exercises** — deepen your understanding
3. **Build a real project** — pick a use case (document Q&A, chatbot, data extraction)
4. **Measure quality** — create an eval dataset for your domain
5. **Deploy** — move from notebook to production (API server, scheduled jobs, etc.)
6. **Monitor** — track API costs, response times, error rates
7. **Iterate** — improve prompts, add features, optimize

---

## 📚 Resources

- **Anthropic Docs:** https://docs.anthropic.com/
- **API Pricing:** https://www.anthropic.com/pricing
- **Prompt Engineering Guide:** https://docs.anthropic.com/claude/docs/how-to-use-claude
- **Models Available:** Check the [Anthropic website](https://www.anthropic.com/) for latest models
- **Community:** Discuss on Twitter/X using #ClaudeAPI

---

## 🏁 Course Complete!

You've gone from "Hello Claude" to building production systems with:
- ✅ Multi-turn conversations
- ✅ Structured output extraction
- ✅ Tool-based integrations
- ✅ Cost optimization
- ✅ Document grounding (RAG)
- ✅ Autonomous agents

**The rest is iteration, measurement, and shipping.** Good luck! 🚀

---

**Questions?** Review [LEARNING_PATH.md](LEARNING_PATH.md) for deeper explanations and decision trees.

**Ready to start?** Follow [QUICK_START.md](QUICK_START.md) to set up and run Phase 1.
