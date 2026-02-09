# Running Dash Evaluations

The directory `dash/evals` contains the evaluation suite for the Dash agent.

## Prerequisites

1.  **Running Application**: The evaluations run against the `dash` agent code, which connects to the database. Ensure your Docker containers are running (`docker compose up -d`).
2.  **Environment Variables**: The tests need `OPENAI_API_KEY` (for the LLM grader) and database credentials. These should be available if you are running from the project root with the `.env` file.

## Running Evaluations

You can run the evaluations using the `run_evals.py` script from the project root.

### 1. Basic Run (String Matching)

Runs all test cases and checks if expected strings appear in the response.

```powershell
python -m dash.evals.run_evals
```

### 2. Run with LLM Grader (Recommended)

Uses an LLM (GPT-4o-mini by default) to grade the response quality, checking for factual correctness and completeness.

```powershell
python -m dash.evals.run_evals --llm-grader
```

### 3. Run Specific Categories

Filter tests by category: `basic`, `aggregation`, `data_quality`, `complex`, `edge_case`.

```powershell
python -m dash.evals.run_evals --category complex
```

### 4. Verbose Mode

Show full agent responses for failed tests, useful for debugging.

```powershell
python -m dash.evals.run_evals --verbose
```

### 5. Compare against Golden SQL

Executes the "Golden SQL" (known correct query) and compares its results against the agent's results.

```powershell
python -m dash.evals.run_evals --compare-results
```

## Adding New Tests

Edit `dash/evals/test_cases.py` to add new `TestCase` objects to the `TEST_CASES` list.

```python
TestCase(
    question="Your new question",
    expected_strings=["Expected Answer Part 1"],
    category="basic",
    golden_sql="SELECT ...", # Optional
)
```
