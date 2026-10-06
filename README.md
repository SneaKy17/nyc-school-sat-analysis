# NYC Public School SAT Analysis (Pandas + SQL + Statistics)

An analysis of SAT results for 375 NYC public high schools. It answers three questions in **Pandas**, reproduces them in **SQL (DuckDB)**, and then goes further with statistical tests.

## Questions
1. Which schools are best for math (average math score of at least 640, i.e. 80% of 800)?
2. Which 10 schools have the highest total SAT score?
3. Which borough has the highest standard deviation of total SAT scores?

## Key findings
- **10 schools** average at least 640 in math. Stuyvesant High School leads (754 math, 2,144 total).
- **Manhattan** has the largest spread in total SAT (SD 230.29, n = 89).
- Staten Island is a close second (SD 222.30) but has only 10 schools. Its bootstrap 95% interval (48.7 to 335.8) contains Manhattan's (184.9 to 269.9), so the data cannot confirm Manhattan's spread is truly larger.
- Boroughs differ in typical score (Kruskal-Wallis p = 3.3e-12, epsilon-squared = 0.15). Manhattan, Queens and Staten Island score higher than Bronx and Brooklyn.
- Schools where more students take the SAT score higher (Spearman rho = 0.61). This is an association, not proof of cause.

![Total SAT by borough](images/sat_by_borough.png)
![Participation vs SAT](images/tested_vs_sat.png)

## Methods
- Data checks: missing values, duplicates, valid 200-800 score range.
- Pandas: filtering, feature creation, `groupby` aggregation.
- SQL (DuckDB): CTEs, `JOIN`, `RANK()` window function, with `assert_frame_equal` checks that SQL matches Pandas.
- Statistics: Shapiro-Wilk, Kruskal-Wallis with effect size, Levene's test, pairwise Mann-Whitney with Bonferroni correction, bootstrap confidence intervals for standard deviations.

## Run it
```bash
pip install -r requirements.txt
jupyter notebook nyc_school_sat_analysis.ipynb
```
`schools.csv` must be in the same folder as the notebook.

## Limitations
Scores are school averages, not student-level data. 20 schools lack `percent_tested`. Staten Island has only 10 schools. Differences between boroughs reflect many unmeasured factors.

## Data
`schools.csv` comes from the DataCamp guided project "Exploring NYC Public School Test Result Scores". The extended SQL and statistical analysis is my own work.
