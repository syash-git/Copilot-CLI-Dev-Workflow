# 🛠️ MODULE 2: REFACTORING (15 minutes)

> 🧭 Module 2 of 5 · [Workshop index](../README.md) · Previous: [Module 1 — Code Review](./01-code-review.md) · Next: [Module 3 — Test Generation](./03-test-generation.md)

## What You're Doing

You've reviewed the code and found issues. Now it's time to **improve it safely**. Refactoring means changing the structure/organization without breaking functionality.

Your code review may have surfaced a different mix of findings depending on how Copilot framed them — counts, categories, and severity labels vary from run to run, and that's normal. That said, two themes come up almost every time on this codebase: **missing type hints** and **weak input validation**. Those are the two we'll tackle in this module — type hints first (a quick, foundational win), then input validation (practical bug prevention). If you have time at the end, the architectural improvements (e.g. the `if/elif` chain in command dispatch) make a great bonus.

---

## Step 1: Add Type Hints (HIGH Priority)

Good Python code uses **type hints**—they tell other developers (and tools) what types your functions expect and return. Let's add them to book_app.py.

**Copy and paste this command:**

```bash
copilot

> Review @samples/book-app-project/book_app.py and add complete type hints 
> to all functions. Add parameter types (e.g., books: List[Book]) and 
> return types (e.g., -> None). Import List from typing.
```

**What happens:**
- Copilot scans the file
- It identifies the functions missing type hints
- It suggests adding types like `def show_books(books: List[Book]) -> None:`
- It might even provide the complete refactored code

**Take 5 minutes**: Read the suggestions. Notice how type hints make code clearer? Could a new developer understand what each function expects?

**Example of what Copilot suggests:**
```python
# Before:
def show_books(books):
    ...

# After:
from typing import List

def show_books(books: List[Book]) -> None:
    """Display books in a user-friendly format."""
    if not books:
        print("No books found.")
        return
    # ...
```

---

## 🧠 Quick Primer: Plan Mode (1 minute)

Dont want copilot to make code changes directly? meet **Plan Mode** — it asks Copilot to *think before it types*. Instead of jumping straight to edits, Copilot drafts a step-by-step plan you can review, tweak, or reject. Perfect for multi-step changes like the exercise below.

**How to use it:** type `/plan` inside the Copilot CLI, then describe your goal. Copilot outlines its approach and waits for your approval before changing any code.

```bash
> /plan add input validation to handle_add() in @samples/book-app-project/book_app.py
```

Try it on the next exercise — review the plan, then say "go" to execute.

---

## 🧩 Step 2: Exercise — Improve Input Validation (HIGH Priority)

Time to practice on your own! This is a HIGH priority issue you'll fix yourself with Copilot CLI.

### 🐛 The Challenge

Open `samples/book-app-project/book_app.py` and look at the `handle_add()` function. It has a sneaky bug: **it trusts the user completely**.

Try running the app and adding a book with:
- An **empty title** (just press Enter)
- An **empty author** (just press Enter)
- A year of **`-500`**, **`99999`**, or **`abc123`**

What happens? You'll discover the app happily accepts garbage data — empty strings get stored as "books," and unreasonable years (like year 99999) sail through without complaint. Over time, this corrupts your library file with invalid entries.

**Your mission:**
1. Identify what bad inputs could break this app.
2. Use Copilot CLI to add proper input validation to `handle_add()`.
3. Verify the fix by trying the same bad inputs again.

**Validation requirements:**
- ❌ Reject empty `title` and `author` (after stripping whitespace).
- ❌ Reject years outside the range **1000–2100**.
- ❌ Reject non-numeric year input with a clear message.
- ✅ Show a friendly error message for each failure and return early (don't add the book).

**Take 4 minutes**: Craft your own prompt to Copilot CLI to fix this. Think about what context Copilot needs (the file, the function, the rules).

> 💡 **Hint**: Try starting with `/plan` (see the primer above) so Copilot proposes an approach before editing. Reference the file with `@samples/book-app-project/book_app.py` and be specific about *which* function to change and *what* rules to enforce.

<details>
<summary>✅ <b>Click to reveal the solution</b> (try it yourself first!)</summary>

**Example prompt — using Plan Mode:**

```bash
copilot

# Step A — ask Copilot to draft a plan first
> /plan Improve input validation in handle_add() in 
> @samples/book-app-project/book_app.py. Rules:
> - Reject empty title and author (after stripping whitespace)
> - Restrict year to the range 1000–2100
> - Reject non-numeric year input
> - Show a friendly error and return early on each failure

# Step B — review the plan, then approve to execute
> Looks good — go ahead and apply it.
```

> 💡 If something in the plan looks off, push back instead of approving:
> *"Also handle the case where year input is empty — treat it as invalid."*
> Copilot will revise the plan, then wait for approval again.

**What Copilot does:**
- **Plan phase:** drafts a step-by-step plan (which checks to add, in what order, what messages to print) and waits for your approval — no code changes yet.
- **Execute phase:** once you approve, it edits `handle_add()` to match the plan with proper error handling and user-friendly messages.

**Example before/after:**

```python
# Before:
def handle_add():
    print("\nAdd a New Book\n")
    title = input("Title: ").strip()
    author = input("Author: ").strip()
    # No validation—user could enter empty strings!
    year_str = input("Year: ").strip()
    try:
        year = int(year_str) if year_str else 0
        collection.add_book(title, author, year)
        print("\nBook added successfully.\n")
    except ValueError as e:
        print(f"\nError: {e}\n")

# After:
def handle_add():
    print("\nAdd a New Book\n")
    title = input("Title: ").strip()
    if not title:
        print("\nError: Title cannot be empty.\n")
        return
    
    author = input("Author: ").strip()
    if not author:
        print("\nError: Author cannot be empty.\n")
        return
    
    year_str = input("Year: ").strip()
    try:
        year = int(year_str)
        if year < 1000 or year > 2100:
            print("\nError: Year must be between 1000 and 2100.\n")
            return
        collection.add_book(title, author, year)
        print("\nBook added successfully.\n")
    except ValueError:
        print("\nError: Year must be a valid number.\n")
```

</details>


---

### 👉 Next up: Module 3 — Test Generation

The code is cleaner, but is it still correct? In the next module you'll generate a pytest suite so future refactors and bug fixes can't silently break behaviour.

[**Continue → Module 3 — Test Generation**](./03-test-generation.md)
