# GenAI RAG Agent — Document Q&A with Measured Evaluation

A Retrieval-Augmented Generation system built from raw API calls (no 
LangChain/frameworks) to understand the core mechanics: chunking, 
embeddings, retrieval, grounding, evaluation, and tool use.

## What it does
Answers questions about a source document (Wikipedia's "Artificial 
Intelligence" article) by retrieving relevant chunks via embedding 
similarity, then generating grounded answers — plus a basic agent 
layer with tool use and error handling.

## Evaluation results
Built an 18-question eval set, graded automatically via LLM-as-judge.

| Version | Accuracy | Avg Tokens/Question |
|---|---|---|
| Baseline (top_n=2) | __% | ___ |
| **top_n=4 (winner)** | __% | ___ |

top_n=4 improved accuracy by fixing multi-part questions that needed 
more retrieved context, at a moderate token cost increase.

## Key engineering decisions
- Distinguished retrieval failures (wrong chunks found) from generation 
  failures (model ignores good context) — different fixes for each
- Chose top_n=4 as the accuracy/cost sweet spot after isolated testing
- Added try/except error handling to the agent's tool-calling loop 
  for graceful failure instead of crashes

## Stack
Python, Groq (Llama 3.3), sentence-transformers, scikit-learn, Google Colab

## What I'd build next
Hybrid search (keyword + embedding), a real vector database, and 
multi-tool agent workflows.
