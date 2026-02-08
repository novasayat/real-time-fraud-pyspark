# Real-Time Fraud Detection with PySpark

End-to-end fraud detection pipeline built with PySpark. The project covers data ingestion, exploratory analysis, feature engineering, model training/evaluation, and a simple structured streaming demo that ingests new CSV files as they arrive.

## Project Overview
This repository demonstrates a full fraud-detection workflow on transaction data:
- Batch ingestion with Spark
- Exploratory Data Analysis (EDA)
- Feature scaling and correlation analysis
- Multiple ML models (Logistic Regression, Random Forest, SVM, Decision Tree, Gradient-Boosted Trees)
- Structured Streaming demo using a file-based source

## Dataset Schema
The pipeline expects a CSV with the following columns:
- `step`: time step of the transaction
- `type`: transaction type (categorical)
- `amount`: transaction amount
- `nameOrig`: origin account ID
- `oldbalanceOrig`, `newbalanceOrig`: origin account balances before/after
- `nameDest`: destination account ID
- `oldbalanceDest`, `newbalanceDest`: destination account balances before/after
- `isFraud`: label (0 = non-fraud, 1 = fraud)

## Pipeline Summary
1. **Load & Inspect**: Read CSV into Spark DataFrame, check schema and missing values.
2. **Clean & Cast**: Drop nulls/duplicates; cast numeric columns to numeric types.
3. **Scale Features**: MinMax scaling for numeric features.
4. **EDA & Visualization**: Distribution plots, correlation heatmap.
5. **Modeling**: Train and evaluate multiple classifiers using a Spark ML pipeline.
6. **Streaming Demo**: Monitor `Input/` for new CSVs and query in-memory table.

## Setup
### Requirements
- Python 3.11+
- Java (tested with JDK 17+)
- PySpark, NumPy, Matplotlib, Seaborn

### Install
```bash
py -3.11 -m pip install pyspark numpy matplotlib seaborn
```

## Run (Notebook)
Open `real-time-fraud_detection.ipynb.ipynb` and run cells in order.

### Streaming Demo
The streaming section reads new CSV files dropped into the `Input/` directory.
1. Place a CSV file (same schema) into `Input/`.
2. Run the streaming cells.
3. Use Spark SQL to query the in-memory table `financefraudtable`.

## Notes
- For meaningful model training, the dataset must include **both** fraud and non-fraud rows.
- The lite sample file is useful for pipeline testing but not for real model performance.

## Output
- `Output/`: temporary streaming output
- `finaldirectory/fraud_data.csv`: consolidated streaming output
