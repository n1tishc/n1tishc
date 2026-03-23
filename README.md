# Hey, I'm Nitish C ☕️

**Software Engineer · Turning coffee into code (and bugs into features).**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/nitishc1) [![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white)](mailto:chandunitish@gmail.com)

I don't just use frameworks, I read the source, profile the runtime, and understand the memory layout. Whether it's a distributed key-value store, a real-time perception pipeline, or an LLM compression strategy, my goal is always the same: know exactly what's happening beneath the API surface.

> 🟢 **Actively seeking full-time new grad SWE roles** — systems, ML infrastructure, or backend. Open to on-site, remote, or relocating as needed.

---

## What I'm Up To

- 🔬 **Vector DB internals** — exploring HNSW, IVF-PQ, and flat index tradeoffs from scratch; building intuition for ANN search latency vs. recall curves at scale
- ⚙️ **ML systems exploration** — digging into inference optimization (quantization, KV cache eviction, batching strategies) and how modern serving stacks actually work under the hood
- 📚 **ML algorithms as a case study** — using classic algorithms (k-means, PCA, gradient descent variants) not just as tools but as lenses to understand how large-scale ML systems are designed and where the real bottlenecks live

---

## About

I'm a Software Engineer with an M.S. in Computer Science from RIT, focused on the intersection of **systems programming** and **machine learning infrastructure**. My work spans backend services handling millions of records, CI/CD pipelines for production microservices, and ML training infrastructure with automated evaluation loops.

What drives me: the belief that the best ML systems are built by engineers who understand the full stack — from TCP socket handling to gradient accumulation, from query execution plans to embedding retrieval latency. I build tools that are fast, observable, and correct.

Currently based in the Research Triangle (NC), exploring roles where systems thinking meets ML at scale.

---

## Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat&logo=openjdk&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=flat&logo=postgresql&logoColor=white)
![C++](https://img.shields.io/badge/C++-00599C?style=flat&logo=cplusplus&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?style=flat&logo=gnubash&logoColor=white)

**ML & Data**

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat&logo=tensorflow&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=flat&logo=huggingface&logoColor=black)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikitlearn&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logo=langchain&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat&logo=numpy&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat&logo=pandas&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat&logo=opencv&logoColor=white)

**Backend & Systems**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat&logo=nodedotjs&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat&logo=django&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat&logo=springboot&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)

**DevOps & Infrastructure**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonwebservices&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat&logo=jenkins&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![Git](https://img.shields.io/badge/Git-F05032?style=flat&logo=git&logoColor=white)

---

## Deep-Dive Projects

### [`go-redis`](https://github.com/n1tishc/go-redis) — Distributed Key-Value Store
> Redis clone built from scratch in Go

Implements PING, GET, SET, HGET, HSET with RESP protocol parsing over raw TCP sockets. Uses goroutines and channels for concurrent client handling, and includes an append-only file (AOF) persistence layer.

**System Insight:** Built the RESP wire protocol parser from byte-level reads — no third-party protocol libraries. The AOF implementation required understanding `fsync` semantics to balance durability vs. write throughput, mirroring the same trade-off real Redis makes in production.

---

### [`flex-search`](https://github.com/n1tishc/flex-search) — GitHub Fixability Search Engine
> Ranks GitHub issues by likelihood of accepting contributions

Full search pipeline: async data ingestion via `httpx` + `aiosqlite`, TF-IDF vectorization with cosine similarity for ranking, FTS5 full-text search with BM25 reranking, and a custom fixability scoring engine (50-point base + weighted signals). Dual interfaces: Streamlit (TF-IDF) and FastAPI (FTS5/BM25). 19 passing `pytest` tests.

**System Insight:** Designed a hybrid ranking formula (`0.6 × cosine_similarity + 0.4 × fixability_score`) that blends textual relevance with structural issue quality signals. The rate-limit-aware GitHub client dynamically switches between Full/Conserve/Minimal enrichment modes based on remaining API quota — a pattern borrowed from production API gateway design.

---

### [`procmap`](https://github.com/n1tishc/procmap) — Process Management Tool
> Cross-platform TUI for real-time process monitoring

Interactive terminal UI (Bubbletea + Lipgloss) with tree/flat/detail views, real-time CPU/memory aggregation, search, process controls (kill/pause/resume), and SQLite snapshot storage with JSON/CSV export.

**System Insight:** Reads process data via `gopsutil` which abstracts `/proc` on Linux and `sysctl` on macOS — but the tree construction algorithm is custom: recursive PID→PPID resolution with O(n) parent lookups using a pre-built hash map, maintaining sub-frame render latency even under high process counts.

---

## GitHub Stats

<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=n1tishc&show_icons=true&theme=github_dark&hide_border=true&count_private=true" alt="GitHub Stats" height="165" />
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=n1tishc&layout=compact&theme=github_dark&hide_border=true&langs_count=8" alt="Top Languages" height="165" />
</p>

---

<p align="center">
  <a href="https://www.linkedin.com/in/nitishc1">LinkedIn</a> · <a href="mailto:chandunitish@gmail.com">Email</a>
</p>
