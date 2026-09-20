# Comparative Analysis of Sequential Models for Mobile Network Traffic Forecasting

Formative Assignment 1, Machine Learning Techniques I
Principie Cyubahiro, BSc Software Engineering, African Leadership University

One-step-ahead forecasting of mobile internet traffic using two months of call detail
records from Milan. Three models from different families are compared across three
geographical areas.

## Research question

How do different sequential models compare for one-step-ahead mobile network traffic
forecasting, and how does their performance vary across geographical areas with
different traffic characteristics?

## Results

Test week 16 to 22 December, mean absolute error, one-step-ahead:

| Square | Seasonal naive | ARIMA(2,0,2) | LSTM | 1D CNN |
|---|---|---|---|---|
| 5161 | 338.59 | 108.36 | **81.72** | 87.03 |
| 5059 | 171.74 | 89.62 | **67.56** | 75.36 |
| 5259 | 470.32 | 81.74 | **64.20** | 77.32 |

The LSTM is lowest on every metric in every area. The ranking is identical across all
three, despite weekend-to-weekday ratios spanning 0.34 to 1.26.

## Data

Telecom Italia, Milan, 1 November 2013 to 1 January 2014. 10,000 grid squares of about
235 m, aggregated into 10-minute intervals. 62 daily tab-separated files, 19.4 GB.

Download from the Harvard Dataverse:
https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/EGZHFV

Extract all files into `data/raw/` so that folder contains the 62 `.txt` files. The
`data/` directory is gitignored because of its size and because the dataset is not
redistributed here.

## Requirements

**Python 3.11 or 3.12.** TensorFlow has no build for Python 3.13 or 3.14, so the
modelling section will fail on those versions.

```bash
python -m venv venv
source venv/Scripts/activate      # Windows Git Bash
# source venv/bin/activate        # macOS or Linux
pip install -r requirements.txt
```

## Running

Open `PrincipieCyubahiro_Formative1_Assignment_Time_Series_Forecasting.ipynb` and run
all cells from top to bottom.

| Section | Time | Note |
|---|---|---|
| 1. Data handling | ~4 min first run | caches to `data/work/`, skipped afterwards |
| 2. Exploratory analysis | ~3 min | STL and ACF are the slow parts |
| 3. Related work | instant | markdown only |
| 4. Forecasting experiments | ~90 min | 27 tuning runs plus 3 areas, CPU |

Total about 100 minutes on first run, roughly 95 afterwards.

Figures are written to `reports/figures/` and tables to `reports/tables/` as they are
produced, so the report can be assembled without rerunning anything.

## Repository layout