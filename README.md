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
├── Modelfile.python            # Ollama "AI Coach" model (Qwen 2.5 Coder 14B)
└── codestral-java-lead.Modelfile  # Ollama Codestral model tuned as a Java lead
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

---

## 📝 Notes

- **Datasets:** download them from [Kaggle](https://www.kaggle.com/) into `data/`. Data files are git-ignored.
- **Turning off inline suggestions in VS Code:** if an AI extension such as Twinny gets in the way, open Settings (`Cmd + ,`), search for `inlineSuggest.enabled` and uncheck it.

---

*Learning in public, one week at a time.* 🧠
