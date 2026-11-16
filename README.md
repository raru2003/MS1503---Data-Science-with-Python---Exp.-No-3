# Experiment 3 : Retail Sales and Profit Analysis Using Pandas

## Aim
To create a sample retail dataset, identify and handle missing values (`NaN`/`None`) and duplicate records, and compute summary statistics using Pandas in Python.

## Algorithm

1. **Start** the program.
2. **Import Library**: Import the `pandas` library as `pd` for tabular data cleaning and analysis.
3. **Initialize Raw Retail Dataset**: Create a Python dictionary `data` containing retail records (`Order_ID`, `Product`, `Region`, `Sales`, `Discount`, `Profit`) with deliberate missing (`None`) entries and duplicate rows.
4. **Construct DataFrame & Inspect**:
   * Convert `data` into a Pandas DataFrame `df` using `pd.DataFrame(data)`.
   * Print the original dataset and its initial dimensions (`df.shape`).
5. **Detect Missing Values**:
   * Count missing entries per column using `df.isnull().sum()`.
6. **Impute Missing Values**:
   * Replace missing numerical values in `Sales`, `Discount`, and `Profit` with their respective column means using `.fillna(df[col].mean())`.
   * Replace missing categorical values in `Region` with the column mode (most frequent category) using `.fillna(df["Region"].mode()[0])`.
7. **Remove Duplicate Records**:
   * Drop exact duplicate rows from `df` using `df.drop_duplicates()`.
8. **Display Cleaned Dataset & Summary Statistics**:
   * Print the cleaned DataFrame, updated dimensions (`df.shape`), and descriptive statistical metrics (`df.describe()`).
9. **Stop** the program.

## Functions and Methods Used

| Category | Function / Method | Purpose / Description |
| :--- | :--- | :--- |
| **Data Creation & Inspection** | `pd.DataFrame()` | Converts a Python dictionary into a labeled 2D tabular DataFrame |
| | `df.shape` | Returns the `(rows, columns)` dimensions before and after cleaning |
| | `df.isnull().sum()` | Counts the number of missing (`NaN`/`None`) values in each column |
| **Missing Value Imputation** | `df[col].fillna()` | Replaces missing values with a specified replacement value |
| | `df[col].mean()` | Calculates the arithmetic mean for numerical column imputation |
| | `df[col].mode()[0]` | Retrieves the most frequent category for categorical column imputation |
| **Deduplication & Summary** | `df.drop_duplicates()` | Identifies and removes duplicate rows from the DataFrame |
| | `df.describe()` | Generates count, mean, standard deviation, min, quartiles, and max for numerical features |

## Program

#Cleaning and Preparing Retail Data using Pandas

#Step 1: Create a sample retail dataset
import pandas as pd

data = {
    'Order_ID': [101, 102, 103, 104, 105, 105, 106, 107],
    'Product': ['Laptop', 'Mobile', 'Tablet', 'Laptop',
                'Mobile', 'Mobile', 'Tablet', 'Laptop'],
    'Region': ['South', 'North', None, 'East',
               'West', 'West', 'South', None],
    'Sales': [50000, 30000, 25000, None,
              40000, 40000, None, 55000],
    'Discount': [5000, None, 2000, 3000,
                 4000, 4000, None, 5000],
    'Profit': [8000, 5000, None, 7000,
               6000, 6000, 4500, None]
}

df = pd.DataFrame(data)

print("Original Dataset:\n", df)
print("\nInitial Shape:", df.shape)

#Step 2: Check for missing values
print("\nMissing Values:")
print(df.isnull().sum())

#Step 3: Fill missing numeric values with column mean
numeric_cols = ['Sales', 'Discount', 'Profit']

for col in numeric_cols:
    df[col] = df[col].fillna(df[col].mean())
    
#Step 4: Fill missing Region with mode (most frequent value)
df['Region'] = df['Region'].fillna(
    df['Region'].mode()[0]
)

#Step 5: Remove duplicate records
df = df.drop_duplicates()

#Step 6: Display summary statistics
print("\nCleaned Dataset:\n", df)

print("\nUpdated Shape:", df.shape)

print("\nSummary Statistics:\n", df.describe())


## Output
Initial Shape: (8, 6)

Missing Values:
Order_ID    0
Product     0
Region      2
Sales       2
Discount    2
Profit      2

Updated Shape: (7, 6)

Summary Statistics:

         Order_ID         Sales      Discount       Profit
count    7.000000      7.000000      7.000000     7.000000
mean   103.428571  38571.428571   3857.142857  6142.857143
min    101.000000  25000.000000   2000.000000  4500.000000
max    107.000000  55000.000000   5000.000000  8000.000000

## Result
The program successfully creates a retail dataset, identifies missing entries and duplicate rows, imputes missing values using mean and mode strategies, removes duplicates, and outputs a clean dataset ready for downstream analysis.

