#  NYC Traffic Safety Analysis Using Spark SQL

This project analyzes New York City's motor vehicle collision data to evaluate whether traffic-safety initiatives (speed limit reductions, road redesigns, etc.) have improved safety outcomes over time.

Using **Spark SQL + Scala**, collision data is retrieved from the **NYC Open Data API**, cleaned, transformed, and aggregated to compute injury-to-death safety ratios for both pedestrians and total persons. The analysis also compares trends across the five boroughs.

---

##  **Objectives**

### 1 Citywide Trends  
Compute and evaluate year-over-year changes in:
- **Pedestrian injury-to-death ratio**
- **Total injury-to-death ratio**

These ratios help indicate whether NYC’s roads are becoming safer.

### 2 Borough-Level Comparison  
Compare safety performance across:
- Bronx  
- Manhattan  
- Queens  
- Brooklyn  
- Staten Island  

This identifies which boroughs improved the most.

---

##  **Technologies Used**
- Apache Spark SQL  
- Scala  
- Socrata Open Data API  
- Jupyter Notebook (Apache Toree Kernel)

---

##  **Data Source (NYC Open Data API)**  
Data is retrieved using the Socrata API with selected fields:

borough,
crash_date,
number_of_pedestrians_injured,
number_of_pedestrians_killed,
number_of_persons_injured,
number_of_persons_killed

Only rows with at least one person **injured OR killed** are included.

---

##  **Main Steps**

### **1. Retrieve API Data**
A Scala function fetches JSON data from the NYC Open Data API and loads it into Spark.

### **2. Extract Crash Year**
A user-defined function slices the crash_date string to create a new `year` column.

### **3. Compute Citywide Ratios**
For each year:
- Pedestrian injuries ÷ pedestrian deaths  
- Total injuries ÷ total deaths  

Zero denominators are safely handled using `when(...).otherwise(...)`.

### **4. Compute Borough-Level Ratios**
Data is filtered by borough and grouped by both `borough` and `year`.

### **5. Format Output**
Ratios are formatted to two decimal places using Spark’s `format_number`.

---

##  **Example Output (Citywide)**

| year | ped_inj_to_death | total_inj_to_death |
|------|------------------|---------------------|
| 2022 | 84.82            | 193.76              |
| 2023 | 78.18            | 202.36              |
| 2024 | 75.52            | 210.91              |

*(Actual numbers may vary depending on updated data.)*

---

##  **Repository Structure**
├── NYC_Traffic_Safety_Analysis.ipynb # Main Spark SQL analysis
├── README.md # Project documentation

---

##  **How to Run**
1. Install Apache Toree or run in a Spark-enabled Jupyter environment  
2. Ensure SparkSession is configured (e.g., driver memory)  
3. Run notebook cells sequentially  

---

##  **Summary**
This project demonstrates:

✔ Data retrieval using a REST API  
✔ Building data pipelines in Spark SQL  
✔ UDF creation for string manipulation  
✔ Aggregation of injury/death statistics  
✔ Borough-level safety comparisons  
✔ A clean and repeatable data-processing workflow  

This notebook can serve as a portfolio-ready example of large-scale data processing using Spark.

---
