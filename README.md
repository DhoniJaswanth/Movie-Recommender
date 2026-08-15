# 🎬 Movie Recommender System

A modern **Movie Recommendation System** built with **Python, FastAPI, Streamlit, TF-IDF, and The Movie Database (TMDB) API**.

The application allows users to search for movies, view detailed information, and discover similar movies using **content-based TF-IDF recommendations** and **genre-based recommendations**.

---

## 🚀 Live Demo

* **Frontend:** Streamlit Cloud
* **Backend:** Render
* **Movie Data:** TMDB API

> Live Demo:https://movie-recommender-appc4fx53zc3wb5wfxpftgl.streamlit.app/

```text
Frontend: https://your-streamlit-app.streamlit.app
Backend: https://your-fastapi-app.onrender.com
```



## ✨ Features

* 🔍 Search movies by title or keyword
* 🎬 Browse trending movies
* ⭐ Popular movies
* 🏆 Top-rated movies
* 🎥 Now-playing movies
* 🔜 Upcoming movies
* 📄 Movie details
* 🖼️ Movie posters and backdrops
* 🤖 TF-IDF content-based recommendations
* 🎭 Genre-based recommendations
* 🔄 Combined recommendation system
* ⚡ FastAPI REST backend
* 🎨 Interactive Streamlit frontend
* ☁️ Cloud deployment support

---

## 🛠️ Technologies Used

| Technology      | Purpose                  |
| --------------- | ------------------------ |
| Python          | Core programming         |
| Streamlit       | Frontend                 |
| FastAPI         | Backend REST API         |
| TMDB API        | Movie information        |
| Pandas          | Data processing          |
| NumPy           | Numerical operations     |
| Scikit-learn    | TF-IDF                   |
| SciPy           | Sparse matrix operations |
| HTTPX           | API requests             |
| Pydantic        | Data validation          |
| Pickle          | ML resource storage      |
| python-dotenv   | Environment variables    |
| Render          | Backend deployment       |
| Streamlit Cloud | Frontend deployment      |

---

# 🏗️ Project Architecture

```text
                    ┌──────────────────┐
                    │      User        │
                    └────────┬─────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │     Streamlit       │
                  │      Frontend       │
                  └──────────┬──────────┘
                             │
                        HTTP Requests
                             │
                             ▼
                  ┌─────────────────────┐
                  │       FastAPI       │
                  │       Backend       │
                  └───────┬───────┬─────┘
                          │       │
                 ┌────────┘       └────────┐
                 ▼                         ▼
        ┌─────────────────┐       ┌─────────────────┐
        │    TMDB API     │       │   Local Data    │
        │                 │       │                 │
        │ Movie Details   │       │ df.pkl          │
        │ Posters         │       │ indices.pkl     │
        │ Genres          │       │ tfidf.pkl       │
        │ Search          │       │ tfidf_matrix.pkl│
        └─────────────────┘       └─────────────────┘
```

---

# 📂 Project Structure

```text
Movie-Recommender/
│
├── app.py
├── main.py
│
├── df.pkl
├── indices.pkl
├── tfidf.pkl
├── tfidf_matrix.pkl
│
├── requirements.txt
├── .env
├── .gitignore
├── render.yaml
└── README.md

🧠 Recommendation System
TF-IDF Recommendation

The project uses a pre-computed TF-IDF matrix to find movies similar to the selected movie.

Selected Movie
      ↓
Find Movie Index
      ↓
Get TF-IDF Vector
      ↓
Calculate Similarity
      ↓
Sort Similarity Scores
      ↓
Return Similar Movies
Genre Recommendation

The application also uses the selected movie's genre and the TMDB API to find movies belonging to the same genre.

Selected Movie
      ↓
Get Movie Details
      ↓
Extract Genre
      ↓
TMDB Discover API
      ↓
Return Genre Recommendations

---

# 🔌 API Endpoints

## Health Check

```http
GET /health
```

## Home Movies

```http
GET /home?category=popular&limit=24
```

Available categories:

```text
trending
popular
top_rated
now_playing
upcoming
```

## Search Movies

```http
GET /tmdb/search?query=batman
```

## Movie Details

```http
GET /movie/id/{tmdb_id}
```

## Genre Recommendations

```http
GET /recommend/genre?tmdb_id=550&limit=18
```

## TF-IDF Recommendations

```http
GET /recommend/tfidf?title=Avatar&top_n=10
```

## Combined Recommendations

```http
GET /movie/search?query=Avatar&tfidf_top_n=12&genre_limit=12
```

---

# 💻 Run Locally

## 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/Movie-Recommender.git
cd Movie-Recommender
```

## 2. Create Virtual Environment

```bash
python -m venv venv
```

### Windows

```bash
venv\Scripts\activate
```

### macOS / Linux

```bash
source venv/bin/activate
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

## 4. Create `.env`

Create a `.env` file:

```env
TMDB_API_KEY=your_tmdb_api_key
```

---

# ▶️ Run Backend

Start FastAPI:

```bash
uvicorn main:app --reload --port 8000
```

Backend:

```text
http://127.0.0.1:8000
```

Swagger documentation:

```text
http://127.0.0.1:8000/docs
```

---

# ▶️ Run Frontend

Open another terminal and run:

```bash
streamlit run app.py
```

Frontend:

```text
http://localhost:8501
```

---

# ☁️ Deployment

The project can be deployed using:

```text
Streamlit Cloud
      +
