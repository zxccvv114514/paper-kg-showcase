# Paper KG Observatory

Interactive showcase for a paper knowledge graph pipeline built around Neo4j, large-scale publication metadata, incremental updates, and a static Web visualization.

**Live demo:** https://zxccvv114514.github.io/paper-kg-showcase/

![Paper KG desktop preview](preview-desktop.png)

## Overview

Paper KG Observatory turns merged publication metadata into a graph-oriented research knowledge base. The pipeline extracts papers, authors, venues, years, keywords, and subjects from raw JSON records; normalizes entity identifiers; exports Neo4j-compatible CSV/Cypher artifacts; validates the imported graph locally; and provides a lightweight Web demo for exploring a sampled subgraph.

The public demo uses sampled graph data only. The full graph and original datasets are not included in this repository.

## Highlights

- **107,200** validated paper nodes
- **154,144** author entities
- **103,366** keyword entities
- **~1.90M** core relationships
- Coverage across venues including INTERSPEECH, NeurIPS, AAAI, CVPR, ACL, EMNLP, ICML, and ICLR
- Static interactive visualization with search, filtering, zooming, node details, and neighborhood inspection

## Architecture

```text
Raw publication JSON
        |
        v
Field extraction and normalization
        |
        v
Stable ID matching and de-duplication
        |
        v
Graph schema construction
        |
        v
Neo4j CSV / Cypher export
        |
        v
Local Neo4j validation + sampled Web demo
```

## Graph Schema

Core node types:

- `Paper`
- `Author`
- `Venue`
- `Year`
- `Keyword`
- `Subject`

Core relationships:

- `(:Paper)-[:AUTHORED_BY {author_order}]->(:Author)`
- `(:Paper)-[:PUBLISHED_IN]->(:Venue)`
- `(:Paper)-[:PUBLISHED_YEAR]->(:Year)`
- `(:Paper)-[:HAS_KEYWORD]->(:Keyword)`
- `(:Paper)-[:HAS_SUBJECT]->(:Subject)`

The pipeline also includes DBLP XML citation-edge extraction and diagnostics, leaving room for future integration with richer citation sources such as OpenAlex, Semantic Scholar, Crossref, or OpenCitations.

## Demo Features

- Full-canvas graph visualization
- Venue-level filtering
- Node type filtering
- Keyword/title/author search
- Click-to-inspect node details
- Neighbor exploration
- Responsive static deployment on GitHub Pages

## Local Preview

```powershell
cd paper_kg_showcase
python -m http.server 8848 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:8848/
```

## Repository Contents

```text
paper_kg_showcase/
  index.html                  # Static interactive showcase
  assets/graph_data.js         # Sampled graph data for public demo
  README.md                    # Project overview
  DEMO_SCRIPT.md               # Demo video script
  DEPLOY_GITHUB_PAGES.md       # Deployment notes
```

## Privacy Boundary

This repository intentionally excludes:

- Original large-scale metadata files
- Local Neo4j database files
- Credentials, database connection strings, and private paths
- Non-public research materials

Only sampled demo data and project documentation are included.
