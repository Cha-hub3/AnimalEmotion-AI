# AnimalEmotion AI — Phase 1 Dataset Audit

This Google Colab notebook performs a manual-ZIP, evidence-driven dataset audit. It does not train a model or create data splits.

## Run in Colab

1. Download the dataset ZIP manually from https://www.kaggle.com/datasets/kk2004/animalemotion/data.
2. Open `AnimalEmotion_AI_Phase1_Audit.ipynb` in Colab.
3. Run all cells. The upload cell requires exactly one `.zip` file.
4. Set `MAX_RECOMMENDED_ZIP_MB` to change the large-upload warning threshold. `files.upload()` remains unchanged and loads the uploaded ZIP into Colab memory.
5. `DATA_DIR` must be empty. Existing extracted files stop the notebook without automatic deletion, preventing mixed dataset versions.
6. Existing ZIP files are never overwritten. A byte-identical existing ZIP is reused; a different ZIP receives a non-conflicting filename.

## Static validation

The final validator scans executable code cells only, excluding itself. It excludes Markdown, validates notebook JSON and unique IDs, parses every executable code cell with `ast.parse`, and detects forbidden Kaggle API/Hub/credential acquisition imports and calls. Live Colab upload/extraction remains dependent on runtime conditions and the uploaded archive.
