
Nicolas Cravino
   • You
AI Engineer | Cybersecurity | Agentic AI Innovator | Author | 20+ Years in Finance & Consulting
3mo • Edited •  

Yesterday I posted the 3-way wiki-vs-RAG an obvious 4th arm was missing. 

**qmd**— Shopify's CEO Tobi Lütke building a local-first search in the open. BM25 + on-device embeddings + local reranker. Zero API per query. 

Added it, re-ran the same 30 queries, same judge:
- Cheapest: ~922 tok · $0.0052 · no embedding API.
- Lowest quality overall: 3.56 vs. 4.45+.

**By category**: 
 - Narrow: tied (~4.9).
 - Branch: collapses to 2.83.
 - Cross-branch: collapses to 3.37.

**Vs. agentic-RAG**: 24 losses, 0 wins, 6 ties.

**Failure**: QMD's reranker ranks peripheral stubs above branch landing pages.
 
QMD is a real Pareto point for grep-shaped questions — not a drop-in for RAG when synthesis matters. For lookups it's ~30% cheaper with zero API. The moment the query spans branches, agentic-RAG still wins.

Repo in the comments.
Activate to view larger image,
chart, radar chart

483 impressions
View analytics
