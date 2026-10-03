# GenAI Engineering Journey 🚀

My hands-on notes, notebooks and projects from the **Coding Shuttle Generative AI course**, written from the point of view of a Java developer learning to build production AI systems in Python.

The course runs for 10 weeks, from Python and LLM basics through RAG, agents, evals, MCP and fine-tuning, and finishes with a capstone demo day on **Nov 28–29**.

---

## 📅 Course Roadmap & Progress

| Week | Topic | Status | Folder |
|------|-------|--------|--------|
| Pre | Python OOP refresher for Java developers | ✅ Done | [`00-python-oop-refresher/`](00-python-oop-refresher/) |
| 1 | **Python for AI & LLM fundamentals**: async APIs, streaming, transformer internals, LLM lifecycle | ✅ Done | [`01-python-for-ai/`](01-python-for-ai/) |
| 2 | **RAG foundations**: embeddings & vector geometry, vector DBs, indexing, chunking | 🟡 In progress | [`02-rag-foundations/`](02-rag-foundations/) |
| 3 | **Enterprise RAG**: hybrid search, cross-encoder re-ranking, query expansion, graph RAG | ⏳ Upcoming | `03-enterprise-rag/` |
| 4 | **Agents & state machines**: ReAct loop, reliable tool calling, LangGraph | ⏳ Upcoming | `04-agents-and-langgraph/` |
| 5 | **Evals**: golden datasets, LLM-as-judge, evaluating agents / RAG / tool calls | ⏳ Upcoming | `05-evals/` |
| 6 | **MCP & multi-agent orchestration**: context engineering, memory, orchestration patterns | ⏳ Upcoming | `06-mcp-and-multi-agent/` |
| 7 | **ML fundamentals & fine-tuning**: core math, LoRA / QLoRA, dataset engineering, quantization | ⏳ Upcoming | `07-ml-and-fine-tuning/` |
| 8 | **Agentic system design & reliability**: scaling, multi-agent topologies, AI security, fallbacks | ⏳ Upcoming | `08-agentic-system-design/` |
| 9 | **Multimodal AI** & capstone kickoff | ⏳ Upcoming | `09-multimodal-ai/` |
| 10 | **Capstone finale & demo day** (Nov 28–29) | ⏳ Upcoming | `10-capstone/` |

---

## 📂 Repository Structure

```
.
├── 00-python-oop-refresher/    # OOP in Python vs Java (notes + notebook)
├── 01-python-for-ai/           # Python for AI: day-wise learning notes, pandas, data loading
├── 02-rag-foundations/         # RAG foundations: vectors & embeddings
├── data/                       # Local datasets (git-ignored, download from Kaggle)
└── Modelfile.python            # Ollama "AI Coach" model (Qwen 2.5 Coder 14B)
```

---

## 🛠 Setup (macOS / Apple Silicon)

```bash
# Tools
brew install python git ollama

# Python environment
python3 -m venv .venv
source .venv/bin/activate
pip install jupyter numpy pandas
```

Use VS Code or PyCharm with the Python and Jupyter extensions.

### 🤖 Local AI Coach (Ollama)

[`Modelfile.python`](Modelfile.python) sets up **Qwen 2.5 Coder 14B** as a personal AI engineering coach. It answers in modern Python 3.12+ with strict type hints, uses Pydantic for validation, and always returns complete code.

```bash
# Make sure the Ollama daemon is running, then:
ollama create ai-coach -f ./Modelfile.python
ollama run ai-coach
```

### 🧠 Local LLM for RAG work (Ollama)

All RAG work in this repo runs on a local **DeepSeek-R1-Distill-Qwen-32B** model (Q3_K_M GGUF, ~16 GB) on a Mac mini M4 Pro with 24 GB of unified memory. It runs fully on the GPU at about 8 tokens/s.

```bash
# 1. Pull the model and give it a short local name
ollama pull hf.co/bartowski/DeepSeek-R1-Distill-Qwen-32B-GGUF:Q3_K_M
ollama cp hf.co/bartowski/DeepSeek-R1-Distill-Qwen-32B-GGUF:Q3_K_M deepseek-r1:32b-q3

# 2. Let the GPU use up to 18 GB of unified memory (resets on reboot, so re-run after restarting)
sudo sysctl iogpu.wired_limit_mb=18432

# 3. Lean KV cache for the Ollama menu-bar app, then quit and reopen the app
launchctl setenv OLLAMA_FLASH_ATTENTION 1
launchctl setenv OLLAMA_KV_CACHE_TYPE q8_0
launchctl setenv OLLAMA_CONTEXT_LENGTH 4096

# 4. Check it
ollama run deepseek-r1:32b-q3 --verbose
ollama ps   # PROCESSOR should show 100% GPU
```

Things to remember when using it in a RAG pipeline:

- **Strip the `<think>…</think>` block.** R1 prints its reasoning before the answer, so remove that block before showing or parsing the output.
- **Keep the retrieved context small.** The context window is 4096 tokens, so the top-k chunks plus the question must fit inside it.
- **Use a separate embedding model.** DeepSeek-R1 generates text and isn't meant for embeddings. Use a dedicated model such as `nomic-embed-text` (`ollama pull nomic-embed-text`) for the vector store.

---

## 📝 Notes

- **Datasets:** download them from [Kaggle](https://www.kaggle.com/) into `data/`. Data files are git-ignored.
- **Turning off inline suggestions in VS Code:** if an AI extension such as Twinny gets in the way, open Settings (`Cmd + ,`), search for `inlineSuggest.enabled` and uncheck it.

---

*Learning in public, one week at a time.* 🧠
