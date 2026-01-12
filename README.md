# NCERT-RAG-Eval  
A Benchmark for Evaluating Retrieval-Augmented Generation on NCERT Textbooks

## Overview

NCERT-RAG-Eval is a benchmark framework for evaluating Retrieval-Augmented Generation (RAG) systems on Indian NCERT school textbooks. It provides a reproducible pipeline that converts NCERT PDFs into a large-scale vector knowledge base and quantitatively compares BM25, dense FAISS, and hybrid retrieval for curriculum-aligned AI tutoring.

Large Language Models (LLMs) are increasingly used in education, but they frequently hallucinate or produce unsupported explanations when not grounded in authoritative textbooks. This project measures whether RAG systems actually retrieve and use correct NCERT content, making it suitable for trustworthy AI tutoring and educational technology research.

## What this Benchmark Measures

NCERT-RAG-Eval evaluates retrieval quality using three metrics:

- Recall@k – Whether the correct NCERT passage is retrieved  
- Precision@k – How much of the retrieved content is actually relevant  
- Faithfulness – Whether the retrieved chunks contain the required textbook facts, formulas, or definitions  

These metrics directly quantify hallucination risk in AI tutors.

## System Pipeline

NCERT PDFs  
↓  
Text Cleaning & Chunking  
↓  
Embedding (SBERT)  
↓  
FAISS Index        BM25 Index  
        \          /  
         \        /  
          Hybrid Retriever  
                 ↓  
          Top-k NCERT Chunks  
                 ↓  
     Evaluation (Recall, Precision, Faithfulness)

## Repository Structure

NCERT-RAG-Eval/

data/  
  raw_pdfs/        – Original NCERT PDFs  
  corpus/         – Cleaned NCERT text  
  chunks/         – Chunked textbook passages  
  questions/      – Benchmark questions  

scripts/  
  pdf_to_text.py  
  chunk_text.py  
  build_indices.py  
  run_retrieval.py  
  run_full_pipeline.py  

requirements.txt  

README.md  

## How to Run

1. Install dependencies  
pip install -r requirements.txt  

2. Place NCERT PDFs into  
data/raw_pdfs/  

3. Run the full benchmark  
python scripts/run_full_pipeline.py  

This will extract text from NCERT PDFs, chunk the corpus, build BM25 and FAISS indices, and run retrieval on benchmark questions.

## Benchmarked Retrieval Methods

BM25 – Classical keyword-based retrieval  
FAISS – Dense semantic retrieval using SBERT embeddings  
Hybrid – Union of BM25 and FAISS results  

## Why This Matters

Most RAG demos evaluate only text similarity (BLEU, ROUGE, BERTScore).  
NCERT-RAG-Eval measures whether the AI actually used the textbook.

This makes it suitable for:
- Trustworthy AI tutors  
- Educational AI benchmarking  
- Hallucination-aware RAG research  
- Indian curriculum alignment  

## Data License

NCERT textbooks are the property of the National Council of Educational Research and Training (NCERT), Government of India.  
This repository distributes only derived text and embeddings for academic benchmarking. Users must obtain the original PDFs from official NCERT sources.

## License

This project is released under the MIT License for academic and research use.
