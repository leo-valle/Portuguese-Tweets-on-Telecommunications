# Portuguese Tweets on Telecommunications Service Problems

Dataset, code, and baseline experiments for the paper **"[Paper title]"**, [submitted to / published in IEEE Access].

- **Authors:** Leonardo Vercosa de Oliveira Valle and Sarah Negreiros de Carvalho Leite
- **Paper:** [DOI / link]
- **Dataset (Kaggle):** [link]

## Overview

Complaints about telecommunications services are increasingly posted on social media, but Portuguese-language resources for automatically detecting and categorizing them are scarce. This repository provides a publicly available dataset of Portuguese tweets about telecommunications service problems, together with baseline experiments for two classification tasks:

1. **Binary task:** does the message report a telecommunications service problem?
2. **Multiclass task:** what type of problem does the message report (five classes)?

The baselines compare classical machine learning models, neural networks, and pretrained Transformers under different text representations, preprocessing strategies, Transformer training strategies (transfer learning, fine-tuning, and few-shot learning), and class-balancing techniques.

## Repository Structure

```
.
├── data/
│   ├── [dataset file, e.g. telecom_tweets.csv]
│   └── splits/                  # Stratified 80/10/10 splits (seed 42)
├── queries/
│   └── search_queries.txt       # Keywords used in the Twitter/X API search
├── notebooks/
│   ├── pipeline_experimentos.ipynb
├── results/                     # Metrics for all trained configurations
├── requirements.txt
└── README.md
```

## Dataset

### Collection

Data were collected through the official Twitter/X API between **29 September and 1 December 2025**. The search was guided by a set of keywords aimed at network failures and connectivity problems (see [`queries/`](queries/)).

| Step | Messages |
|---|---|
| Initially collected | 10,069 |
| After filtering | **5,566** |

Filtering steps:

- Removal of duplicates based on unique tweet IDs
- Removal of invalid records (empty texts, encoding or API errors)
- Removal of messages not written in Portuguese

### Annotation

Both tasks were annotated by two annotators using a consensus-based approach: labels were assigned through joint discussion until agreement was reached. No formal inter-annotator agreement metric was computed.

### Labels

| Binary | Multiclass | Problem type | Count | % (of problem tweets) |
|:---:|:---:|---|---:|---:|
| 0 | – | Not a telecommunications problem | 2,657 | 47.75% (of all tweets) |
| 1 | 0 | Signal and connection quality | 2,174 | 74.73% |
| 1 | 1 | Customer service and support | 366 | 12.58% |
| 1 | 2 | Billing and financial issues | 135 | 4.64% |
| 1 | 3 | Marketing and promotional offers (spam) | 124 | 4.26% |
| 1 | 4 | Other | 110 | 3.78% |

- **Binary task:** 2,657 tweets in class 0 (47.75%) and 2,909 in class 1 (52.25%), so the classes are approximately balanced.
- **Multiclass task:** only the 2,909 tweets with binary label 1 are used. The task is strongly imbalanced.
- **Important:** multiclass label `0` does **not** mean "no problem". It represents "Signal and connection quality" within the subset of problem tweets.

### Columns

| Column | Description |
|---|---|
| `[text]` | Tweet text |
| `[class 3]` | binary and multiclass label |


### Ethics and Privacy

The dataset contains only publicly available messages. The study focuses on the textual content and labels, not on user identities.

### License

[CC0 (public domain), as planned for the Kaggle release. Confirm before publishing.]

## Baseline Experiments

### Setup

- **Splits:** stratified 80% train / 10% validation / 10% test, random seed 42
- **Metrics:** accuracy, precision, recall, F1-score. Macro-averaging is used for the multiclass task (weighted F1 is also reported). Training time is recorded for every model.
- **Total:** 477 trained configurations (binary and multiclass combined)

### Preprocessing

- **No preprocessing:** raw text
- **Embedding-oriented preprocessing:** lowercasing and removal of URLs and `@`-mentions (punctuation, digits, and stopwords are preserved)

