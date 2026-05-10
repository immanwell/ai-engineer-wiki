---
title: "RAG and Retrieval"
aliases:
  - "retrieval-augmented generation"
  - "vector search"
  - "embedding retrieval"
tags:
  - wiki
  - "context-reliability"
domain: "context-reliability"
sources:
  - "AI Engineer Chapter 6 (Chip Huyen, 2025).md"
status: stub
confidence: high
---

Created: Sunday, 10 May 2026, 17:25
Modified: `=dateformat(this.file.mtime, "DDDD, HH:mm")`

---

# RAG and Retrieval

**Summary**: RAG (Retrieval-Augmented Generation) is a two-step pattern — retrieve relevant information from external memory, then generate. The quality of a RAG system depends entirely on the retriever. Retrieval methods range from simple term-based (BM25) to more powerful embedding-based (vector search).

**Sources**: [[raw/AI Engineer Chapter 6 (Chip Huyen, 2025).md|AI Engineering Chapter 6]]

---

## What RAG Is

RAG solves the **context window problem**: models can't hold entire codebases, books, or document collections in their context. Instead of fitting all knowledge into the prompt, RAG:

1. **Retrieves** relevant information from external memory
2. **Generates** a response using that information

Benefits:
- Overcomes context length limits
- Reduces costs (smaller prompts)
- Keeps responses accurate and up-to-date
- Enables models to access information they weren't trained on

## The Two-Step Process

```txt
User Query → Retriever → Top-K Relevant Chunks → Context + Query → Model → Response
```

**Retriever quality is the key variable.** A weak retriever means irrelevant context → bad responses, even with a powerful model.

## Retriever Types

### Term-Based (Light / Fast)

| Method | How It Works | Pros | Cons |
|--------|--------------|------|------|
| **BM25** | Term frequency + inverse document frequency | Simple, fast, good baseline | Ignores synonyms, word order |
| **Elasticsearch** | Inverted index on terms | Scalable, mature infrastructure | Same limitations as BM25 |

Term-based methods are lighter to implement and provide strong baselines. Good starting point before investing in more complex retrieval.

### Embedding-Based (Semantic / Powerful)

Uses **vector embeddings** — text is converted to dense vectors in high-dimensional space. Similar concepts cluster together.

| Method | How It Works | Pros | Cons |
|--------|--------------|------|------|
| **Vector search** | Nearest-neighbor search in embedding space | Captures meaning, synonyms, nuance | More compute intensive |
| **Cross-encoder** | Reranks retrieved results with full context | Higher accuracy reranking | Slower inference |

Embedding-based retrieval is powered by vector search — the same technology behind search engines and recommender systems.

## Choosing a Retriever

**Simple rule**: Start with BM25 or Elasticsearch as a baseline. If retrieval quality is insufficient, upgrade to embedding-based.

BM25 gives you 80% of the benefit for 20% of the complexity. Embeddings add cost and latency — only worth it when baseline is actually failing.

## RAG as a Special Case of Agent

Chip Huyen notes an important relationship:

> "RAG is a special case of agent where the retriever is a tool the model can use."

Both patterns:
- Allow models to circumvent context limitations
- Keep models more up-to-date than training alone permits

But agents can do more — the retriever is just one tool in a larger toolset.

## For AI Tutor Specifically

RAG is directly applicable:
- **Curriculum retrieval**: Given a student's question, retrieve the relevant NCDC topic and subtopics from the curriculum knowledge base
- **Past session retrieval**: Given a student's confusion, retrieve prior session context to maintain continuity

A weak retriever would give the wrong topic explanation — which is worse than giving no explanation at all. The retriever quality determines the tutor's reliability.

## Related Pages

- [[context-reliability]] — memory and context management foundations
- [[agentic-architecture]] — agents use retrieval as one tool among many
- [[prompt-attacks]] — indirect prompt injection via retrieved documents (Ch5 security)
- [[ai-tutor]] — RAG applied to curriculum knowledge base