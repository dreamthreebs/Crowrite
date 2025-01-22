# 0122-better way to use my own code

### Better way to manage my python code

The best way to manage your frequently updated **pure Python code** without manually adding paths is to structure it as a **Python package** and install it in an editable mode (`pip install -e`). Here’s the recommended approach:

***

### **1. Organize Your Code as a Python Package**

Instead of placing scripts randomly, structure your project like this:

```
my_project/
│── my_package/          # Your actual Python code
│   ├── __init__.py      # Makes this directory a package
│   ├── module1.py       # Your code files
│   ├── module2.py
│── scripts/             # Scripts using your package
│   ├── run_analysis.py
│── tests/               # Unit tests
│   ├── test_module1.py
│── setup.py             # Installation script
│── pyproject.toml       # Modern build configuration (optional)
│── requirements.txt     # Dependencies (if any)
│── README.md
```

***

### **2. Write a `setup.py` for Easy Importing**

Since you update your code frequently, installing it in **editable mode** (`pip install -e .`) allows changes to reflect without reinstalling.

Create a `setup.py` in the project root:

```python
from setuptools import setup, find_packages

setup(
    name="my_package",
    version="0.1",
    packages=find_packages(),  # Automatically finds `my_package`
)
```

Now, install your package in **editable mode**:

```bash
pip install -e .
```

After this, **you can import `my_package` from anywhere** in Python scripts without modifying `sys.path` manually:

```python
from my_package import module1
```

***

### **Difference between \` pip install -e . \`and \`pip install .\`**

The difference between `pip install -e .` and `pip install .` lies in **how your Python package is installed** and whether changes to the source code take effect immediately.

***

### **1. `pip install .` (Regular Installation)**

When you run:

```bash
pip install .
```

**What happens?**

* **Copies** your package’s files into the Python environment’s `site-packages` directory.
* The installed version is **static**—changes to your source code **do not** affect the installed package unless you reinstall it.

**Use case:**\
✅ When your code is **stable** and you don’t plan to modify it frequently.

***

### **2. `pip install -e .` (Editable Installation)**

When you run:

```bash
pip install -e .
```

**What happens?**

* Instead of copying files, **a symbolic link (symlink) is created** pointing to your project directory.
* Changes you make to your source code **immediately reflect** without reinstalling.
* The package is marked as **editable** in `pip list`.

**Use case:**\
✅ When you **frequently modify** your code and want the changes to be available **immediately**.

***

### **Comparison Table**

| Feature                                | `pip install .`               | `pip install -e .`                |
| -------------------------------------- | ----------------------------- | --------------------------------- |
| **How it's installed**                 | Copied to `site-packages`     | Symlinked to the source directory |
| **Changes reflect automatically?**     | ❌ No                          | ✅ Yes                             |
| **Reinstallation needed for updates?** | ✅ Yes                         | ❌ No                              |
| **Best for**                           | Stable, production-ready code | Active development                |

***

### **Which One Should You Use?**

* If you **constantly update your code**, use **`pip install -e .`** (editable mode).
* If you're **distributing a stable release**, use **`pip install .`**.

Since your **code is flexible and changes frequently**, **I strongly recommend `pip install -e .`**. 🚀

***

### Use pyproject.toml or setup.py?

***

#### **Advantages of `pyproject.toml` Over `setup.py`**

Modern Python packaging encourages using **`pyproject.toml`** instead of the older `setup.py`. Here’s why:

***

### **1. Future-Proof and PEP 517/518 Compliant**

* `pyproject.toml` follows **PEP 517/518**, which defines a **standardized build system interface**.
* `setup.py` is legacy and might be deprecated in the future.

✅ **Advantage:** Ensures compatibility with modern tools like **Poetry, Hatch, PDM**.

***

### **2. No Need for `setup.py` Execution**

* With `setup.py`, running `pip install .` **executes Python code**, which can cause unexpected behavior.
* `pyproject.toml` is **static**—pip reads it without executing any code.

✅ **Advantage:** More predictable builds, avoiding accidental side effects.

***

### **3. Cleaner and More Readable**

A `pyproject.toml` file is more **structured** and readable than `setup.py`. Compare:

#### **Using `setup.py`**

```python
from setuptools import setup, find_packages

setup(
    name="my_package",
    version="0.1",
    packages=find_packages(),
    install_requires=["numpy", "pandas"],
)
```

#### **Using `pyproject.toml`**

```toml
[build-system]
requires = ["setuptools"]
build-backend = "setuptools.build_meta"

[project]
name = "my_package"
version = "0.1"
dependencies = ["numpy", "pandas"]
```

✅ **Advantage:** **TOML format** is **cleaner**, structured, and easier to read.

***

### **4. Easier Dependency Management**

* `setup.py` requires **managing dependencies manually** inside `install_requires`.
* `pyproject.toml` allows **tooling integrations** (e.g., `Poetry`, `Hatch`) for **better dependency resolution**.

✅ **Advantage:** **Better dependency management** and **modern workflows**.

***

### **5. Works with Modern Build Tools**

* `pyproject.toml` works with **Poetry, Hatch, PDM**, and **Setuptools**.
* `setup.py` is **tied only to Setuptools**.

✅ **Advantage:** **More flexible**—you can switch build systems easily.

***

### **Should You Switch?**

* If you **maintain an old project**, `setup.py` is still fine.
* If you **start a new project**, **use `pyproject.toml`** for modern compatibility.

✅ **Best choice for future-proofing:** **Use `pyproject.toml`**.

Would you like help converting your project to `pyproject.toml`? 🚀
