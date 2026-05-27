# Quick Start Guide

Get up and running in 5 minutes.

## 1️⃣ Prerequisites

- Python 3.8+
- A text editor or Jupyter
- Your Anthropic API key (get one at [console.anthropic.com](https://console.anthropic.com/))

## 2️⃣ Clone & Setup

```bash
cd anthropic-api-course
cp .env.example .env
# Open .env and paste your real API key
nano .env  # (or use your editor)
```

Your `.env` should look like:
```
ANTHROPIC_API_KEY=sk-ant-your-key-here
```

## 3️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

If you don't have `requirements.txt`, create it:
```
anthropic
python-dotenv
jupyter
```

Then:
```bash
pip install -r requirements.txt
```

## 4️⃣ Start Jupyter

```bash
jupyter notebook
```

Open your browser to `http://localhost:8888` and navigate to `notebooks/`.

## 5️⃣ Run Phase 1

Open `notebooks/01_first_request.ipynb` and run each cell top-to-bottom.

You should see output like:
```
Hello! I'm Claude, made by Anthropic.
```

**Congratulations!** You've made your first API call.

---

## 📚 Next Steps

1. **Phase 2:** `02_chatbot.ipynb` — learn multi-turn conversations
2. **Phase 3:** `03_structured_output.ipynb` — extract clean JSON
3. Continue through Phase 8

**See [LEARNING_PATH.md](LEARNING_PATH.md)** for the full course outline and decision trees.

---

## 🔧 Troubleshooting

### `ModuleNotFoundError: No module named 'anthropic'`
→ You skipped the pip install step. Run: `pip install anthropic python-dotenv jupyter`

### `API key not found` or `401 Unauthorized`
→ Check `.env` file: make sure it's in the right directory and your key is pasted correctly (should start with `sk-ant-`)

### `ConnectionError`
→ Check your internet connection and that Anthropic API is accessible

### Jupyter won't open
→ Make sure port 8888 isn't in use. Try: `jupyter notebook --port 8889`

---

## 💡 Tips

- Run cells one at a time with `Shift+Enter`
- Look at `usage` dicts to understand token consumption
- Each phase builds on the previous — don't skip ahead
- Modify code and re-run to experiment
- The mini-exercises at the end of each phase are worth doing

---

Happy learning! 🚀
