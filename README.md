# Data Parsing, Cleansing, and Integration Pipeline

This project demonstrates a complete **data parsing, cleansing, and integration workflow** for job advertisement datasets. The pipeline handles datasets from multiple sources, identifies and resolves schema and data-level conflicts, and produces a clean, integrated dataset suitable for analysis and downstream applications.

The project involves:
- Parsing XML and CSV datasets into structured formats.
- Cleaning and standardizing data with missing values, inconsistent formatting, and typographical errors.
- Integrating multiple datasets with schema alignment, data transformation, and duplicate handling.


## Environment

- **Programming Language:** Python 3  
- **Development Environment:** Jupyter Notebook  
- **Operating System:** Cross-platform (Windows/Mac/Linux)



## Libraries and Tools Used

- `pandas` – Data manipulation and analysis  
- `numpy` – Numerical computations and array operations  
- `datetime` – Handling date and time conversions  
- `re` – Regular expressions for string pattern matching  
- `IPython.display` – Displaying DataFrames neatly in notebooks  



## Project Workflow

### 1. Data Parsing
- **Input:** `dataset1.xml` containing job advertisements with varying formats and missing values.  
- **Process:**  
  - Examined XML structure using Python libraries.  
  - Parsed XML into a Pandas DataFrame with standardized columns:  
    `Id`, `Title`, `Location`, `Company`, `ContractType`, `ContractTime`, `Category`, `Salary`, `OpenDate`, `CloseDate`, `SourceName`.  
  - Converted `OpenDate` and `CloseDate` from `YYYYMMDDThhmmss` to `YYYY-MM-DD HH:MM:SS`.  

- **Output:** Cleaned DataFrame for further processing.



### 2. Data Auditing and Cleansing
- **Objectives:** Identify and fix data quality issues in `dataset1`.  
- **Key Steps:**  
  - Filled missing values with `non-specified` where applicable.  
  - Standardized `ContractType` and `ContractTime` to consistent values:  
    - `ContractType`: `full_time`, `part_time`, `non-specified`  
    - `ContractTime`: `permanent`, `contract`, `non-specified`  
  - Ensured salary values were valid floats with two decimal places.  
  - Corrected typos and inconsistencies in categorical fields.  
  - Documented all errors and fixes in an `errorlist.csv` file for transparency.  

- **Output:** `dataset1_solution.csv` – Cleaned dataset ready for integration.



### 3. Data Integration
- **Input:**  
  - Cleaned dataset: `dataset1_solution.csv`  
  - Additional dataset: `dataset2.csv` from a separate source  

- **Schema Alignment and Transformation:**  
  - Renamed columns in `dataset2` to match `dataset1` format.  
  - Converted monthly payments to yearly salaries and renamed column to `Salary`.  
  - Standardized `ContractType` and `ContractTime` to align with the primary dataset.  
  - Generated unique IDs for records in `dataset2`.  
  - Handled missing company names by replacing nulls with `non-specified`.  
  - Dropped conflicting columns (e.g., `SourceName`) to maintain consistent schema.

- **Merging and Deduplication:**  
  - Combined datasets using `pd.concat()` after schema alignment.  
  - Verified data types consistency across all columns.  
  - Checked for duplicates based on `Id` column and removed any found.  

- **Output:**  
  - Integrated and cleaned dataset: `dataset_integrated.csv`  
  - Contains all records from both sources with standardized schema and consistent data types.



## Dataset Schema (Final Integrated Dataset)

| Column        | Description |
|---------------|-------------|
| Id            | 8-digit unique identifier for the job advertisement |
| Title         | Job title; 'non-specified' if missing |
| Location      | Job location; 'non-specified' if missing |
| Company       | Employer name; 'non-specified' if missing |
| ContractType  | `full_time`, `part_time`, or `non-specified` |
| ContractTime  | `permanent`, `contract`, or `non-specified` |
| Category      | Job category (e.g., IT Jobs, Healthcare & Nursing Jobs) |
| Salary        | Annual salary in float format with two decimals |
| OpenDate      | Job posting start date and time (`YYYY-MM-DD HH:MM:SS`) |
| CloseDate     | Job posting end date and time (`YYYY-MM-DD HH:MM:SS`) |


## Key Features
- Handles multi-source job datasets with schema differences.  
- Converts monthly salaries to annual for consistency.  
- Cleans missing values, inconsistent categories, and typographical errors.  
- Produces a clean, deduplicated, and integrated dataset suitable for analysis.



## Usage
1. Clone the repository.  
2. Open the Jupyter notebooks:  
   - `data_parsing_cleansing.ipynb` – Data parsing and cleansing  
   - `data_integration.ipynb` – Data integration  
3. Execute cells sequentially to generate:  
   - `dataset1_solution.csv`  
   - `errorlist.csv`  
   - `dataset_integrated.csv`  



## Notes
- All data transformations and cleaning decisions are documented in the notebooks.  
- The workflow ensures **data consistency, accuracy, and readiness for analysis**.  
- Designed to handle large datasets efficiently using Pandas and vectorized operations.

