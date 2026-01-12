# Python Numbers: In-Depth Notes

These notes cover the handling of numbers in Python, including internal representations, operations, and useful libraries like `math`, `random`, and `decimal`.

## 1. Types of Numbers

Python primarily deals with three types of numbers:

1. **Integers (`int`)**: Whole numbers (e.g., `2`, `-5`, `1000`).
    
2. **Floating Point Numbers (`float`)**: Numbers with decimal points (e.g., `2.5`, `3.14`, `0.0`).
    
3. **Complex Numbers (`complex`)**: Numbers with real and imaginary parts (e.g., `2 + 3j`).
    

> Internal Processing Python's number handling is robust. Unlike languages like C, integers in Python have arbitrary precision (they can be as large as your memory allows).

---

## 2. Basic Operations & Precedence

### Arithmetic Operators

Standard operators work as expected:

- `+` (Addition), `-` (Subtraction), `*` (Multiplication), `/` (Division - always returns float).
    
- `**` (Exponentiation/Power).
    
- `%` (Modulus/Remainder).
    

Python

```python
x = 2
y = 3
z = 4

print(x + y)    # 5
print(x * y)    # 6
print(x ** y)   # 8 (2 to the power of 3)
print(y % 2)    # 1 (Remainder)
```

### Operator Precedence (BODMAS/PEMDAS)

While Python follows standard mathematical precedence, **relying on it can lead to confusing code.**

- **Bad Practice:** `score = x + y * z` (Hard to read immediately)
    
- **Good Practice:** `score = x + (y * z)` (Explicit and readable)
    

> [!TIP] Production Tip Always use parentheses `()` to make your intentions clear. It prevents bugs and makes code reviews smoother.

### Mixing Types

When you mix integers and floats (e.g., `40 + 2.23`), Python automatically promotes the result to a `float` to preserve precision.

- **Explicit Type Casting:** It is better to convert types explicitly if you need a specific result.
    
    Python
    
    ```python
    a = 40
    b = 2.23
    
    # Implicit
    print(a + b)        # 42.23 (Float)
    
    # Explicit (Better if you specifically need an integer result)
    print(int(b))       # 2
    print(float(a))     # 40.0
    ```
    

---

## 3. Representations: `str()`, `repr()`, and `print()`

The video suggests exploring the difference between these three.

- `print()`: Displays the user-friendly output.
    
- `str()`: Returns the string version of the object (for users).
    
- `repr()`: Returns the "official" string representation (mostly for debugging/developers).
    

**Extra Example:**

Python

```python
import datetime
now = datetime.datetime.now()

print(str(now))  # 2024-02-03 10:00:00.123456 (Readable)
print(repr(now)) # datetime.datetime(2024, 2, 3, 10, 0, 0, 123456) (Unambiguous, code-like)
```

---

## 4. Comparisons & Chaining

Python allows chaining comparison operators, which is unique and powerful.

### Chained Comparison

Python

```python
x = 2
y = 3
z = 4

# This checks: (x < y) AND (y < z)
print(x < y < z)  # True
```

### The "And" vs "Or" Logic

- **AND**: Both conditions must be True.
    
- **OR**: At least one condition must be True.
    

**Tricky Interview Question Example:**

Python

```python
# What happens here?
print(1 == 2 < 3)
```

- Logic: It breaks down to `(1 == 2) and (2 < 3)`.
    
- Result: `False` and `True` → **`False`**.
    

---

## 5. Mathematical Libraries

### The `math` Module

Use this for standard mathematical functions.

- **`math.floor()`**: Rounds **down** to the nearest integer.
    
    - `math.floor(3.5)` → `3`
        
    - `math.floor(-3.5)` → `-4` (Moves left on the number line)
        
- **`math.trunc()`**: Truncates (cuts off) the decimal, moving towards zero.
    
    - `math.trunc(3.5)` → `3`
        
    - `math.trunc(-3.5)` → `-3` (Moves towards 0)
        

### The `random` Module

Essential for games, simulations, and testing.

Python

```python
import random

# Random integer between range
print(random.randint(1, 10)) 

# Choose a random item from a list
teas = ['Lemon', 'Masala', 'Ginger', 'Mint']
print(random.choice(teas))

# Shuffle a list in-place
random.shuffle(teas)
print(teas)
```

---

## 6. Precision & Special Number Types

### Floating Point Issues

Floats in computers are binary approximations.

Python

```python
print(0.1 + 0.1 + 0.1) 
# Output: 0.30000000000000004 (Not exactly 0.3!)
```

### The `decimal` Module

Used for financial calculations where exact precision is required.

Python

```python
from decimal import Decimal

d = Decimal('0.1') + Decimal('0.1') + Decimal('0.1')
print(d) # 0.3 (Correct precision)
```

> [!WARNING] Always pass numbers as **strings** `'0.1'` to `Decimal()` to avoid inheriting the floating-point error initially.

### The `fractions` Module

Handles fractional arithmetic exactly.

Python

```python
from fractions import Fraction

f = Fraction(2, 7)
print(f) # 2/7
```

---

## 7. Sets

Sets are unordered collections of **unique** elements. They are mathematically powerful.

- **Syntax**: `my_set = {1, 2, 3, 4}`
    
- **Empty Set Trap**: `{}` creates a Dictionary. Use `set()` to create an empty set.
    

### Set Operations

Python

```python
s1 = {1, 2, 3, 4}
s2 = {3, 4, 5, 6}

# Union (All unique elements): |
print(s1 | s2) # {1, 2, 3, 4, 5, 6}

# Intersection (Common elements): &
print(s1 & s2) # {3, 4}

# Difference (Elements in s1 but not s2): -
print(s1 - s2) # {1, 2}
```

---

## 8. Number Systems (Binary, Octal, Hex)

Python can handle different bases easily.

|System|Prefix|Example|
|---|---|---|
|**Binary** (Base 2)|`0b`|`0b1010`|
|**Octal** (Base 8)|`0o`|`0o20`|
|**Hexadecimal** (Base 16)|`0x`|`0xFF`|

Export to Sheets

**Conversion Functions:**

Python

```python
x = 64
print(bin(x))  # '0b1000000'
print(oct(x))  # '0o100'
print(hex(x))  # '0x40'

# Convert back to integer
print(int('0x40', 16)) # 64
```

---

## 9. Booleans as Numbers

In Python, `True` and `False` are actually specialized integers.

- `True` == `1`
    
- `False` == `0`
    

**Weird Python Behavior:**

Python

```python
print(True + 5)  # Output: 6
print(False * 10) # Output: 0
```

- `True is 1` → `False` (Values are equal, but they are different types/objects in memory).
    
- `True == 1` → `True`.
    

---

## 10. Extra Examples (For Students)

### Example 1: Large Numbers

Python handles massive numbers automatically without overflow errors (unlike C++ or Java).

Python

```python
# Try this!
print(2 ** 100) 
# Output: 1267650600228229401496703205376
```

### Example 2: Complex Numbers

Useful for electrical engineering or physics simulations.

Python

```python
c = 2 + 3j
print(c.real) # 2.0
print(c.imag) # 3.0
print(c * 2)  # (4+6j)
```

### Example 3: Finding Even/Odd (Modulus)

A classic use of the `%` operator.

Python

```python
num = 15
if num % 2 == 0:
    print("Even")
else:
    print("Odd")
```