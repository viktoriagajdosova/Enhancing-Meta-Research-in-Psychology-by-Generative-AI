# 02. Topic Modeling Setup & Execution Manual

---

**Author:** Viktória Gajdošová  
**Last Updated:** June 2026  

---

## Technical Environment Overview

This setup manual guides you through configuring your computational environment to execute the topic modeling workflows provided in this module. 

> **Important Customization Note:** The code repositories and pipelines included in this folder (`bertopic_meta-research_pipeline.py` and `bertopic_meta-research_notebook.ipynb`) have been explicitly adapted, customized, and pre-configured for **psychological meta-research**. 

For general framework questions, core architectural defaults, or upstream updates unrelated to this behavioral science implementation, please consult the official open-source project channels:
* **Official Reference Documentation:** [BERTopic Documentation](https://maartengr.github.io/BERTopic/index.html)
* **Official Project Website:** [BERTopic Web Hub](https://bertopic.com/)
* **Upstream Source Code:** [BERTopic GitHub Repository](https://github.com/maartengr/bertopic)

---

## Chapter Roadmap

This manual serves as the comprehensive technical documentation and execution guide for the advanced neural topic modeling and research gap analysis pipeline optimized for Google Colab. It is structured into the following sections:

* **[1. Technical Configuration and Dependencies](#1-technical-configuration-and-dependencies)**
* **[2. Pipeline Architecture: Part 1 (BERTopic Core)](#2-pipeline-architecture-part-1-bertopic-core)**
* **[3. Analytical Visualization Artifacts](#3-analytical-visualization-artifacts)**
* **[4. Advanced Research Gap and Dynamics Analysis: Part 2](#4-advanced-research-gap-and-dynamics-analysis-part-2)**
* **[5. Interactive Application: I-O Psychology Research Gap Analyzer](#5-interactive-application-i-o-psychology-research-gap-analyzer)**
* **[6. Step-by-Step Google Colab Execution Manual](#6-step-by-step-google-colab-execution-manual)**

---

## 1. Technical Configuration and Dependencies

The execution environment is custom-tailored for Google Colab, orchestrating high-performance Natural Language Processing (NLP) frameworks alongside advanced manifold compression algorithms. 

### Core Package Stack
The pipeline initializes by provisioning specific external computational modules:
* `bertopic`: The modular neural topic modeling framework.
* `openai`: The programmatic gateway to foundational high-dimensional embedding models.
* `umap-learn` & `hdbscan`: Underlying machine learning engines responsible for topological dimensionality compression and density-based hierarchical clustering.
* `python-calamine`: An ultra-fast, Rust-backed Excel parsing engine implemented to accelerate the ingestion of massive `.xlsx` data repositories.

### Colab Graphics Pipeline Configuration
By default, secure cloud container runtime environments restrict inline rendering of complex interactive Plotly widgets. The pipeline explicitly bypasses this restriction by modifying the system rendering pipeline:
```python
from google.colab import output
output.enable_custom_widget_manager()
pio.renderers.default = "colab"
```

This configuration injects pliant widget execution directly into the cell output frames, enabling full, responsive mouse-hover mechanics and dynamic zooming across high-dimensional data atlases.

Cryptographic Credential Management
To maintain robust security standards and adhere to open-science data hygiene rules, the pipeline completely eliminates hardcoded API credentials. It accesses OpenAI's generative endpoints using Colab's native, isolated storage sandbox (userdata Secrets manager):

```python
client = OpenAI(api_key=userdata.get('OPENAI_API_KEY2'))
```

⚠️ CRITICAL REQUIREMENT FOR MODEL SELECTION:
Researchers must provide their own infrastructure API key configured specifically for the language or embedding model they intend to deploy. While the default pipeline uses an OpenAI endpoint calling text-embedding-3-large via the environment variable OPENAI_API_KEY2, any downstream structural alteration to alternative model ecosystems (e.g., switching to Voyage AI, Cohere, Hugging Face, or Anthropic backbones) requires the researcher to provide their corresponding platform developer token.

To implement this locally within the cloud instance, you must manually register your specific API token inside the Google Colab Secrets management panel (indicated by the key icon 🔑 in the left sidebar) before launching execution.


cat << 'EOF' >> foundations/04_topic_modeling/SETUP.md

---

## 2. Pipeline Architecture: Part 1 (BERTopic Core)

The initial phase of the pipeline ingests raw data vectors, cleans text matrices, and structures a highly stable semantic topic representation model.

---

### A. Data Ingestion, Deduplication, and Vector Caching

The pipeline reads the specified spreadsheet source (`dataset_IO.xlsx`), drops rows missing primary narrative text layers (`.notna()`), and enforces hard deduplication across the target column (`06_abstract`). This layout step prevents duplicate publications from artificially warping density clusters during later modeling stages.

Text segments are projected into a continuous semantic field using OpenAI's premier `text-embedding-3-large` engine, outputting a dense 3072-dimensional vector hidden state. Because repeated API queries generate unnecessary financial overhead and processing delays during hyperparameter tuning, the script deploys a local NumPy caching layer:
* **Baseline Execution Run:** Documents are batched (`batch_size = 100`) to respect API throttling boundaries, and the computed matrices are dumped locally as a binary array file (`embeddings_openai_large.npy`).
* **Subsequent Execution Runs:** The pipeline dynamically catches the local `.npy` cache, loading the complete vector space instantly while consuming zero API credits.

> 📋 **IMPORTANT DATASET CUSTOMIZATION NOTE:**
> If you apply this pipeline to a different dataset, you **must rename the corresponding file references and column targets within the script's configuration block**. Ensure that `excel_file`, `target_column`, `title_column`, and `year_column` are explicitly updated to match your new structural spreadsheet schema before starting execution.

---

### B. Hyperparameter Calibration and Academic Noise Mitigation

The underlying modeling layers discard generic defaults, tuning the computational modules specifically for scientific literature landscapes:

* **UMAP Dimensionality Compression:** Calibrated to `n_components=5` to compress data into a low-dimensional manifold optimized for spatial clustering. It leverages the `cosine` distance metric to evaluate vector alignment based entirely on conceptual trajectory, independent of absolute abstract token counts.
* **HDBSCAN Clustering:** Enforces a rigid `min_cluster_size=40` boundary. This parameter ensures that the algorithm captures broad, highly generalized structural disciplines, deliberately suppressing excessive fragmentation into meaningless micro-topics.
* **Targeted Academic Stop-Word Stripping:** Standard NLP stop-word dictionaries successfully drop basic grammatical filler terms (*the, an, of*) but leave common academic jargon completely untouched. This pipeline introduces an explicit `academic_noise` block list targeting high-frequency boilerplate tokens:
  ```python
  ["study", "research", "results", "participants", "analysis", "paper", "support", "model", "theory", "science", "journal", "data", "findings", "abstract", "conclusions", "significant", "associated", "relationship", "effects", "psychology"]


---

## 3. Analytical Visualization Artifacts

Upon model convergence, the script automatically exports the underlying data configurations into 5 distinct, standalone interactive HTML files, providing a comprehensive multi-perspective audit of the research landscape:

* **`4_umap_document_atlas.html` (UMAP Document Atlas):** A comprehensive 2D scatter plot rendering every abstract as an independent coordinate point. The pipeline dynamically maps the text titles (`title_column`) onto the interactive hover traces, allowing researchers to inspect actual paper titles on mouse-over.
* **`1_distance_map.html` (Intertopic Distance Map):** Visualizes discovered topics as dynamic circles scattered across a two-dimensional coordinate space via multi-dimensional scaling. Geodesic distance between circles directly reflects the semantic distinctiveness of their underlying token vectors.
* **`2_hierarchy.html` (Hierarchical Clustering Dendrogram):** Executes hierarchical agglomerative clustering over the calculated c-TF-IDF matrices, outputting a lineage tree that maps exactly how fine-grained thematic facets merge structurally into macro behavioral paradigms.
* **`3_trends.html` (Topics Over Time Dynamic Map):** Ingests chronological metadata (`07_year`), computing local c-TF-IDF frequencies across specific time slices to chart the historical rise, stabilization, or decline of individual themes.
* **`7_topic_word_scores.html` (Topic Word Scores Barchart):** Generates a comprehensive chart plot indexing the top 200 topics, tracking the explicit c-TF-IDF weight distributions for the top 7 words in each cluster to verify word distinctiveness at a glance.

---

### Model Serialization

The complete optimized model parameters are securely serialized and saved locally to the directory `my_stable_model` using the high-performance, tensor-safe **`safetensors`** standard. This preserves the exact state of your c-TF-IDF transformers and clustering topologies for immediate downstream re-loading without risk of code injection.


---

## 4. Advanced Research Gap and Dynamics Analysis: Part 2

The second phase of the architecture implements **Maximal Marginal Relevance (MMR)** set at a diversity index of `0.5` to update the model. MMR optimizes topic descriptions by finding a strict mathematical balance between word relevance to a cluster and diversity relative to already selected terms, systematically stripping out redundant phrase variations.

The algorithm executes an exhaustive multi-dimensional landscape audit, exporting **5 precise empirical Excel reports**:

| Output Data Filename | Algorithmic Logic & Mathematical Foundation | Meta-Research Utility |
| :--- | :--- | :--- |
| `result_1_bottom_up_gaps.xlsx` | **Semantic Noise Isolation (Topic -1):** Extracts all documents rejected by HDBSCAN due to their placement in low-density vector regions. | Identifies unstructured semantic anomalies, surface trends, and pioneering outlier papers operating outside established paradigms. |
| `result_2_isolated_papers.xlsx` | **Threshold-Based Isolation:** Isolates documents that score $\ge 0.99$ on the semantic isolation equation ($1 - \text{max\_prob}$). | Pins down highly unique manuscripts that exhibit virtually zero alignment or statistical affinity with the core corpus clusters. |
| `result_3_relational_gaps.xlsx` | **Inter-Topic Vector Distance Filtering:** Computes an exhaustive cosine similarity matrix across all valid topic cluster centroids, flagging pairs falling beneath a strict $< 0.65$ threshold. | Highlights profound conceptual fractures and missing bridges where two distinct psychological sub-fields fail to communicate. |
| `result_4_temporal_dynamics.xlsx` | **Chronological Pulse Splitting:** Bisects the corpus into two eras based on the dataset's median year, calculating percentage prevalence shifts across the temporal boundary. | Tags flagging, obsolete fields (decline $> 40\%$) and surging, frontier domains (growth $> 40\%$). |
| `result_6_final_labeled_dataset.xlsx` | **Master Labeled Corporate Matrix:** Merges the original data matrix directly with final topic IDs and explicit, human-readable c-TF-IDF keyword strings. | Constructs a fully structured, semantically annotated tabular master sheet ready for immediate downstream statistical testing. |

---

### The Relational Gap Detection Engine

The Relational Gap Detection engine (**Result 3**) evaluates inter-topic connections by mapping the exact dot product of centroid vector Hidden States ($\mathbf{A}$ and $\mathbf{B}$) divided by the product of their Euclidean lengths, formulated as:

$$\text{similarity} = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$

The top 20 most prominent research gaps—representing the lowest mutual similarity scores—are automatically printed directly to the system console for rapid diagnostic evaluation.


