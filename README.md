# AI Usage Impact Analysis

A data analysis project about how students and professionals use AI tools, and how this usage relates to their productivity, time saved and satisfaction.

I wanted to answer simple questions like:

- Which AI tools and purposes are the most popular?
- Do people who use AI more hours really feel more productive?
- Is there a difference between students and professionals?
- Do paid users get more value than free users?

## Dataset

- **File:** `AI_Usage_and_Impact_on_Students_and_Professionals.csv`
- **Size:** 300 rows and 19 columns (288 rows after removing duplicates)

Main columns: age, gender, country, user type (student / professional), education, profession, monthly income, AI tool, AI purpose, AI usage hours per day, monthly AI cost, productivity score, accuracy rating, satisfaction score, time saved per week, work/study hours per day and would recommend.

The raw data was messy: mixed text and numbers (`16 yrs`, `2 hrs`, `$20`), different spellings (`chatgpt`, `Chat GPT`, `ChatGPT`), missing values, duplicated users and some impossible values.

## Project Structure

```
AI-Usage-Impact-Analysis/
├── Data/
│   ├── raw/                  # original csv
│   └── processed/            # cleaned_data.csv (created by notebook 1)
├── notebooks/
│   ├── 01_Data_UnderStanding___Cleaning.ipynb
│   └── 02_EDA.ipynb
├── images/                   # all plots (saved automatically by notebook 2)
├── requirements.txt
└── README.md
```

## What i did

### 1. Data Understanding & Cleaning (`01_Data_UnderStanding___Cleaning.ipynb`)

- Checked shape, types, missing values and duplicates.
- Removed 12 duplicated users.
- Converted text columns to numbers (age, income, AI cost, hours).
- Standardized names in gender, country, education and AI tool.
- Grouped 120+ different professions into 8 profession groups.
- Handled wrong values:
  - age above 80 (like 97) -> treated as missing
  - AI usage above 16 hours per day (one user had 23) -> treated as missing
  - a student with 250,000 monthly income -> treated as missing
- Filled missing values:
  - age and income -> median per user type (students and professionals are very different)
  - scores, hours, cost -> median
  - accuracy rating -> most common value (it is a 2 to 5 rating, so no 3.5)
  - categories -> `Unknown` (also for `Would_Recommend`, i don't want to invent a "Maybe")
- Created new columns: `Plan` (free / paid), `Age_Group`, `Usage_Level`, `Time_Saved_Ratio`, `Age_Edu_Mismatch`.
- Saved the result in `Data/processed/cleaned_data.csv`.

### 2. EDA (`02_EDA.ipynb`)

- **Categorical analysis:** user type, tools, purposes, profession groups, country, gender, education, recommendation.
- **Univariate analysis:** distribution of every numeric column + boxplots to find outliers.
- **Bivariate analysis:** usage vs productivity, usage vs time saved, correlation heatmap, students vs professionals, tool vs productivity, purpose vs time saved, paid vs free, usage level, age group and country.
- **Statistical checks:** Mann-Whitney and Kruskal tests to see if the differences are real or just by chance.

## Some Results

- **ChatGPT** is the most used tool (119 of 288 users), then Google Gemini, Microsoft Copilot and Claude.
- **Coding** is the most common purpose (65 users), then writing, studying and research.
- The data is almost balanced: 151 students and 137 professionals.
- India has the most users (43), followed by the United States and Canada.
- 170 users would recommend AI tools and 71 would not.
- AI usage hours have a **strong positive relation** with productivity and time saved (Pearson about 0.64 and 0.74 before removing the 23 hours outlier, the notebook prints the final numbers with Spearman too).

### Plots

| | |
|---|---|
| ![AI tools](images/02_ai_tools.png) | ![AI purpose](images/03_ai_purpose.png) |
| ![Usage vs productivity](images/19_usage_vs_productivity.png) | ![Usage vs time saved](images/20_usage_vs_time_saved.png) |
| ![Correlation heatmap](images/21_correlation_heatmap.png) | ![Students vs professionals](images/22_user_type_comparison.png) |
| ![Productivity by tool](images/23_productivity_by_tool.png) | ![Paid vs free](images/25_paid_vs_free.png) |

## Limitations

- Small sample (288 users), and some countries and tools have very few users.
- All the scores are self reported, so they are opinions, not measured productivity.
- Correlation is not causation. Maybe people who are already productive use AI more.
- Missing values were filled with the median, which makes the data a bit more "average".
- Income may be in different currencies, so comparing it between countries is not 100% fair.
- A few rows have strange combinations (like age under 18 with a PhD). They are kept but flagged with `Age_Edu_Mismatch`.

## How to Run

```bash
pip install -r requirements.txt
jupyter notebook
```

Then put the raw csv in `Data/raw/` and run the notebooks in order: `01` then `02`.

## Next Steps

- Build a simple model to predict productivity score from usage, tool, purpose and user type.
- Analyse the `Tasks_Performed` text column.
- Make a dashboard (Power BI / Streamlit) for the main findings.

## Tools

Python, Pandas, NumPy, Matplotlib, Seaborn, SciPy, Jupyter Notebook

## Contact

<a href="mailto:mohamedelkomy367@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Gmail"></a>
<a href="https://www.linkedin.com/in/mohamed-elkomy-me30/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"></a>