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

### The Relational Gap Detection Engine

The Relational Gap Detection engine (**Result 3**) evaluates inter-topic connections by mapping the exact dot product of centroid vector Hidden States ($\mathbf{A}$ and $\mathbf{B}$) divided by the product of their Euclidean lengths, formulated as:

$$\text{similarity} = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$

The top 20 most prominent research gaps—representing the lowest mutual similarity scores—are automatically printed directly to the system console for rapid diagnostic evaluation.


This specific module of your script shifts away from pure description and transforms your structural BERTopic mappings into a **methodological detection framework**. Instead of just looking at what topics exist, it treats the continuous vector boundaries and metadata slices as indicators to extract empirical anomalies, structural fractures, and historical shifts across the literature.

Here is a step-by-step technical deconstruction of how this script operates, broken down by its functional components.

---

## 1. Refining Topic Representations (MMR Optimization)

Before running the gap detection, the script executes a post-hoc lexical tuning phase across the active topics:

```python
representation_model = MaximalMarginalRelevance(diversity=0.5)
topic_model.update_topics(
    docs,
    vectorizer_model=CountVectorizer(stop_words=stop_words, ngram_range=(1, 2)),
    representation_model=representation_model
)

```

### The Logic:

* **The Problem:** Class-based TF-IDF (`c-TF-IDF`) can sometimes yield highly redundant keyword descriptors due to morphological variations or local idioms that sneak past standard filters (e.g., `"burnout"`, `"job burnout"`, `"burnout syndrome"`).
* **The Resolution:** **Maximal Marginal Relevance (MMR)** balances word relevance to a cluster against its phrase diversity relative to words already selected. Setting a diversity index of `0.5` ensures that the 10 descriptive keywords assigned to define your topics capture distinctly different facets of the concept, stripping out lexical overlap to maximize immediate human interpretability.

---

## 2. Bottom-Up Discovery: Unclustered Noise Isolation

```python
gaps_df = df[df['Topic_ID'] == -1].copy()
gaps_df.to_excel("result_1_bottom_up_gaps.xlsx", index=False)

```

### The Logic:

* When HDBSCAN models low-dimensional manifolds, it computes dense spatial hulls. Points situated outside stable density fields are flagged as **Semantic Noise (`Topic -1`)** and left unassigned.
* In traditional modeling, this is viewed as a waste container. In **meta-research**, however, this is a vital exploratory dataset. By exporting these unclustered items to `result_1_bottom_up_gaps.xlsx`, the script isolates manuscripts that deviate from mainstream academic paradigms—representing either highly unaligned, innovative cross-disciplinary studies or unstructured methodological anomalies.

---

## 3. Threshold-Based Semantic Isolation

```python
max_probs = np.max(probs, axis=1) if len(probs.shape) > 1 else probs
df['Isolation_Score'] = 1 - max_probs
df_isolated = df[df['Isolation_Score'] >= iso_threshold].copy()

```

### The Logic:

* If cluster probabilities are enabled during the initial model configuration, `probs` stores the probability vectors of a document belonging to every discovered topic.
* The script calculates a definitive **Isolation Score** formulated as:

$$1 - \max(\text{probabilities})$$


* If a document exhibits a maximum topic assignment probability of near zero, its isolation score scales toward `1.0`. By locking down an absolute threshold restriction of $\ge 0.99$, `result_2_isolated_papers.xlsx` extracts extreme conceptual outliers—papers that are mathematically distinct from the thematic clusters of the core corpus.

---

## 4. Relational Gaps: Inter-Topic Vector Distance Filtering

This is the core mathematical engine of your gap analysis, identifying where active research sub-fields fail to communicate or establish cross-references.

```python
valid_embeddings = [topic_model.topic_embeddings_[i] for i in valid_indices]
sim_matrix = cosine_similarity(valid_embeddings)

```

### The Logic:

1. **Centroid Isolation:** The script extracts the structural vector hidden states (`topic_embeddings_`) for every valid topic cluster, completely ignoring the noise partition (`-1`). These vectors represent the semantic average position (the centroid) of that topic's most representative papers within the 3072-dimensional vector space.
2. **The Cosine Pass:** It executes an exhaustive combinatorial comparison pass across the centroids using **cosine similarity**:

