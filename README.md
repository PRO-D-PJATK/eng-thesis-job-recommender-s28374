# Intelligent Job Recommendation and CV Personalization System Using Large Language Models

The system ranks IT job vacancies for a given CV with Sentence-BERT, compares it with a BM25 keyword baseline, and adapts the CV to a selected job with a large language model.

## Structure

- `docs/` - thesis chapters (PDF)
- `data/raw/` - original datasets
- `data/processed/` - processed data
- `data/samples/` - small previews of the processed data
- `data/docs/` - data README and codebook
- `notebooks/` - data processing notebooks

## Data

The raw Parquet files and processed CSV files are larger than the GitHub file limit and are not stored in the repository. Download the two Parquet files from the links in `data/docs/README.md` and put them here:

```
data/raw/djinni_candidates/train-00000-of-00001.parquet
data/raw/djinni_jobs/train-00000-of-00001.parquet
```

## Running

```
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/01_data_selection.ipynb
```
