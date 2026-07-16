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


## Evaluation Results

Built a 15-20 question eval set with known correct answers, graded 
automatically using LLM-as-judge (a second AI call scoring PASS/FAIL 
against expected answers).

| Version | Accuracy | Avg Tokens/Question |
|---|---|---|
| Baseline (top_n=2 chunks) | __% | ___ |
| top_n=4 chunks | __% | ___ |
| Stricter prompt | __% | ___ |
| chunk_size=2000 | __% | ___ |

**Winner:** top_n=4 — improved accuracy by fixing cases where 2 chunks 
weren't enough to cover multi-part questions, at a moderate token cost 
increase.

## Key learnings
- Retrieval failures (wrong/incomplete chunks) and generation failures 
  (model ignores good context) are distinct problems needing different fixes
- Grounding instructions reduce but don't eliminate hallucination
- Accuracy improvements often come with real cost tradeoffs worth measuring
