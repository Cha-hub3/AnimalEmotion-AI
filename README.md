# AnimalEmotion AI — Phase 1 Dataset Audit

This repository provides a Google Colab/PyTorch notebook for an evidence-driven dataset audit of the Kaggle AnimalEmotion dataset.

- Notebook: [`AnimalEmotion_AI_Phase1_Audit.ipynb`](AnimalEmotion_AI_Phase1_Audit.ipynb)
- Dataset: https://www.kaggle.com/datasets/kk2004/animalemotion/data
- Scope: discovery, integrity and format classification, image metadata, exact/optional perceptual duplicates, annotation mapping review, leakage risk indicators, metadata/license review, and machine-readable reports.
- Excluded by design: model training, automatic image deletion/modification, and train/validation/test splitting.

## Run in Colab

1. Open the notebook from GitHub in Google Colab or upload the `.ipynb` file.
2. Add `KAGGLE_USERNAME` and `KAGGLE_KEY` under Colab **Secrets**, and enable notebook access. The notebook also supports uploading `kaggle.json` without printing its contents.
3. Run all cells. GPU is detected but not required for this audit.
4. Review the annotation mapping and report outputs. By default, no labels are considered verified. After checking documentation and actual sample mappings, set `VERIFIED_LABEL_COLUMNS` in its cell to the reviewed source path and exact column name(s), then rerun the analysis cells below it.
5. The notebook creates `/content/animalemotion/reports` and a downloadable ZIP at `/content/animalemotion/animalemotion_phase1_audit_reports.zip`.

Kaggle access and dataset license/usage restrictions apply. The generated license fields are a review aid, not legal advice.

## Audit details

- Safe ZIP extraction rejects traversal, absolute paths and symlinks.
- Image states distinguish `ok`, `corrupted`, `unsupported_format` (including HEIC/HEIF when no decoder is installed), and `unreadable`.
- EXIF orientation correction is used for reported dimensions and visualizations; source bytes are not rewritten.
- Annotation filename/path columns are discovered heuristically; the notebook emits matched, unmatched, duplicate-reference, conflicting-label, and unlabeled-image reports. Heuristic label candidates are not treated as authoritative.
- Optional perceptual hashing uses banded candidate generation with caps on oversized buckets and candidate pairs; it can miss near-duplicates and is off by default.
- Leakage signals include exact/near duplicates, repeated filename stems and possible repeated subject identifiers. These are review indicators, not proof of leakage or subject identity.
- Stable notebook cell IDs and runtime resource snapshots are included.

## Validation status

The notebook JSON and code cells were statically reviewed for structure, cell IDs, syntax, report paths, schemas, and execution dependencies during this change. It has **not** been run end-to-end in Colab: live execution depends on Kaggle credentials, dataset availability, and Colab runtime. Therefore dataset counts, report contents, successful Kaggle metadata retrieval, and generated visualizations remain unverified until the notebook is run.
