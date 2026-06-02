# 02. Content Validity/Overlap Setup & Execution Manual

---

**Author:** Viktória Gajdošová  
**Last Updated:** June 2026  

---

This module provides three distinct analytical pipelines. Depending on whether you are auditing for validity or redundancy, select the appropriate notebook:

| Notebook | Focus | Method | Colab Link |
| :--- | :--- | :--- | :--- |
| `content_validity_notebook.ipynb` | **Content Validity** | Embedding-based alignment | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1inQUyzOv2h6CMTTgOQIhXW-Ss5GtMBXG#scrollTo=zg05ijvlTX0Z) |
| `content_overlap_prompt_notebook.ipynb` | **Content Overlap** | LLM-based expert judgment | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/17Tgb6oUht12BZbA6cEDTcb_p4z7HY4CK#scrollTo=6GBq11kTVBxg) |
| `content_overlap_embedding_notebook.ipynb` | **Content Overlap** | Embedding-based similarity | [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1oNVLU_uELL6VlQgpCqLPJkHnWFOCMCJe#scrollTo=KI-EMXhzVZpY) |


--- 
# Content Validity: User Guide

This code acts as a **content validator** in a single file. Its goal is to take a list of questionnaire items (e.g., a test for internet gaming disorder) and automatically determine which official diagnostic criteria (DSM-5) each item measures.


## 1. The Core Idea: How it "thinks"
This code uses a **semantic translator** (an embedding model). Every sentence has a hidden mathematical "signature" called an **embedding**—a long list of numbers representing the meaning and context of the words.
* **The Process:** The AI converts both your questionnaire items and the official DSM-5 diagnostic criteria (or whatever criteria you choose) into these lists of numbers. It then uses **Cosine Similarity** (a mathematical way to measure the angle between two lists of numbers) to see which item is "closest" to which diagnostic criterion.
* **The Result:** You get a table showing exactly which diagnostic criterion each item maps to, and how confident the AI is in that mapping.

## 2. How to Set It Up

### A. Platform Selection (Cell 2)
You don't need to be a programmer to use this. You just need to choose your "engine":
* In **CELL 2**, look for the `API_PLATFORM` variable.
* **Default:** It is set to `E5_LOCAL`. This is a free, powerful model that runs directly on your computer (or the Google Colab server) and **requires no API key**.
* **If you want better performance:** You can switch it to `'OPENAI'` or `'GEMINI'`. If you do this, you must store your API key in the Google Colab "Secrets" tab (the key icon on the left sidebar) as `OPENAI_API_KEY` or `GOOGLE_API_KEY`.

### B. Entering Your Data (Cell 3)
Find the section labeled `STEP A: DATA DEFINITION`:
* Look for the `data` dictionary and the `Text_Item` list.
* Simply replace the placeholder strings ("Item number 1", etc.) with your own survey questions. Keep each question inside quotes and separated by commas. Do the same thing with criteria definition.

## 3. Understanding the Outcome
After running the cells (press Shift+Enter on each), the code will print two main tables:

* **Detailed Item Assignment:**
    * **Text_Item:** Your actual survey question.
    * **Best_Match_DSM5:** The number of criterion that the model thinks this item matches best.
    * **Max_Similarity:** A score from 0 to 1. A score of 1 means the item is a perfect semantic match. If this score is very low (e.g., below 0.3), it means your item likely doesn't measure the intended criterion well.
* **Summary Table:**
    * This is your **coverage audit**. It shows the average similarity score for each of the chosem criteria. 
    * If you see a score of `0` for any criterion, it means your questionnaire is **completely missing that diagnostic requirement.**

## 4. Technical Tips for Success
* **GPU Usage:** The code automatically detects if you have a graphics card (GPU) available. You will see a message: `Using device: cuda`. This ensures the math happens in milliseconds rather than seconds.
* **Scientific Rigor:** The code uses `set_all_seeds(42)`. This is a "determinism" setting. It ensures that if you run the code today and then again in a year, you will get the exact same mathematical results, which is vital for scientific studies.
* **Proactive Design:** Instead of waiting to collect data from hundreds of people to see if your items are good, this code allows you to do a "semantic pre-check." If the AI tells you an item doesn't map to your intended diagnostic goal, you can rewrite it before you spend any money or time on human participants.

---




# Content Overlap: LLM-based expert judgment

This tool performs a high-level, expert-grade audit of your questionnaires. While embedding-based similarity (our "quick audit") is great for speed, this **LLM Prompting Method** serves as your "digital clinical supervisor."

## 1. Why use the Prompting Method?
* **Clinical Intelligence:** Unlike simple math (which only sees word similarity), this method evaluates **"Clinical Interchangeability."** It understands if two questions measure the same psychological phenomenon, even if they use completely different words.
* **Structural Critique:** It provides a narrative critique of the content validity gap, unique concepts, and potential redundancies.
* **Why it costs:** This method utilizes advanced reasoning models (like GPT-4o or Gemini 1.5 Pro). Because it requires complex processing to compare full questionnaire sets, it consumes more API tokens and requires a paid account.

## 2. How it works
This code acts as a **Conservative Psychometric Auditor**. 
1. **The Input:** You provide two full sets of questionnaire items.
2. **The Logic:** It doesn't just calculate a score; it performs a qualitative audit, categorizing items into shared themes (e.g., "Withdrawal," "Tolerance") and flagging concepts that are unique to one scale but missing in the other.
3. **The Output:** A strictly formatted **JSON file** containing:
    * `global_similarity_score`: A critical 0–1 score of total overlap.
    * `shared_themes_summary`: An itemized list of how symptoms overlap.
    * `detailed_critique`: An expert summary of the validity gap.

## 3. How to Set It Up
1. **API Setup:** Because this method uses frontier AI, you **must** have an API key. 
   - Store it in the **Secrets** tab of your Colab as `OPENAI_API_KEY` or `GOOGLE_API_KEY`.
2. **Configuration:** 
   - Ensure the `platform` is set to `OPENAI` or `GEMINI`.
   - The code automatically ensures valid JSON output, so your results can be easily saved as a report.

## 4. When to use this vs. Embeddings?
| Method | Speed | Cost | Depth | Best For |
| :--- | :--- | :--- | :--- | :--- |
| **Embeddings** | Instant | Free | Mathematical | Quick scale pruning |
| **LLM Prompting** | Slower | Paid | Expert-Level | Final validation & reports |




# Content Overlap: Embedding-based similarity

This pipeline is designed for **Content Redundancy Analysis**. It compares two entire questionnaires to quantify their "semantic space" overlap, helping you identify redundancy and diagnostic coverage gaps. It works best, when you compare not very complex, nor very abstract items. 



## 1. How it works
This code calculates how well Questionnaire A "covers" the topics in Questionnaire B, and vice versa. It treats this as a bidirectional problem:
* **Directional Coverage:** Determines if Questionnaire A contains everything in Questionnaire B (A covers B) and whether Questionnaire B contains everything in Questionnaire A (B covers A).
* **Unified Overlap Score:** A standardized final metric—a single number representing how identical or redundant the two tools are.

## 2. How to Set It Up
1. **Platform Selection (Cell 2):** - Choose your "engine" by setting the `API_PLATFORM` variable. 
   - `E5_LOCAL` is the default, free model that runs directly in your notebook. 
   - For `OPENAI` or `GEMINI`, ensure your API key is stored in the **Secrets** tab of your Colab (key icon) as `OPENAI_API_KEY` or `GOOGLE_API_KEY2`.
2. **Entering Your Data (Cell 3):**
   - Locate `list_A_items` and `list_B_items`.
   - Replace the placeholder strings with your actual questionnaire items. Keep each item inside quotes and separated by commas.

## 3. Understanding the Outcome
After running the cells, the pipeline will display a semantic audit:
* **Directional Coverage:** Essential for determining which tool is more comprehensive. If A covers B with `0.9` but B covers A with `0.5`, Questionnaire A is significantly more comprehensive.
* **Unified Overlap Score:** Use this number in your research to quantitatively prove the level of redundancy or overlap between existing measures.

## 4. Technical Tips & Best Practices
* **Directional Insight:** Use these scores to identify which questionnaire has more "missing content." This is essential for defending your choice of items in a research paper.
* **The "Scientific" Difference:** By using `cosine_similarity` on high-dimensional vectors, you are moving beyond simple keyword matching. The AI recognizes that words like "sad" and "unhappy" are semantically identical, which is how it detects **Jangle Fallacies** (different labels for the same phenomenon).
* **Proactive Design:** This allows you to do a "semantic pre-check" before collecting data from hundreds of people.

---


