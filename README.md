# 🎬 Content-Based Movie Recommendation System

This is a **content-based recommendation engine** for movies, trained on a custom dataset scraped from IMDb. It leverages metadata, natural language, and participant embeddings to surface similar titles.

> ⚠️ Note: This project uses copyrighted synopsis data from IMDb and is intended **for personal and educational use only**.

---

## 🧠 What It Does

- Recommends similar movies based on:
  - Genre, runtime, release year, and IMDb ratings
  - Natural language from movie synopses
  - Key personnel: actors, directors, etc.

---

## 🛠 Technical Breakdown

### 🎲 Metadata Encoding
- Genres → one-hot encoded
- Numeric values (runtime, year, rating) → normalized

### 📝 Text Embedding (Synopsis)
- **TF-IDF Vectorizer**:
  - Base model; surprisingly effective
  - Suffered from verbosity bias (*The Lord of the Rings* dominated every recommendation list)
- **Dimensionality Reduction**:
  - **Truncated SVD** used to reduce sparse TF-IDF vectors into more manageable dense space

### 🤖 Alternative NLP Attempts
- **Word2Vec (Gensim)**:
  - Tried training on plot text
  - Performance was poor — likely due to limited corpus size
- **Pretrained Transformer (Mini-BERT)**:
  - Imported small HuggingFace BERT-style model for sentence embeddings
  - Resulted in better semantic matching, but slower to compute

### 🎭 Cast & Crew Representation
- Built a custom embedding for movie participants (actors, directors) using co-occurrence and a small neural network
- The model learned relevance between people (e.g., “Tarantino = violence, witty dialogue” → connects to similar films)

---

## 📉 Challenges Faced

- No access to user interaction data → couldn’t use collaborative filtering
- Hard to validate recommendation quality without feedback data
- High-dimensional TF-IDF vectors were memory-heavy
- Overfitting to popular trilogies (e.g. *Lord of the Rings* appeared in nearly every top 10 🤦)

---

## 🧪 Tools & Libraries

- `pandas`, `numpy`, `scikit-learn`
- `tensorflow` for neural components
- `seaborn` for exploratory plots
- `gensim`, `transformers`, `sentence-transformers`
- `BeautifulSoup` & `requests` for web scraping

---

## 🔒 Data Usage Note

All movie synopsis data was scraped from IMDb and is **not included** in this repo due to licensing restrictions.  
The codebase is presented purely as an educational experiment in content-based recommendation.

---

## 🔄 Open-Source Reimplementation (In Progress)

An open-source variant using:
- The [MovieLens](https://grouplens.org/datasets/movielens/) dataset (metadata + ratings)
- Plot summaries via the [TMDb API](https://www.themoviedb.org/documentation/api)

...is currently being reworked to allow commercial or public use.

---

## 🧙 Easter Egg

> “One ring to recommend them all...”  
The TF-IDF model had a particular affinity for *The Lord of the Rings* trilogy.  
No matter what you asked it, Frodo came back for more.

---

