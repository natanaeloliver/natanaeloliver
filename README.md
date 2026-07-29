# Natanael Travi de Oliveira

Platform Engineer | Systems Integration & Cloud Data Infrastructure

I work on the seam between systems that were never designed to talk to each other. Cloud data pipelines, the Kubernetes infrastructure under them, and the business rules they end up carrying.

## Currently

- Running a cloud data platform end to end, from GCP and BigQuery through dbt, Airflow and Terraform, including the Kubernetes cluster it lives on (node pools, pods, scaling)
- Integrating sources that were never meant to be integrated, including Oracle ERP extraction and RPA
- Applying forecasting (SARIMAX), classification and NLP where they solve a real operational problem
- Building [claude-worklog](https://github.com/natanaeloliver/claude-worklog), an open-source session context hub for Claude Code

## Selected work

**Preventive care patient classification & outreach system** *(confidential, private)*

Built the full data flow for a health plan covering 100,000+ beneficiaries. Extraction and batch mapping from TOTVS Protheus, MV Saúde and MK DATA, unified into BigQuery tables on utilization, contact and pending exams/consultations. Powers patient classification for comorbidities and personalized preventive outreach.

**Oracle extraction redesign** *(confidential, private)*

Found `ORA_ROWSCN` and rebuilt extraction around it. Incremental loads keyed on the change number, bucketed by `R_E_C_N_O_` so a single table is pulled in parallel instead of serially. Paired with infrastructure work on node pool sizing, a dedicated node for DAG task execution, autoscaling, and the connection load on the Airflow metadata database. The full run came out more than 3x faster and the infrastructure failures stopped.

**Third-party platform integration** *(confidential, private)*

Pulled data out of a healthcare platform that had no available API. Mapped the application iframes, drove the session through Java variables in AutomationEdge, minted GCP service-account tokens from Python via PowerShell, and landed segmented CSV into BigQuery for dbt to finish inside an Airflow DAG.

**[claude-worklog](https://github.com/natanaeloliver/claude-worklog)**

Session context hub for Claude Code. Hooks auto-inject task context and log sessions across multiple repos, so context survives session resets.

## Tech stack

| Data & Cloud | Databases | Backend | Tools |
|---|---|---|---|
| GCP, BigQuery, ClickHouse, dbt, Airflow, Oracle ERP, Terraform, Kubernetes, Docker | PostgreSQL, MariaDB, Oracle, Redis | Python, FastAPI, SQLAlchemy | SQL, PowerShell, Bash, RPA (AutomationEdge), Power BI |

![Top Langs](./profile/top-langs.svg)

## Contact

[LinkedIn](https://www.linkedin.com/in/natanael-travi-de-oliveira-12460357/) · natanael.oliveira.rosa@gmail.com
