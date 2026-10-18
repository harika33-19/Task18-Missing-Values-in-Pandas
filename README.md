# Task18-Missing-Values-in-Pandas

## Task Overview
Identify missing values in a dataset and practice handling them using Pandas techniques such as dropping and filling missing values.

## Objectives
- Detect missing values in a DataFrame.
- Count missing values by column and across the entire dataset.
- Use `isna()` and `notna()`.
- Compare dropping missing rows with filling missing values.
- Create a cleaned dataset.

## Tools Used
- Python
- Pandas
- Google Colab / Jupyter Notebook

## Dataset
This project uses a small sample student dataset with the columns:
- `Name`
- `Age`
- `Marks`
- `City`

Some entries are intentionally missing (`None`) to demonstrate data-cleaning methods.

## Steps Performed

### 1. Import Pandas
```python
import pandas as pd
```

### 2. Create the sample dataset
```python
data = {
    "Name": ["Ravi", "Sita", "Arjun", "Priya", "Rahul"],
    "Age": [18, None, 20, None, 19],
    "Marks": [85, 90, None, 80, 75],
    "City": ["Guntur", "Vijayawada", None, "Hyderabad", "Guntur"]
}
df = pd.DataFrame(data)
print(df)
```

### 3. Detect missing values
```python
df.isna()
```
`isna()` returns `True` where a value is missing and `False` otherwise.

### 4. Count missing values
```python
df.isna().sum()       # Missing values in each column
df.isna().sum().sum() # Total missing values
```

### 5. Identify available values
```python
df.notna()
df[df["Age"].notna()]  # Rows where Age is available
```
`notna()` returns `True` where a value is present.

### 6. Drop rows with missing values
```python
dropped_df = df.dropna()
```
`dropna()` removes rows containing at least one missing value. The original `df` remains unchanged unless reassigned or modified in place.

### 7. Fill missing values
```python
clean_df = df.copy()

clean_df["Age"] = clean_df["Age"].fillna(clean_df["Age"].mean())
clean_df["Marks"] = clean_df["Marks"].fillna(clean_df["Marks"].median())
clean_df["City"] = clean_df["City"].fillna(clean_df["City"].mode()[0])
```
- **Mean:** average of available numerical values.
- **Median:** middle value of available numerical values.
- **Mode:** most frequent value; useful for categorical columns.

### 8. Verify the cleaned dataset
```python
print(clean_df)
print(clean_df.isna().sum())
```

## Key Findings
- `Age` has 2 missing values.
- `Marks` has 1 missing value.
- `City` has 1 missing value.
- There are 4 missing values in total.
- `dropna()` removes incomplete rows, while `fillna()` preserves rows by replacing missing entries.

## Conclusion
Missing-value handling is an important data-preprocessing step. The choice between dropping and filling values depends on the dataset and the meaning of the missing data. Mean, median, and mode should be selected carefully rather than applied blindly.

## Interview Questions
1. What are missing values?
2. What is the difference between `isna()` and `notna()`?
3. What does `dropna()` do?
4. What does `fillna()` do?
5. When would you use mean, median, or mode to fill missing values?
