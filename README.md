# lca-paid-media-lab

Personal Medallion architecture lab — synthetic paid media pipeline on
Databricks + S3.

📄 **[Architecture & Mission](ARCHITECTURE.md)** — the three flows (software,
platform, data) and why this project exists.

📊 **[Project Progress](PROJECT_PROGRESS.md)** — phase-by-phase build status.

---

## Quick Overview

```
Software flow:  VS Code (EC2) -> Git branch -> GitHub -> Databricks bundle deploy
Platform flow:  EC2 dev server -> Databricks workspace -> compute/job
Data flow:      S3 -> Staging -> Bronze -> Silver -> Gold/AIO
```

No real client (Walmart / Unilever / Nielsen) data, column names, or logic is
ever committed to this repository — synthetic data only.

See [ARCHITECTURE.md](ARCHITECTURE.md) for full details and diagrams.
