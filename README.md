
# Pre-Commit Checks Example

This repository demonstrates how to set up pre-commit checks using `black` for Python code formatting, both locally and via GitHub Actions.

## Setting Up Local Pre-Commit Checks

### Step 1: Clone the Repository
```bash
git clone https://github.com/MeenaBana/pre-commit-checks-example.git
cd pre-commit-checks-example
```

### Step 2: Install Pre-Commit
```bash
pip install pre-commit
```

### Step 3: Create a Pre-Commit Configuration File
Create a `.pre-commit-config.yaml` file with the following content:
```yaml
repos:
  - repo: https://github.com/psf/black
    rev: stable
    hooks:
      - id: black
        language_version: python3
```

### Step 4: Install Pre-Commit Hooks
```bash
pre-commit install
```

### Step 5: Optional - Format All Existing Files
```bash
pre-commit run --all-files
```

### Step 6: Commit and Push Changes
```bash
git add .
git commit -m "Add pre-commit config with black"
git push
```

## Setting Up GitHub Actions

### Step 7: Create GitHub Actions Workflow File
Create a file at `.github/workflows/pre-commit.yml` with the following content:
```yaml
name: Pre-commit

on: [push, pull_request]

jobs:
  pre-commit:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.x'
    - name: Install pre-commit
      run: pip install pre-commit
    - name: Run pre-commit
      run: pre-commit run --all-files
```

### Step 8: Commit and Push the Workflow File
```bash
git add .github/workflows/pre-commit.yml
git commit -m "Add GitHub Actions for pre-commit"
git push
```

### Step 9: Verify GitHub Actions
Monitor the "Actions" tab in your GitHub repository to ensure the workflow runs successfully on subsequent pushes or pull requests.

## Conclusion
With these settings, `black` will format your Python code during local development and GitHub Actions will enforce these formatting checks on the repository. This ensures consistent code quality and style adherence throughout the development process.


## Example Usage

### Before Formatting with Black

**Example Code 1:**
```python
import sys, os

def example_function():
  print("This is a poorly formatted code!")

example_function()
```

**Example Code 2:**
```python
def another_example():
    x = {  'a':37,'b':42,

    'c':927}

    y = 'hello ''world'
    z = 'hello '+'world'
    a = 'hello {}'.format('world')
    return x, y, z, a

another_example()
```

### After Formatting with Black

**Formatted Code 1:**
```python
import sys
import os


def example_function():
    print("This is a poorly formatted code!")


example_function()
```

**Formatted Code 2:**
```python
def another_example():
    x = {'a': 37, 'b': 42, 'c': 927}

    y = 'hello ' 'world'
    z = 'hello ' + 'world'
    a = 'hello {}'.format('world')
    return x, y, z, a


another_example()
```

With the pre-commit hook in place, the original code will be automatically formatted to the cleaner version as shown above.
