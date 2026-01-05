MediQuery – RAG-Based Medical Chatbot

**LLMs · LangChain · Pinecone · Flask · AWS · Gemini**

MediQuery is a **Retrieval-Augmented Generation (RAG) based medical knowledge chatbot** designed to answer medical queries using domain-specific documents.
The system grounds responses in retrieved medical text to **reduce hallucinations** and provide **educational, non-diagnostic explanations**.

> ⚠️ This application is for **educational purposes only** and does not provide medical diagnosis or treatment.


## 🧠 System Overview

The chatbot follows a **RAG pipeline**:

1. Medical PDFs are parsed and cleaned
2. Text is split into chunks
3. Chunks are converted into vector embeddings
4. Embeddings are stored in Pinecone
5. User queries retrieve relevant chunks
6. Google Gemini generates grounded responses using retrieved context

This design separates **retrieval** from **generation**, improving reliability and safety.

---

## 🏗️ Architecture (High Level)

```
PDFs → Text Extraction → Chunking → Embeddings
        ↓
     Pinecone (Vector DB)
        ↓
User Query → Retriever → Gemini LLM → Answer
```

---

## 🛠️ Tech Stack

* **Python**
* **LangChain**
* **Flask**
* **Google Gemini (LLM)**
* **Sentence-Transformers (Embeddings)**
* **Pinecone (Vector Database)**
* **Docker**
* **AWS (EC2, ECR)**
* **GitHub Actions (CI/CD)**

---

## 🚀 Running the Project Locally

### 1️⃣ Clone the repository

```bash
git clone https://github.com/Nidax23/MediQuery.git
cd MediQuery
```

---

### 2️⃣ Create and activate a Conda environment

```bash
conda create -n medibot python=3.10 -y
conda activate medibot
```

---

### 3️⃣ Install dependencies

```bash
pip install -r requirements.txt
```

---

### 4️⃣ Configure environment variables

Create a `.env` file in the root directory:

```ini
PINECONE_API_KEY=your_pinecone_api_key
GOOGLE_API_KEY=your_gemini_api_key
```

---

### 5️⃣ Store embeddings in Pinecone

```bash
python store_index.py
```

---

### 6️⃣ Run the application

```bash
python app.py
```

Open in browser:

```
http://localhost:8080
```

---

## ☁️ Deployment & CI/CD (High Level)

The project supports **containerized deployment** using AWS and GitHub Actions.

### Deployment flow:

1. Application is containerized using Docker
2. Docker image is pushed to Amazon ECR
3. EC2 instance pulls and runs the image
4. GitHub Actions automates build & push

> Detailed AWS and CI/CD setup is intentionally abstracted to keep the project readable and interview-focused.

---

## 🔐 Required GitHub Secrets

Configured in:

```
Repository → Settings → Secrets → Actions
```

```text
AWS_ACCESS_KEY_ID
AWS_SECRET_ACCESS_KEY
AWS_DEFAULT_REGION
ECR_REPO
PINECONE_API_KEY
GOOGLE_API_KEY
```

---

## 🛡️ Safety & Design Considerations

* Uses **RAG** to ground responses in verified documents
* Avoids diagnosis and prescriptions
* LLM is constrained via system prompts
* Designed to be **LLM-agnostic** (Gemini can be swapped)

---

## 🔮 Future Improvements

* Multi-document ingestion
* Advanced retrieval strategies (multi-query, ranking fusion)
* Improved UI/UX for chat interaction
* Medical report interpretation (non-diagnostic)

---
