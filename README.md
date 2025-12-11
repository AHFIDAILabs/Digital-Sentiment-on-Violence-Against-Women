## Digital-Sentiment-on-Violence-Against-Women
A sentiment-analysis–driven system designed to uncover and interpret public attitudes toward violence against women in Nigeria through large-scale social media data.

This project provides an end-to-end NLP workflow for collecting, cleaning, and analyzing online conversations, using advanced language models to classify sentiments, detect harmful or supportive narratives, and reveal patterns in public perceptions of gender-based violence. It delivers a production-ready pipeline—from data preprocessing to model evaluation—that equips researchers, advocates, and policymakers with actionable insights to better understand and address GBV discourse in digital spaces.


## Table of Contents

1. Background
2. Solution
3. Objectives
4. Methodology
5. Tech Stack
6. Project Structure
7. Licenses


## 1. Background
Gender-based violence (GBV) remains a widespread human rights issue in Nigeria, where women and girls face physical, sexual, cultural, and increasingly digital forms of abuse. Social media—while offering space for advocacy and support—has also become a significant channel for the normalization of violence against women, enabling harassment, misogynistic discourse, victim-blaming, and the spread of harmful gender stereotypes. Understanding how these attitudes manifest online is essential for addressing the growing influence of digital spaces in shaping public perceptions of GBV targeted at women.


## 2. Our Solution: A Baseline Sentiment Analysis

To analyze public perceptions of women expressed through social media data in Nigeria, understanding the prevalence of violence, harassment, and misogyny in online discourse, and identifying patterns that contribute to digital violence against women.

## 3. Objectives
1. To collect and integrate social media data from multiple platforms (Twitter/X, TikTok, Facebook) based on gender-related hashtags and keywords
2. To apply sentiment analysis and toxicity detection to classify public attitudes expressed toward women
3. To identify the prevalence and patterns of misogynistic, abusive, and violent content in the dataset
4. To explore platform-level differences in how harmful narratives about women are expressed, shared, and engaged with
5. To examine user engagement indicators such as likes, shares, and comments to understand how digital violence spreads
6. To highlight emerging themes, language patterns, and trends that contribute to online harassment of women
7. To provide evidence-based insights and recommendations that support advocacy, awareness campaigns, and policy interventions

# 4.  Methodology

## a. Data Collection
Social media posts were collected using scraping tools and APIs across multiple platforms, including:

- **Twitter/X**: posts, replies, and retweets  
- **TikTok**: video captions and public comments  
- **Facebook**: public pages and groups  

Posts were identified using gender-related keywords and hashtags such as `#EndViolenceAgainstWomen`, `#16DaysOfActivism`, `#OrangeTheWorld`, `women`, `feminism`, `rape culture`, and related terms. The dataset spans **2007–2025**, with the majority concentrated in 2025, resulting in **4,923 posts**.

## b. Data Structure
The dataset contains **4,923 rows and 17 columns**, including:

| Column         | Type        | Description                                  |
|----------------|------------|----------------------------------------------|
| platform       | Categorical | Social media platform (Twitter, TikTok, Facebook) |
| user_name      | Text       | Username of poster                           |
| user_avatar    | Text       | Profile image URL                            |
| user_location  | Text       | User's stated location                        |
| text           | Text       | Content of the post                           |
| created_at     | Datetime   | Timestamp of post                             |
| likes          | Numeric    | Number of likes/reactions                     |
| shares         | Numeric    | Number of reshares                            |
| plays          | Numeric    | Number of video plays (TikTok)               |
| comments       | Numeric    | Number of comments                            |
| hashtags       | Text       | Hashtags used in post                          |
| verified       | Boolean    | Verified account status                        |
| url            | Text       | Direct link to post                            |
| media          | Text       | Attached media files                           |
| year           | Numeric    | Year extracted from timestamp                  |
| month          | Numeric    | Month extracted from timestamp                 |
| day_of_week    | Categorical | Day of the week                                |

## c. Data Cleaning
Preprocessing steps included:

- Removing duplicates  
- Standardizing temporal features (year, month, day_of_week)  
- Cleaning text (removing URLs, special characters, excessive whitespace)  
- Converting engagement metrics to numeric values  
- Handling missing values and validating data types  

Engagement metrics were highly skewed, with viral outliers reflecting typical social media activity patterns.

## d. Sentiment Analysis
Sentiment classification was performed using a **DistilBERT-based multilingual transformer model** (`lxyuan/distilbert-base-multilingual-cased-sentiments-student`), capable of processing English, Nigerian Pidgin, and local languages. The model outputs three categories: **positive, negative, neutral**.  

**Validation Metrics:**

- Overall Accuracy: 68.1%  
- Macro Precision: 0.61  
- Macro Recall: 0.58  
- Macro F1 Score: 0.58  

Positive sentiment was predicted most accurately, while neutral sentiment was underrepresented.

## e. Toxicity Detection
Toxic content was identified using a **custom lexicon-based approach** targeting:

- Misogynistic expressions  
- Rape culture references  
- Body-shaming and slut-shaming  
- Gendered slurs and hate speech  

Metrics calculated included total toxic expressions, posts containing toxic content, average expressions per post, and temporal patterns.

## f. Emotion Analysis
Emotion detection used the **`j-hartmann/emotion-english-distilroberta-base`** transformer to classify posts into seven categories:

- Neutral  
- Joy  
- Sadness  
- Anger  
- Fear  
- Surprise  
- Disgust  

The model captures nuanced and implicit emotional expressions.

