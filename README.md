<div align="center">

# rag course assistant

**upload your notes, ask questions, study from evidence**

<img alt="Python 3.11" src="https://img.shields.io/badge/Python%203.11-b6c4ff?style=flat-square&labelColor=1e1f25&logo=python&logoColor=e3e1e9"> <img alt="Qwen2.5 1.5B" src="https://img.shields.io/badge/Qwen2.5%201.5B-dce1ff?style=flat-square&labelColor=1e1f25&logo=huggingface&logoColor=e3e1e9"> <img alt="FAISS + BM25" src="https://img.shields.io/badge/FAISS%20%2B%20BM25-c6c6d0?style=flat-square&labelColor=1e1f25"> <img alt="FastAPI" src="https://img.shields.io/badge/FastAPI-b6c4ff?style=flat-square&labelColor=1e1f25&logo=fastapi&logoColor=e3e1e9"> <img alt="Gradio" src="https://img.shields.io/badge/Gradio%205-dce1ff?style=flat-square&labelColor=1e1f25&logo=gradio&logoColor=e3e1e9">

```text
course files → semantic chunks → FAISS + BM25 → reranking → cited answer
```

</div>

## What's in it

- answers only from your course material, with page, module, chapter and topic citations
- refuses questions outside the course instead of guessing
- hybrid retrieval: dense vectors, BM25 and a cross-encoder reranker
- course notes and the official question bank are searched separately
- reads PDFs, slides, Word documents, Markdown and plain text
- runs Qwen2.5 1.5B in 4-bit, so a consumer GPU is enough
- a Gradio study workspace with short per-chat memory

## Install

```bash
git clone https://github.com/ahadarshx/rag-course-assistant.git
cd rag-course-assistant
python3.11 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

On Windows, activate with `.\.venv\Scripts\Activate.ps1`.

## Run

```bash
uvicorn backend.api:app --port 8000     # the API
python frontend/gradio_app.py           # the app, in a second terminal
```

Open `http://127.0.0.1:7860`, upload your notes and click **Upload & index**.

## Configure

Copy `.env.example` to `.env`:

| | |
|---|---|
| `MODEL_NAME` | `Qwen/Qwen2.5-1.5B-Instruct` |
| `DEVICE` | `auto` |
| `STRICT_EXTRACTIVE` | `true` for verbatim passages instead of summaries |
| `CONFIDENCE_THRESHOLD` | `0.35`, below this it refuses |
| `HISTORY_TURNS` | `6` |

## Layout

| | |
|---|---|
| `backend/` | API, ingestion, retrieval, generation |
| `frontend/` | the Gradio study app |
| `evaluation/` | golden-set evaluation, run `python evaluation/evaluate.py evaluation/golden.example.json` |
| `tests/` | `pytest` |

<sub>Qwen2.5 · FAISS · rank-bm25 · sentence-transformers · FastAPI · Gradio</sub>
