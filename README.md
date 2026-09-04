# sales-etl-excel-to-sqlite
Python Project: Sales ETL — Excel to SQLite
This project automates a small ETL (Extract, Transform, Load) pipeline that reads a raw sales export from Excel, calculates order-level revenue, cleans the dataset, and loads the result into a SQLite database — as part of a data analyst portfolio.

Business Question
How can a recurring sales report (Excel export) be turned into a repeatable, automated pipeline that produces a clean, query-ready database without manual copy-pasting each time new data arrives?

Additional questions:

How is total order revenue calculated once discounts are applied?
Which columns are actually needed for downstream analysis, and which can be dropped?
How can the whole process be packaged into a single reusable function?
How can the pipeline run automatically on a daily schedule, without manual intervention?
Tools
Python
pandas
sqlite3
schedule
Google Colab
GitHub
Project Structure
sales-etl-excel-to-sqlite/
│
├── data/
│   └── sales.xlsx
├── database/
│   └── sales.db
├── notebooks/
│   └── etl_prodject.ipynb
└── README.md
Notebook
The project was created in Google Colab, reading the source file directly from a connected Google Drive. The notebook contains the full ETL workflow: data loading and validation, revenue calculation, column filtering and cleaning, SQLite table creation and loading, and a scheduled daily run.

Open in Google Colab

ETL Steps
Read the raw sales export (sales.xlsx) with pandas.read_excel() and validated that all required source columns are present
Calculated total_sum = quantity * price_per_unit * (1 - discount) for every order
Filtered the dataset down to the columns needed downstream: order_id, product, quantity, total_sum, date
Checked for and removed rows with missing values
Mapped pandas dtypes to SQLite column types and created the sales table
Loaded the cleaned data into sales.db, replacing the table on each run so it always reflects the latest export
Wrapped the entire workflow into a single reusable function, process_sales_to_sqlite(), with a scheduled daily run at 09:00 via the schedule library
Result
Running the pipeline on the sample export produced:

30 orders loaded into the sales table, covering 5 distinct products
Total revenue: 57 225 across all orders; average order value: 1 907.5
Top product by revenue: Футболка (9 orders, 22 150), followed by Джинси (9 orders, 16 335)
The resulting sales.db is a flat, query-ready table — no manual cleanup needed before further analysis in SQL, Python, or a BI tool.

Data Privacy Note
The dataset used in this repository is synthetic and prepared for learning purposes. It does not contain real sales or customer data.

How to Use This Repository
Open the notebook in Google Colab.
Upload sales.xlsx or connect your Google Drive and update the file path.
Run the notebook cells in order, or call process_sales_to_sqlite() directly.
Inspect the resulting sales.db with any SQLite client, or query it with pandas.read_sql_query().
To enable the daily 09:00 run, keep the notebook's scheduler loop running (schedule.run_pending() in a loop), or adapt process_sales_to_sqlite() into a standalone script triggered by a system scheduler (e.g. cron).
Portfolio Value
This project demonstrates:

Python data pipeline basics (ETL)
Working with Excel and SQLite from Python
Data validation and cleaning
Writing reusable, parameterized functions
Task scheduling and automation
Ability to package a data process as a portfolio-ready, reproducible project
