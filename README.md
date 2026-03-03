# Regulatory Analysis Workbench (Compliance Copilot)

This project started as a personal experiment: I wanted a simple way to work with large regulatory PDFs using a language model, while keeping full control over privacy and system behavior.

The result is a prototype that explores Agentic RAG and hybrid retrieval techniques in the context of regulatory and compliance analysis. It is not intended as a finished product, but as a technical exploration of how structured retrieval, tool use, and transparent reasoning can be combined to analyze complex legal texts such as DORA or MiCA.

The system focuses on traceability, structured document understanding, and reproducible analysis rather than marketing-style “AI automation”.

## Live Demo

You can try the current cloud demo here:

http://34.23.110.197:8501/

The demo is temporarily exposed via public IP.
DNS and HTTPS configuration are in progress.

The original privacy-first version (fully local, no external APIs) remains the main conceptual reference of the project.

## What This Prototype Explores

- Document ingestion for PDF and DOCX files, including rule-based chunking that preserves structural metadata such as article and chapter references.
- An agent loop that uses explicit tools to search, retrieve, and synthesize information instead of relying on a single prompt.
- Hybrid retrieval combining semantic search and keyword-based ranking to improve recall and precision.
- Structured citation extraction to link answers to specific articles, titles, and page references.
- Basic safeguards against repeated tool calls and malformed LLM outputs.
- A transparent workflow that exposes intermediate steps for inspection during development.

## Technical Stack & Techniques

- **Backend**: Python with FastAPI.
- **Frontend**: Streamlit.
- **Vector Store**: ChromaDB for persistent and scalable storage of document chunks and embeddings.
- **LLM access**: Local mode using an OpenAI-compatible endpoint (e.g., LM Studio). Cloud demo mode using external APIs (Groq and Hugging Face).
- **Embeddings**: Sentence-transformers multilingual models.
- **Retrieval**: Hybrid Search, Dense retrieval via embeddings plus Sparse retrieval (BM25) and Reciprocal Rank Fusion for result merging
- **Chunking Strategy**: Rule-based segmentation with metadata propagation (article/chapter tracking).
- **Tool Calling**: Native tool-use implementation for recursive search and context exploration.
- **Dependency** management: uv.
- **Containerization and deployment**: Docker and Docker Compose.
- **Cloud deployment (demo environment)**: Virtual machine on Google Cloud with CI/CD via GitHub Actions.

## Prerequisites

- **Python 3.12+** (managed with `uv`).
- **LM Studio** or any OpenAI-compatible server running locally on port `1234`.
- **Docker & Docker Compose** (for containerized deployment).

## Installation

```bash
# Clone the repository
git clone <repo-url>
cd Compliance_Copilot

# Install dependencies using uv
uv sync
```

## Execution

1. **Start the Backend**:
   ```bash
   uv run uvicorn app.main:app --reload --port 8000
   ```

2. **Start the UI**:
   ```bash
   uv run streamlit run ui/main.py
   ```

3. **Access the application**: Open your browser at `http://localhost:8501`.
