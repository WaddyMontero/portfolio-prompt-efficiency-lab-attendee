# Portfolio Prompt Efficiency Lab

## Stable commands

- `uv sync`
- `uv run dbt seed`
- `uv run dbt build`
- `uv run dbt test`
- `uv run python scripts/reset_demo_state.py`

## Conventions

- Silver models clean and type raw seed data.
- Gold models contain business-facing reporting logic.
- Business-facing validation lives in dbt tests, not only in prose.
- Keep docs concise; they are indexes, not exhaustive inventories.
