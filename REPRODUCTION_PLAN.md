# GraphRAG Reproduction Plan

## Motivation

The existing pipeline already turns large-scale publication metadata into a Neo4j paper knowledge graph. The next research-oriented question is whether this graph can support literature discovery rather than only visual exploration.

This reproduction focuses on a GraphRAG-style workflow: retrieve candidate papers from text, expand them through graph relations, and return evidence paths that explain why each paper is relevant. The goal is to connect the paper knowledge base to actual research workflows such as topic exploration, related-work discovery, and direction tracking.

## What Is Reproduced

The public demo implements a lightweight version of the core GraphRAG idea:

1. **Text recall baseline**
   - Search over paper titles, abstracts, venues, years, authors, and keywords.
   - Used as a simple non-graph baseline.

2. **Semantic proxy baseline**
   - Uses normalized token overlap as a browser-side proxy for semantic retrieval.
   - Keeps the static demo reproducible without external embedding services.

3. **Graph-enhanced retrieval**
   - Starts from text-recalled candidate papers.
   - Adds graph-context signals from `HAS_KEYWORD`, `AUTHORED_BY`, `PUBLISHED_IN`, and `PUBLISHED_YEAR`.
   - Scores candidates with both text relevance and neighborhood evidence.

4. **Evidence-path display**
   - Returns paper candidates together with graph paths such as:

```text
query -> Keyword(topic) -> Paper, with Venue(...) and Author(...) as graph context
```

## Why This Fits the Paper KG Project

The graph pipeline solves the infrastructure problem: data ingestion, normalization, entity modeling, Neo4j import, and incremental update.

The GraphRAG reproduction solves the application problem: how the graph can be used for research-oriented retrieval and evidence tracing.

Together, the project can be described as:

```text
large-scale publication metadata -> Neo4j paper knowledge graph -> graph-enhanced literature retrieval prototype
```

## Current Public Demo Boundary

The GitHub Pages version is intentionally static and public-safe:

- no private full graph files;
- no local Neo4j connection string;
- no API key or LLM provider;
- no unpublished research material;
- sampled graph data only.

The public GraphRAG Lab is therefore a proof-of-concept layer, not a full production RAG backend.

## Next Implementation Steps

1. Add real embeddings for paper title, abstract, and keywords.
2. Store vectors in Neo4j vector index or a lightweight vector store.
3. Replace browser token overlap with vector retrieval.
4. Use Cypher to expand top-k papers through keywords, authors, venues, years, and citation edges.
5. Add citation edges from OpenAlex, Semantic Scholar, Crossref, or OpenCitations.
6. Add answer synthesis with explicit evidence citations.
7. Evaluate keyword retrieval, vector retrieval, and graph-enhanced retrieval on a small set of research questions.

## Evaluation Sketch

Prepare 20-30 research questions related to the graph coverage, for example:

- representative work on spoken language understanding;
- papers about language model alignment and reliable generation;
- cross-venue trends in multimodal learning;
- bias, reasoning, and evaluation in LLMs.

Compare:

- keyword search;
- vector search;
- graph-enhanced retrieval.

Useful metrics:

- whether relevant papers appear in top-k;
- whether returned evidence paths are interpretable;
- whether graph expansion finds useful related papers missed by text-only recall;
- whether the method helps build a better related-work reading list.
