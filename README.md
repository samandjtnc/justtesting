### Question 1: Reading and Writing to Files

Write a Python program that reads a text file containing student names and their grades (formatted as `Name,Grade` on each line) and writes a new file with each student’s name and their grade increased by 5 points. The program should accept both the input and output filenames as command-line arguments. For simplicity, assume valid input and that grades do not exceed 100 after the increase.

---

### Question 2: Command-Line Argument Parsing

Create a Python script that calculates the sum, product, and average of a list of integers provided as command-line arguments. If the user does not supply any numbers, print an error message indicating that at least one number is required.

*Example:*  
```python
# Command:
>>> %Run stats_calculator.py 4 7 10
# Expected Output:
Sum: 21
Product: 280
Average: 7.0
```

---

### Question 3: Understanding Python Memory Model

Given the following code, describe the memory references created, especially how variables `a`, `b`, and `c` are related in memory after the final assignment.

```python
a = [1, 2, 3]
b = a
c = a[:]
a.append(4)
b[0] = 10
c[1] = 20
```

Explain the values of `a`, `b`, and `c` after these operations and the reason for each.

---

### Question 4: Appropriate Data Structures

Identify the most appropriate data structure (list, set, dictionary, tuple) to use for each scenario and briefly explain why:

a) Representing a deck of cards, where each card is unique  
b) Storing a phone directory that maps each name to a phone number  
c) Keeping track of items in a grocery store, where some items may be repeated in different sections  
d) Representing a single chess board position as coordinates of pieces  

---

### Question 5: Working with Sets

Write a function `unique_items` that takes two lists of items and returns a set containing only those items that appear in both lists. For example, `unique_items([1, 2, 3, 4], [3, 4, 5, 6])` should return `{3, 4}`.

---

### Question 6: Dictionary Manipulation

Write a function `add_prefix` that takes a dictionary of names as keys and email addresses as values, along with a prefix string. The function should return a new dictionary with the prefix added to the beginning of each email address.

*Example:*  
```python
>>> add_prefix({"John": "john@example.com", "Jane": "jane@example.com"}, "dept-")
{'John': 'dept-john@example.com', 'Jane': 'dept-jane@example.com'}
```

---

### Question 7: Recursive Function Analysis

Analyze the following function and explain in one or two sentences what it does, given that `n` is a positive integer:

```python
def sum_digits(n):
    if n < 10:
        return n
    else:
        return n % 10 + sum_digits(n // 10)
```

---

### Question 8: Recursive Patterns with Turtle Graphics

Using Turtle graphics, predict what shape would be drawn by the following function when called as `draw_pattern(200, 3)`, assuming the turtle starts at the origin facing right.

```python
def draw_pattern(side, depth):
    if depth == 0:
        return
    for i in range(4):
        forward(side)
        right(90)
    forward(side / 2)
    draw_pattern(side / 2, depth - 1)
```

Describe the overall pattern that would appear on the screen.

---

### Question 9: Recursive List Filtering

Write a recursive function `only_positive` that takes a list of integers and returns a new list containing only the positive numbers from the original list.

*Example:*  
```python
>>> only_positive([-1, 0, 5, -3, 2])
[5, 2]
```

---

### Question 10: Debugging Recursive Code

The following function is supposed to calculate the factorial of a given integer `n`. However, it contains an error. Identify and correct the error.

```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 2)
```

Explain why this error occurs.

---

### Question 11: Object-Oriented Programming - Class with Custom Methods

Implement a class `Counter` that keeps track of the number of times `increment` and `decrement` methods are called. It should also provide a `current` method that returns the current count and a `reset` method that sets the count back to zero.

*Example:*  
```python
>>> c = Counter()
>>> c.increment()
>>> c.increment()
>>> c.current()
2
>>> c.decrement()
>>> c.current()
1
>>> c.reset()
>>> c.current()
0
```

---

### Question 12: Extending Classes - Advanced OOP

Extend the `Counter` class from the previous question to create a `LimitCounter` that has an additional attribute `limit`. The `increment` method should stop incrementing when the count reaches this limit, and the `decrement` method should stop when the count reaches zero.

*Example:*  
```python
>>> lc = LimitCounter(limit=3)
>>> lc.increment()
>>> lc.increment()
>>> lc.increment()
>>> lc.increment()
>>> lc.current()
3
>>> lc.decrement()
>>> lc.current()
2
>>> lc.decrement()
>>> lc.decrement()
>>> lc.decrement()
>>> lc.current()
0
```

