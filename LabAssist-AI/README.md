# LabAssist AI

### RAG-Based OOPS Lab Guide Chatbot

LabAssist AI is a locally running AI-powered academic chatbot designed to help students understand C++ and Object-Oriented Programming (OOPS).

It uses Retrieval-Augmented Generation (RAG), prompt engineering, local language models and a vector database to generate answers based on uploaded study materials.

---

## 1. Project Objectives

- Provide a chatbot for learning C++ and OOPS concepts.
- Retrieve relevant information from PDF and TXT study notes.
- Generate answers using prompt-engineered instructions.
- Provide different answer styles for different learning needs.
- Display the source filename and page number used for answers.
- Run locally without depending on paid AI APIs.

## 2. Main Features

### RAG-Based Question Answering

- Extracts text from PDF and TXT files.
- Splits documents into smaller chunks.
- Converts chunks into vector embeddings.
- Stores embeddings in ChromaDB.
- Retrieves relevant information for student questions.
- Uses retrieved context to generate answers.

### Five Response Modes

| Mode     | Purpose                                |
| -------- | -------------------------------------- |
| Simple   | Easy-to-understand explanations        |
| Exam     | Structured exam-oriented answers       |
| Lab      | Practical and programming explanations |
| Viva     | Concise oral examination answers       |
| Detailed | In-depth explanations                  |

### Additional Features

- Suggested questions.
- Source filename and page references.
- Relevance filtering.
- Markdown-formatted answers.
- Local AI processing.
- New conversation option.
- Backend connection indicator.
- Knowledge-base file listing.
- Responsive React interface.

## 3. Technologies Used

### Frontend

- React.js
- Vite
- JavaScript
- HTML
- CSS
- React Markdown
- Remark GFM

### Backend

- Python
- FastAPI
- LangChain
- PyPDF
- Uvicorn

### AI and RAG

- Ollama
- Qwen 2.5 3B (language model)
- Nomic Embed Text (embedding model)
- ChromaDB (vector database)

## 4. System Architecture

```text
          STUDENT
             |
             v
       REACT FRONTEND
             |
             v
        FASTAPI BACKEND
             |
             v
       STUDENT QUESTION
             |
             v
       QUERY EMBEDDING
             |
             v
       CHROMADB SEARCH
             |
             v
     RELEVANT DOCUMENT CHUNKS
             |
             v
      PROMPT CONSTRUCTION
             |
             v
       OLLAMA LLM
             |
             v
       GENERATED ANSWER
             |
             v
      SOURCE REFERENCES
             |
             v
       REACT FRONTEND
```

## 5. Project Folder Structure

```text
LabAssist-AI/
|
|-- backend/
|   |-- app/
|   |   |-- main.py
|   |   |-- config.py
|   |   |-- pdf_processor.py
|   |   |-- embeddings.py
|   |   |-- rag.py
|   |   |-- prompts.py
|   |
|   |-- uploads/
|   |-- chroma_db/
|   |-- ingest.py
|   |-- requirements.txt
|
|-- frontend/
|   |-- src/
|   |   |-- App.jsx
|   |   |-- App.css
|   |   |-- index.css
|   |
|   |-- package.json
|   |-- package-lock.json
|
|-- .gitignore
|-- README.md
```

## 6. Installation Requirements

Install the following software:

1. Python 3.12
2. Node.js and npm
3. Visual Studio Code
4. Ollama

Download Ollama:
https://ollama.com/download

Install the required local models:

```bash
ollama pull qwen2.5:3b
ollama pull nomic-embed-text
```

## 7. Backend Setup

Open a terminal in the main project folder.

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it in Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install backend dependencies:

```bash
pip install -r backend/requirements.txt
```

## 8. Document Ingestion

Place your OOPS PDF or TXT notes inside:

```text
backend/uploads/
```

From the main project directory, run:

```bash
python -m backend.ingest
```

This processes the documents, creates chunks, generates embeddings and stores them in the local ChromaDB database.

Run ingestion again whenever you add or replace study notes.

## 9. Start the Backend

From the main project directory:

```bash
python -m uvicorn backend.app.main:app --reload --reload-dir backend/app
```

Backend address:

http://127.0.0.1:8000

API documentation:

http://127.0.0.1:8000/docs

Health check:

http://127.0.0.1:8000/health

## 10. Frontend Setup

Open a second terminal:

```powershell
cd frontend
npm install
```

Start the React application:

```bash
npm run dev
```

Open the local website:

http://localhost:5173/

## 11. Testing

Test the following:

1. Ask a question about the four pillars of OOP.
2. Ask a question about inheritance.
3. Test all five response modes.
4. Ask an unrelated question to verify relevance filtering.
5. Verify source filenames and page numbers.
6. Check the backend connection indicator.
7. Test the suggested questions and New Conversation button.

## 12. How RAG Works in This Project

RAG stands for Retrieval-Augmented Generation.

It combines information retrieval with language generation.

The project follows these stages:

1. Document loading: reads PDF and TXT notes.
2. Text extraction: extracts readable text.
3. Chunking: splits text into smaller sections.
4. Embedding: converts text into numerical vectors.
5. Storage: stores vectors in ChromaDB.
6. Retrieval: finds relevant chunks for a question.
7. Prompt engineering: combines the question, retrieved context and response instructions.
8. Generation: Ollama generates an answer.
9. Response: the frontend displays the answer and available source references.

## 13. Data Storage

The project uses local ChromaDB storage.

Database location:

```text
backend/chroma_db/
```

Uploaded study materials:

```text
backend/uploads/
```

The language model and embedding model run locally through Ollama.

## 14. Limitations

- Answers depend on the quality and coverage of uploaded notes.
- Scanned PDFs may require OCR if they do not contain extractable text.
- Local model speed depends on available system resources.
- Similarity thresholds may need adjustment for different study materials.
- Source references identify retrieved documents but do not independently guarantee that every generated statement is supported.

## 15. Future Scope

- Add more engineering subjects.
- Support additional document formats.
- Add OCR for scanned notes.
- Improve retrieval accuracy.
- Add conversation history persistence.
- Add an optional knowledge graph module.
- Add student progress and quiz features.

## 16. Conclusion

LabAssist AI demonstrates how Retrieval-Augmented Generation and prompt engineering can be combined to create a subject-specific educational chatbot.

By using local language models, embeddings and vector storage, the project provides a private, locally running study assistant that generates answers using indexed academic materials.
