# 001_index_retrieval_and_embeddings - Source Structure Map

## Marker Legend
- `-` source content captured as-is (possibly paraphrased for inventory clarity only).

## Narrative Thread
The notebook introduces vector search fundamentals, then walks from local PGVector setup to index construction, retrieval-mode comparisons, hybrid retrieval fusion, and embedding-space inspection so the reader can understand both mechanics and tradeoffs of retrieval quality.

## Reader Model
The reader is assumed to know only prior cookbook basics, so the notebook progressively introduces vector-search vocabulary, environment setup expectations, PGVector store construction, embedding model selection criteria, retrieval APIs and query modes, and finally why embedding visualization requires direct embedding access rather than store query outputs.

## Source Structure With Paragraph Placement

## `# **LlamaIndex: Vector Search Engine**`
- P0.1 Purpose: introduce RAG retrieval dependence on vector search and define embeddings, vector store, and vector index. Keywords: RAG, embeddings, vector store, vector index. Length [31]
- P0.2 Purpose: motivate semantic retrieval over keyword matching and explain embeddings as meaning vectors. Keywords: semantic search, transformers, meaning. Length [25]
- P0.3 Purpose: enumerate the indexing pipeline from tokenization to normalization. Keywords: tokenization, vectorization, aggregation, normalization. Length [30]
- P0.4 Purpose: list common ANN search algorithm families for vector lookup. Keywords: HNSW, IVFFlat, LSH. Length [16]
- P0.5 Purpose: describe similarity metrics used during nearest-neighbor ranking. Keywords: cosine, Euclidean, dot product. Length [17]
- P0.6 Purpose: provide criteria for selecting a vector database and introduce PGVector as chosen backend. Keywords: scalability, speed, hybrid search, PGVector, PostgreSQL. Length [33]

## `## Setup: PGVector`
- P1.1 Purpose: announce required Python package installation for notebook execution. Keywords: dependencies, llama-index, installation. Length [27]
- P1.2 Purpose: call out system-level pgvector and PostgreSQL requirements for local runtime. Keywords: pgvector, PostgreSQL, setup. Length [24]

## `## Vector Search: Building the Store and Index`
- P2.1 Purpose: frame this section as document-to-embedding transformation, vector storage, and index creation workflow. Keywords: PGVectorStore, embedding generation, indexing. Length [35]
- P2.2 Purpose: explain PGVectorStore benefits and caveat against specialized vector engines for speed. Keywords: PostgreSQL, hybrid search, performance tradeoff. Length [39]
- P2.3 Purpose: instruct reader to start PostgreSQL before creating the store. Keywords: local server, startup prerequisite. Length [46]
- P2.4 Purpose: instruct dotenv password configuration before database creation. Keywords: dotenv, credentials, connection. Length [18]
- P2.5 Purpose: direct reader to instantiate vector store and reference official PGVectorStore API docs. Keywords: API reference, vector store initialization. Length [42]
- P2.6 Purpose: define embedding models and explain semantic preservation in latent space. Keywords: embedding model, encoder, semantic space. Length [27]
- P2.7 Purpose: list embedding-model selection criteria for retrieval use cases. Keywords: quality, dimensionality, speed, domain specificity, licensing, language support. Length [28]
- P2.8 Purpose: explain SBERT as a fixed-length embedding bi-encoder approach. Keywords: SBERT, fixed-length vectors, bi-encoder. Length [18]
- P2.9 Purpose: justify chosen `all-MiniLM-L6-v2` model and provide alternate model catalog link. Keywords: MiniLM, speed-accuracy balance, Hugging Face models. Length [46]
- P2.10 Purpose: transition to document ingestion and index population stage. Keywords: vector index, ingest, retrieval readiness. Length [6]
- P2.11 Purpose: explain SimpleDirectoryReader choice and point to connector and ingestion alternatives. Keywords: SimpleDirectoryReader, LlamaHub, ingestion pipeline. Length [62]
- P2.12 Purpose: state SimpleDirectoryReader is used for this notebook. Keywords: data loader choice. Length [5]

## `## Understanding Retrieval: Accessing Nodes Through the Index`
- P3.1 Purpose: introduce retrieval-focused section objective. Keywords: retrieval, index access. Length [9]
- P3.2 Purpose: explain roles of retrievers and query engines in VectorStoreIndex. Keywords: retriever, query engine, structured responses. Length [37]
- P3.3 Purpose: contrast `as_retriever()` and `as_query_engine()` use cases. Keywords: raw nodes, synthesis, QA workflows. Length [46]
- P3.4 Purpose: describe `as_retriever()` behavior and transition to query execution. Keywords: vector similarity, non-generative retrieval. Length [26]
- P3.5 Purpose: suggest sample natural-language queries for experimentation. Keywords: retrieval prompts, testing questions. Length [51]
- P3.6 Purpose: introduce search-mode taxonomy subsection. Keywords: query modes, ranking strategy. Length [15]
- P3.7 Purpose: define mode families and point to supported PostgreSQL mode examples. Keywords: default, sparse, hybrid, text_search, semantic_hybrid. Length [17]
- P3.8 Purpose: describe semantic `default` mode. Keywords: dense vectors, semantic relevance. Length [31]
- P3.9 Purpose: describe `sparse` keyword matching behavior. Keywords: BM25, exact-term retrieval. Length [18]
- P3.10 Purpose: describe `hybrid` combination of dense and sparse retrieval. Keywords: balanced ranking, mixed strategy. Length [36]
- P3.11 Purpose: describe `text_search` full-text query path. Keywords: PostgreSQL FTS, lexical search. Length [13]
- P3.12 Purpose: describe `semantic_hybrid` weighting and experimentation guidance including `text_search=True`. Keywords: weighted fusion, parameter tuning. Length [10]

