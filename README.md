# adscraper_bqt_scheduler
a simple python script to schedule google scrape and insert to bigquery tables

# Google Search Rankings Tracker

This script tracks Google search rankings and shopping results across multiple locations and devices, storing the data in Google BigQuery for analysis. It monitors ad positions and shopping results for specified keywords across various US locations.

## Features

- Tracks multiple keywords with different search intents (main, commercial, informational, and branded)
- Monitors search results across desktop, mobile, and tablet devices
- Covers 18 different US locations and more if your budget allows.
- Captures both advertising and shopping results
- Stores data in Google BigQuery for analysis
- Comprehensive logging system
- Timezone-aware (Eastern Time)

## Prerequisites

- Python 3.x
- Google Cloud account with BigQuery enabled
- SerpAPI account and API key
- Required Python packages:
  ```
  google-cloud-bigquery
  google-oauth2-httplib2
  serpapi
  pytz
  logging
  ```

## Setup

1. Install required packages:
   ```bash
   pip install google-cloud-bigquery google-oauth2-httplib2 serpapi pytz
   ```

2. Configure credentials:
   - Add your Google Cloud service account JSON key file
   - Set up your SerpAPI key
   - Update the credential placeholders in the script:
     ```python
     credentials = service_account.Credentials.from_service_account_file('YOUR_SERVICE_ACCOUNT_FILE')
     client = bigquery.Client(credentials=credentials, project='YOUR_PROJECT_ID')
     ```
     ```python
     params = {
         "api_key": "YOUR_SERPAPI_KEY",
         # ... other parameters
     }
     ```

3. Configure keywords:
   - Update the `keywords` dictionary with your search terms and corresponding table names
   - Each keyword maps to a dataset and table suffix

## Data Structure

### BigQuery Schema
```python
schema = [
    bigquery.SchemaField("timestamp", "TIMESTAMP"),
    bigquery.SchemaField("location", "STRING"),
    bigquery.SchemaField("type", "STRING"),
    bigquery.SchemaField("position", "INTEGER"),
    bigquery.SchemaField("url", "STRING"),
]
```

### Table Naming Convention
- Base tables (desktop): `rankings`, `rankings_s`, `rankings_p`, `rankings_b`
- Mobile suffix: `_m` (e.g., `rankings_m`)
- Tablet suffix: `_t` (e.g., `rankings_t`)

## Usage

1. Update the configuration variables as needed
2. Run the script:
   ```bash
   python search_rankings_tracker.py
   ```

The script will:
1. Initialize logging system
2. Connect to BigQuery
3. Create necessary datasets and tables
4. Fetch and process search results
5. Store results in BigQuery
6. Log all operations

## Logging

The script maintains two log outputs:
- Console output for real-time monitoring
- `log.txt` file for historical tracking

Log entries include:
- Timestamp
- Log level (INFO, WARNING, ERROR)
- Detailed operation messages

## Error Handling

The script includes error handling for:
- API requests
- URL parsing
- Database operations
- Data processing

All errors are logged with stack traces for debugging.

## Geographic Coverage

The script monitors search results across multiple US locations, including:
- Major metropolitan areas
- Multiple states and counties
- Various demographic regions

## Geographic Coverage

Use VPS native task scheduler or preferred task scheduling software
![image](https://github.com/user-attachments/assets/46c9559f-6036-4884-8ccf-5892b64611ce)

## Maintenance

Regular maintenance tasks:
1. Monitor API usage and costs
2. Review log files
3. Verify data integrity
4. Update locations list as needed
5. Rotate API keys as required

## Charting

Use Looker Studio, Metabase or Flask app to display in preferred format. 

## Security Notes

- Keep all API keys and credentials secure
- Do not commit sensitive credentials to version control
- Regularly rotate API keys and service account credentials
- Monitor API usage for unauthorized access

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request
