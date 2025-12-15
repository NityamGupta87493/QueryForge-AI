# QueryForge-AI

An AI-powered SQL assistant that converts natural-language questions into SQL queries using database schemas, contextual examples, and large language models.

## Overview

QueryForge-AI helps users explore structured data by asking questions in plain English. It combines retrieval-augmented generation (RAG), in-context learning, and schema linking to guide SQL generation.

The project provides an interactive UI, a Python client, and a command-line interface.

## Features

- **Natural Language to SQL:** Generate SQL queries from plain-English questions.
- **Schema Generation:** Generate schema configuration from input data.
- **RAG and In-Context Learning:** Use relevant schema information and example question–SQL pairs to guide generation.
- **Schema Linking:** Map business terminology to database tables and columns. Currently available through the CLI.
- **SQL Checks:** Check generated queries for potentially unsafe patterns. Use appropriate database permissions alongside these checks.
- **Self-Correction:** Validate and correct generated SQL syntax using supported OpenAI GPT models.
- **Query History:** Save question–answer pairs for future reference.
- **Interactive Debugging:** Inspect, modify, and validate generated SQL through the UI.
- **Question Recommendations:** Suggest questions based on the configured dataset.
- **Database Integrations:** SQLite and Databricks, with experimental PostgreSQL support.

## Requirements

- Python `>=3.8.1, <=3.10.0`
- Git
- Poetry
- Credentials for your selected model provider, when required
- Database credentials when connecting to a remote database

Check your Python version:

```bash
python --version
```

## Installation

Clone the repository:

```bash
git clone https://github.com/NityamGupta87493/QueryForge-AI.git
cd QueryForge-AI
```

### Windows — PowerShell

Create and activate a virtual environment:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```powershell
python -m pip install poetry
poetry install
```

### Linux / macOS

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install poetry
poetry install
```

Configure the model credentials and database settings required by your selected integration before generating queries.

Do not commit API keys, passwords, or environment files.

## CLI Usage

Show available commands:

```bash
queryforge-ai --help
```

### Generate a Schema

```bash
queryforge-ai configure generate_schema --data_path "./sample_passenger_statisfaction.csv" --output_path "./table_config.jsonl"
```

### Configure a Local Database

```bash
queryforge-ai configure db-setup -t "./examples/telemetry/table_info.jsonl"
```

### Ask a Question

```bash
queryforge-ai query -q "What is the average number of GPUs?" -s "./examples/telemetry/samples.csv"
```

Replace example paths and questions with values appropriate to your dataset.

### Add Example Question–SQL Pairs

```bash
queryforge-ai learn add-samples
```

### Add Business Context

```bash
queryforge-ai learn update-context
```

### Command Groups

| Command | Purpose |
|---------|---------|
| `configure` | Configure schemas and databases |
| `learn` | Add examples and contextual mappings |
| `query` | Ask a question and generate SQL |

For command-specific options:

```bash
queryforge-ai configure --help
queryforge-ai learn --help
queryforge-ai query --help
```

## Interactive UI

The interactive UI uses H2O Wave.

Download Wave Server version `0.26.3` for your operating system:

https://github.com/h2oai/wave/releases/tag/v0.26.3

Extract the archive and start the Wave server in a separate terminal.

### Windows — PowerShell

From the directory containing `waved.exe`:

```powershell
.\waved.exe -max-request-size="20M"
```

### Linux / macOS

From the directory containing `waved`:

```bash
./waved -max-request-size="20M"
```

With the project environment activated, start the application from the repository root:

```bash
python queryforge/prompter.py
```

If using the existing Makefile workflow with `make` installed:

```bash
make run
```

## Limitations

- Generated SQL may require manual review and correction.
- Schema linking is currently available through the CLI.
- Self-correction currently supports OpenAI GPT models; support for other models is incomplete.
- PostgreSQL integration is experimental and may require fixes.
- Generation quality depends on the model, schema information, and contextual examples.
