# Real-Time-Organizational-Data-Streaming-Pipeline 🚀

This project showcases a real-time streaming pipeline on Azure. Data is fetched from Microsoft Graph APIs via Azure Function Apps, transformed into structured events, and streamed to Azure Event Hubs. Azure Stream Analytics processes this data, joins it with static sources, and outputs results to Power BI dashboards and ADLS Gen2 for storage.


> ⚠️ *Due to confidentiality agreements, API endpoints and authentication details have been abstracted or generalized.*

---

## 📚 Use Case

The system was designed to provide **live organizational insights** by continuously retrieving, transforming, and visualizing data sourced from Microsoft Graph APIs. Aimed at enabling real-time monitoring and reporting in Power BI, this solution is scalable, secure, and modular.

---

## 🧱 Architecture Overview

**Components Used**:
- **Microsoft Graph API** – Source of real-time organizational data
- **Azure Active Directory Enterprise App** – Handles API authentication via delegated permissions
- **Azure Function Apps** – Periodic invokers to fetch, filter, and transform JSON data
- **Azure Event Hubs** – Message ingestion layer for downstream streaming
- **Azure Stream Analytics** – Stream processing, transformation, joining with static sources
- **Azure SQL DB / Excel (Blob Storage)** – Static reference data (for joins)
- **Azure Data Lake Storage Gen2 (ADLS Gen2)** – Long-term structured storage in YYYY/MM/DD folder hierarchy
- **Power BI (Push Dataset)** – Real-time dashboards for business insights
- **Virtual Network (VNet)** – All components except Power BI are hosted within a private VNet

---

## 🗺️ Data Flow

1. Azure Function App fetches and cleanses JSON data from Graph API.
2. Events are batched and sent to Azure Event Hubs.
3. Azure Stream Analytics:
   - Filters and joins event data with static sources.
   - Outputs real-time data to:
     - **Power BI Push Dataset** (for dashboards)
     - **ADLS Gen2** in hierarchical folders by day, month, year.

---

## 🏗️ Folder Structure

```bash
real-time-streaming-pipeline/
├── README.md
├── requirements.txt
├── notebooks/
│   ├── stream_ingest.py            # Databricks-based (optional for future ingestion)
│   └── stream_transform.py
├── function-app/
│   └── main_function.py            # Azure Function App script (sample)
├── diagrams/
│   ├── architecture_diagram.png
│   └── medallion_layers.png
├── configs/
│   └── eventhub_connection.json    # Placeholder config
└── data-samples/
    └── data_structure.md
```

---

## 💡 Sample Storage Format (ADLS Gen2)

```bash
/adls/graph-data/
├── year=2025/
│   ├── month=05/
│   │   ├── day=01/
│   │   │   └── data.json
│   │   ├── day=02/
│   │   │   └── data.json
```

---

## 🧰 Requirements

See `requirements.txt` for Python dependencies. Azure Function App is written in Python 3.11 using `requests`, `azure-identity`, and `json`.

---

## 🔐 Security

All communication is secured through:
- Azure Managed Identities
- Enterprise App Permissions
- VNet Integration
- Event Hub and Function IP restrictions (where applicable)

---

## 📊 Dashboarding

Power BI consumes data from push datasets and renders:
- Live visualizations
- KPI metrics from streamed Graph API data

---

## ✅ Status

- ✅ Architecture and deployment tested in production
- ✅ Secure and scalable for enterprise use
- 🚫 Sample does not include confidential API endpoints or secrets

---

## 📄 License

This repository is open for educational and portfolio purposes only. Any misuse of API credentials or attempts to reverse engineer internal enterprise workflows is prohibited.
