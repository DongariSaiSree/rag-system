# rag-system
Production-grade RAG with hybrid search, reranking &amp; zero-hallucination
# 🔍 Advanced RAG System — Hybrid Search & Zero-Hallucination Architecture

A production-grade **Retrieval-Augmented Generation (RAG)** system that grounds LLM responses in real documents — with zero tolerance for hallucination.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![LangChain](https://img.shields.io/badge/LangChain-latest-green)
![OpenAI](https://img.shields.io/badge/OpenAI-API-orange?logo=openai)
![FastAPI](https://img.shields.io/badge/FastAPI-latest-teal)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 🧠 The Problem

Standard LLMs hallucinate. Ask one a question about your own document — it will make up an answer. Confidently. Convincingly. Completely wrong.

This system fixes that by grounding every response in retrieved document content, with citations you can verify.

---

## ✨ Features

- **Hybrid Search** — Dense embeddings (FAISS) + BM25 keyword matching fused via Reciprocal Rank Fusion
- **Cross-Encoder Reranking** — Scores every retrieved passage against your exact query for maximum precision
- **Citation-Backed Answers** — Every response references its source document chunk
- **Zero-Hallucination Enforcement** — If the answer isn't in the documents, the system says so
- **Multi-Format Support** — 11 file types: PDF, DOCX, TXT, Markdown, CSV, HTML, JSON, PNG, JPG, JPEG + image understanding via Gemini Vision API
- **Streamlit UI** — Clean interface for non-technical users

---

## 🏗️ Architecture

```
User Query
    │
    ▼
┌─────────────────────────────────┐
│         Hybrid Retrieval         │
│  FAISS (Dense) + BM25 (Sparse)  │
│   Fused via Reciprocal Rank     │
└─────────────┬───────────────────┘
              │
              ▼
┌─────────────────────────────────┐
│      Cross-Encoder Reranking    │
│  Scores passages vs exact query │
└─────────────┬───────────────────┘
              │
              ▼
┌─────────────────────────────────┐
│         LLM Generation          │
│  OpenAI API + Citation Grounding│
└─────────────┬───────────────────┘
              │
              ▼
     Citation-Backed Answer
     (or "I don't know")
```

---

## 🛠️ Tech Stack

| Component | Technology |
|---|---|
| Embeddings & Vector Store | FAISS |
| Keyword Search | BM25 |
| Reranking | Cross-Encoder (sentence-transformers) |
| LLM | OpenAI GPT-4 |
| Image Understanding | Gemini Vision API |
| Orchestration | LangChain |
| Backend API | FastAPI |
| Frontend | Streamlit |
| Language | Python 3.10+ |

---

## 📁 Project Structure

```
rag-system/
├── app/
│   ├── main.py              # FastAPI entry point
│   ├── retriever.py         # Hybrid search (FAISS + BM25)
│   ├── reranker.py          # Cross-encoder reranking
│   ├── generator.py         # LLM answer generation with citations
│   ├── ingestion.py         # Document loading & chunking (11 file types)
│   └── vision.py            # Gemini Vision API for image processing
├── ui/
│   └── streamlit_app.py     # Streamlit frontend
├── vector_store/            # FAISS index storage
├── tests/
│   └── test_retrieval.py    # Retrieval evaluation tests
├── requirements.txt
├── .env.example
└── README.md
```

---

## 🚀 Getting Started

```bash
# Clone the repo
git clone https://github.com/yourusername/rag-system.git
cd rag-system

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Add your OPENAI_API_KEY and GEMINI_API_KEY to .env

# Run the FastAPI backend
uvicorn app.main:app --reload

# Run the Streamlit UI (in a separate terminal)
streamlit run ui/streamlit_app.py
```

---

## 📊 Key Results

- ✅ Zero hallucination rate on grounded queries
- ✅ Supports 11 file types including image-based documents
- ✅ Hybrid retrieval outperforms pure dense or sparse search alone
- ✅ Cross-encoder reranking significantly improves answer precision

---

## 🔮 Future Improvements

- [ ] Add user authentication and document namespacing
- [ ] Support for multi-document comparison queries
- [ ] Fine-tuned reranker on domain-specific data
- [ ] Async batch ingestion for large document sets

---

## 📄 License

MIT License — feel free to use, modify, and build on this project.
