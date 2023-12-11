
# Fake News Detection and Summarizer

This project builds multiple machine learning models to detect fake news articles and also includes a news summarizer.

## Overview

The system is trained on a dataset of over 20,000 fake and real news articles scraped from various sources. Several models are trained and evaluated including Logistic Regression, Decision Trees, Random Forest, Gradient Boosting, and SVM. 

In addition to fake news classification, the project also summarizes news articles by extracting key sentences.

## Datasets and Data Processing

The main datasets used are:

- `Fake.csv` - Contains over 20K fake news articles  
- `True.csv` - Contains over 20K real/true news articles

The `data_processing.py` module handles loading these datasets, combining them, and adding additional real and fake samples using NLP techniques:

### Summarizing Real News

- Uses the Google News API to fetch the latest news articles on trending topics
- Scrapes the article content from the website 
- Runs an NLP summary algorithm to get the key sentences
- Saves summaries to `summarys.csv`

### Generating Fake News

- Defines a large corpus of text related to technology, ethics, environment etc.
- Builds a next-word dictionary from this corpus
- Uses the dictionary to generate random fake paragraphs based on a seed topic word
- Saves fake summaries to `random_paragraphs.csv`

The final output is a large CSV file `combined.csv` containing real and fake news samples.

## Preprocessing

The main preprocessing steps are:

### 1. Load and Combine Datasets

- Load fake and real news CSVs
- Add fake/real labels
- Split off small sample for manual testing 
- Concatenate into one dataset
- Shuffle rows 

### 2. Fetch and Summarize Current News

- Use Google News API to get latest articles 
- Scrape article content 
- Run NLP summarization algorithm
- Save summaries to `summarys.csv`

### 3. Generate Fake News

- Build a next-word dictionary from a text corpus  
- Use dictionary to generate random fake paragraphs
- Save to `random_paragraphs.csv`

### 4. Combine All Data

- Concatenate real summaries, fake summaries, and loaded dataset
- Reshuffle all rows randomly

### 5. Preprocess Text

- Clean text by removing special characters, punctuation etc.
- Convert text to TF-IDF vectors


## Models

The following ML models are trained and evaluated:

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting
- SVM 

The models are serialized to .sav files using Pickle.

## Usage

The main entry point is `main.py`. Usage details are:

```
python main.py
```

A manual testing loop is also included to get predictions on custom user-inputted news articles.

Let me know if you need any clarification or have additional suggestions for improving the README!
