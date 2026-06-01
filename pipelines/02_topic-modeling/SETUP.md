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
