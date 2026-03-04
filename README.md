# The Measure of Insight Benchmark - Supplement

This repository provides supplementary technical materials for **“The Measure of Insight: A Benchmark for Evaluating AI Retrieval in Digital Archives”**. The benchmark is an attempt to develop a means of evaluating scholarly retrieval platforms. It is predicated on an important scholarly distinction, the difference between passages that are merely on topic (i.e. those that are relevant) and passages that actually move a project forward by complicating a question, reframing a concept, or opening a plausible line of inquiry.

The public-domain **ECCO-TCP corpus** (2,473 transcribed eighteenth-century volumes) serves as the basis for this benchmark.

Note that this repo is merely illustrative, and not all variables are consistently defined, which may cause these notebooks to break for the time being. This is not the final benchmark release, and so some materials are likely to change from time to time without notice.

### What the benchmark measures

The benchmark is designed to evaluate full-text retrieval and RAG-based systems in a humanities context along three dimensions:

- **R-Score (Relevance):** graded semantic relevance of passages to scholarly queries.
- **A-Score (Abductive Potential):** the capacity of passages to generate new questions, challenge assumptions, and support hypothesis formation, inspired by C. S. Peirce's theory of abductive inference.
- **Structural Metrics:** measures of granularity, “relevance caging,” and support for exploratory workflows.

This evaluation will treat the public-domain ECCO-TCP corpus as a testbed, pooling and deduplicating the top results from three different search engines:

- **A HathiTrust-like System:** BM25 ranking, featuring volume-level retrieval and subsequent search-in-books feature, built using the [HathiTrust Catalog Indexer] (https://github.com/hathitrust/hathitrust_catalog_indexer).
- **Vector retrieval and Rocchio-style feedback:** A simple retrieval tool based on the [Sentence Transformers](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) model developed by Nils Reimers and Iryna Gurevych at the Technical University of Darmstadt in Germany.
- **Passage-level exploratory semantic search:** An elasticsearch platform that I built for the full ECCO dataset (12m passages) with a team at Harvard to illustrate the affordances of granular search and user-directed feedback.

> **Note:** This repository contains *illustrative* data, rubrics, and example code. It is not the full benchmark release. Certain resources are in active development and may change without notice.

---

## Repository contents

- `0_docs`
  - `moi_overview.md` – Conceptual overview of the benchmark and its evaluation goals.
  - `queries.md` - Describes eight searches that could potentially serve for evaluation.
  - `R-A_rubric.md` – Detailed annotation guidelines for R-Score and A-Score (example passages to be added).
  - `R-A_rubric_quick_reference.md` – A shorter reference rubric for evaluators.
  - `tasks_and_metrics.md` – Definitions of static, exploratory, and identity-constrained evaluation tasks, and formal definitions of core metrics (nDCG_R, nDCG_A, granularity/AGS).

- `1_code`
  - `topic_modeling_eccotcp.ipynb` – preparatory notebook that develops metadata and runs topic modeling algorithm for passages.
  - `eccotcp_vector_model.ipynb` – creates and queries a vector retrieval model for the Ecco-tcp.
  - `fuzzy_eccotcp_matching.ipynb` – matches eccco-tcp and full ecco volumes.
  - `ht_search_in_book_simulation.ipynb` – approximates HathiTrust's search-in-book feature.
  - `extract_psgs_from_fullecco_cluster_csv.ipynb` – creates a directory of files from the exploratory search platform for pooling and deduplication.
  - `create_dirs_of_top_tcp_results.ipynb` – creates a directory of files from eccotcp platforms (vector and htsolr) for pooling and deduplication.
  - `pooling_and_deduplication.ipynb` – prepares top results for evaluation.

- `2_data`
  - `example_eccotcp_passages` – an illustrative sample of ECCO-TCP passages (i.e. 139 of 150,643 passages).
  - `eccotcp_psgs_nmf_topics_k80.txt` – topics for ECCO-TCP passages; used to measure the diversity of retrieved results.
  - `eccotcp_psgs_with_topics.csv` – ECCO-TCP metadata, assigning NMF topics to passages.
  - `eccotcp_to_fullecco_matching_in_progress.csv` – a spreadsheet matching ECCO-TCP volumes with items in the full ECCO dataset. Fuzzy matching was done to >90% accuracy, and manual correction of unmatched results will continue over the next two months.

- `3_results`
  - `data` – contains structured results from queries run against three search engines.
  - `passages` – contains top passages for queries run against three search engines.

- `4_screenshots`
  - Screenshots illustrating passage-based retrieval, metadata filtering, exploratory workflows, etc.

---

## Getting started

1. Clone the repository:

   ```bash
   git clone https://github.com/sosadetz/measure-of-insight-benchmark-supplement.git
   cd measure-of-insight-benchmark-supplement

2. Open the example notebook:

   `jupyter notebook 1_code/example_notebook.ipynb`

3. Expect notebooks to error out at certain points. Some are research artifacts and may require minor variable/path changes.
