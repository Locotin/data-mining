# Agent Guidelines for This Repo

## Purpose
- This repository currently contains a single Jupyter notebook: `Entrega-1.ipynb`.
- There are no build, lint, or test tools configured in the repo itself.
- Use this guide to keep edits consistent and avoid inventing tooling that is not present.

## Repo Layout
- `Entrega-1.ipynb`: data exploration notebook using `gdown`, `pandas`, and `numpy`.
- No `requirements.txt`, `pyproject.toml`, or `setup.py` detected.
- No `.cursor` or Copilot instruction files detected.

## Build / Lint / Test Commands
There are no build, lint, or test commands configured in this repository.

If you need to run the notebook locally:
- Start Jupyter Lab/Notebook: `python -m jupyter lab` or `python -m jupyter notebook`.
- Open `Entrega-1.ipynb` and run cells in order.

If you introduce tooling, document it here and prefer these conventions:
- Tests: `pytest` (single test: `pytest path/to/test_file.py::test_name`)
- Lint/format: `ruff` + `black` (lint: `ruff .`, format: `black .`)
- Type checking: `mypy` (if you add type annotations)

## Notebook Execution Notes
- The notebook reads a large dataset from a public URL using `pandas.read_csv`.
- The URL is: `https://www.datos.gov.co/resource/nudc-7mev.csv?$limit=500000`.
- Running the notebook requires network access and enough memory for the dataset.

## Code Style Guidelines (Python)
Follow these unless the repo adds a formatter or lint rules.

### Imports
- Group imports in this order: standard library, third-party, local.
- Separate groups with a single blank line.
- Keep imports at the top of the cell or file unless there is a clear reason to delay.
- Use common aliases: `import numpy as np`, `import pandas as pd`.
- Avoid wildcard imports.

### Formatting
- Aim for PEP 8 compliance.
- Use 4 spaces per indent level; no tabs.
- Keep lines under 88-100 characters when practical.
- Prefer explicit line breaks over backslashes.

### Types and Data
- Use `pandas` dtypes intentionally; avoid implicit type coercion where possible.
- Convert string columns to categorical only if it improves memory/logic.
- When reading external data, specify `dtype=` and `parse_dates=` if known.

### Naming
- Use `snake_case` for variables and functions.
- Use descriptive names over abbreviations.
- For dataframes, `df` is acceptable only for short-lived variables.
- Name derived frames by purpose, e.g., `df_clean`, `df_metrics`.

### Error Handling
- Fail fast for missing columns or unexpected schema.
- Use `assert` for notebook exploration; use explicit exceptions in reusable code.
- When reading remote data, catch network errors and show a clear message.

### Data Cleaning and Transformations
- Keep transformations in small, ordered steps.
- Avoid chaining too many operations in one line.
- Use `.copy()` when creating filtered views to avoid SettingWithCopy warnings.
- Document assumptions about filters or aggregations.

### Performance
- Prefer vectorized operations over loops.
- For large datasets, consider `usecols=` to limit columns.
- Avoid `apply` when a vectorized alternative exists.

### Reproducibility
- Keep notebooks deterministic where possible.
- If randomness is used, set a seed at the top of the notebook.
- Store parameters (URLs, thresholds) in clearly named variables.

## Working With Notebooks
- Execute cells top-to-bottom after edits to validate the state.
- Clear outputs before committing large outputs if this becomes a git repo.
- Avoid storing secrets in notebook cells or outputs.

## External Rules
- Cursor rules: not found (`.cursor/rules/` or `.cursorrules` missing).
- Copilot rules: not found (`.github/copilot-instructions.md` missing).

## When Adding Tests (Future Guidance)
- Place tests under `tests/`.
- Name tests `test_*.py` and functions `test_*`.
- Prefer small unit tests for data transformations.

## When Adding Lint/Format (Future Guidance)
- Add `pyproject.toml` to centralize config.
- Keep formatter and linter settings consistent with this guide.

## When Adding Dependencies (Future Guidance)
- Add `requirements.txt` or `pyproject.toml`.
- Pin versions if reproducibility matters.
- Document setup steps in `AGENTS.md` and `README.md`.
