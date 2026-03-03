# Spam Classifier

An NLP-based email/SMS spam classifier built with **Python, Flask, and Scikit-learn**. The model uses **Logistic Regression** trained on TF-IDF features, exposed through a lightweight web interface. The repository also includes the full Jupyter notebook pipeline for training from scratch.

---

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Model Pipeline](#model-pipeline)
- [Setup & Running](#setup--running)
- [How It Works](#how-it-works)

---

## Overview

Paste any text message or email content into the UI and the classifier instantly predicts whether it is **Spam** or **Ham (Not Spam)**. The pre-trained Logistic Regression model is loaded from a `.pkl` file and the TF-IDF vectorizer is applied before prediction.

---

## Features

- Real-time spam/ham classification
- Pre-trained Logistic Regression model (loaded from `logistic_regression_model.pkl`)
- TF-IDF vectorizer (loaded from `tfidf_vectorizer.pkl`)
- Full training notebook (`index.ipynb`) included
- NLTK-based text preprocessing (lowercasing, punctuation removal, stopword removal, Porter stemming)
- Flask web application with HTML frontend

---

## Tech Stack

| Component | Technology |
|---|---|
| Backend | Python, Flask |
| ML Model | Logistic Regression (Scikit-learn) |
| Text Features | TF-IDF Vectorizer |
| NLP | NLTK (stopwords, PorterStemmer, word_tokenize) |
| Frontend | HTML/CSS (Jinja2 templates) |

---

## Project Structure

```
Spam_Classifier/
├── index.ipynb                      # Training notebook (data → model → evaluation)
├── app.py                           # Flask web application
├── logistic_regression_model.pkl    # Pre-trained Logistic Regression model
├── tfidf_vectorizer.pkl              # Pre-fitted TF-IDF vectorizer
├── requirements.txt                 # Python dependencies
├── templates/
│   └── index.html                   # Web UI
├── static/                          # CSS / JS assets
└── README.md
```

---

## Model Pipeline

The notebook `index.ipynb` covers:

1. **Dataset loading** — labelled spam/ham messages
2. **Text preprocessing:**
   ```
   Lowercase → Remove punctuation → Tokenize → Remove stopwords → Porter stemming → Re-join
   ```
3. **TF-IDF vectorization** — converts processed text to numeric feature vectors
4. **Model training** — Logistic Regression classifier
5. **Evaluation** — accuracy, confusion matrix, classification report
6. **Model persistence** — saves `logistic_regression_model.pkl` and `tfidf_vectorizer.pkl`

---

## Setup & Running

### Prerequisites

- Python 3.8+
- pip

### Install dependencies

```bash
git clone https://github.com/jaideepj2004/Spam_Classifier.git
cd Spam_Classifier
pip install -r requirements.txt
```

### Download NLTK data (first run only)

```python
import nltk
nltk.download('stopwords')
nltk.download('punkt')
```

### Run the Flask app

```bash
python app.py
```

Open `http://127.0.0.1:5000`.

---

## How It Works

1. User types a message and submits the form.
2. Flask receives the text via `POST /predict`.
3. Pre-processing: lowercase → strip punctuation → remove stopwords → stem.
4. Text is vectorized using the loaded TF-IDF vectorizer.
5. Logistic Regression predicts `1` (Spam) or `0` (Ham).
6. Result is displayed on the page.

---

## Example

| Input | Prediction |
|---|---|
| "Win a free iPhone! Click now!" | **Spam** |
| "Team meeting at 3pm tomorrow." | **Ham** |
| "Claim your lottery prize — act fast!" | **Spam** |
| "Please review the attached document." | **Ham** |
