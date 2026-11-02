# Theory: why, comparison, and results

## 1. Why we did it

### Transparency determines whether findings can be checked

A published claim can only be checked if the data, materials, analysis code, and preregistration behind it are shared and can be opened. Munafò et al. (2017) list these practices, together with disclosing funding and conflicts of interest, as one basis of credible research. The SCORE project shows that sharing matters in practice. Among papers for which a reproduction was attempted, approximate or precise reproducibility was achieved for 90.9% of papers with both data and code available, but for only 38.1% when the dataset had to be reconstructed from source data (Miske et al., 2026).

### Measuring transparency does not scale

How often psychology articles share these resources has been measured by manual coding. Hardwicke et al. (2022, 2024) had two coders read each article, find the relevant statements, and open every link, with a third coder resolving disagreements. This is accurate but takes a long time, so studies cover 250 to 400 articles and short time periods. Nobody can read every published paper this way, so the development of transparency across the whole literature, across subfields, and over time is only partly known.

### Existing automated tools check text, not resources

Tools such as ODDPub and rtransparent search the article text for keywords that signal data or code sharing, and metacheck (Lakens, 2026) combines text search with predefined functions for known repositories. They detect that a statement exists. They do not decide on their own how to find a resource and whether it can really be opened, which Hardwicke et al. (2024) treat as central to their coding.

### What we tested

An LLM agent is a system built around a language model that chooses its own actions (searching the web, opening a link, reading a page) and uses the result of each action to choose the next one (Wang et al., 2024). We tested whether such an agent can replace the manual work: find an article, read it, code the transparency indicators, and open every shared resource to check that it is accessible. The goal was a tool for researchers, meta-scientists, and journals that checks transparency on demand and at scale, and to find out how much human checking it still needs.

Research questions:

1. How accurately can the agent code transparency indicators compared with a human-coded reference standard?
2. What kinds of errors does it make, and how should they be interpreted?
3. Are its accuracy and the predictability of its errors sufficient for a screening tool that reduces manual coding, and where is human verification still needed?

## 2. What we compared the agent with

### Reference standard

We used the dataset published with Hardwicke et al. (2024): 400 empirical psychology articles from 2022, 200 sampled from all English-language psychology journals and 200 from the 50 top journals by impact factor. In that dataset two independent coders coded each article and a third coder resolved all disagreements. The resolved value (column suffix `_agreed`) is our reference standard. The reference standard is a human coding product and can contain errors. The results therefore show agreement with it, not correctness in an absolute sense.

### Sample

The agent coded all 400 articles. 21 could not be accessed by either the agent or the researcher and were excluded, leaving 379. For 301 of them the agent found the full text itself, for 73 the researcher supplied a PDF, and for 5 the agent first reported the article as accessible but failed during coding, so a PDF was supplied.

### Variables

The agent coded the same 7 indicators as the human coders: open access, preregistration, materials, data, analysis code, funding statement, and conflict-of-interest statement. For the four artifacts (preregistration, materials, data, analysis code) it decided first whether the article says the artifact is available, then how it can be obtained, and then whether it opened the resource without contacting anyone. Together with their conditional sub-variables this gives 22 variables, and 379 articles x 22 variables = 8,338 comparisons.

Conditional sub-variables are set to "not applicable" when the upstream condition is not met, for example when there is no data statement. Because of this, one wrong upstream decision can cause several wrong downstream values ("cascading errors").

### How the agent worked

1. It tried to find a free full text by DOI and title.
2. For articles it could not find, the researcher uploaded a PDF.
3. In one API call per article it received the coding guideline and returned one flat JSON object with all variables, a verbatim quotation for each statement decision, and the URL it checked for each access decision. It was instructed to open every relevant link and the call was repeated (up to three times) if the response showed no web search.
4. Results were converted to one row per article using the same variable names as the reference dataset.

The model was `gpt-5.6-luna`, run once per article in August 2026.

### Metrics

- **Accuracy:** share of cells where agent and reference standard give the same value.
- **Cohen's κ:** agreement corrected for chance, interpreted with the Landis and Koch (1977) bands. κ cannot be estimated for a variable with almost no variation.
- **Sensitivity:** of the resources that the reference standard marks as available or accessible, the share that the agent also marks as such.
- **Specificity:** of the resources that the reference standard marks as not available, the share that the agent also marks as not available.
- **Precision:** share of the agent's "available" judgments that are correct.
- **F1:** combines sensitivity and precision.

