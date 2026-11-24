# AnimalEmotion AI – Phase 1 Dataset Audit

This repository contains a production-oriented Google Colab notebook for the Phase 1 dataset audit of **AnimalEmotion AI**.

- Dataset: https://www.kaggle.com/datasets/kk2004/animalemotion/data
- Framework: PyTorch / torchvision
- Scope: dataset discovery, integrity checks, duplicate checks, label evidence, imbalance and leakage-risk assessment
- Explicitly excluded: model training, augmentation strategy deployment, and train/validation/test splitting

## Files

- `AnimalEmotion_AI_Phase1_Audit.ipynb` – complete executable Colab notebook

## Run in Google Colab

1. Open https://colab.research.google.com/.
2. Upload `AnimalEmotion_AI_Phase1_Audit.ipynb` or open it from GitHub.
3. Set Colab runtime to a supported Python 3 environment. A GPU is detected but is not required for the audit.
4. In Colab, open **Secrets** from the left panel and add:
   - `KAGGLE_USERNAME`
   - `KAGGLE_KEY`
5. Enable notebook access to those secrets.
6. Run **Runtime → Run all**.

If Colab Secrets are unavailable, the notebook provides a secure upload fallback for `kaggle.json`. Credentials are never printed or written into reports. Kaggle API terms and dataset access requirements still apply.

## Outputs

The notebook writes reports under:

```text
/content/animalemotion/reports
```

It also creates:

```text
/content/animalemotion/animalemotion_phase1_audit_reports.zip
```

and attempts to start a browser download. Key reports include:

- `audit_summary.json`
- `phase1_verdict.json`
- `image_inventory.csv`
- `corrupted_images.csv`
- `exact_duplicates.csv`
- `perceptual_duplicate_candidates.csv` (optional)
- `annotation_manifest.csv`
- `confirmed_label_evidence.csv`
- `class_distribution.csv`
- `imbalance_analysis.csv`
- `hierarchy_discovery.csv`
- `leakage_assessment.json`
- visualizations and a report manifest

## Perceptual duplicate detection

Set `ENABLE_PHASH=True` in the notebook if perceptual duplicate checking is required. It is disabled by default to keep routine audits reproducible and reasonably fast.

## Safety and methodology

- ZIP entries are checked for absolute paths, parent traversal, links, and destination escapes.
- Original images are never deleted or modified.
- Folder names are retained only as inferred evidence.
- Confirmed labels are reported only from explicit annotation evidence.
- No train/validation/test split is created.

## Reproduction

The notebook fixes NumPy, PyTorch, and NumPy random seeds to `42` and uses deterministic PyTorch settings where applicable.

## Disclaimer

Audit results depend on the files and metadata present at download time. The final verdict is evidence-based and explicitly distinguishes confirmed findings from unresolved questions.
