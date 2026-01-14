# 🎵 Hybrid Music Recommendation System

## 📌 Project Overview
Formulated a **hybrid recommender system** by combining **Collaborative Filtering** and **Content-Based Filtering** to generate personalized music recommendations.  
The system leverages **1M+ user listening records** and **50K+ music metadata entries** to ensure scalability and accuracy.

---

## 📊 Dataset Description

### 🎧 Music Metadata (`music_info`)
Performed **Exploratory Data Analysis (EDA)** to understand feature distributions, detect patterns, and identify relationships between audio characteristics and user preferences.

The analysis focused on:
- Understanding how **audio features** (e.g., energy, danceability, tempo, valence) influence listening behavior
- Identifying **genre- and artist-level trends**
- Detecting **outliers and skewness** in numerical features such as loudness and duration
- Analyzing **temporal patterns** using year and release trends

**Features analyzed include:**
- `track_id`, `name`, `artist`
- `spotify_preview_url`, `spotify_id`
- `tags`, `genre`, `year`
- `duration_ms`
- Audio features: `danceability`, `energy`, `key`, `loudness`, `mode`,
  `speechiness`, `acousticness`, `instrumentalness`, `liveness`, `valence`,
  `tempo`, `time_signature`

Insights from EDA were used to guide **feature selection, normalization, and similarity computation** for content-based recommendations.

---

### 👤 User Listening History
Analyzed user interaction data to capture implicit feedback and listening intensity.

- `user_id`
- `track_id`
- `playcount`

EDA helped identify:
- Power users vs casual listeners
- Popular tracks and long-tail listening behavior
- Sparsity patterns in the user–item interaction matrix

---

## 🧠 Recommendation Strategy

- **Collaborative Filtering**
  - Utilized user–item interaction data (`user_id`, `track_id`, `playcount`)
  - Learned user preferences from collective listening behavior

- **Content-Based Filtering**
  - Used audio and metadata features such as `artist`, `tags`, `key`, `time_signature`,
    `duration_ms`, `loudness`, `danceability`, `energy`, `tempo`, `speechiness`,
    `acousticness`, `instrumentalness`, `liveness`, and `valence`
  - Computed similarity using **Cosine Similarity**

- **Hybrid Model**
  - Combined both approaches to improve recommendation accuracy
  - Mitigated cold-start and sparsity issues

---

## ⚙️ MLOps & Production Pipeline

Built a **production-ready recommendation pipeline** using the following technologies:

### 🔧 Core Techniques
- Cosine Similarity for scalable similarity computation

### 📦 Version Control & CI/CD
- **DVC** – Data, pipeline, and experiment versioning  
- **GitHub Actions** – Automated CI/CD workflows for testing, building, and deployment  


### 🐳 Containerization
- **Docker** – Reproducible model environments

### ☁️ Cloud & Deployment (AWS)
- **Amazon S3** – Data storage
- **Amazon EC2** – Model serving
- **Amazon ECR** – Container registry
- **AWS CodeDeploy** – Cloud infrastructure supporting **Blue–Green deployment strategy** for zero-downtime releases, enabling safe traffic switching between production and staging environments 

📌 **Note:**  
This stack enables scalable data processing, systematic experimentation with recommendation strategies and features, automated deployment, and interactive user-facing demonstrations.

--- 
## ⚡ Large-Scale Data Processing & Optimization

Given the large scale of the dataset (**1M+ user interactions**), special care was taken to ensure efficient computation, memory usage, and scalability.

### 🔹 Distributed Computing with Dask
- **Dask** was used to process large datasets that cannot be efficiently handled by in-memory Pandas alone.
- Enabled **parallel and chunk-based computation** during data cleaning, feature transformation, and interaction matrix construction.
- Allowed scalable execution while keeping the codebase close to standard Python workflows.

