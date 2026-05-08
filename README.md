# Databricks SQL Core Framework

A metadata-driven data engineering framework built on Azure Databricks and Databricks SQL Warehouses.

This repository provides a standardized approach for building, deploying, and operating scalable ingestion and transformation pipelines using:

- Databricks Asset Bundles (DAB)
- Databricks SQL Stored Procedures
- Metadata-driven architecture
- CI/CD with Azure DevOps
- YAML and JSON configuration patterns
- Unity Catalog compatible governance

The framework was designed to simplify and standardize development for Data Engineers and Data Scientists working on Databricks.

---

# Architecture Overview

The project follows a metadata-driven architecture where ingestion and transformation logic are dynamically controlled by configuration tables and JSON/YAML definitions.

Instead of creating hardcoded pipelines for every dataset, the framework allows developers to:

- Register datasets through metadata
- Standardize ingestion behavior
- Reuse SQL procedures
- Automate schema management
- Simplify onboarding of new sources
- Centralize governance and operational controls

## Main Goals

- Reduce duplicated pipeline logic
- Improve maintainability
- Centralize dataset configuration
- Enable scalable onboarding of new systems
- Standardize Bronze and Silver processing
- Improve governance and observability
- Support CI/CD and Infrastructure as Code practices

---

# Repository Structure

```text
.
├── azure_pipelines/             # Azure DevOps CI/CD pipelines
├── control_configs/            # Metadata and deployment configuration files
├── fixtures/                   # Test fixtures
├── resources/                  # Databricks job resources
├── scratch/                    # Temporary or experimental assets
├── src/
│   ├── functions/              # Shared Spark SQL utility functions
│   └── procs/                  # SQL procedures and orchestration notebooks
├── tests/                      # Automated tests
├── databricks.yml              # Databricks Asset Bundle configuration
└── README.md
```

---

# Core Components

## 1. Metadata-Driven Configuration

The framework uses configuration metadata to dynamically control ingestion and transformation behavior.

Examples of metadata include:

- Project name
- Source system
- Catalog and schema
- Table names
- Load strategy
- Incremental columns
- Business keys
- Write mode
- Schema definitions

This metadata is centralized in Databricks control tables.

## 2. Control Tables

The framework creates standardized control tables inside Databricks.

These tables act as the identity layer of the platform and provide visibility into:

- Which datasets exist
- Which systems are integrated
- Pipeline configurations
- Processing state
- Schema definitions
- Incremental ingestion state

Benefits:

- Better governance
- Easier troubleshooting
- Simplified onboarding
- Operational transparency

## 3. SQL Procedures

The framework includes reusable Databricks SQL procedures for:

### `proc_load_config`

Loads and validates metadata configurations.

### `proc_prepare_target`

Creates or evolves target tables dynamically.

### `proc_schema_check`

Performs schema validation and compatibility checks.

### `proc_run_bronze_scd1`

Processes Bronze ingestion using standardized logic.

### `proc_silver_scd1`

Executes Silver layer merge and SCD Type 1 processing.

## 4. Utility Functions

Shared SQL utility functions are available inside:

```text
src/functions/
```

These functions centralize reusable Spark SQL logic.

---

# Databricks Asset Bundles (DAB)

The project uses Databricks Asset Bundles for deployment and environment management.

Main configuration file:

```text
/databricks.yml
```

Supported environments typically include:

- dev
- hmg
- prod

Benefits:

- Infrastructure as Code
- Reproducible deployments
- Environment standardization
- Easier CI/CD integration

---

# CI/CD

Azure DevOps pipelines are located under:

```text
azure_pipelines/
```

Pipelines included:

| Pipeline          | Description                   |
| ----------------- | ----------------------------- |
| `code_review.yml` | Validation and quality checks |
| `hmg.yml`         | Homologation deployment       |
| `release.yml`     | Production deployment         |

The framework supports automated deployment and testing workflows.

---

# Development Workflow

## Local Development

Requirements:

- Databricks CLI
- Python
- VS Code or Cursor
- Databricks Extension

Authenticate:

```bash
databricks configure
```

Deploy bundle:

```bash
databricks bundle deploy --target dev
```

Run bundle:

```bash
databricks bundle run
```

Run tests:

```bash
pytest
```

---

# Metadata Standardization Strategy

One of the major goals of this project was refactoring an older framework that used:

- JSON files stored directly in Storage Accounts
- Duplicated metadata
- Non-standard configurations
- Poor governance
- No version control
- Difficult maintenance

The new approach introduced:

- Version-controlled metadata
- Git-integrated configuration management
- YAML and JSON standardization
- Databricks control tables
- Reusable deployment patterns
- Cleaner metadata model

This significantly improved:

- Developer experience
- Governance
- Traceability
- Pipeline scalability
- Team collaboration

---

# Bronze and Silver Processing

## Bronze Layer

Responsibilities:

- Raw ingestion
- Source fidelity preservation
- Incremental capture
- Basic standardization

Typical characteristics:

- Append strategy
- Metadata enrichment
- Audit columns
- Minimal transformations

## Silver Layer

Responsibilities:

- Data cleansing
- Deduplication
- Business logic
- Merge operations
- SCD Type 1 handling

Typical characteristics:

- MERGE operations
- Business key matching
- Latest record selection
- Schema validation

---

# Testing

Tests are located under:

```text
/tests
```

The framework supports automated validation for:

- SQL procedures
- Metadata behavior
- Deployment logic
- Configuration consistency

---

# Key Benefits

## For Data Engineers

- Faster onboarding of datasets
- Reusable pipeline patterns
- Less repetitive code
- Easier maintenance
- Standardized architecture

## For Data Scientists

- Faster access to curated datasets
- Standardized data structures
- Improved discoverability
- Better governance

## For Platform Teams

- Centralized metadata management
- Better operational visibility
- Easier scaling
- CI/CD support
- Improved governance

---

# Technologies Used

- Azure Databricks
- Databricks SQL
- Spark SQL
- Unity Catalog
- Databricks Asset Bundles
- Azure DevOps
- YAML
- JSON
- Python
- Pytest

---

# Future Improvements

Potential roadmap items:

- Automated data quality rules
- PII tagging automation
- Dynamic schema inference
- CDC enhancements
- Monitoring and observability dashboards
- Automated lineage integration
- OpenMetadata or Unity Catalog integration

---

# Getting Started

## 1. Clone Repository

```bash
git clone <repository-url>
```

## 2. Configure Databricks CLI

```bash
databricks configure
```

## 3. Deploy Environment

```bash
databricks bundle deploy --target dev
```

## 4. Execute Procedures

Deploy and execute SQL procedures inside Databricks SQL Warehouse or Jobs.

---

# License

Internal project repository.

---

# Contributors

Built for enterprise-scale metadata-driven data engineering using Azure Databricks.

