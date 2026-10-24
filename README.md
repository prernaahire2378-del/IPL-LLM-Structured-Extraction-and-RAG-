# IPL LLM Structured Extraction and RAG Pipeline

## Project Overview

This project demonstrates a complete **Large Language Model (LLM)** application using the **Google Gemini API** to perform **structured information extraction** from IPL match descriptions and a **Retrieval-Augmented Generation (RAG)** pipeline for answering IPL-related questions.

The project covers the complete workflow from extracting structured data using an LLM, validating it using **Pydantic**, storing the extracted results in JSON format, and building a mini RAG system using **Sentence Transformers** and **FAISS** for semantic search.

This project satisfies the assignment requirements for:

- Structured information extraction
- Schema validation
- Validation failure handling
- JSON output generation
- Retrieval-Augmented Generation (RAG)
- Semantic document retrieval
- Question answering

---

# Objectives

The objectives of this project are:

- Extract structured IPL match information from natural language.
- Validate the extracted data using a predefined Pydantic schema.
- Demonstrate schema validation failures.
- Save validated outputs as JSON.
- Build a Retrieval-Augmented Generation (RAG) pipeline.
- Generate embeddings for IPL documents.
- Perform semantic similarity search using FAISS.
- Retrieve relevant documents to answer IPL-related questions.

---

# Dataset

This project uses IPL match-related text created from historical IPL match information.

The dataset includes match descriptions containing:

- Teams
- Venue
- Winning team
- Match result
- Match summary

A minimum of **15 IPL match records** were processed for structured extraction.

---

# Technologies Used

- Python
- Google Colab
- Google Gemini API
- Pydantic
- LangChain Text Splitters
- Sentence Transformers
- FAISS
- NumPy
- JSON

---

# Project Workflow

## Part 1: Structured Information Extraction

The project uses **Google Gemini** to extract structured information from IPL match descriptions.

Example input:

> Mumbai Indians defeated Chennai Super Kings by 5 wickets at Wankhede Stadium.

The extracted fields include:

- Teams
- Venue
- Winner
- Result
- Match Summary

---

# Pydantic Schema Validation

The extracted responses are validated using a **Pydantic** schema.

Schema fields include:

- teams
- venue
- winner
- result
- summary

Only responses matching the schema are accepted.

---

# Validation Failure Demonstration

The project also demonstrates schema validation failure by intentionally passing an invalid field.

Example:

```python
unexpected_field="This field should not be allowed"
```

Output:

```
ValidationError
Extra inputs are not permitted
```

This demonstrates that invalid fields are rejected successfully.

---

# JSON Output

All validated records are stored in:

```
structured_results.json
```

The JSON file contains structured IPL match information extracted by the Gemini model.

---

# Part 2: Retrieval-Augmented Generation (RAG)

A mini RAG pipeline is implemented using IPL documents.

The workflow includes:

- Creating IPL documents
- Text chunking
- Embedding generation
- FAISS vector database creation
- Semantic retrieval
- Question answering

---

# Text Chunking

Documents are split into smaller chunks using:

```
RecursiveCharacterTextSplitter
```

This improves retrieval quality by creating searchable text segments.

---

# Embedding Generation

Embeddings are generated using:

```
SentenceTransformer
```

Model used:

```
all-MiniLM-L6-v2
```

The embedding vectors represent semantic meaning of IPL documents.

---

# Vector Database

The project stores document embeddings inside a **FAISS vector database**.

FAISS enables fast similarity search for retrieving the most relevant IPL documents.

---

# Retrieval Process

For every user query:

1. Convert query into embedding.
2. Search FAISS vector database.
3. Retrieve most similar chunks.
4. Return retrieved information as the answer.

---

# Example Queries

Example questions used in the project:

- Who defeated Chennai Super Kings?
- Which player scored a century?
- Who won by 7 wickets?
- Which team won by 25 runs?
- Who captained Gujarat Titans?

The retrieved document chunks are used to answer these questions.

---

# Project Structure

```
IPL-LLM-Structured-Extraction-and-RAG/

│── IPL_LLM_Structured_Extraction_and_RAG.ipynb
│── structured_results.json
│── requirements.txt
│── README.md
│── .gitignore
```

---

# Installation

Clone the repository:

```bash
git clone <your-github-repository-link>
```

Install the required libraries:

```bash
pip install -r requirements.txt
```

---

# API Setup

Create a **Google Gemini API Key** from Google AI Studio.

The notebook securely requests the API key at runtime using:

```python
from getpass import getpass

GEMINI_API_KEY = getpass("Enter your Gemini API Key: ")
```

This ensures that API keys are **not hardcoded** into the notebook.

---

# How to Run

1. Open the notebook in Google Colab or Jupyter Notebook.
2. Install all dependencies.
3. Enter your Gemini API key when prompted.
4. Run all notebook cells sequentially.
5. Review the structured extraction output.
6. Validate extracted records.
7. Save the JSON file.
8. Build the FAISS vector store.
9. Execute the RAG pipeline.
10. Ask IPL-related questions.

---

# Results

The project successfully demonstrates:

- Structured information extraction using Gemini
- Pydantic schema validation
- Validation failure handling
- JSON output generation
- Text chunking
- Sentence embeddings
- FAISS vector database
- Semantic document retrieval
- Retrieval-Augmented Generation (RAG)
- Question answering

---

# Future Improvements

Possible enhancements include:

- Larger IPL document collection
- Real IPL datasets
- ChromaDB vector database
- Hybrid search
- Web application using Streamlit
- Multi-document retrieval
- Better prompt engineering
- Real-time IPL knowledge base

---

# Requirements

Main libraries used:

- google-genai
- pydantic
- langchain
- langchain-community
- langchain-text-splitters
- sentence-transformers
- faiss-cpu
- numpy
- pandas

Install using:

```bash
pip install -r requirements.txt
```

---

# Conclusion

This project demonstrates a complete end-to-end LLM application that combines **structured information extraction** with a **Retrieval-Augmented Generation (RAG)** pipeline.

Google Gemini is used to extract structured IPL match information, while Pydantic ensures schema validation and data quality. The extracted records are stored as JSON and used alongside a FAISS-powered vector database to retrieve relevant information for answering IPL-related queries.

The notebook implements structured extraction, schema validation, semantic search, and context-grounded question answering as an end-to-end workflow.

> **Verified run (2026-10-24):** The uploaded executed notebook reports 14 of 15 Gemini extraction calls succeeded and passed Pydantic validation; one call failed with a temporary HTTP 503 `UNAVAILABLE` response. The uploaded `structured_results.json` contains the 14 successful records; I checked that each record has the expected fields and valid value types. In the executed five-query retrieval assessment, top-1 was correct for 1/5 queries and top-2 contained the correct answer for 4/5 queries.
