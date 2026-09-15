# ECE 2112: Advanced Computer Programming and Algorithms

## Experiment 3: Python Data Analysis (Pandas)

**Student Name:** Bendicio, Sedric Lance B.

**Section:** 2ECE-A

**Date Submitted:** September 15, 2026

---

## Table of Contents

1. [Objectives](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#i-objectives)
2. [Repository Contents](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#ii-repository-contents)
3. [Dataset Overview](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#iii-dataset-overview)
4. [Detailed Problem Solutions & Discussion](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#iv-detailed-problem-solution--discussion)
* [Problem A: Positional and Label-Based Slicing](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#problem-a-positional-andd-label-based-slicing)
* [Problem B: Model Lookup](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#problem-b-model-lookup)
* [Problem C: Multi-Model Subsetting](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#problem-c-multi-model-subsetting)


5. [Constraints & Compliance Checklist](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#v-constraints--compliance-checklist)
6. [How to Run](https://github.com/moriaean/ECE2112_PA3/blob/main/README.md#vi-how-to-run)

---

## I. Objectives

At the end of this laboratory activity, the student should be able to:

1. Load a CSV dataset into a Pandas DataFrame.
2. Select rows and columns using positional (`iloc`) and label-based (`loc`) indexing.
3. Filter records using Boolean condition logic on DataFrame columns.
4. Extract well-defined data subsets without altering the source dataset.

---

## II. Repository Contents

* `Programming Assignment 3 (BENDICIO_2ECE-A).ipynb`: Executed Jupyter Notebook containing all Python source code, function calls, and cell output displays.


* `cars.csv`: The input automotive dataset used for data analysis.
* `README.md`: Comprehensive documentation containing problem breakdowns, methodology, code snippets, test case outputs, and execution instructions.

---

## III. Dataset Overview

The experiment utilizes `cars.csv`, a 32-row by 12-column dataset containing motor trend vehicle specifications.

* **Total Rows:** 32


* **Total Columns:** 12


* **Columns Present:** `Model`, `mpg`, `cyl`, `disp`, `hp`, `drat`, `wt`, `qsec`, `vs`, `am`, `gear`, `carb`


---

## IV. Detailed Problem Solutions & Discussion

### Problem A: Positional and Label-Based Slicing

#### Problem Statement

1. Display the total shape and full list of column names of `cars`.
2. Create `cars_6_to_10` containing rows 6 through 10 (where row 1 represents the first data record) using positional slicing.
3. Display columns `Model`, `mpg`, `cyl`, `hp`, and `gear` from `cars_6_to_10` using label-based column indexing.

#### Methods Used

* `pd.read_csv('cars.csv')`: Loads the CSV dataset into memory as a Pandas DataFrame.
* `DataFrame.shape`: Returns a tuple `(rows, columns)` representing DataFrame dimensions.
* `DataFrame.columns`: Extracts an Index object containing all column names.
* `DataFrame.iloc[start:stop]`: Executes 0-indexed positional slicing. To extract 1-based rows 6 to 10 inclusive, indices `5:10` are sliced (indices 5, 6, 7, 8, and 9).


* `DataFrame[[column_list]]`: Extracts a subset of specified columns by label names.

#### Python Code Implementation

```python
import pandas as pd

# Load dataset
cars = pd.read_csv('cars.csv')
cars

```

```python

# Problem A.a: Shape and Column Names
print(cars.shape)
print(cars.columns)

```

```python

# Problem A.b: Positional Slicing for Rows 6 to 10
cars_6_to_10 = cars.iloc[5:10]
cars_6_to_10

```

```python

# Problem A.c: Label-based Column Selection
cars.loc[6:10, ['Model', 'mpg', 'cyl', 'hp', 'gear']]
```

#### Test Cases & Outputs

**Shape & Column Output:**

* **Shape:** `(32, 12)`

* **Columns:** `Index(['Model', 'mpg', 'cyl', 'disp', 'hp', 'drat', 'wt', 'qsec', 'vs', 'am', 'gear', 'carb'], dtype='object')`


**Extracted Table Output (`result_A`):**

| Index | Model | mpg | cyl | hp | gear |
| --- | --- | --- | --- | --- | --- |
| **5** | Valiant | 18.1 | 6 | 105 | 3 |
| **6** | Duster 360 | 14.3 | 8 | 245 | 3 |
| **7** | Merc 240D | 24.4 | 4 | 62 | 4 |
| **8** | Merc 230 | 22.8 | 4 | 95 | 4 |
| **9** | Merc 280 | 19.2 | 6 | 123 | 4 |

#### Technical Discussion

Because Pandas uses 0-based indexing by default, human-readable Row 1 corresponds to index `0`. Therefore, rows 6 through 10 occupy zero-based indices `5` through `9`. Using `iloc[5:10]` applies Python's exclusive upper boundary rule to capture exactly 5 rows (indices 5, 6, 7, 8, and 9). Column filtering is performed on `cars_6_to_10` using explicit column labels to ensure structural compliance without modifying the underlying source DataFrame.

---

### Problem B: Model Lookup

#### Problem Statement

1. Extract and display the complete record for `Toyota Corolla` using Boolean indexing. Save the output in `toyota`.
2. Extract only columns `Model`, `mpg`, `hp`, and `wt` for `Pontiac Firebird` using Boolean indexing. Save the output in `pontiac`.

#### Methods Used

* `DataFrame['Model'] == 'Value'`: Generates a Boolean Series mapping `True` to matching rows and `False` to non-matching rows.
* `DataFrame.loc[boolean_condition, [columns]]`: Performs conditional filtering and isolates designated column labels simultaneously.

#### Python Code Implementation

```python
# Problem B.a: Full row lookup for Toyota Corolla
toyota = cars.loc[cars['Model']=='Toyota Corolla']
toyota

```

```python

# Problem B.b: Specific column lookup for Pontiac Firebird
pontiac = cars.loc[cars['Model']=='Pontiac Firebird',['Model', 'mpg', 'hp', 'wt']]
pontiac

```

#### Test Cases & Outputs

**`toyota` Output:**

| Index | Model | mpg | cyl | disp | hp | drat | wt | qsec | vs | am | gear | carb |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **19** | Toyota Corolla | 33.9 | 4 | 71.1 | 65 | 4.22 | 1.835 | 19.90 | 1 | 1 | 4 | 1 |

**`pontiac` Output:**

| Index | Model | mpg | hp | wt |
| --- | --- | --- | --- | --- |
| **24** | Pontiac Firebird | 19.2 | 175 | 3.845 |

#### Technical Discussion

Rather than hardcoding numerical index positions (e.g., `cars.iloc[19]`), Boolean indexing searches the `Model` column dynamically. `cars['Model'] == 'Toyota Corolla'` yields a mask where index 19 is `True`. Passing this mask into `.loc` allows flexible and precise lookup regardless of how the dataset rows are arranged or reordered in memory.

---

### Problem C: Multi-Model Subsetting

#### Problem Statement

Create a subset DataFrame named `selected_cars` containing records for three specific models: `Datsun 710`, `Lotus Europa`, and `Ferrari Dino`. Retain only `Model`, `mpg`, `cyl`, `hp`, and `gear` columns. Display the resulting DataFrame and verify that its shape is `(3, 5)`.

#### Methods Used

* `Series.isin([list_of_values])`: Checks whether each element in a column matches any element in the provided list, returning a Boolean mask.
* `DataFrame.shape`: Verifies final row and column dimensions.

#### Python Code Implementation

```python
# Problem C: Subset multiple models and specific columns
selected_cars = pd.DataFrame(cars[cars['Model'].isin(['Datsun 710', 'Lotus Europa', 'Ferrari Dino'])], 
                             columns=['Model', 'mpg', 'cyl', 'hp', 'gear'])
selected_cars

```

```python

# Display dimensional check
display(selected_cars)
print(selected_cars.shape)

```

#### Test Cases & Outputs

**`selected_cars` Output:**

| Index | Model | mpg | cyl | hp | gear |
| --- | --- | --- | --- | --- | --- |
| **2** | Datsun 710 | 22.8 | 4 | 93 | 4 |
| **27** | Lotus Europa | 30.4 | 4 | 113 | 5 |
| **29** | Ferrari Dino | 19.7 | 6 | 175 | 5 |

**Shape Verification Output:**

* **`selected_cars.shape`:** `(3, 5)` *(3 rows, 5 columns)*



#### Technical Discussion

The `.isin()` method provides a vectorized alternative to combining multiple `==` OR conditions (`|`). `.loc` filters rows dynamically by model values while simultaneously indexing specified columns. This ensures original row order is preserved and avoids hardcoded index assumptions. The shape check confirms that exactly 3 records and 5 attribute columns were successfully isolated.

---

## V. Constraints & Compliance Checklist

* [x] **No Manual Typing:** Output data was dynamically generated using Pandas indexing/slicing functions.
* [x] **No Hardcoded Row Indexing in Search Queries:** Problems B & C strictly use Boolean filtering (`==` and `.isin()`).
* [x] **Source Data Preservation:** All operations created isolated subset variables (`cars_6_to_10`, `toyota`, `pontiac`, `selected_cars`) without modifying `cars`.
* [x] **Correct Positional Bounds:** `iloc[5:10]` accurately captures 1-based data rows 6 through 10.
* [x] **Required Dimensional Validation:** `selected_cars.shape` verified to equal `(3, 5)`.

---

## VI. How to Run

1. **Clone the Repository:**
```bash
git clone https://github.com/moriaean/ECE2112_PA3.git
cd ECE2112_PA3

```


2. **Ensure Dependencies are Installed:**
Make sure Python 3.x, Jupyter Notebook, and Pandas are installed in your environment:
```bash
pip install pandas jupyter

```


3. **Launch Jupyter Notebook:**
```bash
jupyter notebook "Programming Assignment 3 (BENDICIO_2ECE-A).ipynb"

```


4. **Execute All Cells:**
In the Jupyter Notebook menu, click **Cell** $\rightarrow$ **Run All** to execute the complete workflow from top to bottom.
