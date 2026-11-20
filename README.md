# Handwritten Digit Recognition: KNN vs SVM

Mini project (Introduction to Machine Learning). Comparison of **K-Nearest Neighbours (KNN)** and a **Support Vector Machine (SVM)** for recognising handwritten digits.

## Team

1. Aum Trivedi         2000017437
2. Parthsinh Chavda    2000017025
3. Neel Patel          2000016653


## Dataset
UCI *Optical Recognition of Handwritten Digits* (id 80), fetched in the notebook with the `ucimlrepo` package:
5,620 images of 8x8 pixels (64 features), 10 classes (digits 0 to 9).

## Method (see `Handwritten_Digit_Recognition.ipynb`)
1. Load the dataset with `fetch_ucirepo(id=80)`
2. Stratified 80/20 split (4,496 train / 1,124 test), `random_state=42`
3. `StandardScaler` fitted on the training data only, then applied to the test data
4. KNN (`n_neighbors=5`) and SVM (`kernel='rbf'`), library default settings
5. Accuracy, classification report and confusion matrix for both models

## Results (1,124 test images)
| Metric | KNN | SVM |
|---|---|---|
| Accuracy (%) | 97.78 | **98.67** |
| Precision, macro (%) | 97.78 | **98.70** |
| Recall, macro (%) | 97.77 | **98.66** |
| F1-score, macro (%) | 97.77 | **98.67** |
| Errors | 25 | **15** |
| 95% Wilson CI of accuracy (%) | 96.7–98.5 | 97.8–99.2 |

The SVM made 10 fewer errors, but the two 95% intervals overlap, so the advantage is suggestive rather than conclusive.

Per-class precision (P), recall (R) and F1:

| Digit | KNN P | KNN R | KNN F1 | SVM P | SVM R | SVM F1 |
|---|---|---|---|---|---|---|
| 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| 1 | 0.983 | 1.000 | 0.991 | 0.991 | 0.991 | 0.991 |
| 2 | 1.000 | 1.000 | 1.000 | 1.000 | 0.991 | 0.995 |
| 3 | 0.982 | 0.965 | 0.973 | 0.966 | 0.991 | 0.978 |
| 4 | 0.983 | 0.991 | 0.987 | 0.966 | 1.000 | 0.983 |
| 5 | 0.964 | 0.964 | 0.964 | 0.982 | 0.991 | 0.987 |
| 6 | 0.991 | 1.000 | 0.996 | 0.991 | 0.991 | 0.991 |
| 7 | 0.948 | 0.965 | 0.956 | 1.000 | 0.973 | 0.987 |
| 8 | 0.972 | 0.937 | 0.954 | 1.000 | 0.964 | 0.982 |
| 9 | 0.955 | 0.955 | 0.955 | 0.973 | 0.973 | 0.973 |

## Repository structure
```
.
├── Handwritten_Digit_Recognition.ipynb   # project notebook (all experiments)
├── results_notebook.json                 # metrics used in the paper and slides
├── paper_figures.py                      # redraws the paper figures from results_notebook.json
├── requirements.txt
├── figures/
│   ├── notebook_outputs/                 # screenshots of the notebook outputs
│   └── paper/                            # figures used in the paper
├── paper/                                # IEEE-style research paper (Word)
└── presentation/                         # slides (PowerPoint)
```

## How to run
```bash
git clone https://github.com/aumtrivedi1602/Handwritten-digit-recognition.git
cd Handwritten-digit-recognition
pip install -r requirements.txt
jupyter notebook Handwritten_Digit_Recognition.ipynb     # run all cells (internet needed to fetch the dataset)
python paper_figures.py                                  # optional: redraw the paper figures
```

## Notes on results_notebook.json
Accuracy and per-class values come from the notebook's printed output. The two confusion matrices were read from the notebook's heatmaps and checked: they reproduce the printed accuracies (97.7758% and 98.6655%) and every printed per-class precision, recall and F1 value.

## Limitations
One random split, default hyper-parameters (no tuning), only two models, no ablation study, and images of the same writer may appear in both training and test sets.

## References
See the reference list in `paper/Digit_Recognition_IEEE_Paper.docx`.

