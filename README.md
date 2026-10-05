<div align="center">

# 🏎️ Formula 1 Lakehouse — Azure Databricks & Delta Lake

### 70+ years of F1 race data → raw / processed / presentation layers → "who were the most dominant drivers and teams?"

![Azure Databricks](https://img.shields.io/badge/Azure-Databricks-FF3621?style=flat-square&logo=databricks&logoColor=white)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![Spark SQL](https://img.shields.io/badge/Spark_SQL-E25A1C?style=flat-square&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta_Lake-00ADD4?style=flat-square)
![ADLS Gen2](https://img.shields.io/badge/ADLS_Gen2-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Unity Catalog](https://img.shields.io/badge/Unity_Catalog-governance-FF3621?style=flat-square)
![Azure Data Factory](https://img.shields.io/badge/Azure_Data_Factory-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=flat-square&logo=powerbi&logoColor=black)

</div>

---

## 🏗️ Architecture

```
Ergast F1 files (CSV / JSON, single + multi-line, folders)
        │  ADLS Gen2 — raw container
        ▼
 PySpark ingestion notebooks (schema, rename, audit columns)
        │  ──► processed layer (Parquet → Delta)
        ▼
 Spark SQL transformations — race results, driver & constructor standings
        │  ──► presentation layer (Delta)
        ▼
 Analysis SQL + Databricks dashboards / Power BI
        ▲
 Azure Data Factory orchestrates · Unity Catalog governs · incremental loads keep it current
```

## ✨ Highlights

- **8 source datasets** ingested — circuits, races, constructors, drivers, results, pit stops, lap times, qualifying — each in its own notebook, plus a `0.ingest_all_files` runner
- **Reusable config & helpers** (`includes/configuration.py`, `common_functions.py`) shared across notebooks
- **Delta Lake** — ACID tables, merges/upserts, and **incremental loads** for new race weekends
- **Secure storage access** — access keys, SAS tokens, service principals, cluster-scoped credentials and ADLS mounts, with every secret pulled from **Databricks secret scopes**
- **Analysis** — SQL to find the most dominant drivers and teams, with visualisations

## 📁 Repository map (learning progression)

| Folder | Focus |
|---|---|
| `ADLS Access/`, `ADLS Access IAM/` | Connecting Databricks to ADLS Gen2 securely |
| `Demo Setup/` | Mounts, raw tables, end-to-end first pass |
| `Data Ingestion/` | PySpark ingestion of all 8 datasets |
| `PySpark & SQL operations/` | Ingestion refactored around shared configuration & common functions |
| `Reusing the code/` | Transformations — race results, driver standings, constructor standings |
| `Delta Lake format/` | Spark SQL basics and joins demos |
| `Live Data Incremental/` | Incremental (new-race) loads |
| `Data Operations/` | Full pipeline + dominant-driver / dominant-team analysis |

## 🚀 Run it

1. Create an Azure Databricks workspace and an ADLS Gen2 account with `raw`, `processed` and `presentation` containers.
2. Upload the Ergast F1 files to `raw`.
3. Import the folders into your workspace (Workspace → Import), update `includes/configuration.py` with your paths, and configure storage access.
4. Run `ingestion/0.ingest_all_files`, then the analysis notebooks.

---

<div align="center">

**Built by [Sai Satya Jagannadh Doddipatla (DJ)](https://saisatyajagannadh.github.io/PersonalPortfolio/)** · ⭐ Star the repo if it helped

</div>
