[Contents](../index.md) · H3 · P2

# Python

## In one minute

At senior level Python questions are about writing code others can maintain: knowing how
the language's data model behaves (mutability, references, iteration), using pandas and
NumPy in vectorised form, and structuring code into typed, tested modules.

## Key ideas

- **Mutability and references.** Lists, dicts and sets are mutable; tuples, strings and
  numbers are not. Assignment copies the reference, not the object. Mutable default
  arguments (`def f(x=[])`) are shared between calls. Shallow versus deep copy.
- **Hashing.** Dict keys and set members must be hashable; lookups are O(1) on average,
  `x in list` is O(n).
- **Iteration.** Iterators and generators produce values lazily (`yield`); generator
  expressions avoid building lists; `enumerate`, `zip`, `itertools`.
- **Comprehensions.** List, dict, set; readable up to one condition and one loop.
- **Functions.** `*args`, `**kwargs`, keyword-only arguments, closures, `lambda`.
- **Decorators.** A function that wraps another to add behaviour (timing, caching with
  `functools.lru_cache`, retries).
- **Context managers.** `with` guarantees cleanup; `contextlib.contextmanager`.
- **Classes.** `__init__`, `__repr__`, `__eq__`; `@dataclass` for data holders;
  `@property`; `@classmethod`, `@staticmethod`; composition over deep inheritance.
- **Typing.** Type hints, `Optional`, generics, `Protocol`; checked by mypy or pyright.
- **Errors.** Specific exceptions, no bare `except`, raise early with a clear message.
- **Concurrency.** The global interpreter lock means threads help with input and output,
  not CPU work; use multiprocessing or vectorised libraries for CPU work; `asyncio` for
  many concurrent network calls.
- **NumPy.** Vectorised operations on arrays, broadcasting, views versus copies.
- **pandas.**
  - Vectorise; avoid `iterrows` and row-wise `apply`.
  - `groupby` with `agg` and `transform`; `merge` (check key uniqueness with `validate=`).
  - `.loc` for assignment; chained indexing causes the copy warning.
  - Categoricals and nullable types for memory; `pd.to_datetime`, resampling.
- **Environment and packaging.** Virtual environments, pinned dependencies,
  `pyproject.toml`, installable packages over path hacks; tools such as uv, ruff.
- **Complexity.** Know the cost of common operations; profile before optimising.

## On my CV

Python first in Programming; taught to 200+ students; coding standards at Sertis.

## Likely questions

1. **List versus tuple; why does it matter?** Mutability and hashability.
2. **What is a generator and when is it useful?** Lazy sequence; large files or streams.
3. **What does a decorator do?** Wraps a function; give a short example.
4. **Why is `df.apply(axis=1)` slow?** Python-level loop per row; use column operations.
5. **Senior follow-up: what do you look for in a Python code review?** Correctness and
   tests, clear names, small functions, no hidden state, typed interfaces.

## Pitfalls

- Mutable default arguments.
- Chained assignment in pandas.

## Sources

- The Python tutorial: <https://docs.python.org/3/tutorial/>
- pandas user guide: <https://pandas.pydata.org/docs/user_guide/index.html>
- Ramalho, *Fluent Python* (2nd ed.): <https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/>