Render
```

The **FastAPI backend** is deployed on Render, while the **Streamlit frontend** is deployed on Streamlit Cloud.

---

# 🚀 Deploy FastAPI Backend on Render

## Step 1 — Push Project to GitHub

Make sure your backend files are available in your GitHub repository:

```text
main.py
df.pkl
indices.pkl
tfidf.pkl
tfidf_matrix.pkl
requirements.txt
```

Do **not** upload your `.env` file.

---

## Step 2 — Create Render Web Service

Go to Render and create a new **Web Service**.

Connect your GitHub repository.

Use:

```text
Environment:
Python
```

### Build Command

```bash
pip install -r requirements.txt
```

### Start Command

```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

---

## Step 3 — Add Environment Variable

In Render:

```text
Environment Variables
```

Add:

```text
Key: TMDB_API_KEY
Value: your_tmdb_api_key
```

The FastAPI application reads this value using:

```python
TMDB_API_KEY = os.getenv("TMDB_API_KEY")
```

---

## Step 4 — Deploy

Click:

```text
Create Web Service
```

After deployment, Render will provide a URL similar to:

```text
https://movie-recommender-api.onrender.com
```

Test the backend:

```text
https://movie-recommender-api.onrender.com/health
```

Expected response:

```json
{
  "status": "ok"
}
```

You can also open:

```text
https://movie-recommender-api.onrender.com/docs
```

to access the FastAPI Swagger documentation.

---

# 🌐 Deploy Streamlit Frontend on Streamlit Cloud

## Step 1 — Update API URL

In `app.py`, change the backend URL from the local FastAPI server to your deployed Render URL.

For example:

```python
API_BASE = "https://movie-recommender-api.onrender.com"
```

Your Streamlit application will then send requests to the deployed FastAPI backend.

---

## Step 2 — Push Changes to GitHub

```bash
git add .
git commit -m "Update backend API URL"
git push origin main
```

---

## Step 3 — Deploy on Streamlit Cloud

Create a new Streamlit application and connect your GitHub repository.

Select:

```text
Repository:
YOUR_USERNAME/Movie-Recommender

Branch:
main

Main file:
app.py
```

Click:

```text
Deploy
```

---

## Step 4 — Streamlit Deployment

After deployment, Streamlit Cloud will provide a URL similar to:

```text
https://movie-recommender.streamlit.app
```

Open the URL and test:

1. Home feed
2. Movie search
3. Movie details
4. TF-IDF recommendations
5. Genre recommendations

---

# 🔐 Environment Variables

Never expose your TMDB API key in your source code.

### Local `.env`

```env
TMDB_API_KEY=your_tmdb_api_key
```

### Render

Add:

```text
TMDB_API_KEY
```

through Render's Environment Variables section.

### `.gitignore`

Add:

```text
.env
venv/
__pycache__/
*.pyc
```

---

# 🔗 Deployment Architecture

After deployment, the application works like this:

```text
                  INTERNET
                     │
                     ▼
        ┌────────────────────────┐
        │    Streamlit Cloud     │
        │       Frontend         │
        │                        │
        │       app.py           │
        └────────────┬───────────┘
                     │
                     │ HTTPS
                     ▼
        ┌────────────────────────┐
        │         Render         │
        │                        │
        │       FastAPI          │
        │       main.py          │
        └───────────┬────────────┘
                    │
             ┌──────┴──────┐
             ▼             ▼
      ┌─────────────┐  ┌──────────────┐
      │  TMDB API   │  │ TF-IDF Data  │
      │             │  │              │
      │ Movies      │  │ df.pkl       │
      │ Posters     │  │ tfidf.pkl    │
      │ Genres      │  │ matrix.pkl   │
      └─────────────┘  └──────────────┘
```

---

# ⚠️ Deployment Notes

### Backend URL

The Streamlit frontend must use the deployed FastAPI URL instead of:

```text
http://127.0.0.1:8000
```

For production:

```text
https://your-fastapi-app.onrender.com
```

### API Key

The TMDB API key must be configured in Render as an environment variable.

### Pickle Files

The following files are required by the FastAPI backend:

```text
df.pkl
indices.pkl
tfidf.pkl
tfidf_matrix.pkl
```

Make sure they are included in the repository or otherwise made available to the deployed backend.

---

# 🧪 Testing

Before deployment, test the backend:

```bash
uvicorn main:app --reload --port 8000
```

Then open:

```text
http://127.0.0.1:8000/docs
```

Test:

```text
GET /health
GET /home
GET /tmdb/search
GET /movie/id/{tmdb_id}
GET /recommend/genre
GET /recommend/tfidf
GET /movie/search
```

Then test the Streamlit application:

```bash
streamlit run app.py
```

---

# 🔮 Future Improvements

* 👤 Personalized user recommendations
* ❤️ Favorites and watchlist
* ⭐ Movie ratings
* 🔐 User authentication
* 🧠 Hybrid recommendation system
* 🎯 Improved content similarity
* 🎥 Movie trailers
* 📱 Mobile-friendly UI
* ⚡ Better caching
* 📊 Recommendation analytics

---

# 🎯 Project Objectives

The project demonstrates:

* Machine Learning
* Natural Language Processing
* Content-Based Recommendation
* REST API Development
* FastAPI
* Streamlit
* External API Integration
* Cloud Deployment
* Full-stack ML application development

---

# 👨‍💻 Author

**Jaswanth**

GitHub:

https://github.com/DhoniJaswanth




