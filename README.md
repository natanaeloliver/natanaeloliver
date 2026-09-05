# Natanael da Rosa Travi de Oliveira

Analytics / Data Engineer

I work on the modeled layer of a healthcare payer's data platform, and on everything that has to happen before a model can exist. I pull the data out of ERPs, APIs and event reports like Mosia through RPA, and the entire data stream of a hospital, from the claim (guia de atendimento) to the exam result, in MV. Then I structure the transformations on top, and run the Kubernetes and orchestration underneath.

## Currently

- Building the modeled layer in BigQuery and dbt, with declarative tests and column-level documentation, on top of a GCP platform I helped migrate from an empty environment. Once every KPI had one definition living there, the tickets asking what a number meant fell 80%, around $28K a year that used to go into answering them
- Running the orchestration and the infrastructure under it, from Airflow DAGs to node pools, Helm-versioned pod configuration promoted from dev to production, and Terraform for the infrastructure and the IAM, where I am reworking access for the cloud migration so that roles are simpler and cover buckets as well as datasets
- Building and publishing the Airflow and dbt images in CI, tagged in Artifact Registry, with every model run and tested against a dev dataset before it reaches production
- Making extraction from an Oracle ERP incremental and parallel, and keeping the data quality rules that decide whether a number is publishable
- Keeping all of it running, with two years of production support across the legacy Qlik stack and the current cloud one, where the failures that repeat are source schema changes that break extraction downstream, cloud-to-on-premise access, and network permissions lost to a tool upgrade. Fixing them at the root instead of one ticket at a time gave back 72% of what support used to take, over $65K a year, and that time went into projects. I do not own the monitoring stack, so my part of it is specifying what to detect and how, like the alert for a staging environment that cloned a database and broke DNS resolution
- Building [claude-worklog](https://github.com/natanaeloliver/claude-worklog), an open-source session context hub for Claude Code, so that multi-repo teams can run parallel sessions and always know what happened in which repository without reading every commit. The team has it running every day, and about a quarter of what alignment, definitions and old mistakes used to cost came back, about $25K a year

## Selected work

**Preventive care patient classification & outreach system** *(confidential, private)*

Built the full data flow for a health plan covering 100,000+ beneficiaries. Extraction and batch mapping from [TOTVS Protheus](https://www.totvs.com/sistema-de-gestao/totvs-backoffice-linha-protheus/), [MV Saúde](https://mv.com.br/) and [MK DATA](https://mkdata.com.br/) into BigQuery tables on utilization, contact and pending exams. The three systems do talk to each other, but not on a 1:1, 1:N or N:N relationship, so each field had to be validated in each database before the diagnosis codes would line up across appointments, schedules, clinical documents and execution claims. The classification took the place of a program the payer used to pay for, over $100K a year of fixed cost that left the budget, and reaching the right member first took 20% off what the outreach messages cost.

**Oracle extraction redesign** *(confidential, private)*

Found `ORA_ROWSCN` and rebuilt extraction around it. The change number is per Oracle block rather than per row, and the database does not have `ROWDEPENDENCIES` enabled, which my team has no permission to change, so the design takes the approximate watermark and clears the duplicates downstream, in dbt and in a scheduled dedup job. Loads are bucketed by `R_E_C_N_O_`, `ID` or whatever the table's primary key is, so a single table is pulled in parallel. Paired with infrastructure work on node pool sizing, a dedicated node for DAG task execution, autoscaling, and the connection load on the Airflow metadata database. The full run came out more than 3x faster, and the bill barely moved, because a bigger machine that finishes early costs about what a small one left up all day did. The infrastructure failures stopped. I am now driving the controlled test to enable `ROWDEPENDENCIES` on one of the largest tables with the infrastructure team, comparing both extractions side by side before the dedup window is widened.

**Third-party platform integration ([Mosia](https://mobilesaudejira.atlassian.net/wiki/spaces/MO/pages/3117252616/))** *(confidential, private)*

Pulled data out of a healthcare service platform that had no available API, where the occurrence report is not a table: one file mixes header, creation, state change, closure and survey rows under each protocol, in chronological order, behind a one-time download link. I mapped the application iframes, drove the session through Java variables in AutomationEdge, minted GCP service-account tokens from Python via PowerShell, and landed segmented CSV into BigQuery for dbt to finish inside an Airflow DAG. Once the manager could see a whole protocol without opening the platform, the call center got 50% more out of the same shift, over $20K a year of capacity.

**Cost, from the query to the cloud bill** *(confidential, private)*

Built a cost analytics layer over the platform to find which queries were driving the BigQuery spend, which the bill alone does not tell you. Later broke the GCP bill down by SKU across all services and priced the same environment on Oracle Cloud item by item, then rebuilt the heaviest of our data flows there and ran it on both sides, from the first transformation to the final table, to see what the move would cost in money, elapsed time and processing, and whether the shape of the output would break what the BI layer already showed. The finding that changed policy was that 99.55% of the storage line was cross-region transfer rather than storage; and once that transfer stopped the line all but disappeared, around $5K a year. Designed and documented the Oracle Cloud network for that environment, with public and private subnets, per-subnet route tables and security lists, internet, NAT and service gateways, and a two-tunnel site-to-site VPN back to the on-premise firewall.

**Business rules of a payer warehouse** *(confidential, private)*

Write and continuously audit the business rules the reporting layer runs on: the chart of accounts, how an active membership is counted, how a loss ratio is composed, and the per-item cost of a member's procedure across authorization, execution, accounted and billed claims, down to item, procedure, member, subcontract and contracting company. That means knowing what counts, from which date, and what silently changes the number when a source system changes, even without extraction errors. One rule with one definition, kept in one place, is what stopped the same indicator from being rebuilt in each of the other views, around $17K a year.

**Enablement** *(confidential, private)*

I ran the training that got the department querying BigQuery on its own, at a time when nobody had a reason to trust an empty platform. Their query spend fell 60% once they were writing it themselves, around $6K a year. The two-day AI workshop I attended in May 2026 came back to the data team as a two-hour session I ran in June. Documentation and process are part of how I learn and how I work, and that is where the tool below came from. I built it for my own team to solve a documentation and alignment problem, but it worked well enough that I reworked it into an open-source version.

**[claude-worklog](https://github.com/natanaeloliver/claude-worklog)**

Session context hub for Claude Code. Hooks auto-inject task context and log sessions across multiple repos, so context survives session resets and stays current, and anyone joining the work can pick up their part without asking around, which is what makes parallel sessions practical.

## Tech stack

| Data & Cloud | Databases | Languages & tools |
|---|---|---|
| BigQuery, dbt, Airflow, GCP, ClickHouse, Oracle ERP, Terraform, Kubernetes, Helm, Docker | PostgreSQL, MariaDB, Oracle | Python, SQL, PowerShell (Windows), Bash (Linux), RPA (AutomationEdge), Qlik, Power BI, Metabase |

![Top Langs](./profile/top-langs.svg)

## Contact

[LinkedIn](https://www.linkedin.com/in/natanael-da-rosa-travi-de-oliveira-12460357/) · natanael.oliveira.rosa@gmail.com