## `## The Embedding Space`
- P4.1 Purpose: note PGVector query responses omit embedding vectors and motivate direct embedding inspection workflow. Keywords: missing embeddings, visualization, discussion link. Length [14]

## Consolidations Observed In Source
- Source prose is split across many short markdown cells; concept blocks are fragmented but not explicitly merged.
- Retrieval mode explanations are separated from execution cells, with implicit transitions.
- Hybrid-retrieval rationale appears before and after code setup with partial redundancy.

## Cell Grouping Map (Source)
- M000 -> C002-C004: foundational context and install/setup actions.
- M005/M009/M013/M015/M017/M018/M020 -> C006-C021: PGVector initialization, database connection, embedding model, loading, and indexing.
- M022/M024/M027/M030/M032 -> C023-C034: retrieval execution, query modes, and hybrid/fusion retriever configuration.
- M035/M036 -> C037-C041: embedding visualization and persistence wrap-up.

## Code Cell Intent Map (Source)
- C002: install core LlamaIndex, PGVector, local model runtime, and BM25 dependencies.
- C004: install `pgvector` and PostgreSQL via conda.
- C006: load async cell execution extension.
- C007: initialize local PostgreSQL data directory.
- C008: verify PostgreSQL port availability.
- C010: import OS/database/env dependencies and load dotenv values.
- C011: define DB and user values.
- C012: connect to default DB, create target DB, and close cursor/connection.
- C014: instantiate `PGVectorStore` with PostgreSQL parameters.
- C016: configure `LangchainEmbedding` using Hugging Face sentence-transformer backend.
- C019: load physics documents using `SimpleDirectoryReader`.
- C021: build storage context, index documents, and collect nodes/embeddings.
- C023: import notebook display helpers for rich rendering.
- C025: define and revise sample retrieval query strings.
- C026: execute baseline retriever and display matched text snippets.
- C028: import and set vector query mode values.
- C029: retrieve results under selected query mode and render snippets.
- C031: import settings and fusion retriever utilities.
- C033: define metadata filters and initialize filtered retriever.
- C034: create BM25 retriever and hybrid query-fusion retriever, then run and display results.
- C037: import embedding visualization helpers from local utilities.
- C038: embed a query string and inspect embedding dimensionality.
- C039: visualize document embeddings with query vector overlay.
- C040: persist built index to local assets path.
- C041: empty trailing code cell.

## Fidelity Crosswalk (Source Evidence)
- F01 | source: M013 | type: link | destination: P2.5 | notes: PGVectorStore API reference preserved (`https://docs.llamaindex.ai/en/stable/api_reference/storage/vector_store/postgres/`).
- F02 | source: M015 | type: link | destination: P2.8 | notes: SBERT overview preserved (`https://sbert.net/`).
- F03 | source: M015 | type: link | destination: P2.8 | notes: bi-encoder paper preserved (`https://arxiv.org/pdf/2010.08240`).
- F04 | source: M015 | type: link | destination: P2.9 | notes: selected embedding model card preserved (`https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2`).
- F05 | source: M015 | type: link | destination: P2.9 | notes: model catalog preserved (`https://huggingface.co/models?pipeline_tag=sentence-similarity&sort=trending`).
- F06 | source: M018 | type: link | destination: P2.11 | notes: SimpleDirectoryReader docs preserved (`https://docs.llamaindex.ai/en/stable/module_guides/loading/simpledirectoryreader/`).
- F07 | source: M018 | type: link | destination: P2.11 | notes: connector docs preserved (`https://docs.llamaindex.ai/en/stable/module_guides/loading/connector/`).
- F08 | source: M018 | type: link | destination: P2.11 | notes: ingestion pipeline docs preserved (`https://docs.llamaindex.ai/en/stable/module_guides/loading/ingestion_pipeline/`).
- F09 | source: M027 | type: link | destination: P3.7 | notes: supported PostgreSQL query modes example preserved (`https://docs.llamaindex.ai/en/stable/examples/vector_stores/postgres/`).
- F10 | source: M036 | type: link | destination: P4.1 | notes: PGVector embedding-return limitation discussion preserved (`https://github.com/run-llama/llama_index/discussions/15670`).
