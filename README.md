# CellAgent: A Multi-Brain AI Co-Pilot for Single-Cell Multiomics

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-Scanpy%20%7C%20Muon-green)](https://muon.readthedocs.io/)
[![Docker](https://img.shields.io/badge/Container-Docker-blue)](https://www.docker.com/)
[![Status](https://img.shields.io/badge/Status-Work%20In%20Progress-yellow)]()

> ⚠️ **Development Status:** This project is currently in **active development/prototyping phase**. Features are subject to change, and the codebase is being optimized for broader biological use cases.

**CellAgent** is an autonomous AI agent designed to democratize complex bioinformatics workflows. By leveraging a "multi-brain" architecture, it translates natural language queries into executable `scanpy` and `muon` pipelines, enabling researchers to perform rigorous single-cell multiomics analysis (scRNA-seq + scATAC-seq) without writing code.

---

##  Demo

[Watch the Demo](https://drive.google.com/file/d/1UlxnI962dtE1qEE4xnwYC4mjXKZZIBpZ/view?usp=sharing)

> *Watch CellAgent autonomously plan a QC pipeline, filter cells based on data-driven metrics, and generate custom UMAP visualizations.*

---

##  The Problem

Single-cell multiomics (analyzing RNA and Chromatin Accessibility simultaneously) provides unprecedented insight into cellular biology. However, the barrier to entry is high:

1.  **Complex Tooling:** Tools like `Seurat` (R) and `Muon` (Python) have steep learning curves.
2.  **Fragmented Workflows:** Analysts often switch between disparate scripts for QC, filtering, and dimensionality reduction.
3.  **Reproducibility Crisis:** Ad-hoc manual analysis leads to inconsistent parameters and un-reproducible results.
4.  **Cognitive Load:** Researchers spend more time fixing dependency errors than interpreting biological insights.

---

##  The Solution: A Multi-Brain Agent

CellAgent is not just a chatbot; it is a **stateful, decision-making system**. It uses a "Dual-Brain" Triage Engine to intelligently route user intent, ensuring that the right specialized logic handles the right task.

### Key Capabilities
*  Natural Language Interface: "Filter out cells with >5% mitochondrial reads" $\rightarrow$ Autonomously executes `sc.pp.filter_cells`.
*  Intelligent Planning: Automatically constructs dependency-aware pipelines (e.g., QC $\rightarrow$ Normalize $\rightarrow$ HVG $\rightarrow$ PCA $\rightarrow$ UMAP).
*  Analytical Memory: Remembers context. If you ask, "How many cells were removed?", it recalls the result of the previous filtering step.
*  Proactive Suggestions: Analyzes the data state to recommend the next logical step (e.g., "RNA is processed; shall we start ATAC-seq integration?").
*  Custom Code Generation: Writes secure, sandboxed Python code on-the-fly for custom requests not covered by standard tools.

---

##  System Architecture

The core of CellAgent relies on a Hub-and-Spoke architecture managed by a central `AgentExecutor`. The system routes user inputs through specialized "Brains" depending on the required action.
![System Architecture Diagram](https://drive.google.com/uc?export=view&id=1nRc9eNlFBaN9AuHvNqY9hYY2ZS85K-as)


### The "5-Brain" Logic
1.  **Triage Brain:** The gatekeeper. Classifies intent into `task`, `qa`, or `custom`.
2.  **Planner Brain:** Maps intents to a directed acyclic graph (DAG) of tools in the `TOOL_REGISTRY`.
3.  **QA Brain:** Retrieves structured metadata from `analytical_memory` to answer specific data questions.
4.  **Suggester Brain:** Heuristic engine that proposes the next logical analysis step based on data modality presence.
5.  **Code-Gen Brain:** An LLM specialized in the `scanpy` API to handle edge cases and custom plotting.

---

##  Impact & Performance

* **2x Speedup:** Reduces time-to-insight for standard QC & Clustering workflows from ~4 hours (manual scripting) to <10 minutes.
* **Zero-Code Entry:** Allows wet-lab biologists to perform rigorous computational analysis independently.
* **Reproducibility:** Enforces standardized pipelines via `pipeline_templates.py`, ensuring consistent parameters across datasets.

---

##  Tech Stack

* **Core Logic:** Python 3.10+
* **LLM Integration:** OpenAI GPT-4o (via `python-dotenv`)
* **Bioinformatics:** `scanpy`, `muon`, `anndata`, `pysam`
* **Vector Search (QA):** `opensearch-py` (for RAG modules)
* **Frontend:** Streamlit
* **Deployment:** Docker (Alpine/Slim based)

---