The same strategies are applied across all model families.

### Models

**Classical machine learning**
- Classifiers: SVM (linear kernel), Multinomial Naive Bayes, Logistic Regression, Random Forest (300 estimators), k-NN (k = 3, Euclidean)
- Representations: Bag-of-Words and TF-IDF (2,000 features, 1–2 grams), Word2Vec (150-d, trained on the training split), FastText (300-d pretrained Portuguese, Common Crawl), SBERT (`paraphrase-multilingual-MiniLM-L12-v2`)
- Naive Bayes is restricted to BoW and TF-IDF (non-negative features)

**Neural networks** (Keras, trainable embedding layer)
- MLP, SimpleRNN, LSTM, GRU, BiLSTM, and 1-D CNN
- Additional MLP on precomputed sentence embeddings (Word2Vec, FastText, SBERT)

**Transformers**
- Models: `bert-base-multilingual-cased`, `bertweet-base`, BERTweetBR, `twitter-roberta-base`, BERTimbau (`bert-base-portuguese-cased`), BERTabaporu
- Training strategies:
  - **Transfer learning:** frozen encoder, only the classification head is trained
  - **Fine-tuning:** classification head and last two encoder layers are trained
  - **Few-shot learning:** frozen encoder, trained on 100 or 50 class-balanced examples per class

### Class Balancing (multiclass only)

| Model family | Technique |
|---|---|
| Classical | SMOTE on the vectorized training features |
| Neural networks | Inverse-frequency class weights (`class_weight` in Keras) |
| Transformers | Weighted cross-entropy loss |

Balanced variants are evaluated as separate conditions alongside the non-balanced ones.

## Results

### Best configuration per model family

| Task | Family | Best configuration | F1 |
|---|---|---|---:|
| Binary | Transformers | BERTabaporu, fine-tuned | **0.915** |
| Binary | Classical | [Logistic Regression + BoW] | [0.892] |
| Binary | Neural network | CNN | [0.870] |
| Multiclass | Transformers | BERTweetBR, fine-tuned | **0.751** (macro) |
| Multiclass | Classical | [Random Forest/LogReg + TF-IDF, balanced] | [0.685] |
| Multiclass | Neural network | CNN, balanced | [0.641] |

### Best Transformer per training strategy

| | Binary F1 | Multiclass macro-F1 |
|---|---:|---:|
| Fine-tuning | 0.915 | 0.751 |
| Transfer learning | 0.838 | 0.605 |
| Few-shot (100/class) | 0.821 | 0.558 |

### Main findings

- Fine-tuned Transformers pretrained on Portuguese achieved the best results on both tasks.
- The best classical models came within about three F1 points on the binary task at a small fraction of the training cost.
- Models pretrained only on English were consistently outperformed by Portuguese-pretrained ones.
- Class balancing improved multiclass performance mainly for classical models and neural networks, with no consistent average benefit for Transformers.
- Training cost differs by orders of magnitude: Transformer training took about 106 CPU-hours in total, versus under 1 hour for all classical and neural experiments combined.

## Computational Environment

All experiments ran on the same machine, using **CPU only**.

- **OS / hardware:** Windows 11 Home, Intel Core i7-8565U (4 cores / 8 threads), 20 GB RAM (the NVIDIA MX110 GPU was not used)
- **Python:** 3.10.10 (Jupyter Notebook)
- **Libraries:** scikit-learn 1.7.2, TensorFlow 2.20.0, Keras 3.12.1, PyTorch 2.11.0+cpu, Transformers 5.6.0, Gensim 4.4.0, NumPy 2.2.6, Pandas 2.3.3

## How to Reproduce

```bash
git clone https://github.com/[user]/[repository].git
cd [repository]
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

Then run the notebooks in `notebooks/`. All splits use random seed 42.

## Limitations

- Annotation was consensus-based, with no formal inter-annotator agreement metric.
- The multiclass task is strongly imbalanced.
- Keyword-based collection introduces selection bias toward network failures, which explains the predominance of the "Signal and connection quality" class.
