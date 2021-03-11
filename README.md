# Terminology Extraction

The references are summarized in [Summary.md](https://github.com/honghanhh/terminology-extraction/blob/paper_summary/references/Summary.md).

## ACTER data structures
```
ACTER
│   README.md
│   sources.txt
│
└───en
│   └───corp
│   |   └───annotations
│   |   |   |   corp_en_terms.ann
│   |   |   |   corp_en_terms_nes.ann
│   |   | 
│   |   └───texts
|   |       └───annotated
│   |       |   corp_en_01.txt
│   |       |   corp_en_02.txt
│   |       |   ...
│   |       |
|   |       └───unannotated
│   |           |   corp_en_03.txt
│   |           |   ...
|   |
│   └───equi (equivalent to "corp")
|   |
│   └───htfl (equivalent to "corp")
|   |
│   └───wind (equivalent to "corp")
|
└───fr (equivalent to "en")
└───nl (equivalent to "en")
```
## Architecture

### 1. Preprocess data

- Input
```
    ./ACTER/en/*/*_en_terms.ann
    ./ACTER/en/texts/annotated/*
```
- Command
```
cd models
python prepocess.py
```
- Output

```
    ./preprocessed_data/corp.pkl
    ./preprocessed_data/equi.pkl
    ./preprocessed_data/wind.pkl
    ./preprocessed_data/htfl.pkl
```

### 2. Reformat training data

- Input
```
    ./preprocessed_data/corp.pkl
    ./preprocessed_data/equi.pkl
    ./preprocessed_data/wind.pkl
```
- Command
```
cd models
python format_data.py
```
- Output

```
    ./preprocessed_data/train.csv
```

### 3. Train model & evaluation
- Models trained on [Collab](https://colab.research.google.com/drive/1ZoiQRj_z-V0Pd6ek9VDYxpvg50eD_DA5?usp=sharing)
    - Variants of BERTs: BERT, RoBERTa, DistilledBERT
    - XLNet

- Default settings: 
```
    adam_epsilon: float = 1e-8
    early_stopping_metric: str = "eval_loss"
    early_stopping_patience: int = 3
    eval_batch_size: int = 16
    learning_rate: float = 4e-5
    manual_seed: int = 2203
    max_seq_length: int = 128
    num_train_epochs: int = 4
    optimizer: str = "AdamW"
    weight_decay: float = 0.0
```

- Evaluation metrics:
    - Precision = TP/(TP+FP)
    - Recall = TP/(TP+FN)
    - F1-score = 2 * (Precision * Recall )/ (Precision+Recall)


- Results on English dataset (train/val - 80/20):
    - English terms only

    |               Models                 | Precision | Recall | F1-score |
    |               :----:                 |   :---:   | :----: |  :-----: |
    |        BERT (bert-base-uncased)      |   77.36   |  46.17 |  57.83   |
    |        BERT (bert-base-cased)        |   72.77   |  42.91 |  53.99   |
    |       RoBERTa (roberta-base)         |   69.53   |  40.11 |  50.87   |
    |DistiledBERT (distilbert-base-uncased)|    |   |    |
    |       XLNet (xlnet-base-cased)       |  |   |    |
    |       __Baseline (TALN-LS2N)__       |   34.78   |  70.87  |  46.66  |

    - English terms with Named Entities (NEs)

    |               Models                 | Precision | Recall | F1-score |
    |               :----:                 |   :---:   | :----: |  :-----: |
    |        BERT (bert-base-uncased)      |   77.48   | 44.99  |   56.93  |
    |        BERT (bert-base-cased)        |   71.27   | 42.13  |   52.96  |
    |       RoBERTa (roberta-base)         |   |   |    |
    |DistiledBERT (distilbert-base-uncased)|    |   |    |
    |       XLNet (xlnet-base-cased)       |    |   |    |
    |       __Baseline (TALN-LS2N)__       |   32.58   |  72.68 |  44.99  |
## Issues
## References
- [Shared Task on Automatic Term Extraction Using the
Annotated Corpora for Term Extraction Research (ACTER) Dataset](https://www.aclweb.org/anthology/2020.computerm-1.12.pdf).
- [TALN-LS2N System for Automatic Term Extraction](https://www.aclweb.org/anthology/2020.computerm-1.13.pdf).
## Contributors:
- 🐮 [@honghanhh](https://github.com/honghanhh)