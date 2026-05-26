<img width="468" height="485" alt="image" src="https://github.com/user-attachments/assets/a0e136ee-44a7-42aa-b196-37c048b8d804" /># 04. AI Ethics

This section outlines the ethical standards, data privacy protocols, and transparency requirements for using Generative AI


## 1. Introduction


For the purposes of this research project, Artificial Intelligence (AI) is understood as:
> *"a machine-based system that is designed to operate with varying levels of autonomy and that may exhibit adaptiveness after deployment, and that, for explicit or implicit objectives, infers, from the input it receives, how to generate outputs such as predictions, content, recommendations, or decisions that can influence physical or virtual environments."* (European Union, 2024).

Under this definition, it is crucial to recognize that AI encompasses a wide range of distinct capabilities and tasks (OECD, 2022). In the context of psychological meta-research and methodological auditing, these include:

* **Recognition:** Identifying and categorizing data (e.g., images, video, audio, and text) into specific classifications. Examples include image/object detection and facial recognition.
* **Event Detection:** Connecting disparate data points to identify underlying patterns. Examples include fraud and risk detection, flagging human errors, and intelligent monitoring.
* **Forecasting:** Utilizing historical and existing behavior to predict future outcomes. Examples include intelligent navigation and system failure prediction.
* **Personalization:** Constructing individual profiles to learn from and adapt to specific users over time. Examples include search- and browsing-based recommendation systems and personalized finance.
* **Interaction Support:** Interpreting and generating content to facilitate conversational and other interactions between humans and machines. Examples include Chatbots and virtual voice assistants.
* **Goal-Driven Optimization:** Providing systems with a specific objective and the autonomy to determine the optimal solution to a problem. Examples include resource/logistics optimization, real-time auctions, and scenario simulation.
* **Reasoning with Knowledge Structures:** Inferring new potential outcomes—even those not explicitly present in the existing data—through advanced modeling and simulation. Examples include legal reasoning, automated recruitment screening systems, and diagnostics.

Given that AI can perform a vast array of tasks, offering substantial benefits but also introducing inherent risks tied to the nature of these operations, regulatory and ethical frameworks are currently being implemented on a global scale.


## 2. European and Global Guidelines


### 2.1 The EU AI Act
The EU AI Act is the European regulation for Artificial Intelligence (AI). Although established in 2024, with certain obligations taking effect in 2025, the EU AI Act enters into full force as of August 2026. This regulatory framework classifies AI systems based on their level of risk:

#### Prohibited AI Systems (Unacceptable Risk)
This category includes systems that are strictly banned because they pose a clear threat to people's safety, livelihoods, and rights. These include systems that:
* Deploy subliminal, manipulative, or deceptive techniques (with the aim to distort behavior or impair informed decision-making).
* Exploit the vulnerabilities of specific individuals or groups (to distort their behavior).
* Conduct biometric categorization to deduce sensitive attributes such as race, political opinions, or sexual orientation (excluding legally acquired law enforcement data).
* Perform social scoring based on social behavior or personal characteristics.
* Assess the risk of an individual committing a criminal offense based solely on profiling or personality traits (except when used as a supplement to human assessment).
* Create facial recognition databases through untargeted scraping of CCTV footage or internet images.
* Recognize emotions in workplaces or educational institutions (except for strict medical or safety reasons).
* Use real-time remote biometric identification in publicly accessible spaces (with narrow exceptions such as searching for missing persons, preventing imminent threats, or identifying suspects).

#### High-Risk AI Systems
These systems are permitted but are subject to strict obligations before being deployed, including the creation of technical documentation, comprehensive logging, and mandatory human oversight. These include systems:
* Performing profiling of individuals to assess aspects of their life, such as work performance, economic situation, health, personal interests, reliability, or behavior.
* Utilizing remote biometric identification.
* Managing safety components in the operation and control of critical digital infrastructure.
* Determining access, admission, or assignment to educational and vocational training institutions at all levels.
* Used for recruitment or selection, particularly targeted job advertising, analyzing and filtering applications, and evaluating candidates.
* Used by public authorities to assess eligibility for public assistance benefits and services.
* Utilized by law enforcement to assess the risk of an individual becoming a victim of a crime, polygraphs (lie detectors), or evaluating the reliability of evidence.
* Utilized to assess illegal migration risks, health risks, or to examine applications for asylum, visas, and residence permits.
* Used in the administration of justice to apply the law to concrete facts or to influence the outcomes of elections.

