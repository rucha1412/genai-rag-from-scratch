# GenAI RAG System — Built From Scratch

A Retrieval-Augmented Generation (RAG) chatbot that answers questions 
using only a source document, built to learn the core mechanics of 
production AI systems from the ground up (no frameworks like LangChain — 
raw API calls, manual chunking, and embeddings).

## What it does
- Fetches a Wikipedia article as a source document
- Chunks the text into retrievable pieces
- Embeds each chunk using `sentence-transformers`
- Retrieves the most relevant chunks via cosine similarity for a given question
- Grounds the LLM's answer strictly in retrieved context to reduce hallucination

## What I learned
- How conversation memory actually works (there is none — you resend history every call)
- The difference between retrieval failures (wrong chunks found) and 
  generation failures (model ignores good context)
- Why grounding instructions reduce but don't eliminate hallucination

## Stack
Python, Groq API (Llama 3.3), sentence-transformers, scikit-learn, Google Colab

## Next steps
Building a formal eval set to measure answer quality instead of eyeballing it.
