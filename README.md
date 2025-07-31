# Sudoku Row Validator

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Course](https://img.shields.io/badge/MOOC.fi-Python%20Programming-lightgrey)

A Python function that validates whether a specific row in a Sudoku grid follows the game's fundamental rule: each number 1-9 appears at most once per row. This solution demonstrates list manipulation, duplicate detection, and Sudoku game logic validation.

---

## 📖 Problem Description

Write a function named `row_correct(sudoku: list, row_no: int)` that takes a two-dimensional array representing a Sudoku grid and an integer specifying a row index (0-based). The function should return `True` if the row is valid according to Sudoku rules, or `False` if it contains duplicate numbers.

### Sudoku Row Rules
- Each row must contain numbers 1-9 **at most once**
- Empty cells are represented by `0` and don't count as duplicates
- Multiple `0`s in a row are allowed (incomplete puzzle)
- Any duplicate of numbers 1-9 makes the row invalid

### Example
For the given Sudoku grid:
- Row 0: `[9, 0, 0, 0, 8, 0, 3, 0, 0]` → **Valid** (no duplicates)
- Row 1: `[2, 0, 0, 2, 5, 0, 7, 0, 0]` → **Invalid** (duplicate 2)

---

## 💻 Code Implementation

```python
def row_correct(sudoku: list, row_no: int):
    row = []
    for num in sudoku[row_no]:
        if num > 0 and num in row:
            return False
        row.append(num)
        
    return True

if __name__ == "__main__":
    sudoku = [
        [9, 0, 0, 0, 8, 0, 3, 0, 0],
        [2, 0, 0, 2, 5, 0, 7, 0, 0],
        [0, 2, 0, 3, 0, 0, 0, 0, 4],
        [2, 9, 4, 0, 0, 0, 0, 0, 0],
        [0, 0, 0, 7, 3, 0, 5, 6, 0],
        [7, 0, 5, 0, 6, 0, 4, 0, 0],
        [0, 0, 7, 8, 0, 3, 9, 0, 0],
        [0, 0, 1, 0, 0, 0, 0, 0, 3],
        [3, 0, 0, 0, 0, 0, 0, 0, 2]
    ]
    print(row_correct(sudoku, 0))  # True
    print(row_correct(sudoku, 1))  # False
```

**Output:**
```
True
False
```

---

## 🧠 Algorithm Explanation

The solution uses an **early detection approach** for maximum efficiency:

1. **Initialize** an empty list to track seen numbers
2. **Iterate** through each cell in the specified row
3. **Check duplicates**: If the current number is positive (not 0) and already exists in our tracking list, return `False` immediately
4. **Track numbers**: Add the current number to our tracking list
5. **Return success**: If no duplicates are found, return `True`

**Key Logic:**
- `num > 0` ensures we ignore empty cells (zeros)
- `num in row` efficiently checks for duplicates
- Early return optimizes performance by stopping at first duplicate

**Time Complexity:** O(n²) worst case, O(n) average case (early termination)  
**Space Complexity:** O(n) for the tracking list

---

## 🛠 How to Run

Clone the repo and run:

```bash
python3 sudoku_validator.py
```

Or import the function in your own code:

```python
from sudoku_validator import row_correct

# Test with your own Sudoku grid
my_sudoku = [[1, 2, 3, 0, 0, 0, 0, 0, 0], [0, 0, 0, 1, 1, 0, 0, 0, 0]]
print(row_correct(my_sudoku, 0))  # True - no duplicates
print(row_correct(my_sudoku, 1))  # False - duplicate 1s
```

---

## 🧪 Test Cases

```python
# Test case 1: Valid row with zeros
valid_row = [[1, 2, 3, 0, 0, 0, 0, 0, 0]]
print(row_correct(valid_row, 0))  # Output: True

# Test case 2: Invalid row with duplicates
invalid_row = [[1, 2, 3, 1, 0, 0, 0, 0, 0]]
print(row_correct(invalid_row, 0))  # Output: False

# Test case 3: All zeros (empty row)
empty_row = [[0, 0, 0, 0, 0, 0, 0, 0, 0]]
print(row_correct(empty_row, 0))  # Output: True

# Test case 4: Complete valid row
complete_row = [[1, 2, 3, 4, 5, 6, 7, 8, 9]]
print(row_correct(complete_row, 0))  # Output: True

# Test case 5: Multiple duplicates
multi_dup = [[5, 5, 5, 0, 0, 0, 0, 0, 0]]
print(row_correct(multi_dup, 0))  # Output: False (stops at first duplicate)
```

---

## ✨ Algorithm Design Decisions

This solution prioritizes **efficiency and clarity** through several key choices:

### **Early Termination Strategy**
- Returns `False` immediately upon finding the first duplicate
- Avoids unnecessary processing of remaining cells
- Optimal for invalid rows (common in puzzle validation)

### **Zero Handling Logic**
- `num > 0` condition elegantly handles empty cells
- Allows multiple zeros without triggering false positives
- Maintains Sudoku's incomplete puzzle representation

### **Linear Tracking Approach**
- Uses a simple list to track seen numbers
- `in` operator provides readable duplicate detection
- No need for complex data structures or external libraries

### **Single Responsibility**
- Function focuses solely on row validation
- Clear separation of concerns for modular design
- Easy to extend for column or block validation

---

## 🎯 Sudoku Validation Context

This function serves as a **building block** for complete Sudoku validation:

**Row Validation** (this function):
- Ensures no duplicate numbers 1-9 in any row
- Handles incomplete puzzles with zeros
- Foundation for puzzle integrity checking

**Future Extensions:**
- Column validation using similar logic
- 3×3 block validation for complete Sudoku rules
- Full puzzle validation combining all constraints

---

## 🔍 Alternative Approach

While the current implementation is efficient, here's another valid approach:

### Set-Based Approach:
```python
def row_correct_set(sudoku: list, row_no: int):
    row = sudoku[row_no]
    non_zero_numbers = [num for num in row if num > 0]
    return len(non_zero_numbers) == len(set(non_zero_numbers))
```

---

## 📚 Key Learning Outcomes

* **Sudoku game logic**: Understanding fundamental puzzle validation rules
* **Duplicate detection**: Efficient algorithms for finding repeated elements
* **Early termination**: Optimizing algorithms with strategic return points
* **List operations**: Using `in` operator and `append()` method effectively
* **Conditional logic**: Handling special cases (zeros) in data validation
* **Algorithm optimization**: Balancing readability with performance

---

## 🎓 Course

This project was completed as part of the **MOOC.fi Python Programming course**.
