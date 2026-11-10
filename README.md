# 01-exploratory-data-analysis
Project 01 · Exploratory data analysis with pandas, Matplotlib and Seaborn: cleaning, plotting every variable, and testing hypotheses.
 
**Dataset:** 65 years of Bangladesh weather · **Status:** in progress
 
## Problem
 
How does Bangladesh's climate vary by season, region and decade? This notebook explores monthly records (1948–2013) from Bangladesh Meteorological Department stations. The catch: station coverage is uneven and gaps were filled by an undocumented method, so every pattern is checked against how the data was built.
 
**Data:** [Kaggle: 65 Years of Weather Data Bangladesh](https://www.kaggle.com/datasets/emonreza/65-years-of-weather-data-bangladesh-preprocessed) (not included in this repo).
 
## Hypotheses
 
| # | Hypothesis | False if |
|---|---|---|
| H1 | June–September rainfall is ≥70% of the annual total in most years. | Share < 0.70 in more than half the years |
| H2 | Each decade is warmer than the previous one (stations present in all decades; max and min temperature reported separately). | Any decade is cooler than the one before |
| H3 | Coastal stations are more humid than inland ones. | Inland mean ≥ coastal mean |
| H4 | Cloud cover is stable year to year. | Coefficient of variation of annual means ≥ 10% |
 
 
## Results
 
| # | Result | Verdict |
|---|---|---|
| H1 | — | — |
| H2 | — | — |
| H3 | — | — |
| H4 | — | — |
 
*Figure: to be added.*
 
## Reproduce
 
```bash
conda create -n ml_env python=3.12 -y && conda activate ml_env && pip install -r requirements.txt
# download the dataset into data/weather/
jupyter nbconvert --to notebook --execute --inplace eda_bangladesh_weather.ipynb
```
 
## What I learned
 
*To be written.*
 
Decisions are logged in [DECISIONS.md](DECISIONS.md). Quick looks at Titanic and UCI Heart Disease are in `quicklook_*.ipynb`.