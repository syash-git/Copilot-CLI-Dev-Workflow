# 🧪 MODULE 3: TEST GENERATION (12 minutes)

> 🧭 Module 3 of 5 · [Workshop index](../README.md) · Previous: [Module 2 — Refactoring](./02-refactoring.md) · Next: [Module 4 — Debugging](./04-debugging.md)

## What You're Doing

You've refactored the code. But did you break anything? How confident are you that it still works?

**Without AI**: Manually write 5-10 tests. Probably miss edge cases. Hope nothing breaks.

**With Copilot CLI**: Generate 15-20+ tests automatically, including edge cases you wouldn't think of.

---

## Step 1: Generate Comprehensive Tests

**Copy and paste this command:**

```bash
copilot

> @samples/book-app-project/books.py 
> Generate comprehensive pytest tests. Include tests for:
> - Adding books
> - Removing books
> - Finding by title
> - Finding by author
> - Marking as read
> - Edge cases (empty data, special characters, duplicate entries)
> - Error cases (missing files, corrupted data)
```

**What happens:**
- Copilot CLI analyzes the BookCollection class
- It generates 15-20+ test functions
- Tests cover happy path, edge cases, and error cases
- Each test is runnable, with assertions

**Take 5 minutes**: Look at the generated tests. How many tests were there? Did you spot any testing patterns you didn't expect?

---

## Step 2: Run the Tests

Let's verify those tests actually work.

**In your terminal:**

```bash
cd samples/book-app-project
python -m pytest tests/ -v
```

**What happens:**
- pytest runs all tests
- You see which tests pass/fail
- Green checkmarks = confidence that code works

**Expected result**: All tests pass ✓ (or mostly pass).

**Take 3 minutes**: Watch the tests run. Notice how many tests there are. Could you have written all these manually?

---

## Step 3: Understand What Tests Do

Tests are your safety net. When you refactored earlier, tests would have caught any breaking changes.

**Example test structure you should see:**

```python
# Happy path - normal usage
def test_add_book_creates_book():
    collection = BookCollection()
    collection.add_book("1984", "George Orwell", 1949)
    assert len(collection.list_books()) == 1

# Edge case - empty data
def test_add_book_with_empty_title():
    collection = BookCollection()
    with pytest.raises(ValueError):
        collection.add_book("", "Author", 2020)

# Error case - file doesn't exist
def test_load_books_handles_missing_file():
    collection = BookCollection()
    # Should gracefully handle missing data.json
    assert collection.list_books() == []
```


---

### 👉 Next up: Module 4 — Debugging

With tests in place you have a safety net. Time to use it: in the next module you'll reproduce a real reported bug in the buggy variant of the app and chase it down with Copilot.

[**Continue → Module 4 — Debugging**](./04-debugging.md)
