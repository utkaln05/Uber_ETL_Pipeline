# Uber Data Analytics | Modern Data Engineering GCP Project

## Introduction

The goal of this project is to perform data analytics on Uber data using various tools and technologies, including GCP Storage, Python, Compute Instance, Mage Data Pipeline Tool, BigQuery, and Looker Studio.

## Architecture
<img src="architecture.jpg">

## Technology Used

- Programming Language - Python

Google Cloud Platform
1. Google Storage
2. Compute Instance
3. BigQuery
4. Looker Studio

Modern Data Pipeine Tool - https://www.mage.ai/

Contibute to this open source project - https://github.com/mage-ai/mage-ai

## Dataset Used

TLC Trip Record Data
Yellow and green taxi trip records include fields capturing pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized fares, rate types, payment types, and driver-reported passenger counts.

Here is the dataset used in the video - https://github.com/darshilparmar/uber-etl-pipeline-data-engineering-project/blob/main/data/uber_data.csv

More info about dataset can be found here:
1. Website - https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
2. Data Dictionary - https://www.nyc.gov/assets/tlc/downloads/pdf/data_dictionary_trip_records_yellow.pdf

<img src="data_model.jpeg">


## Quickstart

1. Clone the repository
   ```bash
   git clone https://github.com/<your-username>/uber-etl-pipeline-data-engineering-project.git
   cd uber-etl-pipeline-data-engineering-project
   ```

5. Run the pipeline
   - The ETL blocks live in `mage-files/` as standard Python functions.
   - You can run the example flow (extract → transform → load) using Python or inside a Mage project.

### Run ETL with Python

  Note: The folder name `mage-files/` contains a hyphen, so it cannot be imported as a normal Python module. Either run inside a Mage project, or rename the folder locally to `mage_files/` for direct imports.

  The blocks are split into `extract.py`, `transform.py`, and `load.py`.

  ```python
  # Pseudocode for the flow (illustrative only):
  # 1) df = extract.load_data_from_api()
  # 2) data_dict = transform.transform(df)
  # 3) load.export_data_to_big_query(data_dict)
  ```

  Note: `export_data_to_big_query()` requires a valid `io_config.yaml` and GCP permissions.

## Project Structure
- `mage-files/transform.py` — Builds dimensions and fact table from the raw DataFrame.
- `mage-files/load.py` — Exports transformed tables to BigQuery using `mage-ai` IO connectors.
- `analytics_query.sql` — Example analytical queries to run in BigQuery.
- `data/` — Directory reserved for small, sample datasets (ignored by git by default).
- `io_config.yaml.example` — Template for local BigQuery credentials/config.
- `requirements.txt` — Python dependencies.
- `.gitignore` — Excludes caches, virtualenvs, secrets, and large data.
- `LICENSE` — MIT License.

## Features

- **[Extract]** Pulls Uber sample data CSV from a public URL using `requests`.
- **[Transform]** Builds dimension tables and a fact table using `pandas`.
- **[Load]** Exports to Google BigQuery via `mage-ai` IO connectors.
- **[Analytics]** Includes example SQL in `analytics_query.sql`.

## Prerequisites

- Python 3.9+
- A Google Cloud project with BigQuery enabled
- A service account with BigQuery permissions and a JSON key file

## Setup

```bash
python -m venv .venv
# Windows
. .venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install -r requirements.txt
```

## Configuration

1. Copy `io_config.yaml.example` to `io_config.yaml`.
2. Fill in:
   - `GOOGLE_PROJECT_ID`
   - `GOOGLE_BIGQUERY_DATASET`
   - `GOOGLE_SERVICE_ACC_KEY_FILEPATH` (path to your JSON key)
3. Keep `io_config.yaml` and keys out of git (already covered by `.gitignore`).

## Run with Mage (recommended)

This repository contains Mage-compatible blocks in `mage-files/`. If you are using the Mage orchestrator, create a pipeline and reference these blocks.

## Run locally without Mage

The folder `mage-files/` contains a hyphen and cannot be imported as a module. For direct imports, rename locally to `mage_files/` or execute the files as scripts while managing the PYTHONPATH accordingly. See the pseudocode in the Quickstart section.

## Troubleshooting

- "Permission denied" or auth errors when loading to BigQuery: verify the service account has `BigQuery Data Editor` and `BigQuery Job User` roles.
- Import errors: ensure your virtual environment is activated and dependencies installed.
- BigQuery location errors: set `GOOGLE_LOCATION` in `io_config.yaml` to match your dataset region.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License. See `LICENSE` for details.
