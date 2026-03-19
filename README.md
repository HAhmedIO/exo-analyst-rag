# Exo-Analyst: High-Precision RAG for Exoplanet Habitability

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![LLM: GPT-4o](https://img.shields.io/badge/LLM-GPT--4o-orange)](https://openai.com/)
[![Ragas Score](https://img.shields.io/badge/Ragas%20Faithfulness-0.89-green)](https://github.com/explodinggradients/ragas)

Exo-Analyst is a specialized **Retrieval-Augmented Generation (RAG)** system built to synthesize research on exoplanetary atmospheres and biosignatures. By combining structured planetary catalogs with unstructured scientific literature, this tool provides grounded, cited answers to complex astrophysical queries.

---

## 🌌 The Problem
Standard LLMs often struggle with:
1. **Hallucinations:** Inventing planetary stats or chemical detections.
2. **Knowledge Cutoffs:** Missing the latest JWST (James Webb Space Telescope) findings.
3. **Domain Jargon:** Misinterpreting LaTeX equations or technical spectroscopy terms.

**Exo-Analyst** solves this by forcing the model to retrieve context from a curated database of NASA records and peer-reviewed arXiv papers before answering.



---

## 🚀 Key Features
* **Hybrid Search (Vector + BM25):** Combines semantic understanding with keyword precision to handle specific identifiers like "K2-18b" or "LHS 1140 b."
* **Multi-Source Integration:** Bridges **structured data** (NASA Exoplanet Archive) and **unstructured data** (arXiv PDF research).
* **Late Reranking:** Uses Cohere’s Rerank-3 to filter the most relevant 5 chunks from a retrieved set of 20, improving answer precision.
* **Scientific Evaluation:** Built-in evaluation pipeline using the **Ragas** framework to measure Faithfulness and Answer Relevance.

---

## 📊 Performance Metrics
*Evaluated on a synthetic test set of 50 astrophysics-specific queries.*

| Metric | Score | Interpretation |
| :--- | :--- | :--- |
| **Faithfulness** | 0.89 | Answers are strictly derived from the retrieved papers. |
| **Answer Relevance** | 0.92 | Responses directly address the scientific nuances of the query. |
| **Context Precision** | 0.85 | The retriever successfully identifies the most relevant paper snippets. |

---

## 🛠️ Tech Stack
* **Orchestration:** LlamaIndex / LangChain
* **Vector Database:** Pinecone (Serverless)
* **Embeddings:** `text-embedding-3-small` (OpenAI)
* **Reranker:** `rerank-english-v3.0` (Cohere)
* **Parsing:** Unstructured.io (for LaTeX and Table extraction)

---

## 📁 Project Structure
```text
├── data/               # NASA CSV catalogs and ArXiv PDF samples
├── notebooks/          # EDA and RAG experimentation
├── src/
│   ├── ingestion.py    # Pipeline for PDF parsing & Vector DB indexing
│   ├── retriever.py    # Hybrid search & Reranking logic
│   └── app.py          # Streamlit UI for researchers
├── eval/               # Ragas evaluation scripts
└── requirements.txt