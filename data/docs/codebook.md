# Codebook

Data dictionary for the two datasets used in the thesis. Both come from the Djinni Recruitment Dataset [1]:

| Dataset | Hugging Face id | Raw file | License |
|---|---|---|---|
| Candidate profiles (CVs) | [`lang-uk/recruitment-dataset-candidate-profiles-english`](https://huggingface.co/datasets/lang-uk/recruitment-dataset-candidate-profiles-english) | `data/raw/djinni_candidates/train-00000-of-00001.parquet` | MIT |
| Job descriptions | [`lang-uk/recruitment-dataset-job-descriptions-english`](https://huggingface.co/datasets/lang-uk/recruitment-dataset-job-descriptions-english) | `data/raw/djinni_jobs/train-00000-of-00001.parquet` | MIT |

Missing values, counts and lengths below are measured on the selected IT subset (`data/processed/*_it_v1.csv`, produced by `notebooks/01_data_selection.ipynb`): 132,220 candidates and 20,000 jobs. Text length is counted in words (split on whitespace). Empty cells are stored as empty values in CSV and read as `NaN` by pandas.

## 1. Candidate profiles

| Column | Type | Meaning | Values / range | Missing |
|---|---|---|---|---|
| `id` | string (UUID) | Unique record identifier, used as the key | unique for every row | 0% |
| `Position` | text | Job title the candidate is looking for, written by the candidate | free text, median 3 words, e.g. `Senior .Net Developer` | 0% |
| `Primary Keyword` | categorical | Main specialization selected on the Djinni platform | 41 values in raw candidate data (45 in job data), 23 kept (see section 3) | 0% |
| `Experience Years` | float | Years of commercial experience | 0, 0.5, 1, 1.5, 2, 2.5, 3–11; 11 is the largest value (meaning of the cap is not documented, most likely "10+ years") | 0% |
| `English Level` | categorical (ordinal) | Self-reported English level | `no_english` < `basic` < `pre` < `intermediate` < `upper` < `fluent` | 0.3% |
| `Highlights` | text | Main achievements | free text, median 31 words | 50.6% |
| `Moreinfo` | text | Main "about me" section: experience, projects, skills | free text, median 72 words | 0% |
| `Looking For` | text | What kind of job or team the candidate wants | free text, median 18 words | 49.5% |
| `CV` | text | Full profile text. Concatenation of `Highlights`, `Moreinfo` and `Looking For`. **Main field used for matching** | free text, median 102 words, 1–1,061 words | 0% |
| `CV_lang` | categorical | Language of `CV` detected by the dataset authors | only `en` | 0% |
| `role_family` | categorical | **Added in this project.** Broader role group derived from `Primary Keyword` (section 3) | 8 values | 0% |

## 2. Job descriptions

| Column | Type | Meaning | Values / range | Missing |
|---|---|---|---|---|
| `id` | string (UUID) | Unique record identifier, used as the key | unique for every row | 0% |
| `Position` | text | Job title of the posting | free text, median 3 words | 0% |
| `Company Name` | text | Name of the hiring company | 4,561 distinct companies in the sample | 0% |
| `Primary Keyword` | categorical | Main specialization of the posting on Djinni | same values as for candidates | 0% |
| `Exp Years` | categorical (ordinal) | Required years of experience | `no_exp`, `1y`, `2y`, `3y`, `5y` | 0% |
| `English Level` | categorical (ordinal) | Required English level | `basic` < `pre` < `intermediate` < `upper` < `fluent` | 5.9% |
| `Published` | date-time (string) | Month of publication, ISO 8601 with time zone, always the first day of the month | `2020-01-01T00:00:00+02:00` … `2023-09-01T00:00:00+03:00` | 0% |
| `Long Description` | text | Full job posting: company, responsibilities, requirements. **Main field used for matching** | free text, median 221 words, 19–2,022 words | 0% |
| `Long Description_lang` | categorical | Language of `Long Description` | only `en` | 0% |
| `role_family` | categorical | **Added in this project.** Same mapping as for candidates | 8 values | 0% |

## 3. `role_family` mapping

Only the following `Primary Keyword` values are kept. All other values (Design, Marketing, HR, Recruiter, Sales, Project Manager, Product Manager, Business Analyst, SEO, Lead Generation, Artist, Scrum Master, Technical Writing, Support, Salesforce, Sysadmin, Lead, Other and a few single-row values) are removed.

| `role_family` | `Primary Keyword` values |
|---|---|
| Backend | Java, .NET, Python, PHP, Node.js, Golang, Ruby, Scala, Rust, C++ |
| Frontend / JavaScript | JavaScript |
| Mobile | iOS, Android, Flutter |
| GameDev | Unity |
| Data / ML | Data Science, Data Engineer, Data Analyst, SQL |
| DevOps | DevOps |
| QA | QA, QA Automation |
| Security | Security |

## 4. Removed columns

| Column | Reason |
|---|---|
| `__index_level_0__` | Technical row index left from the original export, has no meaning |

## 5. Known data issues

These are handled in the preprocessing step (Chapter 4), not in the raw files.

- `Primary Keyword` is chosen by the user and is sometimes wrong, e.g. some 2D animators use `Unity`, a 1C developer uses `Flutter`.
- Some texts contain broken characters (`�`), non-breaking spaces and zero-width spaces (`​`).
- A few texts still contain contact data: about 10 phone numbers and some LinkedIn / GitHub / Telegram links.
- `Highlights`, `Moreinfo` and `Looking For` are already included in `CV`, so they are not used as separate inputs.

## References

[1] N. Drushchak and M. Romanyshyn, "Introducing the Djinni Recruitment Dataset: A Corpus of Anonymized CVs and Job Postings," in *Proc. Third Ukrainian Natural Language Processing Workshop (UNLP) @ LREC-COLING 2024*, Torino, Italy, 2024, pp. 8–13. https://aclanthology.org/2024.unlp-1.2