#### Limited Risk AI Systems
The primary obligation for these systems is transparency, information provision, and identifiability. For example, AI-generated content or chatbots must be clearly labeled so that users know they are interacting with an AI.

#### Minimal Risk AI Systems
Systems posing minimal or no risk, such as AI-driven video games or spam filters, are not subject to specific additional legal rules.

---

### 2.2 Council of Europe Framework Convention on Artificial Intelligence, Human Rights, Democracy, and the Rule of Law
The primary objective of this key instrument is to ensure that activities within the lifecycle of AI systems are fully compliant with human rights, democracy, and the rule of law. It was adopted in March 2026 by the European Parliament. Although these commitments are legally directed at states, they serve as a critical framework for individuals to recognize and assert their rights. Under this convention, parties must ensure that AI activities:
* Comply with the obligation to protect human rights.
* Are not utilized to undermine democratic independence or institutional integrity.
* Incorporate measures ensuring fair individual access to public debate.
* Implement appropriate requirements for transparency and oversight.
* Establish mechanisms to ensure accountability for any adverse impacts on rights.
* Promote equality, including gender equality, and enforce the prohibition of discrimination.
* Guarantee the protection of privacy rights and personal data.
* Introduce measures supporting the reliability of AI systems and public trust.
* Create controlled environments (sandboxes) for AI development, experimentation, and testing.

---

### 2.3 Recommendation on the Ethics of Artificial Intelligence – UNESCO
To safeguard ethics and human rights globally, UNESCO established a global—though non-binding—standard on the ethics of artificial intelligence in 2021. The document recommends adhering to 10 core principles:

1. **Proportionality and Do No Harm:** The use of AI systems must not go beyond what is necessary to achieve a legitimate aim.
2. **Safety and Security:** AI actors should avoid unintended harm (safety risks) as well as vulnerabilities to cyberattacks (security risks).
3. **Right to Privacy and Data Protection:** Privacy must be protected and promoted throughout the entire AI lifecycle.
4. **Multi-stakeholder and Adaptive Governance and Collaboration:** International law and national sovereignty must be respected when managing and utilizing data.
5. **Responsibility and Accountability:** AI systems should be fully auditable and traceable.
6. **Transparency and Explainability:** The ethical deployment of AI systems depends heavily on their transparency and explainability.
7. **Human Oversight and Determination:** Member states should ensure that AI systems never replace ultimate human responsibility and accountability.
8. **Sustainability:** AI technologies should be continuously evaluated based on their environmental, cultural, economic, and social sustainability impacts.
9. **Awareness and Literacy:** Public understanding of AI and data should be actively promoted through open and accessible education.
10. **Fairness and Non-discrimination:** All AI-related activities should actively promote social justice, fairness, and absolute non-discrimination.


## 3. General AI Ethical Principles


Moving from formal legal frameworks to broader ethical guidelines for AI developers and users, research should adhere to foundational ethical principles established in meta-analytic literature. A systematic review by Jobin et al. (2019) analyzed 84 documents from the private sector, government institutions, and international organizations, identifying the most frequently recurring global principles:

* **Transparency:** Efforts to improve explainability, interpretability, and active communication regarding information disclosure.
* **Justice and Fairness:** Expressed primarily through fairness, monitoring, and the active mitigation of unwanted bias.
* **Non-Maleficence:** The directive that AI systems must never cause predictable or unintentional harm.
* **Responsibility:** Operating with professional integrity and clarifying the attribution of responsibility and legal liability, preferably specified in advance through agreements.
* **Privacy:** Presented primarily in the context of robust data protection and governance.
* **Beneficence:** Augmenting human capabilities, promoting human well-being, and fostering peace and prosperity.
* **Freedom and Autonomy:** Referring to freedom of expression, self-determination, and protection against automated coercion.
* **Trust:** Frameworks calling for rigorous research and development into verifiably trustworthy AI technologies.
* **Sustainability:** The requirement that AI development and deployment actively account for environmental protection, ecological health, and planetary biodiversity.
* **Dignity:** Intimately linked to human rights, emphasizing the prevention of harm, forced compliance, and demeaning automated classification.
* **Solidarity:** The need to redistribute the benefits of AI to safeguard social cohesion, with specific respect for potentially vulnerable individuals and groups.

