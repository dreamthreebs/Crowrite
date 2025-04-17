# 0417-pytest

Certainly! Here's a **general, best-practice guide** to using `pytest`—including directory structure, naming conventions, output control, and common pitfalls. This is suitable for teaching others or serving as a quick reference.

***

### ✅ General Guide for Using `pytest` Effectively

#### 📁 1. Recommended Project Structure

```
your_project/
├── src/                  # Optional, for better namespace control
│   └── your_package/
│       ├── __init__.py
│       ├── module1.py
│       └── module2.py
│
├── tests/                # All test files go here
│   ├── __init__.py       # Optional
│   ├── test_module1.py
│   └── test_module2.py
│
├── pyproject.toml        # Recommended modern config
├── requirements.txt
└── README.md
```

Alternatively, if you're not using `src/` layout:

```
your_project/
├── your_package/
│   ├── __init__.py
│   ├── module1.py
│   └── ...
├── tests/
│   └── test_module1.py
└── ...
```

***

#### 🧪 2. Writing Tests

* Test files: name them as `test_*.py` or `*_test.py`
* Test functions: start names with `test_`
* Example:

```python
# tests/test_module1.py
from your_package import module1

def test_add():
    assert module1.add(1, 2) == 3
```

***

#### 📦 3. Making Your Package Importable

From the root directory, run:

```bash
pip install -e .
```

This allows test files to import your package using absolute imports like:

```python
from your_package import module1
```

***

#### 🖨️ 4. Seeing `print()` Output

By default, `pytest` **captures stdout**, so you won’t see `print()` unless:

* The test **fails**, or
* You run `pytest` with:

```bash
pytest -s            # disables output capturing
pytest --capture=no  # same effect
```

***

#### ⚠️ 5. Common Pitfalls to Avoid

| Mistake                                         | Why it's a problem                            |
| ----------------------------------------------- | --------------------------------------------- |
| Placing test files in the same folder as code   | Can cause import conflicts                    |
| Using relative imports in test files            | Not robust; breaks easily                     |
| Naming a test file the same as a module         | Import shadowing (`test.py`, `math.py`, etc.) |
| Forgetting to install in editable mode (`-e .`) | Causes `ModuleNotFoundError` in tests         |
| Relying on `print()` without `-s`               | Output won’t appear unless test fails         |

***

#### ⚙️ 6. Optional `pyproject.toml` Configuration

```toml
[tool.pytest.ini_options]
addopts = "-ra -q -s"
testpaths = ["tests"]
python_files = ["test_*.py"]
```

This simplifies your test command to just:

```bash
pytest
```

***

Would you like a GitHub template or cookiecutter starter with this structure?
