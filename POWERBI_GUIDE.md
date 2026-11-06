# Power BI Dashboard Guide

1. Run the notebook in Colab. In the left panel (folder icon), download: **breast_cancer_for_powerbi.csv, model_results_for_powerbi.csv**
2. Open Power BI Desktop > **Get data > Text/CSV** and load both files.
3. Check the data types in Power Query (numbers as numbers, labels as text), then **Close & Apply**.
4. Build the pages below. Use one clear title per chart.
5. Save as `dashboard.pbix`, export a screenshot as `dashboard.png`, and add both to the GitHub repository.

**Measures (Modeling > New measure):**
```
Patients = COUNTROWS(breast_cancer_for_powerbi)
Malignant % = AVERAGE(breast_cancer_for_powerbi[malignant])
```
**Page 1: Overview**
- Cards: `Patients`, `Malignant %` (format as percentage)
- Donut chart: Legend = `diagnosis`, Values = count of `diagnosis`
- Clustered bar chart: Y axis = `diagnosis`, X axis = average of `mean radius`, `mean area`, `mean concave points`
- Slicer: `diagnosis`

**Page 2: Model**
- Table: all columns from `model_results_for_powerbi`
- Column chart: X axis = `predicted_malignant_probability` (create bins of 0.1: right-click the field > New group), Legend = `diagnosis`
- Slicer: `set` (Train / Test)

**Tip:** keep colours consistent (for example red for disease or readmission, blue for no disease) across all pages.
