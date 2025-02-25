# Uncertainty-Aware Genomic Classification of Alzheimer’s Disease

This repository demonstrates how to combine a Transformer model with MC-Dropout and RandomForest, then use OOF-based ensemble weighting by maximizing AUC, and thresholding variance to split into Uncertain/Certain groups.

## Folder Structure

```
JoLab-uncertainty/
├── README.md
├── requirements.txt
├── data/
│   ├── APOE_50kb-1050.raw
│   └── DX-1050.txt
├── src/
│   ├── dataset.py
│   ├── model.py
│   ├── training.py
│   ├── evaluation.py
│   └── main.py
└── result/
```
- `dataset.py`: dataset utilities (`load_data`, `split_into_windows_as_sequence`, `SequenceSNPDataset`)
- `model.py`: `TransformerClassifier` with MC-Dropout
- `training.py`: functions to train/evaluate MC-Dropout
- `evaluation.py`: metrics, subgroup analysis, plotting
- `main.py`: main script, orchestrates cross-validation, alpha/threshold selection, and final testing

## Requirements

- Python 3.8+
- PyTorch >= 1.7
- scikit-learn
- pandas
- seaborn
- matplotlib

pip install -r requirements.txt

## Usage

python src/main.py [raw_file.csv] [dx_file.csv] [prefix]

Example:

python src/main.py data/APOE_50kb-1050.raw data/DX-1050.txt apoe-run

It will create outputs in the `result/` folder, such as:

- `_cv_alpha_scores.csv`: fold-wise alpha vs AUC
- `_oof_alpha_AUC_map.csv`: alpha vs AUC on entire OOF
- `_oof_threshold_score.csv`: thresholds vs (Uncertain AUC + Certain AUC)
- `_test_details.csv`, `_test_summary.csv`: final test metrics (All/Uncertain/Certain)
- `_analysis_plots.pdf`: final test ROC/PR/etc. plots
- `_cv_alpha_AUC_plot.pdf`: fold-wise alpha vs AUC line plot

## License
This code is maintained by the **Taeho Jo Research Group** at [Indiana University School of Medicine](https://medicine.iu.edu).  
For more information, visit our lab website: [JoLab.AI](https://www.jolab.ai).

This repository is provided under the [MIT License](LICENSE).  
