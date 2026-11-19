<div align="center">

# LangChain Projects

**A collection of practical AI applications built with LangChain**

[![Open in Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/Prktriesitout/Langchain_Projects)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?logo=python&logoColor=white)](#-quick-start)
[![LangChain](https://img.shields.io/badge/Framework-LangChain-1C3C3C)](https://python.langchain.com/)
[![License](https://img.shields.io/badge/License-Not%20specified-lightgrey.svg)](#-license)

[Projects](#-project-gallery) · [Architecture](#-system-architecture) · [Quick Start](#-quick-start) · [Tech Stack](#-tech-stack)

</div>

---

## ✨ Overview

This repository explores real-world AI assistants using LangChain orchestration, prompt engineering, document retrieval, conversation memory, and LLM integrations.

```mermaid
flowchart LR
    U[User Input] --> P[Prompt / Few-Shot Template]
    P --> C[LangChain Chain]
    C --> L{LLM Provider}
    L -->|Hugging Face| HF[Open-Source Model]
    L -->|Cohere| CO[Cohere API]
    HF --> O[Structured Output]
    CO --> O
    D[PDF / Resume / Email] --> I[Input Processing]
    I --> C
    O --> R[Response & UI]

    style U fill:#2563eb,color:#fff
    style C fill:#10b981,color:#fff
    style L fill:#7c3aed,color:#fff
    style R fill:#f59e0b,color:#111
```

## 🧭 Project Gallery

| # | Project | Use Case | Core Technique | Open |
|---|---|---|---|---|
| 01 | **HR Resume Screener** | Compare candidate resumes with job descriptions and produce shortlist recommendations | Prompt templates, Hugging Face, structured output | [![Open Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](./Project1.ipynb) |
| 02 | **Research Paper Summarizer** | Transform PDF papers into Problem, Method, and Findings summaries | PDF loaders, text splitting, prompt chains, Gradio | [![Open Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](./Project2.ipynb) |
| 03 | **Financial Report Analyst** | Answer contextual questions across financial PDF reports | RAG, vector search, retrieval chains, conversation memory | [![Open Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](./Project3.ipynb) |
| 04 | **AI Interview Coach** | Evaluate answers and provide realistic, structured interview feedback | Few-shot prompting, role-aware coaching | [![Open Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](./Project4.ipynb) |
| 05 | **Email Tone Improver** | Rewrite abrupt or unprofessional drafts into polished emails | Few-shot prompting, prompt chains | [![Open Notebook](https://img.shields.io/badge/Notebook-Jupyter-orange?logo=jupyter)](./Project5.ipynb) |

---

## 🏗️ System Architecture

### 01 — Resume screening pipeline

```mermaid
flowchart LR
    A[Resume Text] --> C[Resume Screening Chain]
    B[Job Description] --> C
    C --> D[PromptTemplate]
    D --> E[Hugging Face LLM]
    E --> F[Text Parser]
    F --> G[Strengths / Skills / Recommendation]

    style C fill:#2563eb,color:#fff
    style G fill:#10b981,color:#fff
```

### 02 — PDF summarization pipeline

```mermaid
flowchart LR
    PDF[Research PDF] --> LOAD[PyPDFLoader]
    LOAD --> SPLIT[Text Processing]
    SPLIT --> PROMPT[Problem / Method / Findings Prompt]
    PROMPT --> LLM[Cohere LLM]
    LLM --> SUMMARY[Structured Summary]
    SUMMARY --> UI[Gradio Interface]

    style PDF fill:#ef4444,color:#fff
    style SUMMARY fill:#10b981,color:#fff
```

### 03 — RAG and memory pipeline

```mermaid
flowchart TD
    PDF[Financial Report PDF] --> LOAD[PyPDFLoader]
    LOAD --> SPLIT[Recursive Text Splitter]
    SPLIT --> EMB[Hugging Face Embeddings]
    EMB --> DB[(Chroma Vector Store)]

    Q[User Question] --> RETRIEVE[Similarity Retrieval]
    DB --> RETRIEVE
    RETRIEVE --> DOCS[Relevant Report Sections]
    DOCS --> CHAIN[Retrieval Chain]
    MEMORY[(In-Memory Chat History)] --> CHAIN
    Q --> CHAIN
    CHAIN --> ANSWER[Context-Aware Answer]

    style DB fill:#7c3aed,color:#fff
    style MEMORY fill:#f59e0b,color:#111
    style ANSWER fill:#10b981,color:#fff
```

### 04 — Interview coaching loop

```mermaid
sequenceDiagram
    actor Candidate
    participant Coach as Prompt + Few-Shot Chain
    participant LLM as Cohere / Hugging Face

    Candidate->>Coach: Job role + interview question
    Candidate->>Coach: Candidate response
    Coach->>LLM: Structured examples + dynamic prompt
    LLM-->>Coach: Analysis and feedback
    Coach-->>Candidate: Strengths, improvements, recommendation
    Candidate->>Coach: Revised answer
    Coach->>LLM: Re-evaluate
```

### 05 — Email rewriting pipeline

```mermaid
flowchart LR
    RAW[Raw Email Draft] --> TEMPLATE[Few-Shot Prompt]
    EXAMPLES[Polished Email Examples] --> TEMPLATE
    TEMPLATE --> LLM[Cohere / Hugging Face]
    LLM --> CLEAN[Professional Rewrite]
    CLEAN --> USER[Final Email]

    style RAW fill:#ef4444,color:#fff
    style CLEAN fill:#10b981,color:#fff
    style USER fill:#2563eb,color:#fff
```

---

## 🚀 Quick Start

### 1. Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
# .venv\Scripts\activate         # Windows
```

### 2. Install notebook dependencies

```bash
pip install -U notebook
pip install -U langchain langchain-core langchain-community langchain-huggingface
pip install -U langchain-cohere langchain-chroma langchain-text-splitters
pip install -U transformers huggingface_hub accelerate pypdf gradio rich
```

### 3. Configure API credentials

Choose the credentials required by the notebook you run:

```bash
export HUGGINGFACEHUB_API_TOKEN="your_hugging_face_token"
export COHERE_API_KEY="your_cohere_api_key"
```

> When using Google Colab, store these values in **Colab Secrets** rather than placing keys directly in notebook code.

### 4. Launch Jupyter

```bash
jupyter notebook
```

Open any project from the table above and run the cells in order.

### ☁️ Run in Google Colab

Each notebook includes a Colab badge. Alternatively, use this link format:

```text
https://colab.research.google.com/github/Prktriesitout/Langchain_Projects/blob/main/Project1.ipynb
```

Replace `Project1.ipynb` with the notebook you want to run.

---

## 🧰 Tech Stack

| Category | Tools |
|---|---|
| **Orchestration** | LangChain, LangChain Core, LangChain Classic |
| **Models** | Hugging Face, Cohere |
| **Prompting** | PromptTemplate, FewShotPromptTemplate |
| **Document Processing** | PyPDFLoader, RecursiveCharacterTextSplitter |
| **Retrieval** | Hugging Face Embeddings, Chroma vector store |
| **Memory** | InMemoryChatMessageHistory |
| **Output** | StrOutputParser, structured prompt formats |
| **Interfaces** | Jupyter Notebook, Google Colab, Gradio |
| **Utilities** | Transformers, Accelerate, Rich |

---

## 🔐 Environment Variables

| Variable | Used for |
|---|---|
| `HUGGINGFACEHUB_API_TOKEN` | Hugging Face model and endpoint access |
| `COHERE_API_KEY` | Cohere chat model access |

Never commit API keys or secrets to notebooks or Git.

## 🗂️ Repository Layout

```text
Langchain_Projects/
├── README.md
├── Project1.ipynb   # HR resume screening assistant
├── Project2.ipynb   # PDF research paper summarizer
├── Project3.ipynb   # Financial report RAG analyst
├── Project4.ipynb   # AI interview coach
└── Project5.ipynb   # Email tone improver
```

## 🤝 Contributing

Contributions are welcome. Good starting points include:

- Migrating notebooks into reusable Python modules
- Adding automated tests for prompt and chain outputs
- Introducing streaming and configurable model providers
- Building unified Gradio or Streamlit interfaces
- Comparing open-source and hosted embedding models

## 📄 License

Add a license file to define how others may use, modify, and distribute this project.
