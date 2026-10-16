<div align="center">

# 🌱 Environmental Risk Assessment Assistant

### A Retrieval-Augmented Generation (RAG) project for wind and solar energy guidance

**Find relevant environmental guidance. Generate source-grounded answers. Keep references close to the evidence.**

<br/>

![Status](https://img.shields.io/badge/Project-In%20Progress-blue)
![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![RAG](https://img.shields.io/badge/AI-RAG-6A5ACD)
![Domain](https://img.shields.io/badge/Domain-Renewable%20Energy-2E8B57)

</div>

---

## 📌 Overview

The **Environmental Risk Assessment Assistant** is a RAG-based application being developed to help users explore public environmental guidance for **wind and solar energy projects**. It is designed to retrieve relevant passages from technical documents and use them to generate answers grounded in the available sources.

The planned interface will let users select a predefined question or enter a custom query, review potential environmental concerns and mitigation measures, and follow source references for further reading.

> **Project status:** Steps **1–3 are implemented**: document collection, document parsing, and text processing/chunking. Steps **4–11 are planned** and are listed under *Planned Implementation & Future Scope*. Update this status as the implementation progresses.

## 🧭 Workflow at a glance

```mermaid
flowchart TB
    SRC[("Public environmental guidance<br/>wind and solar")]

    subgraph ING["INGESTION PIPELINE - runs offline"]
        direction TB
        S1["1. Document collection<br/>Python, Requests"]
        S2["2. Document parsing<br/>PyMuPDF, BeautifulSoup"]
        S3["3. Text processing and chunking<br/>LangChain Text Splitters"]
        S4["4. Embedding generation<br/>Sentence Transformers"]
        S5[("5. Vector database<br/>ChromaDB")]
        S1 --> S2 --> S3 --> S4 --> S5
    end

    subgraph QRY["QUERY PIPELINE - runs for every question"]
        direction TB
        UQ["User question<br/>Streamlit"]
        S6["6. Query processing<br/>query embedding"]
        S7["7. Semantic retrieval<br/>top-k passages"]
        S8["8. Context assembly<br/>sources preserved"]
        S9["9. LLM answer generation<br/>provider to be selected"]
        S10["10. Response validation<br/>citation checks"]
        S11["11. Final response<br/>Streamlit"]
        UQ --> S6 --> S7 --> S8 --> S9 --> S10 --> S11
    end

    SRC --> S1
    S5 -->|knowledge base| S7

    classDef done fill:#d1fae5,stroke:#059669,stroke-width:2px,color:#064e3b
    classDef planned fill:#f3f4f6,stroke:#9ca3af,stroke-width:2px,color:#374151
    classDef source fill:#dbeafe,stroke:#2563eb,stroke-width:2px,color:#1e3a8a

    class S1,S2,S3 done
    class S4,S5,UQ,S6,S7,S8,S9,S10,S11 planned
    class SRC source
```

### Status legend

- 🟢 **Implemented (green):** Steps 1–3 — collection, parsing, and chunking.
- ⚪ **Planned (grey):** Steps 4–11 — embeddings, vector storage, query retrieval, LLM generation, validation, and UI.

---

## 🧱 Workflow details

### ✅ Implemented

#### 1. Document collection

**Tools:** Python, Requests

- Download selected public environmental guidance documents.
- Record document titles, source URLs, and publication dates where available.

#### 2. Document parsing

**Tools:** PyMuPDF, BeautifulSoup

- Extract text from PDFs and webpages.
- Preserve page numbers, section details, and source references where available.

#### 3. Text processing and chunking

**Tools:** LangChain Text Splitters, Python

- Clean extracted text.
- Split content into overlapping chunks for downstream retrieval.
- Attach metadata such as source, page, section, energy type, and publication date.

### 🚧 Planned implementation & future scope

#### 4. Embedding generation

**Tool:** Sentence Transformers

- Convert document chunks into numerical vectors using a consistent embedding model.

#### 5. Vector database

**Tool:** ChromaDB

- Store chunks, embeddings, and metadata.
- Persist the searchable knowledge base.

#### 6. Query processing

**Tools:** Streamlit, LangChain, Sentence Transformers

- Let users choose a predefined question or enter a custom one.
- Prepare the query and generate its embedding.
- Identify or select the relevant wind/solar category.

#### 7. Semantic retrieval

**Tools:** ChromaDB, LangChain Retriever

- Search stored embeddings.
- Apply relevant metadata filters.
- Retrieve the top-k matching passages with source references.

#### 8. Context assembly

**Tool:** LangChain

- Combine retrieved passages and the user question.
- Preserve source identifiers and construct an evidence-focused prompt.

#### 9. LLM answer generation

**Tool:** LLM API — provider to be selected

- Summarise environmental concerns and potential impacts.
- Suggest mitigation measures supported by retrieved evidence.
- Acknowledge when the available sources do not provide enough information.

#### 10. Response validation

**Tools:** Python, LangChain

- Check that cited source identifiers refer to retrieved documents.
- Flag missing evidence or invalid source references.

#### 11. Final user response

**Tool:** Streamlit

Present a structured response with:

- Environmental concerns
- Potential impacts
- Potential mitigation measures
- Missing or insufficient information
- Source citations and links

---

## 🛠️ Technology stack

| Area | Tools |
|---|---|
| Document collection | Python, Requests |
| PDF and web parsing | PyMuPDF, BeautifulSoup |
| Text processing | Python, LangChain Text Splitters |
| Embeddings *(planned)* | Sentence Transformers |
| Vector database *(planned)* | ChromaDB |
| Retrieval *(planned)* | LangChain Retriever |
| LLM *(planned)* | Provider to be selected |
| User interface *(planned)* | Streamlit |

## 🎯 Intended outcome

The goal is to make public environmental guidance easier to search and interpret for preliminary wind and solar project risk assessment. The assistant is intended to support exploration and early-stage analysis, **not replace formal environmental impact assessments, qualified expert judgement, or regulatory advice**.

## 🗺️ Next milestones

1. Generate embeddings for the processed chunks.
2. Store embeddings, chunk text, and metadata in ChromaDB.
3. Implement retrieval and inspect the relevance of returned passages.
4. Connect an LLM and generate answers grounded in retrieved sources.
5. Add citation checks and insufficient-evidence handling.
6. Build the Streamlit interface and evaluate the end-to-end workflow.

---

<div align="center">

**Built with Python · Focused on evidence-grounded AI for renewable energy**

</div>
