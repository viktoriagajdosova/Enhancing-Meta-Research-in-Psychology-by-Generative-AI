# 01. Embeddings for Psychometrics Foundations
---

**Author:** Viktória Gajdošová  
**Last Updated:** June 2026  

---

## Chapter Roadmap

This chapter provides the theoretical, mathematical, and algorithmic foundations necessary for grounding embedding-based psychometric validation within modern behavioral science. It is structured into the following sections:

* **[1. Problems in Psychometrics](#1-problems-in-psychometrics)**
* **[2. Psychometric Constructs](#2-psychometric-constructs)**
* **[3. Current Research: Integrating LLMs and Embeddings](#3-current-research-integrating-llms-and-embeddings)**
* **[4. Content Validity](#4-content-validity)**
* **[5. Content Overlap](#5-content-overlap)**
* **[6. Application](#6-application)**

---

# 1. Problems in Psychometrics

Psychological science currently faces a foundational crisis characterized by fragmentation, measurement proliferation, and a reliance on Questionable Research Fundamentals (QRFs).

## 1.1 The "Toothbrush Problem" and Fragmentation
Psychology struggles with the "toothbrush problem"—the tendency for researchers to avoid using existing measures, preferring to create their own ad-hoc versions.
* **Fragmentation Drivers:** A lack of barriers to introducing new terms and an incentive structure favoring "novel" constructs over the refinement of existing ones.
* **Research Silos:** With ~79% of constructs not reused more than twice, the literature is deeply fragmented, making it nearly impossible to aggregate evidence.

## 1.2 The Jingle-Jangle Fallacy
This proliferation fuels two primary conceptual errors:
* **Jingle Fallacy:** Assuming two different measures are the same because they share the same name.
* **Jangle Fallacy:** Assuming two identical phenomena are different because they have different names (e.g., "grit" vs. "conscientiousness").

## 1.3 Statistics vs. Measurement: The QRF Crisis
A foundational critique argues that psychology’s "replication crisis" is actually a crisis of QRFs, where researchers mistake statistical regularities for evidence of measurement.
* **The "Lingometrics" Problem:** Semantic algorithms can predict between-item correlations and human response patterns with up to 90% accuracy based solely on text, suggesting psychometric data often measures "lingometrics" (internal language structure) rather than the actual psychological state.
* **The "42% Solution":** Findings claiming to "discover" relationships between variables often simply discover pre-existing semantic overlap built into word definitions.
* **Ontological vs. Epistemological Error:** Researchers frequently mistake their own linguistic descriptions for the phenomena themselves, leading to "pseudo-empirical" research.

## 1.4 Foundational Critiques
* **The Ergodic Fallacy:** Sample-level group averages are often mathematically incorrectly applied to individual-level processes, as study phenomena are non-ergodic.
* **The Modeling Relation:** Psychometric work often neglects the traceable empirical interaction between a research object and a calibrated instrument, focusing only on formal statistical manipulation.

## 1.5 Proposed Pathways Forward
* **SOBER Guidelines:** Authors must demonstrate non-redundancy with existing measures and adhere to established protocols.
* **Respectful Operationalism (RO):** A middle ground focusing on utility by acknowledging constructs as narrowly defined by their specific measures.
* **Semantic Landscape Mapping:** Using LLM embeddings to identify clusters of similar items, allowing for systematic pruning of redundant constructs into a parsimonious taxonomy.
* **Methodological Rigor in LLMs:** To ensure replicability, researchers must use seed parameters, document model versions, and prioritize local, stable open-source models (e.g., Llama) over nondeterministic proprietary ones.

---

# 2. Psychometric Constructs

Psychometrics is the field concerned with the scientific measurement of psychological and educational attributes, applying technical, mathematical, and statistical principles to ensure accurate information about individuals and groups.

## 2.1 Foundational Principles
The development and evaluation of tests rest on three essential pillars:
* **Validity**: The degree to which theory and evidence support the intended interpretations of test scores for specific uses. It is the most fundamental consideration in psychometrics, focusing on the inferences drawn rather than the test itself.
* **Reliability/Precision**: The consistency of scores across different replications (e.g., different forms, occasions, or raters), indicating the influence of random measurement errors.
* **Fairness**: A fundamental aspect of validity ensuring that interpretations are valid for all relevant subgroups and are not compromised by characteristics unrelated to the measured construct.

## 2.2 Measurement Models
Psychometricians utilize specific mathematical frameworks to interpret results:
* **Classical Test Theory (CTT)**: Conceptualizes an observed score as the sum of a hypothetical error-free "true score" and random measurement error.
* **Item Response Theory (IRT)**: Models the relationship between a test taker's ability and their performance on specific items.
* **Generalizability Theory (G Theory)**: Analyzes specific sources of error to evaluate test consistency.

## 2.3 Item and Test Properties
Accurate measurement requires establishing specifications for items, including:
* **Difficulty**: The ease or hardness of an item for the target population.
* **Discrimination**: The ability of an item to distinguish between test takers with different levels of the measured trait.
* **Inter-item correlations**: The relationships between individual items within a test.

## 2.4 Inherent Challenges and Threats
The accuracy and fairness of tests can be compromised by several systemic issues:

### Threats to Validity
* **Construct Underrepresentation**: The test fails to capture important aspects of the intended construct.
* **Construct-Irrelevant Variance**: Scores are affected by extraneous factors (e.g., reading skills in a math test).

### Sources of Measurement Error (Reliability)
* **Internal Fluctuations**: Changes in a test taker’s motivation, attention, or application of skills.
* **External Variations**: Inconsistent testing conditions (e.g., noise) or subjectivity among scorers.

### Threats to Fairness
* **Measurement Bias**: Characteristics resulting in different score meanings across subgroups, such as Differential Item Functioning (DIF).
* **Accessibility Barriers**: Physical disabilities or language proficiency issues that obstruct the opportunity to demonstrate true standing on a construct.
* **Lack of Opportunity to Learn**: Holding individuals accountable for content they were never taught.

### Limitations of Frameworks
* Frameworks like IRT rely on strong assumptions (e.g., unidimensionality), and if data fails to fit these, indices may be invalid. Similarly, G Theory can be difficult to implement due to the extensive studies required to isolate all potential sources of variation.

---

# 3. Current Research: Integrating LLMs and Embeddings

The integration of Large Language Models (LLMs) and semantic embeddings into psychometrics has transitioned from experimental curiosity to a robust methodological toolkit. The research is currently structured across several key application domains:

## 3.1 Automated Item Generation and Evaluation
* **Computerized Adaptive Testing (CAT):** Research by Gao et al. demonstrates that LLMs (GPT, Claude, ERNIE) can generate high-quality items for Big Five personality inventories with marginal reliability exceeding .97.
* **Multi-Agent Systems:** Lee et al. (2026) introduced LM-AIG, a system where collaborative agents (Item Writer vs. Reviewer Agents) evaluate content relevance and bias, outperforming human-generated items in preliminary tests.
* **Low-Cost Filtering:** Liu et al. (2025) and Milano et al. (2026) demonstrate that LLMs can serve as effective "first-pass" respondents, narrowing down massive item pools and assessing Content Validity (CVR) with accuracy levels comparable to psychology graduate students.

## 3.2 Semantic Structure and Misfit Evaluation
* **Pre-Empirical Audits:** Feraco & Toffalini (2025) introduced *SEMbeddings*, allowing researchers to evaluate potential model misfit in CFA models before collecting a single human response.
* **Factorial Structure Prediction:** Milano et al. (2025) and Voss et al. (2026) show that the factorial structure (factor loadings) of personality scales can be predicted with >90% accuracy using solely the semantic text of the items, suggesting that internal language structure is a dominant driver of psychometric outcomes.
* **Pseudo-Factor Analysis (PFA):** Varrasi et al. (2026) developed PFA as a data-efficient alternative to traditional EFA, using item embeddings as proxies for human responses to recover factor structures.

## 3.3 Construct Clarification (Jingle-Jangle Fallacies)
* **Taxonomic Parsimony:** Wulff & Mata (2025b) and Hanfstingl et al. (2024) utilize semantic space mapping to detect Jingle (same label, different content) and Jangle (different label, same content) fallacies. 
* **Global Mapping:** Research (e.g., Hommel & Arslan, SQuID method by Pellert et al.) provides tools like *SurveyBot3000* or *SQuID* to predict item correlations and recover value structures (like Schwartz’s Values) across dozens of countries without empirical data.

## 3.4 Scale Abbreviation and Refinement
* **Data-Efficient Short Forms:** Studies by Jung & Seo (2025) and Kilmen & Bulut (2025) prove that scales (e.g., IPIP-50, ECR) can be shortened using semantic cluster proximity. These abbreviated forms maintain 96% accuracy compared to original structures while bypassing the need for large-scale pre-testing samples.

## 3.5 Methodological and Privacy Considerations
* **Data Privacy:** Eberhardt et al. (2025) emphasize local deployment of LLMs (e.g., Llama) to handle sensitive therapy transcripts, ensuring patient confidentiality.
* **Language/Model Sensitivity:** Research warns of "Model Drift" and language sensitivity (e.g., Varrasi et al., 2026), suggesting that for high-stakes research, one must document model versions, seed parameters, and utilize stable, open-source local models to ensure replicability.
* **The "Lingometrics" Critique:** Lehtonen et al. (2025) suggest that survey responses often reflect the "semantic grid" of the language itself rather than individual differences, necessitating a cautious interpretation of "latent" construct discoveries.


### Key Takeaway
The field is moving toward **Algorithmic Psychometrics**, where the semantic analysis of item text provides an empirical "prior" or "baseline." This allows researchers to identify problematic items, redundant constructs, and structural misfits *a priori*, significantly increasing the efficiency and conceptual clarity of psychometric scale development.

---
# 4. Content Validity

In modern psychometrics, content validity is viewed as **evidence based on test content**. It is a fundamental property evaluating whether a measurement tool adequately covers the domain of the construct it is intended to assess.



## 4.1 Foundations of Content-Oriented Evidence
Evidence based on test content establishes the relationship between the test's content (themes, wording, format) and the targeted psychological construct.
* **Content Specifications:** The creation of a "theoretical blueprint" that delineates the knowledge, skills, and characteristics to be measured.
* **The Role of Experts:** Historically, diverse panels of subject matter experts evaluate item importance, frequency, and criticality.
* **Sensitivity Reviews:** A critical fairness check to remove language or contexts that may be offensive or differentially familiar across subgroups.

## 4.2 Threats to Content Validity
Failure to establish robust content evidence leads to two primary "rival hypotheses":
* **Construct Underrepresentation:** The test fails to capture essential aspects of the construct (e.g., an anxiety scale ignoring cognitive components).
* **Construct-Irrelevant Variance:** Scores are impacted by extraneous factors, such as complex vocabulary on a math test, which penalize individuals based on traits unrelated to the construct.

## 4.3 The Embedding-Based Paradigm Shift
Embeddings represent test items as high-dimensional dense vectors, allowing us to quantify semantic meaning and linguistic nuances algorithmically.
* **Algorithmic Mapping:** By calculating the cosine similarity between item vectors and the theoretical construct definition, we can objectively identify items that deviate from the blueprint.
* **Scalability:** This process identifies redundancies and coverage gaps without the need for initial human response data, providing a replicable alternative to subjective panel reviews.
* **Lexical Proficiency:** LLMs are particularly proficient at validating concise, trait-descriptive items (e.g., Big Five adjectives), sometimes matching or exceeding the accuracy of human validators.

## 4.4 Hybrid Validation Systems
Current research advocates for a **Hybrid Validation Model** rather than a total replacement of human judgment:
1. **Human Expertise:** Superior at interpreting behavioral items requiring deep contextual and cultural understanding.
2. **AI Precision:** Superior at large-scale semantic analysis, automated flagging of construct-irrelevant variance, and pre-testing item pools before human administration.

### Key Documentation Standards
To maintain professional rigor, developers must document:
* The **logical structure** mapping items to the content domain.
* The **sampling strategy** used to prioritize specific areas.
* The **qualifications of expert judges** involved in the hybrid review.
* **Alignment evidence** between items and specifications.

---

# 5. Content Overlap

Content overlap refers to the degree to which different measurement instruments feature identical item content or symptoms. In psychometric research, this is quantified using metrics such as the Jaccard Index, where 0 indicates no overlap and 1 indicates full overlap.

## 5.1 The Problem of Low Overlap
Research indicates that commonly used depression scales often exhibit low to moderate content overlap (e.g., a mean Jaccard Index of 0.41), which undermines their clinical and research utility.

## 5.2 Core Challenges
* **Failure of Interchangeability:** Researchers often erroneously assume that different scales are interchangeable measures of the same construct. Low overlap suggests these instruments are not measuring the same set of symptoms.
* **Idiosyncratic Research Results:** Findings may become specific to the chosen scale rather than representative of the disorder. This threatens the replicability and generalizability of scientific findings across different studies.
* **Misleading Convergent Validity:** High correlations between total "sum-scores" of two scales are often misinterpreted as evidence that they measure the same construct. Scales can achieve high correlations (e.g., 0.69) despite sharing zero symptoms, based simply on scale length and minimal inter-item correlations.
* **Clinical and Diagnostic Inconsistency:** Differences in symptom prioritization (e.g., somatic focus in HRSD vs. cognitive focus in BDI) lead to inconsistent severity categorization for the same patient. Because individual symptoms relate differently to risk factors and treatment responses, this inconsistency directly impacts external variable relationships.
* **Systematic Bias in Treatment Efficacy:** Lack of overlap can bias research findings. For example, the HRSD’s heavy focus on somatic symptoms (insomnia, fatigue) may capture drug side effects as changes in depression severity, potentially biasing decades of antidepressant efficacy research.

## 5.3 Embedding-Based Detection of Redundancy
Within the context of this pipeline, (Content Overlap) leverages embeddings to mitigate these issues:
* **Inter-item Similarity Matrices:** By computing distances between item vectors, we can identify clusters of items sharing high semantic similarity.
* **Automated Pruning:** This allows for the systematic identification and removal of redundant items that measure the same specific variance, leading to more parsimonious and reliable instruments.

---


# 6. Application

The traditional 18-step scale development process (Stefana et al.) is now significantly enhanced by LLM-based agentic workflows. We map these technologies across the five core phases of psychometric development.

## 6.1 Phase 1: Preliminary Phase
* **Need Definition (Step 1):** LLMs act as conceptual auditors, using semantic mapping to identify "Jingle/Jangle" fallacies and define the construct's nomological net.
* **Measurement Search (Step 2):** Semantic search engines allow researchers to query thousands of existing instruments, identifying whether a new tool is necessary or if adaptation is sufficient.
* **Planning (Step 3):** Multi-agent systems coordinate development tasks while ensuring data privacy through local (on-premise) LLM deployment.

## 6.2 Phase 2: Item Development Phase
* **Item Pool Generation (Step 4):** Automatic Item Generation (AIG) via "Item Writer Agents" uses deductive (theory-driven) and inductive (web-crawled behavior) methods to build diverse item pools.
* **Expert Review & Bias Audit (Step 7):** Fine-tuned models (e.g., Cross Encoder MPNet) evaluate Content Validity Ratios (CVR) with human-like accuracy. Specialized agents scan items for demographic bias before human testing.
* **Pre-Data Calibration (Step 7):** Tools like *SEMbeddings* and *Pseudo-Factor Analysis (PFA)* fit CFA models to item vectors, allowing for item revision before a single human participant is recruited.
* **Population Testing (Step 9):** "LLM Respondents" provide a low-cost, preliminary filter to identify ambiguities in item phrasing before human cognitive interviews.

## 6.3 Phase 3: Scale Construction Phase
* **Synthetic Data Generation (Step 11):** Semantic response agents generate synthetic data reflecting human proficiency distributions, allowing for "ex-ante" testing of the survey's technical functionality.
* **Ex-Ante Factor Extraction (Step 12):** PFA can predict factor loadings and latent structures with high correlations to human-derived solutions.
* **Item Triaging (Step 13):** Ensemble clustering ranks items by their likelihood of high empirical factor loadings, ensuring only the strongest candidates proceed to final versions.

## 6.4 Phase 4: Scale Evaluation Phase
* **Reliability Benchmarking (Step 15):** Tools like *SurveyBot3000* and *SQuID* predict Cronbach's alpha and McDonald's omega from text alone, flagging potentially unstable scales early.
* **Validity Testing (Step 16):** * **Content Validity:** LLMs provide objective, scalable audits of item-construct alignment.
    * **Convergent/Discriminant:** AI models predict inter-scale correlations, ensuring the scale remains distinct from established constructs.
    * **Criterion Validity:** LLM-scored open-ended assessments correlate with real-world outcomes (e.g., work performance), providing evidence for criterion-related validity.

## 6.5 Phase 5: Finalization Phase
* **Optimized Sequencing (Step 17):** Item order is determined by predicted factor loadings, prioritizing high-impact items to counteract respondent fatigue.
* **Documentation (Step 18):** AI agents synthesize the development history, reviewer feedback, and psychometric audit reports, automating the creation of inventory manuals and anchor articles.

---

### Summary of Impact
| Phase | Traditional Limitation | AI Enhancement |
| :--- | :--- | :--- |
| **Preliminary** | Subjective, time-consuming | Automated Jingle/Jangle detection |
| **Development** | Expert panel bottleneck | High-precision pre-testing (SEMbeddings) |
| **Construction** | Large human sample needed | Synthetic benchmarking (PFA) |
| **Evaluation** | Late-stage discovery of misfit | A-priori model misfit flagging |
| **Finalization** | Manual documentation | Automated synthesis of technical reports |

*The integration of these technologies enables researchers to shift from "reactive validation" (fixing mistakes after data collection) to "proactive semantic design," resulting in more parsimonious and reliable psychometric instruments.*



## References

Abdurahman, S., Ziabari, A. S., Moore, A. K., Bartels, D. M., & Dehghani, M. (n.d.). A Primer for Evaluating Large Language Models in Social-Science Research.

American Educational Research Association, American Psychological Association, & National Council on Measurement in Education. (2014). *Standards for educational and psychological testing*. American Educational Research Association.

Anvari, F., Alsalti, T., Oehler, L. A., Hussey, I., Elson, M., & Arslan, R. C. (2025). Defragmenting psychology. *Nature Human Behaviour*, 9(5), 836–839. https://doi.org/10.1038/s41562-025-02138-0

Arnulf, J. K., Olsson, U. H., & Nimon, K. (2024). Measuring the menu, not the food: “Psychometric” data may instead measure “lingometrics” (and miss its greatest potential). *Frontiers in Psychology*, 15, 1308098. https://doi.org/10.3389/fpsyg.2024.1308098

Eberhardt, S. T., Vehlen, A., Schaffrath, J., Schwartz, B., Baur, T., Schiller, D., Hallmen, T., André, E., & Lutz, W. (2025). Development and validation of large language model rating scales for automatically transcribed psychological therapy sessions. *Scientific Reports*, 15(1), 29541. https://doi.org/10.1038/s41598-025-14923-y

Elson, M., Hussey, I., Alsalti, T., & Arslan, R. C. (2023). Psychological measures aren’t toothbrushes. *Communications Psychology*, 1(1), 25. https://doi.org/10.1038/s44271-023-00026-9

Feraco, T., & Toffalini, E. (2025). SEMbeddings: How to evaluate model misfit before data collection using large-language models. *Frontiers in Psychology*, 15, 1433339. https://doi.org/10.3389/fpsyg.2024.1433339

Fried, E. I. (2017). The 52 symptoms of major depression: Lack of content overlap among seven common depression scales. *Journal of Affective Disorders*, 208, 191–197. https://doi.org/10.1016/j.jad.2016.10.019

Gao, Y., Ma, Y., Qi, Y., & Liu, T. (n.d.). Development of a Computerized Adaptive Item Bank for the Big Five Personality Based on Large Language Models.

Hanfstingl, B., Oberleiter, S., Pietschnig, J., Tran, U. S., & Voracek, M. (2024). Detecting jingle and jangle fallacies by identifying consistencies and variabilities in study specifications – a call for research. *Frontiers in Psychology*, 15, 1404060. https://doi.org/10.3389/fpsyg.2024.1404060

Hommel, B. E., & Arslan, R. C. (n.d.). Language Models Accurately Infer Correlations Between Psychological Items and Scales From Text Alone.

Jung, S.-J., & Seo, J.-W. (2025). A transformer-based embedding approach to developing short-form psychological measures. *Frontiers in Psychology*, 16, 1640864. https://doi.org/10.3389/fpsyg.2025.1640864

Kilmen, S., & Bulut, O. (2025). Shortening Psychological Scales: Semantic Similarity Matters. *Educational and Psychological Measurement*, 85(5), 910–934. https://doi.org/10.1177/00131644251319047

Lee, P., Son, M., & Jia, Z. (2026). AI-powered Automatic Item Generation for Psychological Tests: A Conceptual Framework for an LLM-based Multi-Agent AIG System. *Journal of Business and Psychology*, 41(1), 71–99. https://doi.org/10.1007/s10869-025-10067-y

Lehtonen, E., Buder-Gröndahl, T., & Nordhoff, S. (2025). Revealing the Influence of Semantic Similarity on Survey Responses: A Synthetic Data Generation Approach. *IEEE Access*, 13, 40285–40301. https://doi.org/10.1109/ACCESS.2025.3546565

Liu, Y., Bhandari, S., & Pardos, Z. A. (2025). Leveraging LLM respondents for item evaluation: A psychometric analysis. *British Journal of Educational Technology*, 56(3), 1028–1052. https://doi.org/10.1111/bjet.13570

Milano, N., Luongo, M., Ponticorvo, M., & Marocco, D. (2025). Semantic analysis of test items through large language model embeddings predicts a-priori factorial structure of personality tests. *Current Research in Behavioral Sciences*, 8, 100168. https://doi.org/10.1016/j.crbeha.2025.100168

Milano, N., Ponticorvo, M., & Marocco, D. (2026). Human Expertise and Large Language Model Embeddings in the Content Validity Assessment of Personality Tests. *Educational and Psychological Measurement*, 86(1), 30–53. https://doi.org/10.1177/00131644251355485

Pellert, M., Lechner, C. M., Sen, I., & Strohmaier, M. (n.d.). Neural network embeddings recover value dimensions from psychometric survey items on par with human data.

Schoenegger, P., Greenberg, S., Grishin, A., Lewis, J., & Caviola, L. (2025). AI can outperform humans in predicting correlations between personality items. *Communications Psychology*, 3(1), 23. https://doi.org/10.1038/s44271-025-00205-w

Speer, A. B., Delacruz, A. Y., Chawota, T. A., Perrotta, J., & Rudolph, C. W. (2026). Unpacking the Validity of Open-Ended Personality Assessments Using Fine-Tuned Large Language Models. *Organizational Research Methods*, 10944281251413746. https://doi.org/10.1177/10944281251413746

Stefana, A., Damiani, S., Granziol, U., Provenzani, U., Solmi, M., Youngstrom, E. A., & Fusar-Poli, P. (n.d.). *Psychological, psychiatric, and behavioral sciences measurement scales: Best practice guidelines for their development and validation*.

Uher, J. (2025). Statistics is not measurement: The inbuilt semantics of psychometric scales and language-based models obscures crucial epistemic differences. *Frontiers in Psychology*, 16, 1534270. https://doi.org/10.3389/fpsyg.2025.1534270

Uher, J., Arnulf, J. K., Barrett, P. T., Heene, M., Heine, J.-H., Martin, J., Mazur, L. B., McGann, M., Mislevy, R. J., Speelman, C., Toomela, A., & Weber, R. (2025). Psychology’s Questionable Research Fundamentals (QRFs): Key problems in quantitative psychology and psychological measurement beyond Questionable Research Practices (QRPs). *Frontiers in Psychology*, 16, 1553028. https://doi.org/10.3389/fpsyg.2025.1553028

Varrasi, S., Platania, G. A., Castellano, S., Ferraioli, F., Massimino, S., Vicario, C. M., Di Nuovo, S., & D’Urso, E. D. (2026). Expanding psychometrics with pretrained language models: Evaluating pseudo-factor analysis in applied and multilingual contexts. *Methods in Psychology*, 14, 100244. https://doi.org/10.1016/j.metip.2026.100244

Voss, N. M., Wu, F. Y., Javalagi, A. A., & Kell, H. J. (2026). Integrating Ensemble Clustering and Text Embeddings for Estimating the Factor Loadings of Self-Report Scales. *Educational and Psychological Measurement*, 00131644261430762. https://doi.org/10.1177/00131644261430762

Wulff, D. U., & Mata, R. (n.d.). Escaping the Jingle-Jangle Jungle: Increasing Conceptual Clarity in Psychology Using Large Language Models.

Wulff, D. U., & Mata, R. (2025a). Addressing Longstanding Challenges in Cognitive Science with Language Models (Version 2). arXiv. https://doi.org/10.48550/ARXIV.2511.00206

Wulff, D. U., & Mata, R. (2025b). Semantic embeddings reveal and address taxonomic incommensurability in psychological measurement. *Nature Human Behaviour*, 9(5), 944–954. https://doi.org/10.1038/s41562-024-02089-y
