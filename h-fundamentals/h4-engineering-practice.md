[Contents](../index.md) · H4 · P2

# Engineering practice

## In one minute

Good engineering practice in data science means changes are small, reviewed, tested and
reproducible. Git gives history and review, Pytest gives confidence that a change did not
break behaviour, Docker gives the same environment everywhere, and written standards make
those habits the team's default instead of one person's preference.

## Key ideas

- **Git.**
  - Feature branches and pull requests; small commits with clear messages.
  - `merge` keeps history as it happened; `rebase` replays commits for a linear history
    (do not rebase shared branches).
  - Resolving conflicts; `revert` to undo a pushed commit safely; `reset` only locally;
    `stash`; `bisect` to find the commit that introduced a bug.
  - `.gitignore` for data, secrets and build output. No credentials in history.
  - Trunk-based development versus long-lived development branches.
- **Pytest.**

  ```python
  import pytest

  @pytest.fixture
  def customers():
      return make_sample_customers()

  @pytest.mark.parametrize("spend, expected", [(99, False), (100, True), (101, True)])
  def test_threshold_is_inclusive(spend, expected):
      assert is_eligible(spend) is expected
  ```

  - *Fixtures*: reusable setup, with scopes; `tmp_path`, `monkeypatch` built in.
  - *Parametrize*: one test over many cases, ideal for boundaries.
  - *Mocking*: replace external systems (databases, APIs).
  - `pytest.approx` for floats; `pytest.raises` for errors.
- **Testing data code.** Small hand-made inputs with known outputs; test boundaries,
  nulls, duplicates and empty input; a local Spark session for PySpark functions;
  property checks (row count preserved, key unique).
- **Test pyramid.** Many unit tests, fewer integration tests, a few end-to-end runs.
- **Docker.** Image (built from a Dockerfile, layered and cached) versus container (a
  running instance). Pin versions; put rarely changing layers first; keep images small;
  volumes for data; compose for several services.
- **Continuous integration.** Lint, type-check and test on every pull request.
- **Coding standards typically cover.** Project layout, naming, formatting and linting
  (ruff, black), type hints, docstrings, config handling, logging over printing, tests
  required, notebook rules, dependency pinning, review checklist.
- **Reproducibility.** Seeds, pinned environments, data versions, config recorded with
  results.

## On my CV

Docker, Git and Pytest in Platforms and Tools. "Wrote the team's coding standards for
machine learning projects" (Sertis). Docker packaged the self-hosted AutoML pipeline. CI
at AIS was built by an engineer, not by me.

**To fill in (only I know):** what the Sertis standards covered, why the team needed
them, and how they were adopted.

## Likely questions

1. **Merge or rebase?** Rebase my own branch to tidy it; merge shared branches.
2. **How do you test a data transformation?** Small fixture, expected output, boundaries.
3. **What goes in your coding standards and why?** The few rules that prevent the bugs
   the team actually had.
4. **Image versus container?** Template versus running instance.
5. **Senior follow-up: the team resists writing tests.** Start with tests for the rules
   that have caused incidents, make them easy to run, and require them for changed code
   only.

## Pitfalls

- Tests that only check the code runs.
- Standards nobody enforces.

## Sources

- Pro Git book: <https://git-scm.com/book/en/v2>
- pytest documentation: <https://docs.pytest.org/en/stable/>
- Docker, building best practices: <https://docs.docker.com/build/building/best-practices/>
