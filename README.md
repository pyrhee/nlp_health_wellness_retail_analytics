# nlp_health_wellness_retail_analytics
NLP-powered analysis of customer reviews in the health and wellness retail industry. Extracts sentiment, keywords, and topics to uncover product insights. Supports data-driven marketing and product development strategies.

# 🧴 NLP Analysis of Health & Wellness Retail Reviews

> This project leverages NLP to analyze customer reviews in the **cosmetic and wellness retail industry**, aiming to uncover brand insights and support data-driven marketing strategy.

---

## 📌 Project Overview

- **Targets**:  
  - Top 30 skincare & suncare products sold in health/wellness retail (e.g., Olive Young)  
  - Products by the brand *Round Lab*

- **Goals**:
  - Extract meaningful sentiment and topics from customer reviews
  - Identify product strengths, weaknesses, and opportunities
  - Provide actionable marketing recommendations

---

## 📁 Project Structure
```
├── data/                     # Raw review data
├── preprocessing/            # Text cleaning, spell check, tokenization
├── sentiment_analysis/       # Sentiment & keyword extraction
├── topic_modeling/           # LDA topic modeling code
├── visualization/            # Visual outputs (PNG, HTML)
├── final_presentation/       # Final presentation slides (PPTX)
└── README.md
```

---

## 🧠 Technologies Used

- **Language**: Python  
- **Libraries**:
  - Web scraping: `requests`, `BeautifulSoup`
  - NLP: `kss`, `kiwipiepy`, `kospellpy`, `NLTK`
  - Visualization: `Matplotlib`, `Seaborn`, `Plotly`, `pyLDAvis`
  - Topic modeling: `gensim`

---

## 📊 Key Results

### 1. Sentiment & Keyword Analysis

- **Positive**: moisturizing, mild, recommended, repurchase  
- **Negative**: sticky, whitening cast, breakouts  

📈 *Word frequency by sentiment*  
![sentiment-analysis](./visualization/sentiment_analysis_result.png)

---

### 2. ⭐ LDA Topic Modeling

> LDA extracted 3 main review themes based on product attributes and customer experience.

📍 *Interactive Visualization*  
![lda-topic-modeling](./visualization/lda_topic_modeling.png)  
Or 👉 [View interactive HTML](./visualization/lda_topic_modeling.html)

#### Code Snippet:
```python
from gensim import corpora, models
import pyLDAvis.gensim_models as gensimvis
import pyLDAvis

texts = preprocessed_reviews  # List of tokenized and cleaned reviews

# Dictionary & Corpus
dictionary = corpora.Dictionary(texts)
corpus = [dictionary.doc2bow(text) for text in texts]

# Train LDA Model
lda_model = models.LdaModel(corpus=corpus,
                            id2word=dictionary,
                            num_topics=3,
                            passes=10,
                            random_state=42)

# Visualize
vis = gensimvis.prepare(lda_model, corpus, dictionary)
pyLDAvis.save_html(vis, './visualization/lda_topic_modeling.html')
