# HFD-MDR
miRNA–Drug Resistance Association Prediction Based on Multi-source Feature Representations and Hierarchical Fusion of Drug Features

## 1. Overview

This repository provides the implementation of HFD-MDR for predicting miRNA–drug resistance associations using pretrained miRNA representations and hierarchical fusion of multi-source drug features.

The repository is organized as follows:

- `data/` contains the MDR dataset and drug features:
  - `associations.xlsx`: known miRNA–drug resistance association matrix.
  - `drugs.xlsx`: DrugBank IDs and SMILES strings.
  - `mirnas.xlsx`: miRNA names and sequences.
  - `positive.edgelist`: known positive association pairs.
  - `negative.edgelist`: candidate negative pairs from unknown associations.
  - `admet.csv`: drug ADMET features.
  - `targets.csv`: drug-target feature vectors.
  - `drug_info.csv`: drug indices, DrugBank IDs, and SMILES strings.

- `code/` contains the model and experiment scripts:
  - `data.py`: data preprocessing and batch construction.
  - `model.py`: the HFD-MDR model.
  - `paths.py`: data, model, and output paths.
  - `train_split.py`: training and evaluation with an 80:20 pair-level split.
  - `train_cv.py`: five-fold cross-validation.
  - `analyze_weights.py`: fusion-weight analysis and heatmap generation.

- `models/chemberta/`: directory for ChemBERTa configuration, tokenizer, and pretrained weights.
- `main.py`: the unified experiment entry point.
- `results/`: experiment outputs, created automatically.


## 2. Dependencies

The software versions used in the current training environment are:

- Python == 3.10.20
- torch == 2.1.2+cu118
- torch-geometric == 2.4.0
- numpy == 1.24.4
- pandas == 2.3.3
- rdkit == 2026.3.1
- transformers == 4.37.2
- rna-fm == 0.2.2
- scikit-learn == 1.7.2
- matplotlib == 3.10.9
- openpyxl == 3.1.5

PyTorch uses the CUDA 11.8 build. The RNA-FM package is imported as `fm` in the code.

Before training, ensure that the original ChemBERTa pretrained weights are available in `models/chemberta/` alongside the configuration and tokenizer files. RNA-FM pretrained weights must also be available to `fm.pretrained.rna_fm_t12()`.


## 3. Quick Start

1. Download and unzip the code and data files.
2. Activate the training environment and prepare the pretrained model weights.
3. Run the required experiment from the project root containing `main.py`.


### Five-fold cross-validation

```bash
python main.py cv
```

### Fusion-weight analysis and heatmaps

```bash
python main.py weights
```

Results are saved to `results/split/`, `results/cv/`, and `results/weights/`, respectively.
