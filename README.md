# 🎵 Moosic: Automated Playlist Curation with Machine Learning

> A Machine Learning prototype to scale human-curated music playlists by clustering Spotify audio features.

---

## 📖 About the Project

**Moosic** is a fast-growing startup that provides users with highly curated, mood-based playlists. Historically, these playlists have been hand-crafted by human music experts. However, as the business scales, human curation has become a bottleneck. 

The goal of this project is to build a **Data Science prototype** that automates the initial grouping of songs into cohesive playlists using a dataset of over 5,000 tracks pulled from the Spotify API. 

### The Challenge
Some stakeholders were skeptical that algorithms could capture the subjective "mood" of a song. Our mission was to prove whether mathematical audio features (tempo, energy, acousticness, etc.) could replicate the "vibe" that human curators listen for.

---

## 🧠 Methodology

To translate subjective music tastes into mathematical models, the following pipeline was developed:

1. **Data Preprocessing & Scaling:** * Isolated purely numeric audio features (dropping text metadata like Artist and Song ID).
   * Applied `MinMaxScaler` to ensure features with large ranges (like tempo) didn't overpower smaller-scale features (like acousticness).
2. **Dimensionality Reduction (PCA):**
   * Condensed 13 distinct audio features into **4 Principal Components**.
   * *Why?* This removed statistical "noise" and isolated the core "Musical DNA" of the tracks, capturing over 80% of the variance.
3. **Clustering (K-Means):**
   * Used the Elbow Method to evaluate the optimal number of clusters. 
   * **Product Pivot:** While the mathematical elbow suggested **9 broad clusters**, we intentionally over-fitted the model to **50 clusters**. This reduced the average playlist size to ~105 songs, shifting the output from "broad genre buckets" to highly curated, specific "moods" (which aligns better with Moosic's business model).

---

## 📊 Business Insights & Evaluation

This prototype was evaluated against two primary business questions:

### 1. Are Spotify’s audio features able to identify "similar songs"?
**Yes.** When evaluating the clusters, the model successfully grouped songs with humanly recognizable similarities without ever looking at the genre tags or artist names. 
* *Example:* "Playlist 1" successfully grouped high-energy, high-tempo, major-key tracks from various Indie/Garage Rock bands, creating a highly cohesive "Raw Garage Vibe" driven entirely by audio signals.

### 2. Is K-Means a good method to create playlists?
**Yes, as a strong baseline.** K-Means is excellent at finding hidden mathematical similarities quickly. Moving forward, the recommendation is a **"Hybrid Curation"** model:
* **The AI** acts as the foundation, instantly grouping 5,000 songs into 50 cohesive buckets.
* **Human Experts** act as the finishers, reviewing the clusters, naming them (e.g., "Late Night Acoustic" or "Gym Power"), and removing any minor outliers.

---

## 💻 Tech Stack

* **Data Manipulation:** `pandas`, `numpy`
* **Machine Learning:** `scikit-learn` (KMeans, PCA, MinMaxScaler)
* **Data Visualization:** `matplotlib`, `seaborn`

---
