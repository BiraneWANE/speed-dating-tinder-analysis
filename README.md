# Speed Dating Tinder Analysis

Business-oriented exploratory data analysis of the **Speed Dating** experiment used to understand what makes two people interested enough to agree on a second date.

## Project context

This project answers the business question described in the brief: **what makes people interested enough in each other to want a second date?** The deliverable expected a notebook with **descriptive statistics, visualizations, and interpretations** explaining why participants say yes to a second date.

I chose to frame the project from a Tinder / product perspective:

- distinguish what exists **before the interaction** (profile, preferences, demographics, lifestyle),
- from what emerges **during the interaction** (attractiveness, fun, shared interests, overall liking),
- and identify which signals are actually the most useful to explain the final outcome.

## Main business objective

Understand which variables are most associated with:

- an individual **positive decision** (`dec`),
- and a **mutual match** (`match`).

This helps answer a product question for a dating app:

> Should matching rely mostly on profile similarity, or should it try to maximize the probability of a good interaction?

## Dataset

The project uses the classic **Speed Dating** dataset gathered during experimental events from **2002 to 2004**.

### Scope

- **8,378 rows**
- **4,184 unique speed dates**
- **551 unique participants**
- **21 waves**
- each row = **one participant's view of one date**
- therefore, one real date usually appears **twice** in the raw table

## What this notebook does

The notebook goes beyond a basic EDA while staying aligned with the course:

1. **clarifies the unit of analysis**: row level, participant level, pair level;
2. checks **data quality** and missing values;
3. studies both business targets: **`dec`** and **`match`**;
4. answers the main questions suggested in the brief;
5. adds a **light and rigorous modeling bonus** to compare profile-only vs interaction-based information.

## Key questions answered

- What are the least desirable attributes in a partner?
- Does this differ by gender?
- How important is attractiveness compared with its real impact?
- Are shared interests more important than a shared racial background?
- Can people predict their own value in the dating market?
- Is it better to be someone's first speed date or last one?

## Key results

### 1) Matches are rare
- individual **yes rate**: **42.0%**
- mutual **match rate**: **16.5%**

### 2) Men say "yes" more often, but do not get more matches
- women yes rate: **36.5%**
- men yes rate: **47.4%**
- women match rate: **16.5%**
- men match rate: **16.5%**

### 3) Shared interests matter far more than simple demographic similarity
- different race match rate: **16.1%**
- same race match rate: **17.1%**
- very low shared interests match rate: **4.9%**
- very high shared interests match rate: **34.2%**

Interpretation:
- **same race** has only a **small effect**
- **shared interests** have a **very strong effect**

### 4) Participants are only partially calibrated
- correlation between **expected matches** and **actual matches**: **0.43**
- average overconfidence bias, women: **+3.5 points**
- average overconfidence bias, men: **+7.2 points**

Interpretation:
- people are **not completely wrong**
- but they are **too optimistic on average**
- the bias is **stronger for men** in this dataset

### 5) The order of the date has only a weak effect
- correlation between relative order in the evening and match: **-0.020**

Interpretation:
- there may be a small fatigue / sequencing effect
- but it is clearly **secondary** compared with interaction quality

### 6) Small age gaps are better
- match rate with age gap 0–1 years: **18.9%**
- match rate with age gap 6+ years: **12.5%**

### 7) Interaction signals beat profile-only signals
Grouped participant split logistic regression:
- **profile-only model** ROC-AUC: **0.565**
- **date-impression model** ROC-AUC: **0.776**
- **combined model** ROC-AUC: **0.774**

Interpretation:
- profile variables alone explain relatively little
- variables built during the interaction explain much more
- adding profile variables on top of date impressions adds almost nothing

## Product recommendations for Tinder

1. **Do not over-invest in demographic similarity**
   - same-race similarity is weak compared with lived compatibility.

2. **Prioritize compatibility signals**
   - shared interests, fun, and overall liking are much more actionable.

3. **Treat profile variables as weak priors**
   - they can help rank possibilities,
   - but should not dominate the product logic.

4. **Design for quality of interaction**
   - prompts, ice-breakers, interest-based cues, and conversation starters are likely more useful than static similarity alone.

## Repository structure

```text
speed-dating-tinder-analysis-github/
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── speed_dating_data.csv
│   └── speed_dating_data_key.doc
├── notebooks/
│   ├── speed_dating_tinder_analysis_v3.ipynb
│   └── speed_dating_tinder_analysis_v3_executed.ipynb
└── docs/
    ├── executive_summary_v3.md
    ├── presentation_5_levels_fr.md
    ├── soutenance_questionnaire_fr.md
    └── lexique_5_niveaux_fr.md
```

## How to run

### 1. Clone the repository
```bash
git clone <your-repository-url>
cd speed-dating-tinder-analysis-github
```

### 2. Create an environment
```bash
conda create -n speed_dating_311 python=3.11 -y
conda activate speed_dating_311
pip install -r requirements.txt
```

### 3. Launch Jupyter
```bash
jupyter notebook
```

### 4. Open the notebook
Use:

- `notebooks/speed_dating_tinder_analysis_v3.ipynb` to rerun the project
- `notebooks/speed_dating_tinder_analysis_v3_executed.ipynb` to see a ready-to-read executed version

## Improvements made compared with the raw project folder

This GitHub-ready version improves the original folder by:
- removing noisy temporary files from the public repo structure;
- creating a cleaner repository layout;
- adding a real **README**;
- adding a **requirements.txt**;
- keeping a clean executed notebook and a rerunnable notebook;
- adding French defense materials: presentation, questionnaire, and lexicon.

## Limitations

- The dataset comes from a **speed dating experiment**, not a modern mobile app.
- Several strong variables are collected **after the interaction**, so they explain outcomes well but are not all directly available before matching.
- Observations are not fully independent because each participant appears multiple times.
- This is still an **EDA-first project**, not a production-grade causal study.

## Author

Prepared by **Birane WANE** for the Jedha Bloc 2 Speed Dating project.
