# MedalForge — Project Progress

Personal Medallion-architecture lab replicating the production paid media
data pipeline pattern used at DataPoem, built with synthetic data only.

Repo: `lca-paid-media-lab`

---

## Status: In Progress

| Phase | Description | Status | Date |
|---|---|---|---|
| 1 | GitHub repository setup | ✅ Complete | 2026-08-19 |
| 2 | AWS EC2 dev server provisioned | ✅ Complete | 2026-08-19 |
| 3 | VS Code Remote-SSH connection to EC2 | ✅ Complete | 2026-08-19 |
| 4 | Branch protection + first feature branch | ⏳ Not started | — |
| 5 | S3 bucket + landing/archive/rejected prefixes | ⏳ Not started | — |
| 6 | Unity Catalog: catalog + schemas (staging/bronze/silver/gold) | ⏳ Not started | — |
| 7 | Staging table (schema from `dataset_config.csv`) | ⏳ Not started | — |
| 8 | Bronze Raw ingestion (append-only, batch metadata) | ⏳ Not started | — |
| 9 | Bronze Standardized (config-driven column mapping) | ⏳ Not started | — |
| 10 | Basic DQ checks on Bronze | ⏳ Not started | — |
| 11 | Databricks Asset Bundle deploy (`validate → deploy → run`) | ⏳ Not started | — |
| 12 | Row-count reconciliation (source vs Bronze) | ⏳ Not started | — |

---

## Phase 1 — GitHub Repository ✅

- Created public repo: `PARESHRANJAN299/lca-paid-media-lab`
- Default branch: `main`
- Purpose: personal, synthetic-data-only Medallion architecture lab
- No real client (Walmart/Unilever/Nielsen) data or column names will ever
  be committed here — synthetic data only, per company confidentiality rules

## Phase 2 — AWS EC2 Dev Server ✅

- Instance name: `lca-paid-media-dev`
- Instance ID: `i-0395a20af1d2821c6`
- Instance type: `t2.micro` (AWS Free Tier eligible)
- AMI: Ubuntu Server 24.04 LTS
- Storage: 20 GiB
- Region: US East (N. Virginia)
- Security group: SSH (port 22) open, key-pair authentication only
  (`lca-dev-key.pem`) — no password login
- Status: Running

**Note:** Instance is stopped when not actively in use to avoid unnecessary
compute cost (stopping does not affect stored data or the attached volume).

## Phase 3 — VS Code Remote-SSH Connection ✅

- SSH config added at `~/.ssh/config` (local Windows machine) with a
  `lca-dev` host entry pointing to the EC2 instance's Public IPv4 address.
- `.pem` private key permissions restricted to the current user only
  (`icacls` — Windows equivalent of `chmod 400`), which resolved an initial
  `Permission denied (publickey)` error.
- Connected successfully via key-based authentication (no password) — VS
  Code Server now runs on the EC2 instance itself.
- **Known limitation:** the EC2 instance does not have an Elastic IP, so its
  Public IPv4 address changes every time the instance is stopped and
  restarted. The `HostName` in `~/.ssh/config` must be manually updated to
  the new IP after every restart. Elastic IP was deliberately not used to
  avoid its idle-attachment cost.

---

## Architecture Reference

This project follows three independent flows, kept deliberately separate:

```
Software flow:  VS Code -> Git branch -> GitHub -> Databricks bundle deploy
Platform flow:  EC2 dev server -> Databricks workspace -> compute/job
Data flow:      S3 -> Staging -> Bronze -> Silver -> Gold/AIO
```

Full details in `architecture.md`.

---

## Next Step (Phase 3)

Install the Remote-SSH extension in VS Code, connect to the EC2 instance at
its public IP using the `lca-dev-key.pem` key pair, and clone this repository
directly on the EC2 server (not locally) — matching a real company development
setup.
