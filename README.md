
# 📄 PDF Question Answering System using RAG

A Python-based PDF Question Answering System that allows users to upload a PDF document and ask questions in natural language. The system retrieves the most relevant text from the PDF using semantic search (FAISS + Sentence Transformers) and extracts the exact answer using a pre-trained DistilBERT Question Answering model.

---

# 📌 Project Overview

This project demonstrates a simple Retrieval-Augmented Generation (RAG) pipeline without using any external APIs or Large Language Models.

The workflow includes:

- Uploading a PDF
- Extracting text from each page
- Splitting text into chunks
- Creating embeddings using Sentence Transformers
- Storing embeddings in a FAISS vector database
- Retrieving the most relevant chunks
- Using DistilBERT Question Answering model to find the exact answer
- Displaying both the answer and supporting context

---

# 🛠 Technologies Used

- Python
- Google Colab
- PyPDF
- Sentence Transformers
- FAISS
- Hugging Face Transformers
- PyTorch
- NumPy

---

# 📚 Libraries

```python
pypdf
sentence-transformers
faiss-cpu
transformers
torch
numpy
re
```

Install using:

```bash
pip install pypdf sentence-transformers faiss-cpu transformers torch
```

---

# 📂 Project Workflow

```
PDF Upload
     │
     ▼
Extract Text
     │
     ▼
Chunk Text
     │
     ▼
Generate Embeddings
     │
     ▼
Store in FAISS Index
     │
     ▼
User Question
     │
     ▼
Convert Question to Embedding
     │
     ▼
Retrieve Top Relevant Chunks
     │
     ▼
DistilBERT QA Model
     │
     ▼
Return Best Answer + Context
```

---

# 📖 Step 1: Upload PDF

The user uploads a PDF file using Google Colab.

```python
from google.colab import files

uploaded = files.upload()
pdf_path = list(uploaded.keys())[0]
```

---

# 📖 Step 2: Extract Text

Read every page of the PDF and extract text.

```python
from pypdf import PdfReader

reader = PdfReader(pdf_path)
```

Output:

- Total pages
- Extracted text

---

# 📖 Step 3: Text Chunking

Large pages are divided into overlapping chunks.

Example:

```
Chunk Size = 150 words

Overlap = 30 words
```

Benefits:

- Better retrieval
- Better QA accuracy
- Preserves context

---

# 📖 Step 4: Generate Embeddings

Each chunk is converted into a numerical vector using:

```
SentenceTransformer

Model:
all-MiniLM-L6-v2
```

Example:

```python
embedder = SentenceTransformer("all-MiniLM-L6-v2")
```

---

# 📖 Step 5: Create FAISS Index

Embeddings are stored inside FAISS.

```python
index = faiss.IndexFlatL2(dimension)
```

FAISS performs fast similarity search over all chunks.

---

# 📖 Step 6: Load Question Answering Model

Model Used

```
distilbert-base-cased-distilled-squad
```

This model predicts

- Start position
- End position

of the answer inside the retrieved context.

```python
AutoModelForQuestionAnswering
```

---

# 📖 Step 7: Retrieve Relevant Chunks

When the user asks a question:

Example

```
What are compound semiconductors?
```

The system:

- Converts the question into an embedding
- Searches FAISS
- Retrieves the Top-3 most similar chunks

---

# 📖 Step 8: Extract Answer

Each retrieved chunk is passed into DistilBERT.

The model returns

- Answer
- Confidence Score

The highest-scoring answer is selected.

---

# 📖 Step 9: Display Result

Example

```
Question:

What are compound semiconductors?

Answer:

Examples are CdS, GaAs, CdSe and InP.

Supporting Content:

Examples are:

• Inorganic:
CdS
GaAs
CdSe
InP

Organic:
anthracene
doped phthalocyanines

Organic polymers:
polypyrrole
polyaniline
polythiophene
```

---

# 📊 Project Pipeline

```
User Uploads PDF
        │
        ▼
Extract Text
        │
        ▼
Chunk Text
        │
        ▼
Sentence Embeddings
        │
        ▼
FAISS Vector Store
        │
        ▼
User Question
        │
        ▼
Question Embedding
        │
        ▼
Similarity Search
        │
        ▼
Top Relevant Chunks
        │
        ▼
DistilBERT QA
        │
        ▼
Answer
```

---

# 📁 Project Structure

```
PDF-QA-System/

│
├── README.md
├── pdf_qa.ipynb
├── sample.pdf
├── requirements.txt
└── images/
```

---

# 📦 Requirements

```
pypdf

sentence-transformers

faiss-cpu

transformers

torch

numpy
```

---

# 🎯 Features

- Upload any PDF
- Automatic text extraction
- Intelligent text chunking
- Semantic search using embeddings
- Fast retrieval using FAISS
- Accurate question answering using DistilBERT
- Displays supporting context
- No OpenAI API required
- Works entirely on local models

---

# ✅ Advantages

- Fast retrieval
- Lightweight models
- Easy to understand
- Free to use
- Suitable for educational projects
- Can be extended into a chatbot

---

# ⚠ Limitations

- Works best on text-based PDFs
- Cannot process scanned image PDFs without OCR
- Limited context window (384 tokens)
- Uses extractive QA only
- Does not generate new content beyond the document

---

# 🚀 Future Enhancements

- Add OCR support using Tesseract
- Multi-PDF search
- Streamlit web interface
- Chat history
- Hybrid search (BM25 + Embeddings)
- Replace DistilBERT with larger LLMs
- Add source highlighting
- Support multiple languages
- Deploy on Hugging Face Spaces

---

# 📌 Applications

- Academic document search
- Research paper assistant
- Legal document analysis
- Company policy assistant
- E-book search
- Medical document QA
- Knowledge base chatbot

---

# 👨‍💻 Author

**Name:** Kavibalan

**Project:** PDF Question Answering System using Retrieval-Augmented Generation (RAG)

**Technology Stack:** Python, Sentence Transformers, FAISS, Hugging Face Transformers, PyTorch

---

# ⭐ Conclusion

This project implements a Retrieval-Augmented Generation (RAG) pipeline for answering questions from PDF documents. It combines semantic retrieval using Sentence Transformers and FAISS with extractive question answering using DistilBERT. The approach enables efficient, accurate, and offline document question answering without relying on external APIs or cloud-based large language models.
