
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

The project trains an ensemble of different ML models on the fake news classification task, including:

- Logistic Regression
- Decision Tree
- Random Forest
- Gradient Boosting
- SVM with Linear Kernel

Using an ensemble approach provides several key advantages:

**1. Improved Accuracy**

By combining multiple models together, the overall accuracy is improved compared to any individual model. Each model can capture different nuances in the data.

**2. Overcome Individual Weaknesses** 

Every model has its own limitations. For example, decision trees can overfit easily. By combining with other models like random forests and boosting algorithms which reduce overfitting, we can overcome these individual weaknesses.

**3. Robustness**

Ensembling multiple models reduces variance and makes the overall predictions more robust. For example, if a new data point causes one model to fail, the other models can compensate and still provide the right prediction.  

The models are combined using simple majority voting - if 3 or more models predict a news article as Fake, we classify it as such. The threshold can be adjusted to tradeoff between precision and recall.

By training an ensemble of diverse ML models instead of relying on any single technique, our fake news classifier is more accurate, robust and resilient to new/unseen data. The ultimate goal is to maximize detection rates so harmful fake content can be effectively moderated.

The models are serialized to `.sav` files using Pickle to not train the model every single time we run the program.

## Usage

The main entry point is `main.py`. Usage details are:

```
python main.py
```

A manual testing loop is also included to get predictions on custom user-inputted news articles.
