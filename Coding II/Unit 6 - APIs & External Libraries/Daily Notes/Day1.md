# Day 1: Pip & Package Management
**Learning Target:** I can install and manage Python packages using pip and virtual environments.

### Key Concepts
**pip:** Package installer for Python
**Virtual environment:** Isolated Python setup for projects
**requirements.txt:** Lists project dependencies

### Code Examples
```bash
# Install package
pip install requests

# Install specific version
pip install requests==2.28.0

# Upgrade package
pip install --upgrade requests

# Uninstall package
pip uninstall requests

# List installed packages
pip list

# Create virtual environment
python -m venv my_env

# Activate (macOS/Linux)
source my_env/bin/activate

# Activate (Windows)
my_env\Scripts\activate

# Create requirements.txt
pip freeze > requirements.txt

# Install from requirements.txt
pip install -r requirements.txt
```

### Python Code Examples
```python
import requests

# Check if package is installed
try:
    import requests
    print("requests is installed")
except ImportError:
    print("requests not installed")
```

### Guided Practice
Create virtual environment, install packages, generate requirements.txt.

### Practice Problems
**Problem 1 — Beginner:** Install a package with pip.

**Problem 2 — Intermediate:** Create virtual environment and install multiple packages.

**Problem 3 — Challenge:** Create requirements.txt for a project.

<details>
<summary>✅ Sample Answers</summary>

```bash
# Problem 2
python -m venv my_project
source my_project/bin/activate
pip install requests matplotlib numpy
pip freeze > requirements.txt
```
</details>

---

---
