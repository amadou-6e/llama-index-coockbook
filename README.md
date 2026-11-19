# LlamaIndex Cookbook Tutorials

Hands-on notebooks that build a Retrieval-Augmented Generation (RAG) stack with LlamaIndex, from vector indexing to tool-using agents. By the end, you can run local retrieval workflows on PostgreSQL/pgvector and extend them with multi-step agent reasoning.

## Setup and Dependency Installation

### For Conda (PostgreSQL tools)
```powershell
conda install -y -c conda-forge postgresql
```

### For Python with pip (venv + project extras)
```powershell
python -m venv .venv
. .\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install -e ".[notebooks]"
```

### Environment Variables
Create a `.env` file in this folder for notebook cells that call hosted models:

```dotenv
OPENAI_API_KEY=your_key_here
```

## Why You Need This

Most RAG examples stop at a single retriever call. This tutorial path focuses on practical system behavior: indexing quality, retrieval controls, synthesis strategies, conversational state, and agent planning over multiple tools.

The notebooks also show a realistic local-first setup using PostgreSQL + pgvector, so you can iterate without relying entirely on hosted vector databases.

## What You Will Learn (Notebook by Notebook)

### 1. Vector Indexing and Retrieval Foundations
- Notebook: [`001_index_retrieval_and_embeddings.ipynb`](./001_index_retrieval_and_embeddings.ipynb)
- Learn: Build embeddings, store vectors in `PGVectorStore`, create a `VectorStoreIndex`, and test retrieval modes.
- Example end-result: A local semantic search pipeline that returns relevant chunks from indexed documents.

### 2. RAG Query Engines and Response Synthesis
- Notebook: [`002_rag_with_query_engines.ipynb`](./002_rag_with_query_engines.ipynb)
- Learn: Connect retrievers to response synthesis, compare local and API-backed generation, and apply post-processors/rerankers.
- Example end-result: A RAG query engine that answers questions with citation-ready supporting context.

### 3. Conversational RAG with Chat Engines
- Notebook: [`003_chat_engines.ipynb`](./003_chat_engines.ipynb)
- Learn: Convert retrieval pipelines into multi-turn chat engines with memory and configurable prompts.
- Example end-result: A context-aware chat assistant grounded in your indexed corpus.

### 4. Query Planning and Agent Orchestration
- Notebook: [`004_query_planning_and_agents.ipynb`](./004_query_planning_and_agents.ipynb)
- Learn: Break complex questions into sub-questions, route across tools/query engines, and synthesize final outputs.
- Example end-result: A planning agent that decomposes tasks and combines tool outputs into one response.

### 5. Custom Tool Use with Agents
- Notebook: [`005_agents_with_custom_tool_use.ipynb`](./005_agents_with_custom_tool_use.ipynb)
- Learn: Implement custom retrieval tools and wire them into structured/function-calling agent workflows.
- Example end-result: An agent that can invoke a full-document retrieval tool when targeted evidence is needed.

## Runtime Notes

- Several notebooks initialize a local PostgreSQL data directory under `./vectorstore/postgres` via `initdb` and `pg_ctl`.
- Notebooks import a local `utils` module. If missing in your environment, add `utils.py` with the helper functions referenced in cells.
