# Data Documentation for Intelligent Job Recommendation System

## Datasets Overview
1. **Resume Dataset (`resume_dataset_train_raw.csv`, `resume_dataset_eval_raw.csv`)**
   - Source: HuggingFace (Open Source)
   - Contains: Raw resume texts across professional categories.
   - License: Apache-2.0
2. **Data Science Job Descriptions (`ds_job_descriptions_raw.jsonl`)**
   - Source: HuggingFace
   - Contains: Detailed job postings and requirements.
   - License: WTFPL
3. **Resume-Job Fairness Evaluation Dataset (`fairness_eval_pairs_raw.csv`)**
   - Source: HuggingFace
   - Contains: Long-text pairs of CVs and Jobs for testing LLM personalization.
   - License: MIT

## Preprocessing Steps (Planned)
- Lowercasing all text.
- Removing HTML tags and special characters.
- Tokenization for Sentence-BERT embeddings.
Raw data is strictly read-only. All cleaned data will be saved in `data/processed/`.