# Spam Email Classifier

A machine learning project that classifies emails as spam or ham (legitimate) using various text vectorization and classification techniques.

## Project Overview

This project implements and compares multiple spam detection models using the classic SpamAssassin Public Corpus dataset. The goal was to explore different combinations of text vectorization methods and classification algorithms, then evaluate their performance on both test data and modern email samples.

## Dataset

- **Source:** [SpamAssassin Public Corpus](https://spamassassin.apache.org/old/publiccorpus/)
- **Size:** 3,595 emails
- **Distribution:** 30.1% spam, 69.9% ham
- **Time period:** 2002-2005
- **Split:** 67% training, 33% testing

## Models Implemented

The project tests four different model combinations:

1. **CountVectorizer + Naive Bayes**
2. **CountVectorizer + Logistic Regression**
3. **TF-IDF Vectorizer + Naive Bayes**
4. **TF-IDF Vectorizer + Logistic Regression**

## Results

### Test Set Performance

| Model | Accuracy | Precision | Recall | F1-Score | AUC |
|-------|----------|-----------|--------|----------|-----|
| Count + LogReg | **97.6%** | 97.6% | 97.6% | 97.6% | 0.993 |
| TF-IDF + LogReg | 96.6% | 96.6% | 96.6% | 96.6% | 0.995 |
| Count + NB | 96.8% | 96.8% | 96.8% | 96.8% | 0.987 |
| TF-IDF + NB | 96.8% | 96.8% | 96.8% | 96.8% | 0.995 |

### Real-World Testing (Modern Emails)

To assess model generalization, I tested on 19 AI-generated modern emails:

| Model | Overall Accuracy | SPAM Detection | HAM Detection |
|-------|-----------------|----------------|---------------|
| **TF-IDF + LogReg** | **73.7%** | 80.0% | 66.7% |
| Count + NB | 68.4% | 100.0% | 33.3% |
| TF-IDF + NB | 68.4% | 90.0% | 44.4% |
| Count + LogReg | 63.2% | 90.0% | 33.3% |

## Key Findings

### Performance Gap Analysis

There's a 23-35% accuracy drop when moving from test set to modern emails. This is expected because:

- The training dataset is from 2002-2005 (20+ years old)
- Spam tactics have evolved significantly (phishing, social engineering)
- Legitimate email patterns have changed (automated notifications, marketing)
- Modern emails contain language patterns not present in the original corpus

Despite this temporal gap, achieving 73.7% accuracy on contemporary emails shows the models learned robust fundamental patterns.

### Top Discriminative Features

**Spam indicators:** click, free, credit, remove, money, mortgage, email  
**Ham indicators:** date, wrote, said, users, url, supplied

### Model Optimization

- **Naive Bayes:** Best alpha = 0.1 (97.3% accuracy)
- **Logistic Regression:** Best C = 100 (98.1% accuracy)

## Technologies Used

- Python 3.10
- scikit-learn (CountVectorizer, TfidfVectorizer, MultinomialNB, LogisticRegression)
- pandas
- numpy
- matplotlib
- seaborn


## Conclusions

The project demonstrates that while classical ML models can achieve excellent performance on spam detection (97.6% on test data), their effectiveness degrades when confronted with modern email patterns. The TF-IDF + Logistic Regression combination proved most robust for generalization.

For production use, these models would benefit from:
- Periodic retraining with recent email samples
- Hybrid approach combining ML with rule-based pattern detection
- Active learning from misclassified examples
- Integration with modern NLP techniques (embeddings, transformers)

## Future Improvements

- Test with modern datasets
- Implement deep learning approaches (LSTM, BERT)
- Add feature engineering (email metadata, sender reputation)


