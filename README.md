# HealthTalk — Medical Q&A Chatbot (LLMs + Vector Search)

An interactive medical assistant prototype that combines local LLM inference with a Pinecone vector index over medical documents. Built with Flask, LangChain, Hugging Face embeddings and CTransformers for the local model backend.

**Project Goal:** Showcase an end-to-end retrieval-augmented generation (RAG) system that answers medical questions by retrieving relevant passages from uploaded PDFs and using a local LLM to produce concise, contextual responses.

--

**Key Highlights**

- **Retrieval-first architecture:** Documents in `data/` are embedded and stored in a Pinecone index ([store_index.py](store_index.py)).
- **Embeddings:** Uses `sentence-transformers/all-MiniLM-L6-v2` via `HuggingFaceEmbeddings` (`src/helper.py`).
- **Local LLM inference:** `CTransformers` is configured in `app.py` to run a GGML-compatible model from `model/`.
- **Simple web UI:** Chat interface at `templates/chat.html` served by Flask (`app.py`).

**Useful files**

- [app.py](app.py) — Flask server and chat endpoints.
- [store_index.py](store_index.py) — Build Pinecone index from PDFs in `data/`.
- [src/helper.py](src/helper.py) — PDF loader, text splitter, and embeddings helper.
- [templates/chat.html](templates/chat.html) — Frontend chat UI.
- [static/style.css](static/style.css) — UI styles.
- [requirements.txt](requirements.txt) — Python dependencies.

--

**Quick Start (for recruiters / evaluators)**

1. Clone the repo and open the project root.

2. Create and activate a Python environment (Conda example):

```bash
conda create -n mchatbot python=3.8 -y
conda activate mchatbot
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

4. Set environment variables (create a `.env` file in the project root):

```text
PINECONE_API_KEY=your_pinecone_api_key
PINECONE_API_ENV=your_pinecone_env
```

5. Prepare the vector index from PDF documents (optional, required if you want the chatbot to use your own documents):

```bash
# Put PDFs under the data/ directory, then run:
python store_index.py
```

6. Run the Flask app:

```bash
python app.py
```

7. Open the chat UI in your browser: http://localhost:8080

--

**Notes for Evaluators / Recruiters**

- The app uses Pinecone for vector storage and requires `PINECONE_API_KEY` and `PINECONE_API_ENV`.
- Local LLM is loaded via `CTransformers` in `app.py`. Place your GGML model file at `model/llama-2-7b-chat.ggmlv3.q4_0.bin` (or update the path in `app.py`).
- Embedding model: `sentence-transformers/all-MiniLM-L6-v2` — downloaded automatically by LangChain's `HuggingFaceEmbeddings`.

**Security & Responsible Use**

- This prototype is intended for demonstration and research only — it is not a medical device. Responses should be validated by a qualified clinician before acting on medical advice.
- Never commit API keys or model binaries to version control.

--

**Development & Extensibility**

- Add more documents to `data/` (PDFs) and re-run `store_index.py` to refresh the index.
- Swap the local model path in `app.py` to experiment with different GGML models or remote LLM providers.
- To containerize, add a `Dockerfile` that installs system deps for `ctransformers` and copies the model artifacts.

--

**Author**

Project by Yatish Kumar — contact: yatishappy@gmail.com

If you'd like, I can also add a short demo GIF, sample interview bullet points highlighting your contributions, or a one-page PDF summary for recruiters.

**License**

See `LICENSE` for licensing details.