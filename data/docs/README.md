# Data

Two English parts of the Djinni Recruitment Dataset (anonymized IT CVs and job postings from djinni.co, 2020-2023).

| Dataset | Source | License | Local folder |
|---|---|---|---|
| Candidate profiles (210,250 CVs) | https://huggingface.co/datasets/lang-uk/recruitment-dataset-candidate-profiles-english | MIT | `data/raw/djinni_candidates/` |
| Job descriptions (141,897 postings) | https://huggingface.co/datasets/lang-uk/recruitment-dataset-job-descriptions-english | MIT | `data/raw/djinni_jobs/` |

Paper: N. Drushchak, M. Romanyshyn, "Introducing the Djinni Recruitment Dataset: A Corpus of Anonymized CVs and Job Postings", UNLP 2024. https://aclanthology.org/2024.unlp-1.2

## Files

- `data/raw/` - original Parquet files and dataset cards from Hugging Face. Not changed.
- `data/processed/candidates_it_v1.csv` - 132,220 CVs with IT roles only.
- `data/processed/jobs_it_v1.csv` - random sample of 20,000 IT job postings.
- `data/samples/` - 50 rows of each processed file.
- `data/docs/codebook.md` - description of all columns.

The processed files are created by `notebooks/01_data_selection.ipynb` (`random_state = 5267`).
