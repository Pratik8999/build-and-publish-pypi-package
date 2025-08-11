# 📦🚀 Steps to Build and Publish a Python Package to PyPI

This guide shows how to structure, build, and upload a Python package to PyPI using **pyproject.toml**, `setuptools`, and `twine`.

***

## 🛠️ 1. Prerequisites

Before you start, ensure you have:

- **A PyPI account** *(register at pypi.org)*
- **A PyPI API access token** with “Upload” scope  
  - Create it at: Account Settings → API Tokens
  - Copy and store securely (used for `.pypirc` or directly in commands)
- **Python 3.7+** installed
- **Required tools**:
  - `setuptools`, `build`, `twine`  
  *(Install later in step 2)*

***

## 📂 2. Project Structure Example

```

root_dir/
│
├── src/
│   └── project_dir/
│       ├── __init__.py
│       └── main.py
│
├── LICENSE
├── README.md
├── pyproject.toml

```

***

## 📝 3. Example `pyproject.toml`

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "project_name"
version = "0.1.0"
description = "Project Description which will appear on PyPI."
readme = "README.md"
requires-python = ">=3.7"
license = { text = "MIT" }
authors = [
    { name = "Your Name", email = "your.email@example.com" }
]

[project.urls]
Homepage = "https://github.com/yourusername/your-repo"
Repository = "https://github.com/yourusername/your-repo"
"Bug Tracker" = "https://github.com/yourusername/your-repo/issues"
```


***

## 🔧 4. Install Required Tools

```bash
pip install --upgrade setuptools build twine
```


***

## 🔐 5. Optional but recommended: Configure `.pypirc` for Twine

Create a `.pypirc` file in your home directory for easier authentication.

**Linux / macOS:**

```bash
nano ~/.pypirc
```

**Windows (PowerShell):**

```powershell
notepad $env:USERPROFILE\.pypirc
```

**Add:**

```
[pypi]
  username = __token__
  password = <your_api_token>
```


***

## 🏗️ 6. Build the Package

**Clean old builds:**

```bash
rm -rf dist build *.egg-info
```

**Build the new package:**

```bash
python3 -m build
```

This creates `.whl` and `.tar.gz` files in the `dist/` folder.

***

## 📤 7. Upload to PyPI

**You cannot re-upload the same version number. For changes, bump the version in `pyproject.toml` before rebuilding.**

**To upload:**

```bash
twine upload dist/*
```


***

## 🔍 8. Verify on PyPI

Check your project at:

```
https://pypi.org/project/project_name/
```


***

## ⬇️ 9. Install the Published Package

Others (or you) can install it using:

```bash
pip install project_name
```