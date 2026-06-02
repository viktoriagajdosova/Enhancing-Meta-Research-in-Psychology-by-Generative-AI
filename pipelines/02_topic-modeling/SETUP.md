# 02. Topic Modeling Setup & Execution Manual

---

**Author:** Viktória Gajdošová  
**Last Updated:** June 2026  

---

## Technical Environment Overview

This setup manual guides you through configuring your computational environment to execute the topic modeling workflows provided in this module.

**Whole code can be found here:** 💻 [Google Colab](https://colab.research.google.com/drive/1yTRo4xLimRikVyykBknLrWnhL5hA4Duz?usp=sharing)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/viktoriagajdosova/Enhancing-Meta-Research-in-Psychology-by-Generative-AI/blob/main/pipelines/02_topic-modeling/bertopic_meta-research_notebook.ipynb)

> **Important Customization Note:** The code repositories and pipelines included in this folder (`bertopic_meta-research_notebook.ipynb`) have been explicitly adapted, customized, and pre-configured for **psychological meta-research**. 

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

### Cryptographic Credential Management
To maintain robust security standards and adhere to open-science data hygiene rules, the pipeline completely eliminates hardcoded API credentials. It accesses OpenAI's generative endpoints using Colab's native, isolated storage sandbox (userdata Secrets manager):

```python
client = OpenAI(api_key=userdata.get('OPENAI_API_KEY2'))
```

> ⚠️ **CRITICAL REQUIREMENT FOR MODEL SELECTION:**
> Researchers must provide their own infrastructure API key configured specifically for the language or embedding model they intend to deploy. While the default pipeline uses an OpenAI endpoint calling text-embedding-3-large via the environment variable OPENAI_API_KEY2, any downstream structural alteration to alternative model ecosystems (e.g., switching to Voyage AI, Cohere, Hugging Face, or Anthropic backbones) requires the researcher to provide their corresponding platform developer token.

To implement this locally within the cloud instance, you must manually register your specific API token inside the Google Colab Secrets management panel (indicated by the key icon 🔑 in the left sidebar) before launching execution.


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
| `result_2_isolated_papers.xlsx` | **Threshold-Based Isolation:** Isolates documents with a semantic isolation score of $\ge 0.99$ | Pins down highly unique manuscripts that exhibit virtually zero alignment or statistical affinity with the core corpus clusters. |
| `result_3_relational_gaps.xlsx` | **Inter-Topic Vector Distance Filtering:** Computes an exhaustive cosine similarity matrix across all valid topic cluster centroids, flagging pairs falling beneath a strict $< 0.65$ threshold. | Highlights profound conceptual fractures and missing bridges where two distinct psychological sub-fields fail to communicate. |
| `result_4_temporal_dynamics.xlsx` | **Chronological Pulse Splitting:** Bisects the corpus into two eras based on the dataset's median year, calculating percentage prevalence shifts across the temporal boundary. | Tags flagging, obsolete fields (decline $> 40\%$) and surging, frontier domains (growth $> 40\%$). |
| `result_6_final_labeled_dataset.xlsx` | **Master Labeled Corporate Matrix:** Merges the original data matrix directly with final topic IDs and explicit, human-readable c-TF-IDF keyword strings. | Constructs a fully structured, semantically annotated tabular master sheet ready for immediate downstream statistical testing. |

---

## 4. Advanced Research Gap and Dynamics Analysis: Part 2

The second phase of the pipeline moves beyond simple thematic description. It transforms your BERTopic results into a **Methodological Detection Framework**. Instead of just identifying "what topics exist," this module treats your topic clusters as nodes in a network, allowing you to mathematically pinpoint conceptual fractures, historical shifts, and empirical anomalies in your field.

---

### 4.1 Refining Topic Representations (MMR Optimization)

Standard keyword lists often suffer from redundancy (e.g., `"burnout"`, `"job burnout"`, and `"burnout syndrome"` all appearing as separate top keywords). The script uses **Maximal Marginal Relevance (MMR)** to clean this up.

* **Psychological Analogy:** Think of MMR as an automated "item-pool pruning" process. It calculates a balance between *Relevance* (how well a keyword describes a topic) and *Diversity* (how distinct it is from keywords already chosen).
* **The Result:** By setting a diversity index of `0.5`, the model ensures that the keywords assigned to a topic capture distinctly different facets of the concept, stripping away redundant synonyms and maximizing the clarity of your final thematic labels.

---

### 4.2 Semantic Noise Isolation (Topic -1)

HDBSCAN naturally rejects documents that don't fit into stable density clusters, dumping them into `Topic -1`.

* **The Logic:** In standard data cleaning, this is "trash." In **Meta-Research**, this is a vital exploratory dataset.
* **Research Utility:** By exporting these documents to `result_1_bottom_up_gaps.xlsx`, you isolate manuscripts that deviate from the mainstream academic paradigm. These are often your most innovative, cross-disciplinary, or highly specific "outlier" papers that define the bleeding edge of the field.

---

### 4.3 Threshold-Based Semantic Isolation

This function calculates an **Isolation Score** for every paper:


$$\text{Score} = 1 - \max(\text{Probability})$$

* **Psychological Analogy:** If a paper has an isolation score $\ge 0.99$, it means the algorithm is "confused" by it—it doesn't belong to *any* major theme identified in your dataset.
* **Research Utility:** This allows you to pinpoint unique manuscripts that exhibit virtually zero statistical affinity with your core corpus. These are often the "lone wolf" papers that may be tackling a construct that is currently ignored by the rest of the literature.

---

### 4.4 Relational Gaps: Inter-Topic Vector Distance Filtering

This is the "engine room" of the gap analysis. It identifies sub-fields that are active but structurally disconnected.

* **The Logic:** The model computes the **Cosine Similarity** between every pair of topic centroids:

$$\text{similarity} = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$


* **Finding the Gap:** While most search tools look for *high* similarity to find "related" work, this engine filters for **low** similarity ($< 0.65$).
* **Research Utility:** Pairs of topics with very low similarity scores represent a **Structural Fracture**. For example, if the engine flags a massive gap between *"Statistical Validation Frameworks"* and *"Cross-Cultural Adaptation Methods,"* it provides you with empirical evidence that two vital sub-fields are failing to communicate. You have successfully mapped a "missing bridge" in your field.

---

### 4.5 Temporal Dynamics: The "Pulse" of the Field

* **The Logic:** It splits your entire dataset into two halves based on the median publication year. It then tracks how the prevalence of every topic shifts across these two eras using the formula:

$$\Delta \% = \frac{\text{Count}_{\text{Era 2}} - \text{Count}_{\text{Era 1}}}{\text{Count}_{\text{Era 1}}} \times 100$$

$$Δ% = ((Count_Era2 - Count_Era1) / Count_Era1) * 100$$



* **The Diagnostic Categorization:**
* **📉 Declining (Temporal Gap):** Themes with a decline $> 40\%$. These represent fading theoretical paradigms or obsolete research questions.
* **🔥 Emerging (Hot Topic):** Themes with a growth $> 40\%$. These are your "frontier domains"—the rapidly accelerating areas where the field is currently concentrating its attention.
* **⚖️ Stable:** Themes that remain consistent pillars of the literature.



---

### 4.6 Master Labeled Dataset Compilation

The final step merges your original data with the model's findings, outputting `result_6_final_labeled_dataset.xlsx`.

* **Why this matters:** You now have a fully structured, semantically annotated "Master Matrix" where every single abstract in your literature review is tagged with its formal topic ID and human-readable keyword string. This file is ready for immediate ingestion into SPSS, R, or JASP for your final hypothesis testing or qualitative report writing.


---



## 5. Interactive Application: I-O Psychology Research Gap Analyzer

This final module transforms your static model into an **interactive diagnostic probe**. Instead of manually searching through thousands of rows in a spreadsheet, this interface allows you to query any arbitrary theoretical construct (e.g., *"Algorithmic Management Overload"*) and instantly see if it exists as an **Established Discourse** or a **Latent Research Gap** within your dataset.

---

### 1. User Interface & State Initialization

The engine uses **`ipywidgets`** to build a clean control panel directly inside your notebook.

* **The Psychology Perspective:** Think of this as your "Lab Control Panel." You provide a concept, and the system instantly tells you where it sits on the field’s "map." The `output_area` keeps your results organized, so you can test dozens of hypotheses without cluttering your notebook.

---

### 2. Real-Time Vector Proving (The "Semantic Translator")

When you type a construct and click **Analyze**, the script uses the same engine that indexed your literature to "understand" your query.

* **The Logic:** It sends your text to OpenAI to convert it into a 3,072-dimensional vector.
* **Why it works:** Because your literature was indexed using this exact same engine, your query and your literature now "speak the same mathematical language." It allows the model to calculate how close your new idea is to the existing body of work.

---

### 3. Macro Thematic Alignment Pass (The "Proximity Audit")

The system automatically compares your query vector against your model’s pre-trained **Topic Centroids**.

* **The Logic:** A centroid is the "geometric center" of a theme. By calculating the **Cosine Similarity** between your query and these centers, the model identifies the single most relevant existing topic.
* **The Psychology Perspective:** This is an automated literature search. It tells you: *"If this topic were a paper, it would be most similar to the research being done in [Topic Name]."*

---

### 4. Diagnostic Verdict Matrix (The "Evidence-Based Decision")

The app doesn't just give you a similarity score; it interprets the statistical significance of that score for your research design:

| Status | Threshold | Interpretation |
| --- | --- | --- |
| 🚨 **Confirmed Latent Gap** | $< 0.30$ | The construct is geographically isolated from your literature. You have found a **genuine research void**. |
| 🟡 **Minimal Representation** | $0.30 - 0.40$ | The construct is marginally touched upon, but lacks structural development in your dataset. |
| ✅ **Established Discourse** | $\ge 0.40$ | The construct aligns clearly with active research. You are working within an **existing paradigm**. |

---

### 5. Granular Source Verification (The "Reality Check")

To ensure the machine isn't hallucinating, the engine performs a secondary audit at the document level.

* **How it works:** It ignores the clusters and compares your query against **every single individual abstract** in your dataset.
* **The Result:** It prints the Top 10 most similar papers, including their **DOI** and **Year of Publication**.
* **Why it matters:** This allows you to perform an immediate "sanity check." You can click the DOI and read the top papers to verify if the model is correctly identifying the construct you are probing.

---

### 6. Historical Logging & Empirical Audit Trail

Every time you perform an analysis, the app logs your query, the alignment score, and your diagnostic verdict into a session history.

* **Research Utility:** With one click, you can export this session as `rq4_alignment_summary.xlsx`. This serves as an **audit trail of your investigation**—useful if you need to defend your selection of a research gap during your dissertation defense or when preparing an empirical justification for your research questions.

---

> **Pro-Tip:** Run this tool for every hypothetical research question you are considering. If you find a "Confirmed Latent Gap" ($< 0.30$) with a high-quality literature set, you have found strong empirical grounds to justify a novel research study.

---

### 💡 Execution Note for Google Colab

To run this application successfully, you must execute the script block directly inside a notebook cell. The final line of code:

```python
display(header, widgets.VBox([text_input, widgets.HBox([analyze_btn, export_btn])]), output_area)

```

orchestrates the hierarchical visual stacking of the widgets and pipes them directly into the browser display framework, activating the live UI right below your code cell.


   
---

## 6. Step-by-Step Google Colab Execution Manual

To guarantee a successful, error-free execution of this pipeline, follow this protocol. We have designed this sequence to ensure your environment is "clean" before the heavy statistical modeling begins.

---

### Step 1: Prepare the Cloud Laboratory

1. **Launch:** Open a fresh Google Colab notebook instance.
2. **Assign Computing Power:** Navigate to the top menu, select **Runtime -> Change runtime type**.
3. **Select Hardware:** In the **Hardware accelerator** dropdown, select **T4 GPU** (or any available GPU) and click **Save**.

> 💡 **Why this matters:** While your data is processed by OpenAI's servers, the complex spatial modeling (UMAP and HDBSCAN) happens on your machine. Using a GPU acts like a powerful research assistant, reducing a 20-minute wait time down to a few seconds.

---

### Step 2: Secure Your Research Credentials

We never hard-code your private keys into the script. Instead, we use Google’s secure "Vault."

1. Look for the **Key icon (🔑)** in the vertical sidebar on the left of your Colab screen. This is the **Secrets** panel.
2. Click **Add new secret**.
3. **Name:** Enter exactly `OPENAI_API_KEY2` (the code looks specifically for this name).
4. **Value:** Paste your OpenAI API token.
5. **Permissions:** Toggle the **Notebook access** switch to **ON**. This grants your notebook permission to "read" the key without ever displaying it in your code cells.

---

### Step 3: Import Your Data

1. Click the **Folder icon (📁)** in the left sidebar to open the file drawer.
2. Drag and drop your source file (e.g., `dataset_IO.xlsx`) from your local computer into the `/content/` area.
3. **Verification:** Ensure your Excel file contains the exact column names specified in the script's configuration (e.g., `06_abstract`, `03_title`, `07_year`). If the script can't find a column, it will stop and notify you—a simple renaming of your Excel headers is usually all that’s needed.

---

### Step 4: Assemble the Tooling & "Refresh" the Lab

Before you can run the model, you need to install the specialized computational libraries.

1. Create a new code cell at the very top of your notebook.
2. Paste the following command and hit the **Play** button:
```bash
!pip install bertopic openai umap-learn hdbscan pandas numpy python-calamine

```



> ⚠️ **THE CRITICAL RESTART:** > Once the installation finishes, **you must restart the session.** Go to **Runtime -> Restart session** (or `Ctrl+M .`).
> *Why?* Installing these libraries adds new C++ system components that the Python environment cannot "see" until it is forced to reboot. If you skip this, the model will likely crash with a "segmentation fault." Restarting ensures the lab bench is clean and ready for work.

---

### Step 5: Execute Core Model Pipeline (Part 1)

1. Paste the **PART 1: BERTopic** code block into a new cell.
2. Run the cell. The console will report the progress of embedding extraction.
3. **What to expect:** You will see interactive maps (the UMAP Atlas, Intertopic Distance Map) render directly inside the notebook.
4. **Final Check:** Look at your file drawer. You should see a new folder named `my_stable_model` and a file called `embeddings_openai_large.npy`. These indicate your model has been saved successfully for future use.

---

### Step 6: Trigger the Research Gap Audit (Part 2)

1. Create a new cell, paste **PART 2: ADVANCED RESEARCH GAP ANALYSIS**, and execute.
2. This is your "analytical audit." It ignores the visual maps and focuses on the underlying Excel data.
3. **Check your File Drawer:** Refresh the file list (click the ⟳ icon in the drawer). You will see the five generated Excel reports (`result_1` through `result_6`). Download these by clicking the three dots next to the file names.

---

### Step 7: Launch the Research Gap Analyzer (Part 3)

1. Paste the **PART 3: APP** code block into a final cell and execute it.
2. A custom graphical interface will appear directly below the cell.
3. **How to use it:** Type a concept (like "Emotional Intelligence" or "Technostress") into the box and click **Analyze Topic Alignment**.
4. The tool will instantly provide a diagnostic (🚨 Gap, 🟡 Minimal, or ✅ Established) and pull the Top 10 most relevant abstracts from your dataset, complete with **DOI links** for your rapid literature review.
