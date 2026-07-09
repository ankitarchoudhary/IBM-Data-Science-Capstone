# SpaceX Falcon 9 First-Stage Landing Prediction

A data science capstone project analyzing SpaceX Falcon 9 launch data to predict whether the
first stage will land successfully, and what factors influence that outcome.

## Problem Statement

SpaceX advertises Falcon 9 launches at a fraction of the cost charged by other providers, largely
because it reuses the first stage instead of discarding it after every flight. If the outcome of
a landing attempt can be predicted from launch conditions (payload, orbit, site, and booster
characteristics), that prediction can be used to estimate launch cost. This project builds and
compares several classification models to make that prediction, after collecting and exploring
the underlying launch data end to end.

## Project Workflow

| Phase | Description | Notebook |
|---|---|---|
| 1 | Data Collection - SpaceX REST API and Wikipedia web scraping | `Phase1_Data_Collection.ipynb` |
| 2 | Data Wrangling - deriving the landing outcome (`Class`) label | `Phase2_Data_Wrangling.ipynb` |
| 3 | EDA with Data Visualization - Matplotlib and Seaborn | `Phase3_EDA_Visualization.ipynb` |
| 4 | EDA with SQL - 10 queries against the dataset | `Phase4_EDA_SQL.ipynb` |
| 5 | Interactive Visual Analytics - Folium map and Plotly Dash dashboard | `Phase5_Interactive_Visual_Analytics.ipynb` |
| 6 | Predictive Analysis - Logistic Regression, SVM, Decision Tree, KNN | `Phase6_Predictive_Analysis.ipynb` |

## Dataset

- **90 Falcon 9 launches**, collected from the [SpaceX REST API](https://github.com/r-spacex/SpaceX-API)
  and the [Wikipedia list of Falcon 9 and Falcon Heavy launches](https://en.wikipedia.org/wiki/List_of_Falcon_9_and_Falcon_Heavy_launches)
- Features include payload mass, orbit type, launch site, number of previous flights, booster
  block version, and whether the booster had grid fins, landing legs, or was previously reused
- Target variable: `Class` (1 = first stage landed successfully, 0 = it did not)

## Key Results

**Overall landing success rate: 66.7%** (60 successful landings out of 90)

**Success rate by launch site:**
| Launch Site | Launches | Success Rate |
|---|---|---|
| KSC LC-39A | 22 | 77.3% |
| VAFB SLC-4E | 13 | 76.9% |
| CCAFS SLC-40 | 55 | 60.0% |

**Success rate by orbit type (highest to lowest):**
ES-L1, GEO, HEO, and SSO orbits all show a 100% success rate, VLEO follows at 85.7%, while GTO
(the most common orbit in the dataset, with 27 launches) has the lowest success rate at 51.9%.

**Success rate improved substantially over time:** from 0% in the earliest years (2010-2013) to
83-90% by 2017-2020, reflecting SpaceX's growing landing expertise.

**Best predictive model: K-Nearest Neighbors (KNN)**, with 94.4% accuracy on the held-out test
set, ahead of Decision Tree (88.9%), and Logistic Regression and SVM (83.3% each). Full
hyperparameter tuning was performed for all four models using `GridSearchCV`.

## Tools and Libraries

- **Data collection:** `requests`, `BeautifulSoup4`
- **Data analysis:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`, `plotly`
- **SQL:** `sqlite3`
- **Interactive mapping:** `folium`
- **Dashboard:** `dash`
- **Machine learning:** `scikit-learn` (Logistic Regression, SVM, Decision Tree, KNN, `GridSearchCV`)

## Repository Structure

```
.
├── Phase1_Data_Collection.ipynb
├── Phase2_Data_Wrangling.ipynb
├── Phase3_EDA_Visualization.ipynb
├── Phase4_EDA_SQL.ipynb
├── Phase5_Interactive_Visual_Analytics.ipynb
├── Phase6_Predictive_Analysis.ipynb
├── dataset_part_1.csv          # Raw data from the SpaceX API
├── dataset_part_2.csv          # Raw data scraped from Wikipedia
├── spacex_wrangled.csv         # Cleaned dataset with the Class label, used from Phase 3 onward
└── README.md
```

## How to Run

All notebooks were built and tested in Google Colab.

1. Open a notebook in [Google Colab](https://colab.research.google.com)
2. Upload the required CSV file(s) listed at the top of that notebook, using the Files panel
3. Run all cells in order

## Author

**Ankita Choudhary**
