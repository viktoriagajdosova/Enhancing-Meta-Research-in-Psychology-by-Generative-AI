GUIDELINE_TEXT = """
You are coding a scientific article for research transparency indicators.

GENERAL RULES:
- Evaluate every field below. If a field is conditional (marked "only if..."), and the
  condition is not met, set its value to "NA".
- For every *_access_status field, you must ACTIVELY find and open the relevant link
  (e.g. a data repository, materials repository, preregistration, or analysis script
  repository) and verify whether it can really be accessed, downloaded, and viewed —
  do NOT infer this just from the statement text. "Available upon request" always
  counts as NO for access_status.
- Do not default to "NO"/"broken link"/"unclear access instructions" out of
  excessive caution. If a link resolves and shows the expected repository/content
  (even if the page layout is unfamiliar, or you cannot fully browse every file),
  that counts as accessible ("YES"). Only mark "NO" if you genuinely could not load
  the page at all, the page shows an explicit error (404, "page not found"), or the
  content is clearly behind a login/paywall/access request form.
- *_verbatim fields must be an EXACT quote from the article, not a paraphrase.
- If you cannot verify something (e.g. broken link, requires login), say so explicitly
  in the relevant *_access_detail or reason field instead of guessing.
- Read the ENTIRE article before concluding a statement is absent. Funding and
  conflict-of-interest statements are usually near the END of the article (after the
  Discussion, in Acknowledgments/Declarations), not in the abstract. Do not conclude
  "NO there is no funding statement" or "NO there is no conflict of interest
  statement" unless you have actually reached and read that part of the article.
- You MUST always respond using the exact JSON structure requested — never respond
  with plain prose, an apology, or a request for more information, even if you were
  unable to access the article. If you cannot access the full text at all, still
  return the JSON: set open_access_status_agreed to the appropriate value based on
  what you could determine, and set every other field's "value" to "NA" with a short
  note in the "verbatim" or "reason" field explaining you could not access the text.
- NEVER invent, guess, or generate placeholder-style content that merely looks
  plausible (e.g. example-style IDs such as "NCT12345678", generic names like
  "XYZ Grant 123" or "Grant 123", or any invented registry number, DOI, author
  name, or figure). Every verbatim quote, ID, URL, and number you report MUST be
  something you actually read in the real article or web page — never something
  you inferred should probably be there based on the pattern of similar articles.
  If you did not actually see a specific ID, number, or exact quote, leave that
  field as "NA" or write "not verified" rather than filling in a plausible-looking
  value.

FIELDS TO CODE:

0. open_access_status_agreed: whether a free, full-text version of the article is
   available. Values: "Yes" / "No I can only access the article through a paywall"

   IMPORTANT: Do not conclude "paywall" after a single search or after seeing a
   publisher page that shows only an abstract. Many articles have a free version
   elsewhere. Before answering "No", try AT LEAST these strategies:
   (a) search by the DOI directly, (b) search by the exact title as a general web
   search, (c) search for the title plus "PDF", "PMC", "preprint", "OSF", or
   "free full text", (d) check PubMed Central (PMC) and preprint servers (e.g.
   PsyArXiv). Only answer "No I can only access the article through a paywall" if
   none of these searches surface a free full-text version.
   If a full-text URL was already found in a prior step (given to you below as
   "KNOWN ACCESSIBLE URL"), use that URL as your starting point — actually open it
   and read the full article there, do not search from scratch or give up early.

1. prereg_statement: whether the article states the study (or an aspect of it) was
   preregistered BEFORE data collection/analysis, in a registry (e.g. OSF, AsPredicted,
   ClinicalTrials.gov, PROSPERO).

   IMPORTANT: Preregistration statements and links (e.g. to AsPredicted, OSF Registries)
   can appear anywhere in the article — in the abstract, Methods section, or as a
   footnote — not only in a dedicated "Transparency" section. Scan the ENTIRE article
   text for registry names (OSF, AsPredicted, ClinicalTrials.gov, PROSPERO, etc.) or
   registration numbers/URLs before concluding there is no statement.

   Values: "NO there is no statement about preregistration" /
           "YES the statement says that there is a preregistration" /
           "YES the statement says that there is no preregistration"
   1a. prereg_statement_verbatim: exact quote
   1b. prereg_access_method: which registry (only if "there is a preregistration")
       Values: Open Science Framework / ClinicalTrials.gov / AsPredicted / PROSPERO /
               Netherlands Trial Register / Clinical Research Information Service /
               Chinese Clinical Trial Registry / Both Open Science Framework and
               AsPredicted / UNCLEAR
   1c. prereg_access_status: actually open the link. YES/NO (only if "there is a
       preregistration")
   1d. prereg_access_detail: if NO, why — "Broken link" / "Unclear access instructions"

2. data_statement: whether the article states RAW/PRIMARY data (individual-level, NOT
   summary/aggregated data) are available. If a third-party data source is cited
   WITHOUT a clear statement of availability, use the UNCLEAR category — do not count
   as available.
   Values: "NO there is no data availability statement" /
           "YES the statement says that the data are available" /
           "YES the statement says that the data are not available" /
           "UNCLEAR a third party source is identified without any indication of availability"
   2a. data_statement_verbatim: exact quote
   2b. data_reason: stated reason if "not available" —
       Not applicable / Not permitted by third party / Participant privacy /
       No participant consent / Data collection ongoing
   2c. data_access_method: how data are accessed (only if "available") —
       Upon request from the authors / An online, third-party repository (e.g., OSF,
       FigShare etc.) / From a third party / Personal or institution website /
       Supplementary materials hosted by the journal / UNCLEAR
   2d. data_access_status: ACTUALLY open the link and try to download. YES/NO (only if
       "available"). "Upon request" = NO.
   2e. data_access_detail: if NO — "Broken link" / "Unclear access instructions" /
       "Upon request"

3. materials_statement: same logic as data, but for research materials (e.g. survey
   instruments, stimuli, non-analysis code).
   Values: "NO there is no materials availability statement" /
           "YES the statement says that the materials are available" /
           "YES the statement says that the materials are not available" /
           "UNCLEAR a third party source is identified without any indication of availability"

   IMPORTANT — distinguish two very different situations when the article names a
   measure/instrument:

   (a) STANDARDIZED, PUBLISHED SCALES/QUESTIONNAIRES cited with an original
   publication reference (e.g. "the 6-item Gratitude Questionnaire (McCullough
   et al., 2002)", "the Mental Health Continuum-Short Form (Keyes, 2013)", "the
   Reading the Mind in the Eyes Test"). These are established, publicly known
   instruments that any researcher could obtain independently by looking up the
   cited publication — mentioning them is NOT a materials availability concern
   in this coding scheme. Use "NO there is no materials availability statement"
   unless the article ALSO makes an explicit statement about sharing/accessing
   ITS OWN version of the materials (e.g. modified items, translated version,
   full item wording as an appendix).

   (b) STUDY-SPECIFIC OR THIRD-PARTY-OWNED MATERIALS without a clear availability
statement — e.g. custom-made stimuli, video clips, a proprietary/unpublished
instrument, or materials attributed to "the project team" or an unnamed
internal source... This also includes generic, unnamed references to specific
measurement tools (e.g., "two psychometric measures were used," "a
questionnaire assessing X was administered") where the article does not
name the instrument or cite its source — the mere fact that a measure was
used, without identifying it, is enough to trigger UNCLEAR.

    In short: a bare citation to a well-known, previously published scale = NO
   statement. A reference to unpublished, custom, or ambiguously-sourced
   material with no access information = UNCLEAR.

   3a. materials_statement_verbatim: exact quote
   3b. materials_reason: stated reason if "not available" —
       Data collection ongoing / No participant consent / Not applicable /
       Not intended for public use / Not permitted by third party
   3c. materials_access_method: (only if "available") —
       An online, third-party repository (e.g., OSF, FigShare etc.) / Supplementary
       materials hosted by the journal / Within the article (or appendices) / Upon
       request from the authors / Personal or institution website / From a third
       party / UNCLEAR
   3d. materials_access_status: ACTUALLY open the link and try to download. YES/NO
       (only if "available"). "Upon request" = NO.
   3e. materials_access_detail: if NO — "Broken link" / "Unclear access instructions" /
       "Upon request"

4. analysis_statement: whether analysis scripts/code (or point-and-click instructions)
   used to produce the reported results are available. (No UNCLEAR category here.)
   Values: "NO there is no analysis script availability statement" /
           "YES the statement says that the analysis scripts are available" /
           "YES the statement says that the analysis scripts are not available"
   4a. analysis_statement_verbatim: exact quote
   4b. analysis_reason: stated reason if "not available" —
       Not applicable / Data collection ongoing
   4c. analysis_access_method: (only if "available") —
       An online, third-party repository (e.g., OSF, FigShare etc.) / Upon request
       from the authors / Supplementary materials hosted by the journal / Within the
       article (or appendices)
   4d. analysis_access_status: ACTUALLY open the link and try to download. YES/NO
       (only if "available"). "Upon request" = NO.
   4e. analysis_access_detail: if NO — "Broken link" / "Upon request"

5. funding_statement: whether the article includes an explicit funding statement
   (disclosing a source, OR explicitly stating there was none). Absence of any
   mention = "NO there is no funding statement". Use UNCLEAR only if a statement
   exists but is ambiguous.

   IMPORTANT: Funding statements are very often located AFTER the main text, near
   the end of the article — commonly under headings like "Funding", "Acknowledgments",
   "Declaration of Interest", "Financial Support", or in a "Transparency" section.
   If you searched but only read the abstract/introduction, you have NOT verified
   this field yet — you must locate and read the end matter of the article
   (Acknowledgments/Declarations/Funding section) before answering "NO there is no
   funding statement".

   Values: "NO there is no funding statement" /
           "YES the statement discloses at least one source of funding" /
           "YES the statement says that there was no relevant funding" / "UNCLEAR"
   5a. funding_statement_verbatim: exact quote

6. coi_statement: whether the article includes an explicit conflict-of-interest
   statement (disclosing a conflict, OR explicitly stating there were none). Absence
   of any mention = "NO there is no conflict of interest statement". Use UNCLEAR only
   if a statement exists but is ambiguous.
   Values: "NO there is no conflict of interest statement" /
           "YES the statement says that there were no conflicts of interest" /
           "YES the statement discloses at least one conflict of interest" / "UNCLEAR"
   6a. coi_statement_verbatim: exact quote

7. research_design_agreed: classify the overall research design of the study.
   This is a multi-select field — if the article combines both experimental and
   non-experimental components, use the combined value.
   Values: "Experimental" / "Non-experimental" / "Meta-analysis" /
           "Experimental, Non-experimental"
"""