# 4. RESULTS AND FINDINGS

## a. Sentiment Distribution
Among 4,923 posts:

- Negative: 1,798 (52.2%)  
- Positive: 1,622 (47.1%)  
- Neutral: 26 (0.8%)  

> The online discourse is highly polarized, with negative sentiment dominating, reflecting harassment, victim-blaming, and misogyny, while positive sentiment reflects advocacy and support for gender equality. Neutral discourse is nearly absent.

## b. Emotion Distribution
Dominant emotions:

| Emotion | Count | Percentage |
|---------|-------|------------|
| Neutral | 1,802 | 36.6%      |
| Anger   | 1,179 | 23.9%      |
| Joy     | 539   | 10.9%      |
| Sadness | 537   | 10.9%      |
| Fear    | 501   | 10.2%      |
| Surprise| 216   | 4.4%       |
| Disgust | 149   | 3.0%       |

> Anger is the main negative emotion, reflecting both outrage at violence and hostility toward women's rights discussions. Joy and sadness appear equally, indicating mixed emotional engagement.

## c. Toxicity and Misogyny
- Posts containing toxic expressions: 30.88% (1,862/4,923)  
- Average toxic expressions per post: 0.38  
- Most frequent expressions: "abuse" (31%), "feminism" (16.7%), "rape culture" (9.5%), "misogyny" (6.9%)  

> Online discourse is frequently hostile, often layering multiple toxic expressions in single posts.

## d. Geographic Patterns
Analysis of 93 posts with Nigerian location tags shows overwhelmingly negative sentiment across states:

| Location | Negative % | Positive % | Neutral % |
|----------|------------|------------|-----------|
| Akure, Ondo | 84.0% | 16.0% | 0.0% |
| Minna, Niger | 68.6% | 31.4% | 0.0% |
| Abuja, FCT   | 66.7% | 33.3% | 0.0% |
| Other states | 100%  | 0.0%  | 0.0% |

> Coverage gaps exist in 28 of 36 states plus the FCT, highlighting the need for expanded data collection.

## e. Temporal Trends
- Toxic content surged in **2025** (769 expressions, ~6× increase from 2024), coinciding with the **16 Days of Activism** campaign.  
- Monthly peaks occurred in **November** (~400 toxic expressions) and **October** (~270), reflecting campaign activity.  
- Baseline activity persisted year-round, indicating ongoing discourse outside awareness campaigns.

# 5. Tech Stack

twikit <br>
config planner <br>
facebook graph api <br>
pandas <br>
numpy <br>
regex <br>
datetime <br>
lxyuan/distilbert-base-multilingual-cased-sentiments-student for sentiment analysis <br>
j-hartmann/emotion-english-distilroberta-base for emotion detection <br>

# 6. Project Structure

```pgsql
Gender-Based-Violence-Sentiment-Analysis/
│
├── README.md
├── requirements.txt
├── setup.py
├── .gitignore
│
├── data/
│   ├── raw/
│   │   └── (Unprocessed datasets: scraped text, CSVs, JSON files)
│   ├── interim/
│   │   └── (Partially processed data)
│   ├── cleaned/
│   │   └── (Final cleaned datasets ready for modeling)
│   └── external/
│       └── (Data obtained from third-party sources)
│
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_feature_engineering.ipynb
│   ├── 04_model_building.ipynb
│   ├── 05_model_evaluation.ipynb
│   └── 06_results_interpretation.ipynb
│
├── scripts/
│   ├── scraping/
│   │   ├── scrape_twitter.py
│   │   ├── scrape_reddit.py
│   │   └── scrape_websites.py
│   ├── preprocessing/
│   │   ├── text_cleaning.py
│   │   ├── data_cleaner.py
│   │   └── tokenizer.py
│   ├── feature_engineering/
│   │   ├── embeddings.py
│   │   ├── vectorizers.py
│   │   └── sentiment_features.py
│   ├── modeling/
│   │   ├── train_model.py
│   │   ├── evaluate_model.py
│   │   └── save_model.py
│   └── utils/
│       ├── helpers.py
│       └── logger.py
│
├── src/
│   ├── data/
│   │   ├── load_data.py
│   │   └── make_dataset.py
│   ├── preprocessing/
│   │   ├── clean_text.py
│   │   └── normalize.py
│   ├── features/
│   │   └── build_features.py
│   ├── models/
│   │   ├── model_defs.py
│   │   └── predict.py
│   ├── evaluation/
│   │   └── metrics.py
│   └── visualization/
│       └── plots.py
│
├── reports/
│   ├── figures/
│   │   └── (Graphs, charts, wordclouds, confusion matrices)
│   ├── tables/
│   │   └── (Summary stats, model comparison tables)
│   └── final_report.md
│
├── docs/
│   ├── project_overview.md
│   ├── methodology.md
│   ├── data_documentation.md
│   ├── model_documentation.md
│   └── api_documentation.md
│
├── deployment/
│   ├── streamlit_app/
│   │   ├── app.py
│   │   ├── pages/
│   │   └── assets/
│   ├── flask_app/
│   │   ├── app.py
│   │   ├── routes/
│   │   └── templates/
│   ├── models/
│   │   └── (Serialized models: .pkl, .pt, .h5)
│   └── config/
│       └── settings.yaml
│
├── tests/
│   ├── test_data_loading.py
│   ├── test_preprocessing.py
│   ├── test_feature_engineering.py
│   ├── test_model_training.py
│   └── test_api.py
│
└── logs/
    └── (Training logs, error logs, scraping logs)
````
