# 🔧 Workshop Troubleshooting

Common issues you might hit during the [Workshop](./README.md), and how to fix them.

---

## "Command not found: copilot"

**Problem**: Copilot CLI isn't installed

**Solution**:
```bash
npm install -g @github/copilot
```

Then verify:
```bash
copilot --version
```

## "Authentication failed"

**Problem**: GitHub Copilot isn't authenticated

**Solution**:
```bash
copilot auth login
```

Your browser will open. Approve access. Done!

## "FileNotFoundError: samples/book-app-project/..."

**Problem**: You're in the wrong directory

**Solution**:
```bash
# Make sure you're in the repo root
cd copilot-cli-for-beginners

# Verify the file exists
ls samples/book-app-project/book_app.py

# If not found, clone the repo fresh
git clone https://github.com/github/copilot-cli-for-beginners
cd copilot-cli-for-beginners
```

## "Python: command not found"

**Problem**: Python isn't installed or not in PATH

**Solution**: Install Python 3.10+ from [python.org](https://python.org)

## "ModuleNotFoundError: No module named 'pytest'"

**Problem**: pytest isn't installed

**Solution**:
```bash
cd samples/book-app-project
pip install pytest
```

## Tests fail unexpectedly

**Problem**: Generated tests don't run on your machine

**Solutions**:
1. Check Python version: `python --version` (need 3.10+)
2. Install dependencies: `pip install pytest`
3. Make sure you're in correct directory: `cd samples/book-app-project`
4. Run with verbose output: `python -m pytest tests/ -vv`

## "Copilot CLI took forever to respond"

**Problem**: Request timed out or was very slow

**Solutions**:
1. Use smaller file references: `@samples/book-app-project/books.py` instead of `@samples/book-app-project/`
2. Simplify your prompt: Remove extra details
3. Try again: Sometimes just a temporary slowdown
4. Use screenshots: If time-critical, reference expected output instead
