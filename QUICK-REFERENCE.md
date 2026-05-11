# 📋 Quick Reference: All Prompts

Reusable prompt templates from the [Workshop](./README.md). Save these for use on your own code.

---

## Plan Mode
```bash
# Ask Copilot to draft a plan before editing
copilot
> /plan [describe the goal, reference files with @path]
```

## Code Review Templates
```bash
# Basic review
copilot
> Review @[file] for code quality

# Focused review
copilot
> Review @[file] for [specific concern: security, performance, etc.]

# Full project
copilot
> Review @[project-path] and create a markdown checklist...
```

## Refactoring Templates
```bash
# Specific refactoring
copilot
> @[file] Refactor [describe problem]. Show the new approach and explain benefits.
```

## Test Generation Templates
```bash
# Comprehensive tests
copilot
> @[file] Generate comprehensive pytest tests. Include tests for:
> - [feature 1]
> - [feature 2]
> - Edge cases
> - Error handling
```

## Debugging Templates
```bash
# Debug a symptom
copilot
> @[file] [Describe symptom or error]. Debug why and provide a fix.

# Trace an issue through code
copilot
> @[file1] @[file2] Users report [symptom]. Trace where it originates.
```