$$\text{similarity}(A, B) = \frac{\mathbf{A} \cdot \mathbf{B}}{\|\mathbf{A}\| \|\mathbf{B}\|}$$


3. **Inverse Threshold Filtering:** Standard search systems look for *high* cosine similarity scores to group data. This script intentionally implements an inverse loop—filtering for pairs that drop below a strict threshold boundary of **$< 0.65$**.
4. **Ascending Order Sorting:** The script records these weak linkages and sorts them from lowest similarity to highest. The pairs at the absolute top of `result_3_relational_gaps.xlsx` represent profound **Structural Fractures** in the literature—two topics that are actively published but remain highly disconnected in semantic trajectory.

---

## 5. Temporal Dynamics: Pulse of the Field

```python
median_year = df[year_column].median()
era1_counts = df[df[year_column] <= median_year].groupby('Topic_ID').size()
era2_counts = df[df[year_column] > median_year].groupby('Topic_ID').size()

```

### The Logic:

Instead of forcing a complex continuous regression curve across a sparse time series, the script applies an empirical **Chronological Bisection**:

* It isolates the absolute **median publication year** across the corpus and uses this marker to bisect the entire document dataset into two chronological eras: *Era 1 (Historical Baseline)* and *Era 2 (Contemporary Horizon)*.
* It tabulates topic counts across the eras and computes a definitive velocity percentage change metric:

$$\Delta \% = \frac{\text{Count}_{\text{Era 2}} - \text{Count}_{\text{Era 1}}}{\text{Count}_{\text{Era 1}}} \times 100$$


* It applies a rigid three-tier diagnostic status categorization block:
* **$\Delta \% < -40\%$:** Tagged as 📉 `DECLINING (Temporal Gap)`. These themes represent losing traction or fading theoretical paradigms.
* **$\Delta \% > 40\%$:** Tagged as 🔥 `EMERGING (Hot Topic)`. These clusters capture surging research trends or contemporary paradigm shifts.
* **Otherwise:** Tagged as ⚖️ `STABLE`. This output maps out standard, consistently sustained structural pillars of the field.



---

## 6. Master Labeled Dataset Compilation

```python
final_df = df.merge(topic_info, left_on='Topic_ID', right_on='Topic', how='left')
final_df.to_excel("result_6_final_labeled_dataset.xlsx", index=False)

```

### The Logic:

The code concludes by joining your raw tabular input data with your newly generated spatial parameters. It maps the internal integer `Topic_ID` assignments directly against their human-readable c-TF-IDF keyword descriptive headers.

The resulting file (`result_6_final_labeled_dataset.xlsx`) acts as a fully sémancally annotated Master Corporate Matrix. Every abstract is cleanly labeled with its exact thematic family, providing an empirical foundation ready for immediate ingestion into secondary statistical testing blocks or regression models.
---


## 5. Interactive Application: I-O Psychology Research Gap Analyzer

This final block of your pipeline transforms your static, trained topic model into an **interactive, real-time diagnostic engine**. Instead of forcing you to wade through massive spreadsheets to see if an emerging construct is present in your literature corpus, this code functions as an automated probe. It allows you to query any arbitrary text string or theoretical construct, projects it into your exact latent space, and flags whether it represents an established discourse or a genuine research gap.

Here is the structured technical deconstruction of how this interactive engine runs under the hood.

---

## 1. Interface Layer & State Initialization

```python
history_log = []
header = widgets.HTML("<h2>🔍 I-O Psychology Topic Probe</h2>...")
text_input = widgets.Text(placeholder='e.g., Resilience, Care Economy...')
analyze_btn = widgets.Button(description='Analyze Topic Alignment', button_style='success')
output_area = widgets.Output()

```

### The Logic:

