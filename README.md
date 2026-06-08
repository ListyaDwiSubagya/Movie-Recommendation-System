[README_movie.md](https://github.com/user-attachments/files/28711448/README_movie.md)
# 🎬 Movie Recommendation System

![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat&logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.x-orange?style=flat&logo=scikit-learn)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat)
![Platform](https://img.shields.io/badge/Platform-VS%20Code-blue?style=flat&logo=visualstudiocode)

> Sistem rekomendasi film yang membangun **3 pendekatan sekaligus**: Content-Based Filtering, Collaborative Filtering, dan Hybrid Recommendation menggunakan dataset MovieLens 100K.

---

## 📌 Overview

Sistem rekomendasi adalah teknologi inti yang digunakan oleh platform seperti Netflix, Spotify, dan YouTube untuk menyarankan konten yang relevan kepada pengguna. Proyek ini mengimplementasikan dan membandingkan tiga pendekatan rekomendasi film yang berbeda untuk memahami kelebihan dan kekurangan masing-masing metode.

---

## 📊 Dataset

| Atribut | Detail |
|---|---|
| Sumber | MovieLens 100K (GroupLens Research, University of Minnesota) |
| Total Film | 9.742 film |
| Total User | 610 pengguna |
| Total Rating | 100.836 rating |
| Rata-rata Rating | 3.50 / 5.00 |
| Periode Data | Maret 1996 — September 2018 |

**File Dataset:**

| File | Deskripsi |
|---|---|
| `movies.csv` | ID, judul, dan genre film |
| `ratings.csv` | Rating user terhadap film (0.5 — 5.0) |
| `tags.csv` | Tag yang diberikan user ke film |
| `links.csv` | ID penghubung ke IMDb & TMDb |

---

## 🛠️ Tech Stack

| Kategori | Library |
|---|---|
| Data Manipulation | `pandas`, `numpy` |
| Visualisasi | `matplotlib`, `seaborn` |
| NLP / Feature Extraction | `scikit-learn` (TfidfVectorizer) |
| Similarity Computation | `scikit-learn` (cosine_similarity) |
| Evaluasi | `scikit-learn` (mean_squared_error) |
| Model Saving | `joblib` |

---

## 🔄 Alur Proyek

```
Raw Data (movies, ratings, tags, links)
   │
   ▼
Exploratory Data Analysis (EDA)
├── Distribusi rating
├── Top 10 film terbanyak dirating
└── Top 10 genre terpopuler
   │
   ▼
Feature Engineering
├── Gabungkan genre + tags menjadi fitur 'content'
└── TF-IDF Vectorization
   │
   ▼
Membangun 3 Sistem Rekomendasi
├── Content-Based Filtering
│   └── TF-IDF + Cosine Similarity (genre & tags)
├── Collaborative Filtering
│   └── Item-Based Cosine Similarity (user-movie matrix)
└── Hybrid Recommendation
    └── Gabungan Content (50%) + Collaborative (50%)
   │
   ▼
Evaluasi
└── RMSE Baseline: 0.9827
   │
   ▼
Simpan Model
```

---

## 🤖 Metode Rekomendasi

### 1. Content-Based Filtering
Merekomendasikan film berdasarkan **kemiripan konten** (genre dan tags).

```python
get_content_recommendations('Toy Story (1995)', n=10)
```

| Film | Genre | Similarity Score |
|---|---|---|
| Bug's Life, A (1998) | Adventure\|Animation\|Children\|Comedy | 0.8622 |
| Toy Story 2 (1999) | Adventure\|Animation\|Children\|Comedy\|Fantasy | 0.6440 |
| Monsters, Inc. (2001) | Adventure\|Animation\|Children\|Comedy\|Fantasy | 0.3579 |

### 2. Collaborative Filtering (Item-Based)
Merekomendasikan film berdasarkan **pola rating pengguna** yang serupa.

```python
get_collaborative_recommendations('Toy Story', n=10)
```

| Film | Genre | Similarity Score |
|---|---|---|
| Toy Story 2 (1999) | Adventure\|Animation\|Children\|Comedy\|Fantasy | 0.5726 |
| Jurassic Park (1993) | Action\|Adventure\|Sci-Fi\|Thriller | 0.5656 |
| Forrest Gump (1994) | Comedy\|Drama\|Romance\|War | 0.5471 |

### 3. Hybrid Recommendation ✅
Menggabungkan Content-Based (50%) dan Collaborative (50%) untuk hasil terbaik.

```python
get_hybrid_recommendations_v2('Toy Story (1995)', n=10)
```

| Film | Content Score | Collab Score | Hybrid Score |
|---|---|---|---|
| Bug's Life, A (1998) | 0.8622 | 0.4792 | 0.6707 |
| Toy Story 2 (1999) | 0.6440 | 0.5726 | 0.6083 |
| Monsters, Inc. (2001) | 0.3579 | 0.5047 | 0.4313 |

---

## 📈 Evaluasi

| Metrik | Nilai |
|---|---|
| RMSE Baseline (Movie Average) | **0.9827** |

> 💡 RMSE 0.9827 berarti rata-rata prediksi rating meleset sekitar 0.98 bintang dari rating asli. Ini adalah baseline yang wajar untuk sistem rekomendasi sederhana tanpa matrix factorization.

---

## 🔍 Key Insights

1. **Content-Based** cocok untuk film dengan genre dan tags yang jelas, tapi kurang beragam
2. **Collaborative** lebih beragam karena berdasarkan perilaku user, tapi butuh banyak data rating
3. **Hybrid** memberikan hasil terbaik — menggabungkan kelebihan kedua metode
4. Film animasi anak-anak cenderung memiliki similarity score tinggi karena genre yang spesifik
5. Rating terbanyak ada di angka **4.0** — pengguna cenderung memberi rating positif

---

## 💡 Cara Menggunakan Sistem Rekomendasi

```python
# Content-Based: Berdasarkan genre & tags
get_content_recommendations('The Dark Knight (2008)', n=10)

# Collaborative: Berdasarkan pola rating user
get_collaborative_recommendations('The Dark Knight', n=10)

# Hybrid: Kombinasi keduanya (Rekomendasi)
get_hybrid_recommendations_v2('The Dark Knight (2008)', n=10)
```

---

## 🚀 Cara Menjalankan

1. Clone repository ini:
```bash
git clone https://github.com/ListyaDwiSubagya/movie-recommendation-system.git
cd movie-recommendation-system
```

2. Buat virtual environment:
```bash
python -m venv venv
venv\Scripts\activate  # Windows
```

3. Install dependencies:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn joblib
```

4. Jalankan notebook:
```bash
jupyter notebook movie_recommendation.ipynb
```

---

## 🏆 Pencapaian

- ✅ Berhasil membangun 3 sistem rekomendasi berbeda dalam satu proyek
- ✅ Hybrid Recommendation menggabungkan kelebihan Content-Based dan Collaborative
- ✅ Memproses 100.836 rating dari 610 user dan 9.742 film
- ✅ RMSE Baseline 0.9827 sebagai benchmark evaluasi

---

## 👤 Author
**Listya Dwi Subagya**
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-blue?style=flat&logo=linkedin)](https://linkedin.com/in/listyadwis)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-black?style=flat&logo=github)](https://github.com/ListyaDwiSubagya)

biasakan untuk readme sertakan itu ya

## 📝 Citation

Dataset yang digunakan:
> F. Maxwell Harper and Joseph A. Konstan. 2015. The MovieLens Datasets: History and Context. ACM Transactions on Interactive Intelligent Systems (TiiS) 5, 4: 19:1–19:19.

## 📝 License

Proyek ini dibuat untuk keperluan pembelajaran dan pengembangan portofolio data science.