Following the rapid expansion and widespread user adoption of Generative AI (GenAI), the ethical landscape has expanded to incorporate specialized guidelines tailored to these models (Laine et al., 2025):

* **Respect for Intellectual Property:** GenAI systems and their operators must recognize and protect the rights and ownership of creators regarding their original works.
* **Truthfulness:** GenAI systems should be designed and utilized to accurately represent information, empirical facts, and analytical results, minimizing hallucinations.
* **Robustness:** GenAI systems should consistently maintain high performance across diverse scenarios while effectively and safely handling edge cases or exceptions.
* **Misuse Prevention:** GenAI applications must be engineered with robust safeguards to prevent potential malicious exploitation or harmful misuse.
* **Socio-Cultural Responsibility:** GenAI systems must be designed and deployed to operate responsibly, maintaining awareness of their broad societal and cultural implications.
* **Human-Centered Design:** GenAI development must prioritize the cognitive needs, psychological well-being, and lived experiences of human users.


## 4. Ethical Guidelines for Development, Science, and Research


Since our work focuses directly on meta-research, it is vital to remain aware of ethical recommendations regarding research execution and publication practices. De Veiga (2025) analyzed the foundational ethical guidelines of 10 major publishing houses (including Elsevier, Springer Nature, Wiley, MDPI, Taylor & Francis, IEEE, OUP, ACS Publications, Wolters Kluwer, and Sage Publications). This analysis identified clearly accepted and unaccepted uses of AI in scientific publishing.