* The application builds an inline graphical user interface (GUI) inside the notebook by leveraging **`ipywidgets`**.
* It instantiates a stateless list (`history_log`) to track user interactions across the session, configures HTML descriptors, provides a string parsing input box (`text_input`), and binds execution buttons.
* The **`widgets.Output()`** layer acts as a isolated, responsive sub-canvas. It allows the script to clear and re-render complex plaintext prints and metrics dynamically within a designated cell container without distorting the rest of your notebook's visual layout.

---

## 2. Real-Time Vector Proving (Stage 2)

Once the user inputs a construct (e.g., *"Algorithmic Management Overload"*) and triggers the green analysis button, the backend initializes data ingestion and maps the new term onto your exact model coordinate rules:

```python
client = OpenAI(api_key=userdata.get('OPENAI_API_KEY2'))
res = client.embeddings.create(input=[concept], model="text-embedding-3-large")
concept_vec = np.array(res.data[0].embedding).reshape(1, -1)

```

### The Logic:

To evaluate spatial alignment accurately, the target concept must be measured using the exact same measuring stick as your baseline dataset. The code hits the OpenAI API to extract a dense **`text-embedding-3-large`** vector footprint. Reshaping the output matrix via `.reshape(1, -1)` transforms the native array into a 2D row tensor ($1 \times 3072$), satisfying the mathematical input expectations of `scikit-learn`'s vector distance functions.

---

## 3. Macro Thematic Alignment Pass (Stage 3)

The script computes how closely your new concept fits into the broader topics discovered by your stabilized BERTopic model:

```python
tm = BERTopic.load(CONFIG["model"])
topic_embeddings = np.array(tm.topic_embeddings_)
topic_sims = cosine_similarity(concept_vec, topic_embeddings).flatten()
best_topic_idx = np.argmax(topic_sims)

```

### The Logic:

1. **Centroid Matrix Retrieval:** The code reloads your pre-compiled model configuration (`my_stable_model`) to extract the exact spatial positions of your topic centroids (`topic_embeddings_`).
2. **Global Proximity Pass:** It executes a pairwise **cosine similarity** comparison, evaluating your single concept vector against *every single topic centroid* simultaneously. Flattening the output vector transforms the result into a clean, one-dimensional array of similarity scalars (`topic_sims`).
3. **Maximum Probability Selection:** By applying **`np.argmax()`**, the engine isolates the absolute index position of the highest similarity score. This step programmatically flags the single closest semantic topic matched to your query string.

---

## 4. Threshold Interpretation Rule Matrix (Stage 4)

The script maps the raw maximum scalar cosine score onto a definitive three-tiered methodological decision matrix:

```python
if overall_alignment_score < 0.30:
    verdict, color = "CONFIRMED LATENT GAP", "🚨"
elif 0.30 <= overall_alignment_score < 0.40:
    verdict, color = "MINIMAL REPRESENTATION", "🟡"
else:
    verdict, color = "ESTABLISHED DISCOURSE", "✅"

```

### The Logic:

* **`🚨 CONFIRMED LATENT GAP` ($< 0.30$):** The vector path of your concept sits at a sharp angle away from every established cluster centroid in the model. This mathematically proves that the construct represents a completely unaddressed theme or a major blind spot within your literature corpus.
* **`🟡 MINIMAL REPRESENTATION` ($0.30 \le \text{Score} < 0.40$):** The construct is within striking distance of an existing topic field, but its vector alignment is too weak to signal mature thematic integration. This means it is marginally mentioned or hovering on the periphery of the domain.
* **`✅ ESTABLISHED DISCOURSE` ($\ge 0.40$):** The concept aligns cleanly with an active, robust cluster density field. This indicates that the construct is already a well-documented element of mainstream scientific discussion.

---

## 5. Granular Source Verification (Stage 5)

To protect your analysis against abstract model misclassifications, the engine switches from macro topic centroids down to a micro **document-level literature verification check**:

```python
doc_sims = cosine_similarity(concept_vec, embeddings_internal).flatten()
top_indices = doc_sims.argsort()[-10:][::-1]

```

### The Logic:

