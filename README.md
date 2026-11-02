# MetricLens 📊

**Turn Data into Insights with MetricLens.**

MetricLens is an interactive data analytics workspace built with **Python, Streamlit, Pandas, Plotly, and SQLite**. It helps users upload spreadsheet data, inspect data quality, explore visual patterns, run SQL queries, and export a cleaned dataset for Tableau.

## Features

- **CSV and Excel upload** — supports `.csv`, `.xlsx`, and `.xls` files.
- **Dataset overview** — view total records, columns, missing cells, and duplicate rows.
- **Data quality profiling** — inspect detected data types, missing values, and unique values.
- **Cleaning options** — optionally remove duplicate rows and fill numeric missing values with the median. The original uploaded file is not overwritten.
- **Interactive visualizations** — explore numeric distributions, category comparisons, time trends (when date fields are detected), and category breakdowns.
- **SQL Query Lab** — run read-only `SELECT` queries against the uploaded data using SQLite.
- **Tableau export** — download a Tableau-ready CSV and Excel analysis report.
- **Optional local SQLite save** — save the cleaned data and column profile locally.

## Tech Stack

- Python
- Streamlit
- Pandas
- Plotly Express
- SQLite
- Tableau Public / Tableau Desktop (for downstream visualization)

## Project Structure

```text
MetricLens/
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
├── sample_sales.csv
└── tableau/
    └── TABLEAU_GUIDE.md
```

## Run Locally (Windows)

1. **Clone the repository**
   ```powershell
   git clone https://github.com/YOUR-USERNAME/MetricLens.git
   cd MetricLens
   ```

2. **Create a virtual environment**
   ```powershell
   py -m venv .venv
   ```

3. **Activate it**
   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

   If PowerShell blocks activation, use Command Prompt and run:
   ```bat
   .venv\Scripts\activate.bat
   ```

4. **Install dependencies**
   ```powershell
   python -m pip install -r requirements.txt
   ```

5. **Start MetricLens**
   ```powershell
   python -m streamlit run app.py
   ```

6. Open the local URL shown in the terminal, usually:
   `http://localhost:8501`

## Run on macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

## Using MetricLens

1. Open the app in your browser.
2. Upload a CSV or Excel file, or download the included sample CSV.
3. Review the dataset snapshot and column quality profile.
4. Choose whether to remove duplicate rows or fill numeric missing values with the median.
5. Explore the generated charts and category summaries.
6. Open **SQL Query Lab** and run a `SELECT` query.
7. Download the **Tableau-ready CSV** or Excel analysis report.

### Example SQL Queries

The uploaded dataset is exposed as the SQLite table `uploaded_data`.

```sql
-- Preview records
SELECT * FROM uploaded_data LIMIT 10;

-- Count records
SELECT COUNT(*) AS total_records
FROM uploaded_data;

-- Count records by category (replace Company with a column in your file)
SELECT Company, COUNT(*) AS total_records
FROM uploaded_data
GROUP BY Company
ORDER BY total_records DESC
LIMIT 10;
```

Only `SELECT` statements are accepted by the SQL interface.

## Connect the Export to Tableau

1. In MetricLens, click **Tableau-ready CSV** in the Export Center.
2. Open Tableau Public or Tableau Desktop.
3. Choose **Connect → Text File** and select `cleaned_tableau_data.csv`.
4. Create worksheets and charts using the exported fields.
5. Choose **Dashboard → New Dashboard** and arrange the worksheets.
6. Add filters and titles to complete your dashboard.

See [`tableau/TABLEAU_GUIDE.md`](tableau/TABLEAU_GUIDE.md) for a short guide.

> **Note:** MetricLens exports a Tableau-ready file. The Streamlit app and Tableau workbook are separate; the export does not automatically live-sync changes into Tableau.

## Data Privacy

- Uploaded files are processed by the app while it is running.
- The optional SQLite save writes a local database under `database/`.
- Do not commit private, personal, financial, or confidential datasets to a public GitHub repository.
- Tableau Public workbooks are public. Do not publish confidential data there.

## Future Improvements

- More configurable chart types and filters
- Advanced data cleaning controls
- Exportable chart images and PDF reports
- Database connectors for larger datasets
- Automated dashboard recommendations

## License

No license has been added. Unless you choose a license, the project remains under the default copyright terms.