### 🔹 Sparse Matrix Optimization for Similarity Search
- User–item interaction data is inherently **sparse**, as users interact with only a small fraction of available tracks.
- Interaction and feature matrices were stored in **compressed sparse `.npz` format** to:
  - Reduce memory footprint
  - Improve disk I/O performance
  - Enable fast cosine similarity computation on large matrices

### 🔹 Performance Impact
- Significantly faster similarity searches on large datasets
- Lower RAM usage compared to dense matrix representations
- Improved scalability for both collaborative and content-based recommendation pipelines

📌 **Outcome:**  
This optimization strategy ensures the recommender system remains **efficient, scalable, and production-ready**, even with very large datasets.

---

## 🚀 Tech Stack

### 🧠 Machine Learning
- **Cosine Similarity** – Measures similarity between tracks based on feature vectors  
- **Collaborative Filtering** – Learns user preferences from user–item interactions  
- **Content-Based Filtering** – Recommends tracks based on audio and metadata similarity  



---
### 🐍 Backend & Libraries
- **Python** – Core programming language for data processing and ML logic  
- **NumPy** – Efficient numerical computations and array operations  
- **Pandas** – Data manipulation and analysis  
- **Scikit-learn** – Machine learning algorithms and similarity computations  
- **SciPy** – Scientific computing and optimized distance/similarity operations  
- **Dask** – Parallel and distributed computing for large-scale data processing  
- **Streamlit** – Interactive web application for showcasing and testing recommendations  

---


## 📂 Project Structure

```text
spotify-hybrid-recommender-system/
│
├── .github/
│   └── workflows/
│       └── ci.yml
│           # CI/CD pipeline (lint, test, build, Docker & deploy)
│
├── deploy/
│   └── scripts/
│       ├── install_dependencies.sh
│       │   # Install system & Python dependencies
│       └── start_docker.sh
│           # Start Docker containers
│
├── data/
│   ├── music_info.csv.dvc
│   └── user_listening_history.csv.dvc
│       # DVC-tracked datasets
│
├── notebooks/
│   ├── EDA_Spotify_Dataset.ipynb
│   ├── Spotify_Collaborative_Filtering.ipynb
│   └── Spotify_Content_Based_Filtering.ipynb
│       # EDA and experimentation
│
├── app.py
│   # Application entry point
│
├── content_based_filtering.py
│   # Content-based recommendation logic
│
├── collaborative_filtering.py
│   # Collaborative filtering logic
│
├── data_cleaning.py
│ 
│
├── Dockerfile
├── Makefile
├── README.md
├── appspec.yml
│   # AWS CodeDeploy configuration
│
├── dvc.yaml
├── dvc.lock
│   # DVC pipeline configuration
├── hybrid_recommendation.py
│   # Hybrid recommendation strategy
│
├── READme.md
├── requirements.txt
├── test_app.py
├── transform_filtered_data.py
│   # Data preprocessing
└── LICENSE

```
---

## 🧪 Application Health Check & Testing

The project includes a lightweight **deployment smoke test** to verify application availability after startup.

### `test_app.py`
- Sends an HTTP request to the Streamlit application endpoint
- Waits for application initialization during container startup
- Asserts a successful HTTP response (`200 OK`)
- Used in CI/CD pipelines to validate successful deployment

📌 **Purpose:**  
Ensures the Streamlit application is accessible and running correctly before marking deployment as successful.


## 🚀 Key Highlights
- Designed a scalable **hybrid recommendation architecture** combining collaborative and content-based filtering  
- Applied **insight-driven feature engineering** through comprehensive EDA on large-scale music datasets  
- Built an **end-to-end automated ML pipeline** with data versioning, CI/CD, and cloud deployment  
- Implemented **production-grade MLOps practices**, including containerization, Blue–Green deployments, and deployment health checks  


---
## 🧑‍💻 Author

**Sourav Raj**  
Data Scientist | Data Analyst

Feel free to connect on LinkedIn or explore my other projects.

🔗 LinkedIn: https://www.linkedin.com/in/sourav664