1. **Document-Level Similarity Pass:** The engine computes the absolute cosine similarity between your new concept vector and *every individual document embedding matrix* cached during your Stage 1 data run (`embeddings_openai_large.npy`).
2. **Ordinal Sort via Argsort:** Calling **`.argsort()[-10:][::-1]`** performs an optimized sequence extraction. It sorts document similarities in ascending order, extracts the indices of the top 10 values, and reverses the slice array to sort them in descending order (highest similarity first).
3. **Dynamic Metadata Extraction:** The script scans the Excel corpus using a generator expression to dynamically locate column headers containing identifiers like title, year, or DOI, neutralizing the risk of code crashes if your raw dataset alters its column indexing schemas. It loops through the extracted indices to print the exact year, title, precise document similarity score, and **DOI link** for immediate academic verification.

---

## 6. Historical Logging and Spreadsheet Export

```python
history_log.append({ ... })
export_btn.on_click(lambda b: pd.DataFrame(history_log).to_excel("rq4_alignment_summary.xlsx", index=False))

```

### The Logic:

Every evaluated concept string, matched topic name, scalar similarity calculation, and diagnostic verdict is cleanly structured as a dictionary block and appended to your running session cache (`history_log`).

Clicking the blue *Export Results* button invokes an inline lambda expression function. This dynamically reads your running cache list, builds a clean Pandas DataFrame configuration, and dumps your entire research exploration log out into an organized Excel spreadsheet named **`rq4_alignment_summary.xlsx`**. This step provides you with a clear audit trail tracking every construct you tested during your gap exploration sessions.

---

### 💡 Execution Note for Google Colab

To run this application successfully, you must execute the script block directly inside a notebook cell. The final line of code:

```python
display(header, widgets.VBox([text_input, widgets.HBox([analyze_btn, export_btn])]), output_area)

```

orchestrates the hierarchical visual stacking of the widgets and pipes them directly into the browser display framework, activating the live UI right below your code cell.


   
---
## 6. Step-by-Step Google Colab Execution Manual

To ensure a flawless runtime execution cycle within Google Colab without encountering environment corruption, missing compilation variables, or credential leakage, adhere strictly to the following sequential protocol:

### Step 1: Provision Cloud Compute Runtime
1. Open a clean Google Colab notebook instance.
2. Navigate to the top application menu and click **Runtime -> Change runtime type**.
3. Under the **Hardware accelerator** dropdown, select **T4 GPU** (or any available high-performance hardware accelerator) and click **Save**.

> 💡 **Why GPU Acceleration?** While the initial text embedding step requests vector generation remotely from OpenAI's API endpoints, local downstream manifold calculations executed by UMAP and density-based clustering via HDBSCAN require parallel processing capabilities to maintain efficient wall-clock execution times.

### Step 2: Configure Cryptographic Secrets
1. Navigate to the left-hand sidebar menu in Colab and click the **Secrets** panel (represented by the key icon 🔑).
2. Click **Add new secret** and create a variable with the exact name: `OPENAI_API_KEY2`.
3. Paste your active developer token into the **Value** input box.
4. Toggle the **Notebook access** switch next to the variable to the **ON** position to grant your execution runtime secure permission to inherit the credential.

### Step 3: Ingest Data Repository Files
1. Click the **Files** folder icon in the left-hand sidebar menu.
2. Drag and drop your raw spreadsheet data file (e.g., `dataset_IO.xlsx`) directly into the root storage drawer container (`/content/`).
3. Verify that the file name and internal column labels align precisely with the parameters defined in your script's configuration block (`target_column`, `title_column`, `year_column`).

### Step 4: Execute Initial Dependency Assembly
Instantiate a clean code cell at the absolute top of your notebook, paste the following shell command, and launch execution to compile the required software architecture:

```bash
!pip install bertopic openai umap-learn hdbscan pandas numpy python-calamine
```

⚠️ CRITICAL METASCIENCE BEST PRACTICE:
Immediately after the package installer routine successfully concludes, you must completely restart the active notebook session. Navigate to the top menu and select Runtime -> Restart session (or use the shortcut Ctrl+M .). This step forces the Python compiler environment to cleanly load the newly compiled underlying C++ matrix headers for HDBSCAN, preventing downstream segmentation faults.
