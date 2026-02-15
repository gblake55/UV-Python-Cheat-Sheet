# UV Python Package Manager Cheat Sheet

**UV** by Astral - An extremely fast Python package and project manager written in Rust  
Replaces: pip, pip-tools, pipx, poetry, pyenv, virtualenv, and more (10-100x faster than pip)

---
```
hello
```


## Installation

```bash
# Linux/macOS
curl -LsSf https://astral.sh/uv/install.sh | sh
```

# Windows
```
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

# Update UV
```
uv self update
```
```

---

## Python Version Management

```bash
# Install Python versions
uv python install 3.10 3.11 3.12

# List installed Python versions
uv python list

# Set Python version for directory
uv python pin 3.12

# Use specific Python in command
uv run --python 3.11 script.py
uv venv --python 3.12.0
```

---

## Virtual Environments

```bash
# Create virtual environment
uv venv                          # Uses default Python
uv venv --python 3.12           # Specify version
uv venv my_env                  # Custom name

# Activate (same as standard venv)
source .venv/bin/activate       # Linux/macOS
.venv\Scripts\activate          # Windows
```

---

## Project Management

```bash
# Initialize new project
uv init myproject
cd myproject

# Add dependencies
uv add requests numpy           # Add packages
uv add --dev pytest            # Add dev dependency
uv add --group testing pytest  # Add to group

# Remove dependencies
uv remove requests

# Run commands in project environment
uv run python script.py
uv run pytest

# Lock dependencies
uv lock                        # Create lockfile
uv lock --check               # Verify lockfile is current

# Sync environment with lockfile
uv sync                        # Install all dependencies
uv sync --no-dev              # Skip dev dependencies
```

---

## Pip-Compatible Interface

```bash
# Install packages
uv pip install requests
uv pip install -r requirements.txt
uv pip install -e .           # Editable install

# Uninstall packages
uv pip uninstall requests

# Compile requirements (like pip-compile)
uv pip compile requirements.in -o requirements.txt
uv pip compile pyproject.toml -o requirements.txt

# Sync dependencies (like pip-sync)
uv pip sync requirements.txt

# List packages
uv pip list
uv pip show requests

# Freeze dependencies
uv pip freeze
```

---

## Scripts (Single-File)

```bash
# Add dependencies to script inline
uv add --script myscript.py requests pandas

# Run script with dependencies
uv run myscript.py             # Uses inline metadata

# Example script with inline metadata:
# /// script
# dependencies = ["requests", "pandas"]
# ///
```

---

## Tools (like pipx)

```bash
# Run tool temporarily
uvx ruff check .               # Ephemeral environment
uv tool run black .

# Install tool globally
uv tool install ruff
uv tool install pytest

# Uninstall tool
uv tool uninstall ruff

# List installed tools
uv tool list

# Upgrade tool
uv tool upgrade ruff
```

---

## Package Building & Publishing

```bash
# Build package
uv build

# Publish to PyPI
uv publish
uv publish --token $PYPI_TOKEN
```

---

## Common Options

```bash
--python <version>             # Specify Python version
--no-cache                     # Disable cache
--index-url <url>             # Custom package index
--extra-index-url <url>       # Additional package index
--offline                      # Use only cached data
--system                       # Use system Python
--quiet / -q                   # Minimal output
--verbose / -v                 # Detailed output
```

---

## Configuration

```bash
# Create/modify pyproject.toml for UV settings
[tool.uv]
index-url = "https://pypi.org/simple"
dev-dependencies = ["pytest>=7.0"]

# Environment variables
export UV_INDEX_URL="https://custom-index.com"
export UV_CACHE_DIR="~/.cache/uv"
export UV_NO_CACHE=1
```

---

## Quick Reference

| Task | UV Command |
|------|------------|
| Create venv | `uv venv` |
| Install package | `uv pip install <pkg>` or `uv add <pkg>` |
| Run script | `uv run script.py` |
| Install Python | `uv python install 3.12` |
| Lock deps | `uv lock` |
| Sync deps | `uv sync` |
| Run tool | `uvx <tool>` |
| Help | `uv --help` or `uv <cmd> --help` |

---

**Documentation:** https://docs.astral.sh/uv  
**GitHub:** https://github.com/astral-sh/uv
