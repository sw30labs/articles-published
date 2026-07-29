# Wiki vs RAG: Where the Old Approach Still Wins

*The comparison is not just about retrieval quality. It is also about cost, latency, and the shape of the query.*

Yesterday I posted the three-way comparison between wiki-based retrieval and RAG. An obvious fourth option was missing.

That fourth approach is qmd: Shopify CEO Tobi Lütke’s local-first search stack, built in the open. It combines BM25, on-device embeddings, and a local reranker with zero API cost per query.

## What changed when I added qmd

I re-ran the same 30 queries with the same judge.

The results were clear:

- Cheapest: about 922 tokens and $0.0052 per run, with no embedding API
- Lowest quality overall: 3.56 versus 4.45+ for the stronger systems

## By category

- Narrow queries: roughly tied at about 4.9
- Branch queries: dropped to 2.83
- Cross-branch queries: dropped to 3.37

## Against agentic RAG

Against agentic RAG, the results were:

- 24 losses
- 0 wins
- 6 ties

## The real conclusion

The failure mode is important: qmd’s reranker tends to rank peripheral stubs above branch landing pages.

That makes qmd a genuine Pareto point for grep-shaped questions, but not a drop-in replacement for RAG when synthesis matters. For lookups, it is about 30 percent cheaper and uses zero API calls. The moment the query spans branches, agentic RAG still wins.

This is a useful reminder that retrieval design is not one-size-fits-all. Different architectures fit different query patterns better than others.
