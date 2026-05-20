# Portfolio Prompt Efficiency Lab

`portfolio_prompt_efficiency_lab` is a compact `dbt-duckdb` project centered on portfolio reporting. It is designed to bootstrap quickly on a local machine and provide a small but realistic surface area for analysis and change.

## What this repo is for

- Provide a small dbt project that can be explored locally with an AI coding agent.
- Support analysis, review, and small implementation tasks in a local dbt project.
- Keep the project small enough to bootstrap and validate quickly on attendee machines.

## Quickstart

Run these commands from the repository root:

1. Create your local environment file from the example:

```bash
cp .env.example .env
```

2. Then run the setup and validation commands:

```bash
uv sync
uv run dbt seed
uv run dbt build
uv run dbt test
```

`uv run` reads `.env`, so `DBT_PROFILES_DIR=.` is loaded automatically and no extra flags are needed after you create that file.

For a one-command clean bootstrap:

```bash
uv run python scripts/bootstrap_demo.py
```

## Workshop Flow

Your facilitator will provide the exact tasks during the workshop. The attendee-side flow is:

1. Create your local `.env` and bootstrap the clean baseline.

   ```bash
   cp .env.example .env
   uv sync
   uv run python scripts/bootstrap_demo.py
   ```

2. Run the tasks using the prompts provided outside this repository.
3. Validate your changes with the dbt commands requested during the session.
4. When a run is complete, reset the repo back to the baseline:

   ```bash
   uv run python scripts/reset_demo_state.py
   ```

5. Re-bootstrap if you want a fully rebuilt clean state:

   ```bash
   uv run python scripts/bootstrap_demo.py
   ```

If you are asked to repeat the exercise with a fresh agent session, restart your tool before the next run so prior chat context does not carry over.

## Repo shape

```text
models/silver/                   cleaned source-like models
models/gold/portfolio_reporting/ portfolio reporting outputs
models/gold/compliance/          compliance-oriented reporting outputs
models/gold/archived/            archived models kept for reference
analyses/                        scratch SQL and ad hoc exploration
docs/                            working documentation artifacts
scripts/                         bootstrap and reset helpers
```

## Resetting between runs

To restore the demo to its starting state after a live run:

```bash
uv run python scripts/reset_demo_state.py
```

That script:

- rewrites `docs/repo_map.md` to the starter template
- rewrites `docs/dbt_lineage_notes.md` to the starter template
- removes dbt build artifacts and the local DuckDB file

If you want a fresh build immediately after reset, run:

```bash
uv run python scripts/bootstrap_demo.py
```

## Validation expectations

The baseline repo should pass `dbt build` and `dbt test` before the workshop starts. During implementation tasks, a correct scoped change should also pass after edits to the reporting slice.
