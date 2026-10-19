# 🎬 Cinelytics — Netflix Movies & TV Shows Data Analysis

A data science capstone project that explores a real-world Netflix titles dataset. It covers loading, understanding, and cleaning the data, exploratory data analysis (EDA) with visualizations, and feature engineering that prepares the data for future analysis or modeling.

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![NumPy](https://img.shields.io/badge/NumPy-Numerical-013243)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557c)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Plots-4c72b0)
![Jupyter](https://img.shields.io/badge/Notebook-Jupyter%20%7C%20Colab-F37626)

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Objectives](#-objectives)
- [Dataset](#-dataset)
- [Tech Stack](#-tech-stack)
- [Project Workflow](#-project-workflow)
- [Key Results](#-key-results)
- [Feature Engineering](#-feature-engineering)
- [Getting Started](#-getting-started)
- [Project Structure](#-project-structure)
- [Output Files](#-output-files)
- [Limitations](#-limitations)
- [Future Work](#-future-work)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📖 Project Overview

**Cinelytics** analyzes the Netflix catalogue to uncover patterns in content type, genres, countries of origin, release years, durations, and the timeline of titles added to the platform. The notebook walks through a complete, reproducible data science workflow, with an explanation, a guiding question, and an interpretation for every step.

## 🎯 Objectives

- Load and inspect a real-world dataset
- Identify and handle data quality issues (missing values, types, outliers)
- Answer practical questions through visual analysis
- Engineer and encode features that are ready for future modeling
- Export clean, reusable datasets

## 📂 Dataset

| Property | Details |
|---|---|
| **Source** | [Netflix titles CSV](https://raw.githubusercontent.com/prasertcbs/basic-dataset/refs/heads/master/netflix_titles.csv) |
| **Rows** | 6,234 titles |
| **Columns** | 12 (14 after cleaning) |
| **Content types** | Movie (4,265) · TV Show (1,969) |

**Columns:** `show_id`, `type`, `title`, `director`, `cast`, `country`, `date_added`, `release_year`, `rating`, `duration`, `listed_in`, `description`

**Missing values in the raw data**

| Column | Missing |
|---|---|
| director | 1,969 |
| cast | 570 |
| country | 476 |
| date_added | 11 |
| rating | 10 |

## 🛠 Tech Stack

- **Python 3**
- **NumPy**: numerical operations
- **Pandas**: data loading, cleaning, and transformation
- **Matplotlib**: plotting
- **Seaborn**: statistical visualizations
- **Jupyter Notebook / Google Colab**: development environment

## 🔄 Project Workflow

1. **Import libraries**: set up NumPy, Pandas, Matplotlib, and Seaborn with a consistent chart theme
2. **Load the dataset**: download the CSV directly from a public URL, with a manual-upload fallback for Colab
3. **Understand the data**: shape, data types, summary statistics, unique values, and missing values
4. **Clean the data**
   - Standardize column names and trim whitespace
   - Remove duplicates (none were found)
   - Convert `date_added` to datetime and `release_year` to numeric
   - Validate release years (valid range: 1900 to the current year)
   - Parse `duration` into `duration_value` and `duration_unit`
   - Flag movie-duration outliers with the IQR method
5. **Exploratory Data Analysis**
   - Movies vs TV Shows
   - Titles by release year
   - Top 10 countries
   - Top 10 genres
   - Movie duration distribution
   - Titles added to Netflix per year, by type
   - Correlation heatmap
6. **Feature preparation**: feature engineering, categorical encoding, scaling, and feature matrix creation
7. **Findings and export**: summary statistics and CSV exports

## 📊 Key Results

- **Content mix:** The dataset has **4,265 Movies** and **1,969 TV Shows**, so movies are roughly twice as common.
- **Top countries by title count:** United States (2,609), India (838), United Kingdom (601), Canada (318), France (271)
- **Top genres and categories:** International Movies (1,927), Dramas (1,623), Comedies (1,113), International TV Shows (1,001), Documentaries (668)
- **Movie duration:** Mean of **99.1 min** and median of **98 min**
- **Outliers:** 231 movies fall outside the IQR bounds of **42.5 to 158.5 minutes**. They were flagged, not removed, because they may be legitimate.
- **Release years:** Titles span **1925 to 2020**, with a median release year of 2016.

> Country and genre counts overlap because many titles list several countries or categories. Totals should not be summed as if each title belonged to only one.

## 🧪 Feature Engineering

| Feature | Description |
|---|---|
| `added_year`, `added_month` | Extracted from `date_added` |
| `genre_count` | Number of genres listed per title |
| `cast_count` | Number of cast members listed per title |
| `log_duration` | Log-transformed duration (`log1p`) |
| `genre_*` | One-hot indicators for the 10 most common genres |
| `type_encoded` | Movie = 0, TV Show = 1 |
| `*_scaled` | Min-max scaled `release_year`, `duration_value`, `genre_count`, `cast_count` |

The final feature matrix `X` has shape **(6234, 19)**, with the optional target `y` (`type_encoded`) for a possible classification exercise. No model is trained in this notebook.

## 🚀 Getting Started

### Option 1: Run in Google Colab

1. Upload `Cinelytics.ipynb` to [Google Colab](https://colab.research.google.com/)
2. Select **Runtime → Run all**

### Option 2: Run locally

```bash
# Clone the repository
git clone https://github.com/<ZuhaibHassan13>/<Cinelytics>.git
cd <Cinelytics>

# (Optional) create a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install numpy pandas matplotlib seaborn jupyter

# Launch the notebook
jupyter notebook Cinelytics.ipynb
```

> **Note:** The notebook's fallback upload cell and the final download cell use `google.colab`. When running locally, skip those cells. The dataset downloads automatically from the URL, and the exported CSVs are saved in the working directory.

## 📁 Project Structure

```
├── Cinelytics.ipynb                    # Main analysis notebook
├── README.md                           # Project documentation
├── netflix_cleaned.csv                 # Cleaned dataset (generated)
├── netflix_features_engineered.csv     # Dataset with engineered features (generated)
├── netflix_feature_matrix.csv          # Model-ready feature matrix X (generated)
└── netflix_target.csv                  # Encoded target y (generated)
```

## 📤 Output Files

| File | Contents |
|---|---|
| `netflix_cleaned.csv` | Cleaned data, including parsed duration columns |
| `netflix_features_engineered.csv` | Cleaned data plus all engineered features |
| `netflix_feature_matrix.csv` | Numeric feature matrix `X` (19 features) |
| `netflix_target.csv` | Encoded content type `y` (0 = Movie, 1 = TV Show) |

## ⚠️ Limitations

- Missing values in `director`, `cast`, and `country` were **not imputed**, since inventing values would distort the analysis.
- Multi-valued fields (country, genre, cast) overlap, so category counts are not mutually exclusive.
- `release_year` is the original release year, which differs from the year Netflix added the title.
- The dataset is a snapshot, so it may not reflect Netflix's current catalogue.
- Correlation analysis is limited because the dataset has few numeric columns, and correlation does not imply causation.
- In any future ML work, scaling parameters should be fit on training data only to avoid data leakage.

## 🔮 Future Work

- Build a classifier to predict Movie vs TV Show using the prepared feature matrix
- Add text analysis (TF-IDF / NLP) on the `description` column
- Build a content-based recommendation system
- Create an interactive dashboard with Plotly, Streamlit, or Power BI
- Analyze rating distributions and director/cast networks

## 🤝 Contributing

Contributions, issues, and feature requests are welcome. Feel free to open an issue or submit a pull request.

## 📄 License

This project is licensed under the [MIT License](LICENSE). The dataset belongs to its original source and is used here for educational purposes.

## 👤 Author

**Your Name**
- GitHub: [@ZuhaibHassan13](https://github.com/ZuhaibHassan13)
- LinkedIn: [Zuhaib Hassan](https://www.linkedin.com/in/iamzuhaibhassan)

---

⭐ If you found this project helpful, consider giving it a star!
