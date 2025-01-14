# Retail Orders Data Processing and SQL Loading

This repository contains a Python script to process a retail orders dataset. The script performs data extraction, transformation, and loading (ETL) tasks, preparing the data for analysis by loading it into a SQL Server database.

---

## Features

1. **Download Data from Kaggle**  
   - The dataset is downloaded using the Kaggle API (`orders.csv`).

2. **Extract Data from ZIP**  
   - The downloaded file is extracted from a ZIP archive.

3. **Data Cleaning and Handling**  
   - Handles missing values, marking specific placeholders (e.g., `Not Available` and `unknown`) as `NaN`.

4. **Data Transformation**  
   - Renames columns to lowercase and replaces spaces with underscores.
   - Derives a new column `profit` from existing columns.
   - Converts the `order_date` column to a `datetime` format.
   - Drops unnecessary columns like `list_price`, `cost_price`, and `discount_percent`.

5. **Data Loading**  
   - Loads the processed data into a SQL Server database using the SQLAlchemy library.
   - Supports both `replace` and `append` options for database table updates.

---

## Installation

### Prerequisites
- Python 3.x
- SQL Server with a configured instance
- Kaggle API credentials (`kaggle.json` file)

### Libraries
Install the required libraries:
```bash
pip install kaggle pandas sqlalchemy pyodbc
```

---

## Usage

### 1. Set Up Kaggle API
1. Download your `kaggle.json` file from your Kaggle account.
2. Place the file in the appropriate directory:
   - `~/.kaggle/` on Linux/macOS
   - `C:\Users\<YourUsername>\.kaggle\` on Windows

### 2. Run the Script
Execute the script step by step:
1. Download the dataset:
   ```python
   !kaggle datasets download ankitbansal06/retail-orders -f orders.csv
   ```
2. Extract the dataset:
   ```python
   zip_ref = zipfile.ZipFile('orders.csv.zip') 
   zip_ref.extractall()
   zip_ref.close()
   ```
3. Process and clean the data:
   - Handle missing values
   - Rename columns
   - Derive new fields
4. Load the data into SQL Server:
   ```python
   engine = sal.create_engine('mssql://<server>/<database>?driver=ODBC+DRIVER+17+FOR+SQL+SERVER')
   df.to_sql('df_orders', con=conn, index=False, if_exists='append')
   ```

---

## Outputs
1. Processed dataset ready for analysis.
2. Data loaded into SQL Server for advanced querying.
