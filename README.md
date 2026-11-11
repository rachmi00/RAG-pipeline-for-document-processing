# 📄 Document Q&A System with Multi-Engine OCR & Smart RAG

This notebook implements a complete and robust **multi-document Question Answering (RAG)** system capable of segmenting, classifying, and querying PDF files (native or scanned) using a locally optimized pipeline.

---

## 🚀 Key Features

1. **Automatic Document Classification**
   - Fast algorithm based on weighted keyword patterns.
   - Automatic detection of document types: invoices, payslips, contracts, loan statements, tax returns, and more.

2. **Hybrid Extraction Pipeline with Three OCR Engines**
   - Native extraction of digital text for maximum speed.
   - Automatic fallback to **three configurable OCR engines**: **Tesseract**, **EasyOCR**, and **PaddleOCR** to efficiently process scanned documents.

3. **Intelligent Segmentation & Indexing (RAG)**
   - Semantic chunking that respects sentence boundaries to preserve context.
   - Vector indexing using **FAISS**, with a global index and document-type-specific sub-indexes.
   - Automatic query routing to the appropriate document type to improve relevance and reduce noise.

4. **Local LLM Inference**
   - Local integration of **Llama 3.1** through `llama.cpp` with GPU acceleration (CUDA).
   - Generation of accurate, source-backed answers restricted to the provided context.

5. **Gradio Web User Interface**
   - Intuitive interface with PDF previews.
   - On-the-fly OCR engine selection.
   - Interactive chatbot with document-type filtering and adjustable retrieval parameters.

6. **Performance Evaluation Framework**
   - Integrated evaluation tools for calculating **Recall@K**, **Precision@K**, **MRR (Mean Reciprocal Rank)**, **Hit Rate**, and routing accuracy.
   - Performance report generator with formatting suitable for PowerPoint.

---

## 🛠️ Pipeline Architecture

```text
📥 [PDF File]
       │
       ▼
📖 [PDF Extractor] ── Direct digital text extraction or OCR fallback:
       │              Tesseract / EasyOCR / PaddleOCR
       ▼
🏷️ [Document Classifier] ── Routing and document boundary detection
       │
       ▼
✂️ [Document Chunker] ── Semantic segmentation
       │
       ▼
🗂️ [Intelligent Retriever] ── Embedding generation and FAISS indexing by type
       │
       ▼
💬 [Local LLM / Gradio UI] ── Source-backed answer generation using context
```

---

## ⚙️ Prerequisites & Installation

To run this pipeline, use an environment equipped with a GPU, such as a T4, L4, or A100 on Google Colab. The first notebook cells automatically install:

- Interface and PDF packages: `gradio`, `gradio_pdf`, and `pymupdf`.
- Deep learning and vector search tools: `sentence-transformers`, `faiss-cpu`, and `llama-cpp-python`.
- OCR engines and dependencies: `pytesseract`, `easyocr`, `paddlepaddle-gpu`, and `paddleocr`.

---

## 📖 Usage Guide

1. **Step 1: Run the installation cells** — `Package installation for pipeline` and `Install OCR Engines`.
2. **Step 2: Initialize the configuration and import libraries** — includes automatic GPU detection.
3. **Step 3: Load the LLM locally** — the approximately 4.9 GB model file downloads automatically on the first run.
4. **Step 4: Compile the modules** — Classifier, Extractor, Chunker, and Retriever.
5. **Step 5: Launch the Gradio interface** — interact with your documents through the generated link.
6. **Step 6: Evaluate the system** — use the evaluation module after processing your documents.