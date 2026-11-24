# AnimalEmotion AI — Phase 1 Dataset Audit

Google Colab notebook for a non-destructive, evidence-driven audit of the AnimalEmotion dataset.

- Notebook: [`AnimalEmotion_AI_Phase1_Audit.ipynb`](AnimalEmotion_AI_Phase1_Audit.ipynb)
- Dataset page: https://www.kaggle.com/datasets/kk2004/animalemotion/data
- Scope: file/image discovery, integrity, EXIF-aware metadata, exact/optional near duplicates, annotation mapping review, verified-label EDA, leakage indicators, and audit reports.
- No model training, train/validation/test splits, Kaggle API credentials, or automatic image deletion/modification.

## Run in Google Colab

1. Download the dataset ZIP manually from the Kaggle dataset page. Any Kaggle sign-in or dataset terms acceptance is handled by you on Kaggle.
2. Open `AnimalEmotion_AI_Phase1_Audit.ipynb` in Colab and run cells top-to-bottom.
3. In the upload prompt select exactly one `.zip` dataset file. The notebook requires no Kaggle API token, KaggleHub, Colab Secrets, or Kaggle CLI.
4. The archive is saved under `/content/animalemotion/uploads/` and safely extracted into `/content/animalemotion/dataset/`. Reports are kept separately at `/content/animalemotion/reports/`.
5. The notebook preflights archive paths, rejects traversal/absolute paths/symlinks and duplicate ZIP members, checks ZIP integrity, and refuses to overwrite existing extraction files. The original ZIP is retained. If a prior runtime has colliding extracted files, use a fresh Colab runtime or choose an empty dataset directory; do not delete data unless you choose to do so yourself.
6. Review annotation mapping outputs. Labels are not authoritative by default. After checking source documentation and samples, configure `VERIFIED_LABEL_COLUMNS` explicitly to produce class distributions and per-class galleries.
7. Review the dataset license/usage status manually. Dataset version and license are not guaranteed to be embedded in the manually uploaded ZIP; the report records uncertainty rather than inventing values.

## Reports

The notebook creates CSV/JSON inventories and findings under `/content/animalemotion/reports`, validates its expected reports, and offers `animalemotion_phase1_audit_reports.zip` for download. Near-duplicate pHash detection is optional and capped; a bounded candidate search can still miss pairs. Leakage indicators such as repeated stems and subject-like columns require human interpretation.

## Validation caveat

Static notebook structure and Python-cell checks are included. The repository update itself is not a live Colab run: actual upload, ZIP extraction, image counts, report values, and browser download must be verified by executing it in Colab.
