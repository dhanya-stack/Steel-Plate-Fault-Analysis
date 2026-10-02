# Steel Plate Faults: Exploratory Data Analysis

## Project overview

This project explores a steel plate faults dataset using SQL, pandas and Python visualisation. The aim was to understand how recorded fault types vary with steel grade, plate thickness, defect size and defect geometry.

The analysis is exploratory rather than causal. The dataset contains fault instances, but it does not provide the total number of non-faulty plates inspected. Because of that, the results describe patterns among recorded faults rather than true defect rates or causes.

## Questions explored

1. How do fault types differ between A300 and A400 steel?
2. Do different plate thicknesses show different fault distributions?
3. Do different fault types have characteristic sizes or shapes?

## Tools used

- SQL with SQLite for aggregation and grouped queries
- pandas for reshaping and descriptive analysis
- Matplotlib and seaborn for visualisation
- Kaggle Notebook for the analysis workflow

## Dataset summary

**Dataset source:** Steel Plates Faults, UCI Machine Learning Repository (Buscema, Terzi & Tastle, 2010), accessed via Kaggle. DOI: 10.24432/C5J88N.


The dataset contains 1,941 recorded fault instances across seven fault categories:

- Pastry
- Z_Scratch
- K_Scatch
- Stains
- Dirtiness
- Bumps
- Other_Faults

The two steel types represented are A300 and A400.

## Analysis performed

### Steel type comparison

I compared the number and percentage distribution of fault categories within A300 and A400 steel. A300 contains 777 recorded fault instances and A400 contains 1,164.

The distributions differ noticeably. A300 is dominated by Bumps and Other_Faults, while A400 has much larger shares of K_Scatch and Other_Faults.

These results should not be interpreted as defect rates because the total number of inspected plates for each material is unknown.

### Plate thickness

I grouped faults by plate thickness and compared both total fault counts and the percentage mix of fault categories. A heatmap was used to make the differences between thickness groups easier to compare.

Some thicknesses contain many more recorded observations than others. Several thickness groups contain only a handful of records, so patterns in those groups should be treated cautiously.

### Fault size

I used `Pixels_Areas` as a measure of the image area occupied by a detected defect.

K_Scatch stands out clearly. Its median pixel area is 6,281 pixels, compared with medians of roughly 120 to 209 pixels for most other fault types. Stains are particularly small, with a median pixel area of 16.5 pixels.

The distributions also contain several large outliers. These were retained because the dataset does not provide enough information to determine whether they are errors or genuine extreme faults.

### Fault geometry

I derived two additional features:

- `fault_width = X_Maximum - X_Minimum`
- `fault_height = Y_Maximum - Y_Minimum`

The geometry analysis shows that fault classes can have different dimensional characteristics. K_Scatch has a much larger median width than the other categories. One K_Scatch observation also has an exceptionally large fault height, so a zoomed plot was used to compare the typical distributions without deleting the extreme value.

## Key findings

- A300 and A400 contain different distributions of recorded fault types.
- Fault observations are unevenly distributed across plate thicknesses.
- K_Scatch defects are substantially larger in pixel area than most other fault categories.
- Fault categories also show different width and height distributions.
- The dataset is better suited to fault-characterisation and classification questions than to estimating manufacturing defect rates or proving causes.

## Limitations

The most important limitation is the absence of a denominator: the dataset does not show the total number of plates inspected for each steel grade or thickness. Therefore, this analysis cannot determine whether one material or thickness is genuinely more fault-prone.

Some groups also have very small sample sizes, and several variables are image-derived features rather than direct manufacturing-process measurements.

## Reflection

This project changed the way I think about exploratory analysis. I initially approached the data expecting to identify which material or thickness might be associated with particular faults. As I worked through the dataset, I realised that the questions I could answer were constrained by what the data actually contained.

The project gave me practice combining SQL and pandas, reshaping data with `melt()`, comparing percentages rather than only raw counts, and choosing different visualisations for categorical comparisons, distributions and grouped patterns.

## Files

- `steel-plates-faults-analysis.ipynb` — full analysis notebook
- `steel-plate-faults-report.docx` — short portfolio report with selected charts and observations

