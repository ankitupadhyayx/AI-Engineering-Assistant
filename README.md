# AI Engineering Assistant

A local AI assistant that answers questions from custom documents using Retrieval Augmented Generation (RAG).

## Features

- Document ingestion (PDF, DOCX, TXT)
- Semantic search using FAISS
- LLM response generation using Microsoft Phi-2
- Sentence Transformer embeddings
- Desktop GUI using Tkinter

## Tech Stack

Python  
Transformers  
Sentence Transformers  
FAISS  
Tkinter

## How it Works

1. Documents are loaded and chunked
2. Embeddings are generated
3. Stored in FAISS vector database
4. User asks a question
5. Relevant context is retrieved
6. LLM generates the answer