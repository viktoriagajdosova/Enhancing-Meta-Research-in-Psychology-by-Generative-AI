# Setup and Execution

This manual explains how to run the agent on your own list of articles using Google Colab.

## Requirements

- A Google account (for Google Colab).
- An OpenAI API key with access to a model that supports the `web_search` tool in the Responses API. The paper used `gpt-5.6-luna`.
- A list of articles as a CSV file.
- For paywalled articles: PDF files that you have legal access to.

## 1. Prepare the article list

Create a CSV file with one row per article. Required columns:

| Column | Content |
|---|---|
| `article_id` | Any unique identifier (used as the PDF file name) |
| `DOI` | Full DOI link, e.g. `https://doi.org/10.1177/...` |
| `journal_name` | Journal name |
| `title` | Article title |

## 2. Add the API key

1. Open the notebook in Google Colab.
2. In the left panel choose **Secrets** (key icon) and add a secret named `OPENAI_API_KEY2` with your key.
3. Enable notebook access for that secret.

Never paste the key into a notebook cell or commit it to GitHub.

## 3. Run the notebook

Run the cells in order.

| Step | What happens |
|---|---|
| 0 | You upload the article list (CSV) |
| 1 | The agent tries to find a free full text for each article |
| 2 | Articles are split into "found by the agent" and "needs PDF" |
| 3 | You upload PDFs named `<article_id>.pdf` for the second group (skip if none) |
| 4 | The coding instructions and the JSON response template are loaded |
| 5 to 6 | Each article is coded. If a response is not valid JSON, or the agent did not use web search, the call is repeated up to three times. If an article that was found online turns out to be unreachable, the notebook pauses and asks for a PDF |
| 7 | Results are flattened into one row per article and saved |

## 4. Outputs

The notebook downloads three files:

- `agentic_coding_results_wide.csv`: one row per article, one column per variable, plus verbatim quotations and checked URLs.
- `accessibility_check.csv`: result of Step 1 (found online or not, and the URL).
- `agentic_search_log.csv`: the raw record of web searches made by the model, taken from the API response (independent of what the model says it did).

## 5. Changing the model

The model is set in one variable at the top of the notebook:

```python
MODEL = "gpt-5.6-luna"
```

Replace it with another model that supports `web_search`. No other change is needed. Results may differ between models, so re-check accuracy before using a different one.

## 6. Checking the results

The agent's output should be verified by a person, especially for:

- every `*_access_status` value of "NO" (the agent often under-reports access),
- every materials statement coded `UNCLEAR`,
- articles where the output contains empty values or a note that the text could not be read,
- any funding or conflict-of-interest statement coded as absent.

Compare agent and human values with the same variable names and compute agreement (percentage and Cohen's κ). The definitions of the metrics are in [`THEORY.md`](THEORY.md).

## Notes

- Long PDFs: if the extracted text is longer than 16,000 characters, only the first 12,000 and last 4,000 characters are sent to the model. Information in the middle of the article is not seen.
- Costs depend on the model and the number of articles. Test on 10 to 20 articles first.
- Do not upload full-text PDFs to a public repository.

