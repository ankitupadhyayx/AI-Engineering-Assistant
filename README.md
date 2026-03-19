# AI Engineering Assistant

Build, test, and demo Retrieval-Augmented Generation end-to-end on your laptop—no cloud calls, no API keys, and your documents never leave the machine.

---

## Why this exists

I wanted to learn RAG beyond glossy blog posts. The goal was to wire every stage manually: loading heterogeneous files, chunking, embedding, vector search, and prompting a local LLM. The result is a desktop assistant that answers questions using only the documents you drop into the project.

---

## Feature highlights

- Works entirely offline once the models are downloaded; great for prototypes with sensitive data.
- Accepts PDF, DOCX, and TXT sources and performs overlapping chunking for better recall.
- Creates dense embeddings with `all-MiniLM-L6-v2` and stores them inside a FAISS vector index.
- Answers come from Microsoft `phi-2`, loaded locally through Hugging Face Transformers.
- Ships with a Tkinter desktop chat UI that mimics the dark console aesthetic shown in the screenshots.

---

## Tech stack

| Layer | Tools |
| --- | --- |
| LLM | Microsoft Phi-2 (causal decoder) |
| Embeddings | Sentence Transformers – all-MiniLM-L6-v2 |
| Vector store | Facebook AI Similarity Search (FAISS) |
| UI | Tkinter desktop client |
| Glue | Python, Hugging Face Transformers, pdfplumber, python-docx |

---

## Pipeline overview

1. **Ingest** every file under `Documents/` (PDF, DOCX, TXT) and normalize text.
2. **Chunk** with overlap so answers can reference full thoughts instead of cut sentences.
3. **Embed** chunks via Sentence Transformers and persist the vectors into FAISS (`IndexFlatL2`).
4. **Retrieve** top-k matches for each question using semantic search.
5. **Prompt** Phi-2 with the retrieved context plus an instruction-tuned system prompt.
6. **Respond** inside the Tkinter chat window with cited snippets.

---

## Getting started

### Prerequisites

- Python 3.10+
- Git
- (Optional but recommended) a Hugging Face access token for faster/model downloads

### Setup

```bash
git clone https://github.com/ankitupadhyayx/AI-Engineering-Assistant.git
cd AI-Engineering-Assistant

python -m venv .venv
.\.venv\Scripts\activate            # PowerShell / cmd

pip install -r requirements.txt

# Authenticate once so Transformers can pull phi-2
.venv\Scripts\python.exe -m huggingface_hub.cli.hf auth login --token <HF_TOKEN>

# Drop your PDFs / DOCX / TXT files into the Documents/ folder
python assistant.py
```

When the GUI opens, type a natural-language question. The assistant will pull supporting context from your local files and respond using Phi-2.

---

## Project layout

```
AI-Engineering-Assistant/
├── assistant.py        # Main Tkinter app + RAG pipeline
├── requirements.txt    # Python dependencies
├── README.md           # You are here
└── Documents/          # Place your knowledge base files
```

---

## Roadmap

- [ ] FastAPI backend so the engine can power a web UI
- [ ] React dashboard for multi-document conversations
- [ ] Optional GPU acceleration toggle for embedding+LLM steps
- [ ] Eval harness to compare different retrieval strategies

---

## Share & feedback

If you tinker with the assistant, post your results or questions on LinkedIn (link in the project description) or open an issue here. Happy hacking!