We also reviewed all 964 disagreements one by one and grouped them into recurring patterns, without a predefined scheme.

## 3. Results

### Overall agreement

| Measure | Result |
|---|---|
| Matches with the reference standard | 7,374 of 8,338 comparisons |
| Overall accuracy | 88.4% (95% CI 87.7 to 89.1; article-level bootstrap 87.3 to 89.5) |
| Accuracy excluding cells that were "not applicable" for both | 74.3% (2,784 of 3,748 cells; bootstrap CI 72.1 to 76.4) |
| Accuracy excluding the weakest variable (materials statement) | 90.4% (7,198 of 7,959) |
| Variables with substantial or almost-perfect agreement (κ > 0.60) | 12 of 22 |

55.0% of all comparisons (4,590) are cells where both agent and reference standard say "not applicable". These always match and raise the overall figure, so 74.3% is the stricter estimate for the cells where coding was actually needed.

### Agreement by variable (selected)

| Variable | Accuracy | κ |
|---|---|---|
| Preregistration, access method | 96.8% | 0.854 |
| Preregistration, statement | 95.3% | 0.853 |
| Analysis code, access method | 96.8% | 0.863 |
| Analysis code, statement | 94.7% | 0.798 |
| Funding, statement | 89.7% | 0.805 |
| Data, statement | 83.6% | 0.736 |
| Conflict of interest, statement | 85.2% | 0.723 |
| Open access status | 84.4% | 0.534 |
| Data, access status | 85.2% | 0.740 |
| Materials, access status | 78.9% | 0.482 |
| Materials, statement | **46.4%** | **0.207** |

Mean κ by indicator: funding 0.805, conflict of interest 0.723, preregistration 0.668, data 0.657, analysis code 0.567, open access 0.534, materials 0.383. For `analysis_reason`, κ could not be estimated because only one article had a value other than "not applicable", although raw agreement was 99.7%.

### Sensitivity, specificity, precision, F1

| Variable | Sensitivity | Specificity | Precision | F1 |
|---|---|---|---|---|
| Funding, statement | .924 | .985 | .991 | .956 |
| Data, statement | .889 | .981 | .974 | .930 |
| Preregistration, statement | .889 | .991 | .930 | .909 |
| Open access status | .964 | .500 | .847 | .902 |
| Conflict of interest, statement | .833 | .997 | .962 | .893 |
| Analysis code, statement | .827 | .991 | .935 | .878 |
| Materials, statement | .807 | .855 | .609 | .694 |
| Analysis code, access status | .512 | .994 | .913 | .656 |
| Data, access status | .526 | .975 | .789 | .632 |
| Preregistration, access status | .486 | .991 | .857 | .621 |
| Materials, access status | .537 | .885 | .500 | .518 |

Three patterns:

1. **Access status:** for all four artifacts the agent has low sensitivity (0.486 to 0.537) and high specificity. It often failed to confirm access to resources that were accessible, and rarely said a resource was accessible when it was not. Specificity is somewhat inflated, because articles with no artifact count as correct negatives.
2. **Open access:** the opposite direction. The agent judged 49 paywalled articles as accessible and 10 accessible articles as paywalled. Most of the 49 were cases where it found a copy on a third-party site such as ResearchGate or PubMed instead of the publisher.
3. **Materials statement:** sensitivity is comparable to other variables (0.807), but precision is the lowest of all statement variables (0.609), so about 4 in 10 positive judgments were wrong.

### The materials variable is hard for humans too

The two original coders agreed with each other on only 48% of materials statements before the third coder resolved them (Hardwicke et al., 2024). Each coder agreed with the final value in 70.7% and 66.8% of cases, which is the lowest of all statement variables for them as well. The agent's 46.4% is still about 20 to 24 percentage points below either coder, so the ambiguity of the category explains only part of the weakness.

### Prevalence estimates

Because the agent under-reports access, estimates of how common sharing is would be too low:

| Resource accessible | Agent | Reference standard |
|---|---|---|
| Data | 10.0% (38 of 379) | 15.0% (57 of 379) |
| Analysis scripts | 6.1% | 10.8% |
| Preregistration | 5.5% | 9.8% |
| Materials | 19.0% | 17.7% |

For materials the two estimates are similar only because errors in both directions cancel (precision was 0.50).

### Types of errors