---

**End of Practice Exam**

---

**Solutions**

---

### Question 1: Solution

```python
import sys

def increase_grades(input_filename, output_filename):
    with open(input_filename, 'r') as infile, open(output_filename, 'w') as outfile:
        for line in infile:
            name, grade = line.strip().split(',')
            new_grade = min(100, int(grade) + 5)  # Cap the grade at 100
            outfile.write(f"{name},{new_grade}\n")

if __name__ == "__main__":
    increase_grades(sys.argv[1], sys.argv[2])
```

---

### Question 2: Solution

```python
import sys

def calculate_stats(numbers):
    if not numbers:
        print("Error: Please provide at least one number.")
        return
    total = sum(numbers)
    product = 1
    for num in numbers:
        product *= num
    average = total / len(numbers)
    print(f"Sum: {total}")
    print(f"Product: {product}")
    print(f"Average: {average}")

if __name__ == "__main__":
    args = [int(arg) for arg in sys.argv[1:]]
    calculate_stats(args)
```

---

### Question 3: Solution

**Explanation**:
- `a` and `b` refer to the same list in memory.
- `c` is a shallow copy of `a`, so it’s a new list but shares references to the inner items of `a`.
- Modifying `a` will affect `b` since they point to the same object, but `c` will remain partially unaffected.

Final values:
- `a = [10, 2, 3, 4]`
- `b = [10, 2, 3, 4]` (same as `a`)
- `c = [1, 20, 3]` (independent copy)

---

### Question 4: Solution

a) Set – to ensure each card is unique.  
b) Dictionary – to map names to phone numbers.  
c) List – allows for repeated items and ordering.  
d) Tuple – immutable and compact for storing a fixed set of coordinates.

---

### Question 5: Solution

```python
def unique_items(list1, list2):
    return set(list1) & set(list2)
```

*Example:*  
```python
>>> unique_items([1, 2, 3, 4], [3, 4, 5, 6])
{3, 4}
```

---

### Question 6: Solution

```python
def add_prefix(email_dict, prefix):
    return {name: f"{prefix}{email}" for name, email in email_dict.items()}
```

*Example:*  
```python
>>> add_prefix({"John": "john@example.com", "Jane": "jane@example.com"}, "dept-")
{'John': 'dept-john@example.com', 'Jane': 'dept-jane@example.com'}
```

---

### Question 7: Solution

This function calculates the sum of the digits of `n`.

---

### Question 8: Solution

The function `draw_pattern(200, 3)` will draw a fractal pattern of nested squares. Each successive square is half the size of the previous one, creating a recursive pattern with depth.

---

### Question 9: Solution

```python
def only_positive(numbers):
    if not numbers:
        return []
    if numbers[0] > 0:
        return [numbers[0]] + only_positive(numbers[1:])
    else:
        return only_positive(numbers[1:])
```

*Example:*  
```python
>>> only_positive([-1, 0, 5, -3, 2])
[5, 2]
```

---

### Question 10: Solution

**Error**: The code incorrectly calls `factorial(n - 2)` instead of `factorial(n - 1)`. This will skip values and cause an incorrect result.

**Corrected Code**:
```python
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```

---

### Question 11: Solution

```python
class Counter:
    def __init__(self):
        self.count = 0

    def increment(self):
        self.count += 1

    def decrement(self):
        if self.count > 0:
            self.count -= 1

    def current(self):
        return self.count

    def reset(self):
        self.count = 0
```

*Example:*
```python
>>> c = Counter()
>>> c.increment()
>>> c.increment()
>>> c.current()  # 2
>>> c.decrement()
>>> c.current()  # 1
>>> c.reset()
>>> c.current()  # 0
```

---

### Question 12: Solution

```python
class LimitCounter(Counter):
    def __init__(self, limit):
        super().__init__()
        self.limit = limit

    def increment(self):
        if self.count < self.limit:
            self.count += 1

    def decrement(self):
        if self.count > 0:
            self.count -= 1
```

*Example:*  
```python
>>> lc = LimitCounter(limit=3)
>>> lc.increment()
>>> lc.increment()
>>> lc.increment()
>>> lc.increment()  # Should stop incrementing at limit
>>> lc.current()  # 3
>>> lc.decrement()
>>> lc.current()  # 2
>>> lc.decrement()
>>> lc.decrement()
>>> lc.decrement()  # Should stop decrementing at zero
>>> lc.current()  # 0
```


