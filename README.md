# Doc Chat AI

## Overview

Doc Chat AI is a document-grounded assistant that pairs a Streamlit chat interface with a FastAPI backend. Upload one or more Docs(currently supports PDFs; future versions will support multiple file formats through expanded ingestion functions), let the service index them with retrieval-augmented generation (RAG), and ask questions that are answered with citations drawn from your own files. The separation between UI and API keeps the solution easy to deploy, scale, and extend with additional actors, tools, or model providers.

---
## Ui

![architecture](https://raw.githubusercontent.com/kommineniamrutha111-cloud/Doc_ChatAI/refs/heads/main/PROJ_IMAGES/ui.png)

## Features

- Upload and index multiple Docs, then query them via chat.
- Switch between Groq and Gemini models while reusing the same vector store.
- Token-based chunking for high-quality context windows.
- Built-in vector store inspector for transparency and debugging.
- Downloadable chat history with full metadata.
- Streamlit frontend communicating with a clean REST API layer in FastAPI.

---

## 🏗️ Architecture
![architecture](https://raw.githubusercontent.com/kommineniamrutha111-cloud/Doc_ChatAI/refs/heads/main/PROJ_IMAGES/Mermaid%20Chart.png)

---

## Tech Stack

- **Frontend:** Streamlit
- **Backend:** FastAPI
- **LLM Providers:** Groq (via `langchain-groq`) and Google Gemini (via `langchain-google-genai`)
- **Embeddings:** HuggingFace Transformers & Google Generative AI
- **Vector Store:** ChromaDB
- **Document Parsing:** PyPDF
- **Orchestration:** LangChain (core, community, classic modules)

---

## Prerequisites

- Python 3.11 (recommended)
- Groq API key – [console.groq.com](https://console.groq.com/)
- Google Gemini API key – [ai.google.dev](https://ai.google.dev/)

---

## Installation

```bash
git clone https://github.com/kommineniamrutha111-cloud/Doc_ChatAI.git
cd Doc_ChatAI
```

Create and activate a virtual environment:

```bash
python -m venv venv
# macOS/Linux
source venv/bin/activate
# Windows PowerShell
.\venv\Scripts\Activate.ps1
```

Install backend dependencies :

```bash
cd server
pip install -r requirements.txt
```

Install frontend dependencies:

```bash
cd ../client
pip install -r requirements.txt
```

---

## Configuration

Create a `.env` file inside `server/` with your keys:

```env
GROQ_API_KEY=your-groq-key
GOOGLE_API_KEY=your-google-key
```

Optional environment variables (see `server/config/settings.py`) can override model defaults and vector store locations.

---

## Running Locally

Start the FastAPI backend:

```bash
# From the project root
cd server
uvicorn main:app --reload
```

Start the Streamlit frontend in a second terminal:

```bash
cd client
streamlit run app.py
```

Access the UI at `http://localhost:8501` and the API at `http://localhost:8000`.

---

## Project Structure

```text
Doc-Chat-fastapi/
├── client/                     # Streamlit frontend
│   ├── app.py                  # Streamlit entrypoint
│   ├── components/             # UI components
│   ├── state/                  # Session state management
│   ├── utils/                  # API client helpers
│   └── requirements.txt
├── server/                     # FastAPI backend
│   ├── api/                    # API routes & schemas
│   ├── config/                 # Settings & environment
│   ├── core/                   # Document, LLM, and vector-store logic
│   ├── utils/                  # Logging helpers
│   ├── main.py                 # FastAPI app
│   └── requirements.txt
├── assets/                     # GIFs and static assets
└── README.md                   # Project documentation
```

---

## UI Highlights

| View       | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| Chat       | Conversational interface with PDF-aware answers and chat history download. |
| Inspector  | Tools to inspect stored vectors and debug retrieval quality.               |

![UI Demo](/assets/rag-bot-fastapi.gif)

---

## Tools Panel (Streamlit)

| Button      | Purpose                                        |
|-------------|------------------------------------------------|
| Reset       | Clears the session state and restarts the app. |
| Clear Chat  | Removes chat history and uploaded documents.   |
| Undo        | Deletes the most recent Q&A pair.              |

---

## Chat History Export

Chat transcripts are stored in Streamlit session state and can be downloaded as CSV with columns: `question`, `answer`, `model_provider`, `model_name`, `pdf_files`, and `timestamp`. This makes it easy to audit responses or share conversations.

---
