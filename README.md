# Cinelytics: Netflix Movies & TV Shows EDA 🎬📊

A comprehensive data analysis and exploratory data analytics (EDA) project evaluating the global Netflix catalog. This project inspects content type distributions, release year trends, international contributions, genre popularity, and runtime patterns using Python's data science stack.

---

## 📌 Project Overview

The objective of this project is to clean, process, and analyze raw catalog data from Netflix to extract meaningful business insights into streaming trends. 

### Key Deliverables:
1. **Data Ingestion & Cleaning:** Standardizing schema, handling missing values, converting temporal features, and formatting runtimes.
2. **Exploratory Data Analysis (EDA):** Uncovering catalog composition across genres, content types, countries, and release years.
3. **Outlier Detection:** Identifying anomalies in movie runtimes using the Interquartile Range (IQR) technique.

---

## 🛠️ Tech Stack & Libraries

- **Language:** Python
- **Data Manipulation:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Environment:** Google Colab / Jupyter Notebook

---

## 📂 Dataset Summary

- **Source:** Netflix Titles Catalog
- **Dimensions:** 6,234 rows × 12 columns
- **Key Attributes:**
  - `show_id`: Unique identifier for each title.
  - `type`: Content format (`Movie` or `TV Show`).
  - `title`: Title of the movie or show.
  - `director`: Director(s) involved.
  - `cast`: Main cast members.
  - `country`: Production country/countries.
  - `date_added`: Date the title was added to the Netflix library.
  - `release_year`: Original public release year.
  - `rating`: Content rating (e.g., TV-MA, TV-14, PG-13).
  - `duration`: Length in minutes (movies) or seasons (TV shows).
  - `listed_in`: Associated genres/categories.
  - `description`: Summary of the plot.

---

## 🔄 Project Pipeline

1. **Environment Setup & Data Import:**
   - Loaded and styled visualizations using `seaborn` (`whitegrid` theme).
   - Automated dataset download with a fallback mechanism for local uploads.

2. **Data Profiling & Inspection:**
   - Checked dataset dimensions, column data types, non-null counts, and summary statistics (`describe(include='all')`).
   - Assessed sparsity: identified missing records primarily in `director` (~1,969), `cast` (~570), and `country` (~476).

3. **Data Cleaning & Preprocessing:**
   - Standardized column headers (trimmed spaces, converted to lowercase).
   - Cleaned string fields and cast empty strings to `NaN`.
   - Converted `date_added` to `datetime64[ns]` and `release_year` to numeric format.
   - Parsed the `duration` feature into separate numeric (`duration_value`) and unit (`duration_unit`) columns to enable mathematical evaluation.
   - Applied Interquartile Range (IQR) analysis on movie durations, detecting statistical outliers beyond the bounds of 42.5 minutes and 158.5 minutes.

4. **Exploratory Visualizations:**
   - **Content Type Balance:** Analyzed the ratio of Movies vs. TV Shows in the catalog.
   - **Historical Production Trends:** Plotted titles by original release year to observe catalog age distribution.
   - **Geographic Representation:** Exploded multi-country listings to rank the top 10 content-producing nations.
   - **Genre Popularity:** Unnested multi-genre listings (`listed_in`) to discover top streaming categories.
   - **Runtime Distribution:** Plotted movie durations via a kernel density estimate (KDE) histogram to determine standard distribution centers.

---

## 📈 Key Insights

- **Catalog Composition:** Movies form the dominant portion of the catalog (~68.4%) compared to TV Shows (~31.6%).
- **Top Producing Countries:** The United States leads content generation, followed by India and the United Kingdom.
- **Top Genres:** *International Movies*, *Dramas*, and *Comedies* represent the most frequent genre tags.
- **Average Movie Runtime:** Movie lengths roughly follow a normal distribution centered around a median of **98.0 minutes** (mean of **99.1 minutes**).

---

## 🚀 How to Run

### Option 1: Run via Google Colab
1. Open the repository's `.ipynb` file.
2. Click the **Open in Colab** badge (if configured), or upload the notebook directly to [Google Colab](https://colab.research.google.com/).
3. Run the cells sequentially (`Runtime` > `Run all`).

### Option 2: Run Locally
1. Clone the repository:
   ```bash
   git clone [https://github.com/](https://github.com/)<your-username>/<your-repo-name>.git
   cd <your-repo-name>