### Accepted Practices for AI Use in Scientific Publishing
* **Author Accountability and Liability:** Human authors bear ultimate and baseline responsibility for their work. They must actively monitor, review, and verify all AI-generated content.
* **Human Oversight:** Rigorous human review and oversight are mandatory to guarantee the accuracy, integrity, ethics, quality, and authenticity of the research.
* **AI-Assisted Tools (Non-Generative):** Broad consensus exists that AI-assisted tools (e.g., Grammarly) may be used to improve readability, edit manuscript draft language, and enhance grammar, as well as to manage citations (e.g., Mendeley, EndNote, or Zotero).
* **Generative AI Tools:** Generative AI tools may be used in the early stages prior to writing for idea generation, brainstorming, or literature search/classification. However, this must be accompanied by strict human verification. Authors remain fully accountable for the text. Furthermore, there is a consensus that AI tools can be used as part of the research design or methodology—for instance, when analyzing findings or automating data coding. However, all publishers require full transparency and disclosure of such use (e.g., in a cover letter, acknowledgments, methods section, or a formal AI declaration, depending on the specific journal's requirements).

### Unaccepted Practices for AI Use in Scientific Publishing
* **Attribution of Authorship:** All major publishers strictly adhere to the principles of COPE (Committee on Publication Ethics), which mandate that an author must be capable of taking legal and scientific responsibility for the manuscript. Current standards explicitly prohibit listing AI as a co-author.
* **Deriving Recommendations and Conclusions:** Core research tasks—specifically synthesizing arguments, drawing conclusions, and generating final recommendations—must be performed exclusively by humans.
* **Creating, Editing, or Manipulating Raw Data and Results:** AI must never alter key research data or experimental outcomes. Using AI to generate autonomous empirical results or fake datasets is strictly prohibited.
* **Generating or Altering Images:** Publishing houses state that generative AI tools must not be used to create or artificially modify figures, data visualizations, or images within manuscripts.


## 5. Ethical Considerations in Psychology and Mental Health

The field of psychology and mental health cannot operate without specific ethical guidelines regarding the integration of Artificial Intelligence. Pillay (2025) proposed a preliminary ethical framework that synthesizes the ethical codes of the American Counseling Association (ACA), the American Psychological Association (APA), the American Medical Association (AMA), and the National Association of Social Workers (NASW). These recommendations are organized into 5 core pillars:

### (1) Autonomy and Informed Consent
* **i. Mandatory Disclosure:** Clinicians must inform the client whenever AI is utilized in their treatment workflow. This disclosure must explicitly cover the AI’s capabilities, limitations, potential impact on diagnosis, access to care, and any cost implications.
* **ii. Operational Transparency:** Clinicians must provide detailed information regarding the specific types of AI tools deployed, their impact on the client’s treatment, methods of data collection, storage, and analysis, as well as the role and involvement of any third-party vendors in the process.
* **iii. Right of Refusal:** Clinicians must guarantee the client’s right to refuse AI-assisted treatment or algorithmic decision-making processes and, whenever feasible, offer a human-centered alternative.
* **iv. Accessible Language:** Clinicians must ensure that the language used to describe AI operations provides clear, jargon-free, and understandable details, thereby enabling clients to grant fully informed consent.

### (2) Beneficence and Non-Maleficence
* **i. Centrality of the Therapeutic Relationship:** The therapeutic relationship remains the core of ethical clinical care. Consequently, the use of AI must never be viewed as a replacement for human connection, but rather as a complementary modality that strengthens the therapeutic alliance during assessment, diagnosis, and treatment planning.
* **ii. Professional Competence:** AI may only be explored as a complementary tool when the clinician has established the necessary professional competence to fully understand, interpret, and explain the algorithmic outputs to the client and relevant stakeholders.
* **iii. Evidence-Based and Culturally Appropriate Selection:** Clinicians must select AI tools that are culturally appropriate to minimize the exacerbation of systemic inequalities. These tools must be reliable, valid, and rigorously backed by evidence-based psychological research.
* **iv. Welfare Promotion and Bias Audit:** Clinicians must use AI tools strictly to promote client well-being and mitigate risk, rather than to justify or contribute to discriminatory practices. This requires deploying algorithms designed to audit, identify, and resolve ethical concerns or unintended harms.
* **v. Standards and Continuous Evaluation:** AI applications must meet established professional and ethical standards, and they must undergo regular evaluation to ensure ongoing accuracy and clinical appropriateness.

### (3) Confidentiality and Transparency
* **i. Stringent Data Privacy Standards:** AI tools must adhere to identical data confidentiality standards as traditional practices (e.g., full compliance with HIPAA, federal and state laws, and relevant professional codes), including secure data handling, ethical record-keeping, end-to-end encryption, and robust storage protection.
* **ii. Third-Party Compliance:** Clinicians must actively ensure that confidentiality, privacy, and ethical standards are strictly maintained when utilizing external AI platforms or third-party technology providers.
* **iii. Ethical Accountability:** Clinicians bear ultimate ethical responsibility for the deployment of AI tools and must provide truthful information regarding their capabilities and constraints, avoiding any misleading or exaggerated claims.
* **iv. Algorithmic Transparency:** Clinicians should advocate for transparency by disclosing how the underlying AI models are developed and how their specific algorithms are clinically applied.

### (4) Justice, Fairness, and Inclusivity
* **i. Mitigation of Discrimination:** Clinicians are responsible for ensuring that deployed AI systems do not disadvantage individuals or justify systemic discrimination based on marginalized or intersectional identities.
* **ii. Cultural Bias Assessment:** Clinicians must rigorously evaluate the function, design, and outputs of any AI system to ensure equitable, ethical application, systematically checking evaluations for cultural bias and unfairness.
* **iii. Advocacy for Inclusive Design:** Clinicians must actively support AI systems that enhance justice and safety for all clients, while advocating for inclusive and transparent design elements in technology development.

### (5) Professional Integrity and Accountability
* **i. Competence Boundaries:** Clinicians should utilize AI tools only if they possess the formal training and verified competence required to responsibly and accurately interpret results, fully grasping the underlying implications, limitations, and ethical dimensions of AI.
* **ii. Continuous Digital Ethics Education:** Clinicians must stay informed about best practices and emerging risks associated with new technologies by engaging in continuous education regarding AI and digital ethics, ideally collaborating directly with AI technologists.
* **iii. Supervision and Mentorship:** Clinical supervisors must model ethical AI utilization and actively guide their trainees and supervisees to critically evaluate algorithmic tools within their clinical and research practices.


## 6. Open Ethical Challenges in Artificial Intelligence

To conclude this ethical framework, it is necessary to address the ongoing, unresolved ethical questions that continue to challenge the development and deployment of Artificial Intelligence (Huang et al., 2022). These challenges persist across three distinct levels:

### (1) Individual-Level Ethical Challenges
* **Safety Concerns:** Critical issues regarding physical and psychological safety, such as algorithmic failures or accidents caused by autonomous vehicles.
* **Privacy and Data Protection:** Ongoing debates surrounding user surveillance, ubiquitous data collection, and the ethical boundary of utilizing personal data to train proprietary foundation models without explicit, ongoing consent.
* **Autonomous Decision-Making:** Questioning human agency and whether a decision heavily influenced or guided by AI outputs can truly be considered free and self-determined.
* **Human Dignity:** Threats to baseline dignity, heavily highlighted by the development of lethal autonomous weapons systems or demeaning automated profiling.

### (2) Societal-Level Ethical Challenges
* **Fairness and Justice:** The systemic reinforcement of human biases, as evidenced by documented racial and socio-economic biases in AI applications deployed within judicial and law enforcement systems.
* **Accountability and Liability:** The legal and moral vacuum regarding who bears ultimate liability—the developer, the user, or the deploying institution—when algorithmic decision-making results in harm.
* **Algorithmic Transparency:** The "black box" problem, where the internal mechanisms and specific reasoning pathways of complex deep learning models remain opaque and unexplainable to human auditors.
* **Surveillance and Data Logging:** The societal implications of continuous mass surveillance and the permanent digital logging of public behavioral data.
* **AI Governance and Control:** Challenges regarding the absolute auditability, containment, and long-term control of highly autonomous AI systems.
* **Socio-Economic Disruption:** Ethical dilemmas regarding the large-scale displacement of human labor, the transformation of job markets, and the potential erosion or artificial replacement of authentic human relationships.

### (3) Environmental-Level Ethical Challenges
* **Natural Resource Consumption:** The severe ecological impact of manufacturing AI hardware, which requires a substantial volume of finite raw materials and rare-earth elements.
* **Carbon Footprint and Energy Consumption:** The immense electrical energy demanded by high-performance data centers to train and run large language models, contributing significantly to global carbon emissions and atmospheric pollution.
* **Ecological Sustainability:** The open question of how to align future AI development with sustainable human development goals while simultaneously preserving the capacity of natural ecosystems to provide vital resources.






## References

da Veiga, A. (2025). Ethical guidelines for the use of generative artificial intelligence and artificial intelligence-assisted tools in scholarly publishing: A thematic analysis. *Science Editing*, 12(1), 28–34. https://doi.org/10.6087/kcse.345

European Union. (2024). Regulation (EU) 2024/1689 of the European Parliament and of the Council of 13 June 2024 laying down harmonised rules on artificial intelligence (Artificial Intelligence Act). *Official Journal of the European Union*. https://eur-lex.europa.eu/eli/reg/2024/1689/oj

Huang, C., Zhang, Z., Mao, B., & Yao, X. (2022). An overview of artificial intelligence ethics. *IEEE Transactions on Artificial Intelligence*, 4(4), 799–819. https://doi.org/10.1109/TAI.2022.3193245

Jobin, A., Ienca, M., & Vayena, E. (2019). The global landscape of AI ethics guidelines. *Nature Machine Intelligence*, 1(9), 389–399. https://doi.org/10.1038/s42256-019-0088-2

Laine, J., Minkkinen, M., & Mäntymäki, M. (2025). Understanding the ethics of generative AI: Established and new ethical principles. *Communications of the Association for Information Systems*, 56, 1–25. https://doi.org/10.17705/1CAIS.05601

OECD. (2022). *OECD Framework for the Classification of AI systems* (OECD Digital Economy Papers No. 323). OECD Publishing. https://doi.org/10.1787/cb618401-en

Pillay, Y. (2025). Ethical decision-making guidelines for mental health clinicians in the artificial intelligence (AI) era. *Healthcare*, 13(23), Article 3057. https://doi.org/10.3390/healthcare13233057

UNESCO. (2022). *Recommendation on the Ethics of Artificial Intelligence*. UNESCO Publishing. https://unesdoc.unesco.org/ark:/48223/pf0000381137



**Author:** Viktória Gajdošová
**Last Updated:** May 2026
