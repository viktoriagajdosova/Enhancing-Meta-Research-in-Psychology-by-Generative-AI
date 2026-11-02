# 03. Open Science Audit
---

**Author:** Viktória Gajdošová  
**Last Updated:** November 2026  

---

## Chapter Roadmap

This module contains an LLM agent that checks whether psychology articles share their data, materials, analysis code, and preregistrations, and whether those resources can actually be opened. It replicates the manual coding scheme of Hardwicke et al. (2024) and compares the agent's output with the human coding of the same articles.

**Whole code can be found here:** 💻 [Google Colab]( https://colab.research.google.com/drive/1WicGmaDaFApfiRWkFQFWrrp2uuTjexxi?usp=sharing)

[![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/viktoriagajdosova/Enhancing-Meta-Research-in-Psychology-by-Generative-AI/blob/main/pipelines/02_topic-modeling/bertopic_meta-research_notebook.ipynb)


## Directory Structure

This sub-folder is organized as a self-contained production environment:

```text
pipelines/03_transparency_audit
├── README.md                          # Module landing page
├── THEORY.md                          # Background, design of the agent, metrics, error analysis
├── SETUP.md                           # Installation and execution manual on Google Colab
├── transparency_agent_notebook.ipynb  # Google Colab notebook that runs the agent
├── guideline_prompt.md                # Full coding instructions given to the model
```
