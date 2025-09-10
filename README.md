## World Happiness Report (2015–2017)

This project performs exploratory data analysis (EDA) and visualization on World Happiness Report datasets (2015, 2016, 2017). All analyses live in the `world_happiness_report.ipynb` notebook.

## Table of Contents
- **Purpose**
- **Datasets**
- **Setup and Execution**
- **Notebook Workflow**
- **Visualizations**
- **Findings**
- **Column Descriptions**
- **Year-Specific Column Name Differences**
- **Reproducibility Steps**
- **License and Source**

## Purpose
Analyze happiness scores for 2015–2017 and the core contributing factors (economy, social support, life expectancy, freedom, perceived corruption, generosity), compare top/bottom countries, and perform cross-year comparisons.

## Datasets
CSV files located at the project root:
- `2015.csv`
- `2016.csv`
- `2017.csv`

2015 and 2016 share similar column names. The 2017 dataset uses dotted and slightly different naming (see "Year-Specific Column Name Differences").

## Setup and Execution
### Requirements
- Python 3.8+
- Jupyter Notebook/Lab

### Recommended environment setup
```bash
python -m venv .venv
.venv\Scripts\activate  # Windows
pip install --upgrade pip
pip install pandas seaborn matplotlib jupyter
```

### Run the notebook
```bash
jupyter notebook
# Then open "world_happiness_report.ipynb"
```

## Notebook Workflow
The notebook first explores the 2016 dataset, then proceeds to cross-year comparisons for 2015–2017.

- **Data loading and first look**: `pd.read_csv(...)`, `head`, `tail`, `info`, `isnull`, `dtypes`.
- **Unique countries**: coverage via `data["Country"].unique()`.
- **Country-level visualizations**:
  - Top 10 and bottom 10 countries by happiness (bar plots).
  - Filtering a specific country (e.g., `data[data["Country"] == "Turkey"]`).
  - Highest/lowest examples for the economy indicator (GDP per capita).
- **Overlaid bar plots**: Overlaying Happiness Score and Economy on the same axis with distinct colors.
- **Top 10 by factor**: Economy, Family (social support), Health (life expectancy), Freedom, Trust (government corruption), Generosity.
- **Cross-year comparison**: Information and samples for 2015/2016/2017; year-wise happiness score plots.
- **Concatenation**: `pd.concat([data1, data2, data3], ignore_index=True)` yielding a 470-row combined frame; retaining only `Country`, `Happiness Rank`, `Happiness Score` for a simple top-10 visualization.

## Visualizations
- Top/bottom 10 countries (2016).
- Economy (GDP per capita) highest/lowest examples.
- Overlaid bar plots for Happiness Score and Economy.
- Year-wise bar plots for 2015–2017 happiness scores.
- Six-panel chart for top 10 by individual factors.

## Findings
- Scandinavian countries (Norway, Denmark, Iceland, Finland, Sweden) consistently rank near the top in 2015–2017.
- Higher GDP per capita, stronger social support, and longer life expectancy typically associate with higher happiness scores.
- The 2016 dataset has no missing values (157 rows, 13 columns). The 2015 and 2017 datasets are also largely complete.

## Column Descriptions (2016 reference)
- **Country**: Country name
- **Region**: Geographic region
- **Happiness Rank**: Rank by happiness (1 is highest)
- **Happiness Score**: Overall happiness score
- **Lower/Upper Confidence Interval**: Confidence interval bounds for the score
- **Economy (GDP per Capita)**: Contribution of GDP per capita
- **Family**: Social support
- **Health (Life Expectancy)**: Expected lifespan
- **Freedom**: Freedom to make life choices
- **Trust (Government Corruption)**: Perceived corruption (lower is better)
- **Generosity**: Generosity
- **Dystopia Residual**: Reference component for comparison

## Year-Specific Column Name Differences
- 2015 & 2016: `Happiness Score`, `Economy (GDP per Capita)`, `Health (Life Expectancy)`, etc.
- 2017: `Happiness.Score`, `Economy..GDP.per.Capita.`, `Health..Life.Expectancy.`, `Whisker.high`, `Whisker.low`, etc.

When combining years, consider renaming 2017 columns for consistency. Example mapping:
```python
rename_2017 = {
    "Happiness.Score": "Happiness Score",
    "Happiness.Rank": "Happiness Rank",
    "Whisker.high": "Upper Confidence Interval",
    "Whisker.low": "Lower Confidence Interval",
    "Economy..GDP.per.Capita.": "Economy (GDP per Capita)",
    "Health..Life.Expectancy.": "Health (Life Expectancy)",
    "Trust..Government.Corruption.": "Trust (Government Corruption)",
    "Dystopia.Residual": "Dystopia Residual"
}
```

## Reproducibility Steps
1. Install the required packages (see Setup).
2. Open the notebook in Jupyter.
3. Execute cells sequentially. Jupyter's default settings will render the plots (or use `%matplotlib inline`).

## License and Source
- Data source: World Happiness Report. See `https://worldhappiness.report/` for the official reports and datasets.
- This repository is for educational EDA/visualization purposes only.


