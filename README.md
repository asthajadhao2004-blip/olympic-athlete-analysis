# Olympic Athlete Analysis: 120 Years of Olympic History

A data analysis project on the **"120 Years of Olympic History"** dataset: 271,116 athlete-event records covering every Olympic Games from **Athens 1896 to Rio 2016**. Each row is one athlete competing in one event, with age, height, weight, nationality, sport and medal outcome.

The project cleans the data, investigates data-quality issues (missing values, duplicates, outliers) and explores how the Games have changed over time.

## Questions explored

- How has Olympic participation changed over time?
- How has male vs. female participation evolved?
- Which countries (NOCs) have won the most medals?
- What is the age distribution of athletes, and does age affect medal chances?
- How does athlete height vary across sports?
- Which sports have been the most popular over time?
- How has the number of participating countries grown (globalization)?
- How are height and weight related?

## Project structure

```
olympic-athlete-analysis/
├── data/
│   └── athlete_data.csv                 # Dataset (271,116 rows x 15 columns)
├── notebook/
│   └── olympic_athlete_analysis.ipynb   # Main analysis (code + charts + insights)
├── scripts/
│   └── olympic_analysis.py              # Same analysis as a plain Python script
├── presentation/
│   └── Olympic_Athlete_Analysis.pptx    # Project presentation slides
├── requirements.txt
├── .gitignore
└── README.md
```

## Dataset columns

| Column | Description |
|--------|-------------|
| ID | Unique athlete number |
| Name | Athlete's name |
| Sex | M or F |
| Age | Age at the time of the Games |
| Height / Weight | In cm / kg |
| Team / NOC | Team name / National Olympic Committee 3-letter code |
| Games / Year / Season | e.g. "1992 Summer", 1992, Summer or Winter |
| City | Host city |
| Sport / Event | Sport and specific event |
| Medal | Gold, Silver, Bronze, or NA (no medal) |

## Methodology

1. **Data loading and understanding**: shape, types, summary statistics, missing values.
2. **Data cleaning**
   - Removed **1,385 exact duplicate rows** (271,116 to 269,731).
   - Repeated athlete IDs were kept: one athlete can legitimately compete in several events.
   - Blank `Medal` means "no medal", so it was filled with `No Medal`.
   - Missing `Age`, `Height` and `Weight` were imputed with the **median within each Sport + Sex group**, falling back to the overall median.
   - Outliers were found with the **IQR method** and investigated manually. They are real athletes (e.g. older Art Competition entrants, Yao Ming, super-heavyweight wrestlers), so they were **kept**.
3. **Feature engineering**: added a boolean `Medalist` column.
4. **Exploratory data analysis** with matplotlib and seaborn (10 charts, each with a written insight, plus Key Insights, Data Limitations and Conclusion sections).

## Key findings

- Olympic participation and the number of competing countries grew substantially over the 120 years.
- Female participation rose significantly, narrowing the historical gender gap.
- The United States has the most medals in the dataset.
- Most athletes are young adults, with a median age of about 25.
- Medalists and non-medalists have very similar average ages (about 25.9 vs 25.4), so age alone is not a strong predictor of winning.
- Height varies a lot by sport (e.g. Basketball, Volleyball and Water Polo are tall), and height and weight are strongly positively correlated.

## Getting started

### 1. Clone the repository
```bash
git clone (https://github.com/asthajadhao2004-blip/olympic-athlete-analysis.git)
cd olympic-athlete-analysis
```

### 2. Install dependencies
pip install -r requirements.txt
```bash
python -m venv venv
# Windows:  venv\Scripts\activate
# Mac/Linux: source venv/bin/activate
pip install -r requirements.txt
```

### 3. Run the analysis

**Option A: Jupyter Notebook (recommended)**
```bash
cd notebooks
jupyter notebook olympic_athlete_analysis.ipynb
```
Then choose **Kernel > Restart & Run All**.

**Option B: Python script**
```bash
cd scripts
python src/olympic_analysis.py
```
Charts open one after another; close each window to continue.

> The data path is relative (`../data/athlete_data.csv`), so run the notebook or script from inside its own folder (`notebook/` or `scripts/`).

## Pushing your own copy to Git

```bash
git init
git add .
git commit -m "Initial commit: Olympic athlete analysis"
git branch -M main
git remote add origin <your-repo-url>
git push -u origin main
```

`data/athlete_data.csv` is about 41 MB, which is under GitHub's 100 MB per-file limit, so a normal push works. (GitHub may show a large-file notice above 50 MB, which does not apply here.)

## Tech stack

Python, pandas, NumPy, matplotlib, seaborn, Jupyter

## Credits

Dataset: "120 years of Olympic history: athletes and results" (originally scraped from sports-reference.com, shared on Kaggle).