The review of the 964 disagreements shows a small number of recurring causes:

- **Cascading errors:** roughly half or more of the disagreements in conditional variables follow from one upstream mistake.
- **Overlooked end-of-article statements:** funding and conflict-of-interest statements were missed (empty quotation in 18 of 20 and 30 of 32 such cases).
- **Restricted-access phrasing:** "available upon request" and explicit "not applicable" statements were not recognised as valid data statements.
- **UNCLEAR category for materials:** involved in 173 of 203 materials disagreements (85%).
- **Reporting a resource as inaccessible although a link was checked:** across all four access-status variables.
- **Naming a reason where the reference standard had none:** 13 of 19 disagreements for the data reason and 4 of 6 for the materials reason.
- **Technical failures:** six articles where the extracted text was incomplete or corrupted.

Open access over-claims in 12 cases came from an inconsistency in the pipeline itself: the agent had already requested a PDF but still answered "Yes".

## 4. What this means

- At 88.4% overall agreement, about one field in nine is wrong, and about one in four among cells that were applicable to at least one coder. The agent is therefore not suitable for unsupervised use.
- Errors are concentrated in a few identifiable places, so a person can check these specifically (every negative access verdict, every UNCLEAR materials statement, empty funding or conflict-of-interest results) and rely on the agent for the remaining fields.
- Because the agent mostly under-claims, prevalence estimates from it would need to be corrected for its known error rates, or each negative access verdict checked by a person, before being used to track transparency over time.

## 5. Limitations

- One model, one run per article, one set of instructions. The instructions were piloted on 10 articles and then fixed, and they were not tested on a separate new sample.
- The evidence that the agent opened a resource is its self-reported `url_checked` value and the search log, which records requests rather than pages that loaded. Repositories displayed with JavaScript, such as OSF, may not load for a search tool, so low access sensitivity can be a tool limitation.
- PDF text longer than 16,000 characters was cut to the first 12,000 and last 4,000. Agreement was 85.6% for articles coded from PDFs and 89.2% for articles the agent found itself, but the two groups differ in other ways as well.
- We did not re-audit the human reference standard.

## 6. Possible improvements

- Check every extracted URL with a direct HTTP or repository API request.
- Ask the model for a confidence score per variable and use it to prioritise human checks.
- Compare several runs or models.
- Test revised instructions on a new sample of articles.

## References

- Hardwicke, T. E., Thibault, R. T., Clarke, B., Moodie, N., Crüwell, S., Schiavone, S. R., Handcock, S. A., Nghiem, K. A., Mody, F., Eerola, T., & Vazire, S. (2024). Prevalence of transparent research practices in psychology: A cross-sectional study of empirical articles published in 2022. *Advances in Methods and Practices in Psychological Science, 7*(4). https://doi.org/10.1177/25152459241283477
- Hardwicke, T. E., Thibault, R. T., Kosie, J. E., Wallach, J. D., Kidwell, M. C., & Ioannidis, J. P. A. (2022). Estimating the prevalence of transparency and reproducibility-related research practices in psychology (2014 to 2017). *Perspectives on Psychological Science, 17*(1), 239 to 251. https://doi.org/10.1177/1745691620979806
- Lakens, D. (2026). *The Metacheck Manual*. https://www.scienceverse.org/metacheck_book/
- Landis, J. R., & Koch, G. G. (1977). The measurement of observer agreement for categorical data. *Biometrics, 33*(1), 159 to 174. https://doi.org/10.2307/2529310
- Miske, et al. (2026). Investigating the reproducibility of the social and behavioural sciences. *Nature*. https://doi.org/10.1038/s41586-026-10203-5
- Munafò, M. R., Nosek, B. A., Bishop, D. V. M., Button, K. S., Chambers, C. D., Percie Du Sert, N., Simonsohn, U., Wagenmakers, E.-J., Ware, J. J., & Ioannidis, J. P. A. (2017). A manifesto for reproducible science. *Nature Human Behaviour, 1*(1), 0021. https://doi.org/10.1038/s41562-016-0021
- Wang, L., Ma, C., Feng, X., Zhang, Z., Yang, H., Zhang, J., Chen, Z., Tang, J., Chen, X., Lin, Y., Zhao, W. X., Wei, Z., & Wen, J. (2024). A survey on large language model based autonomous agents. *Frontiers of Computer Science, 18*(6). https://doi.org/10.1007/s11704-024-40231-1

