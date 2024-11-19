# Working with Numbers in Python

## Understanding Floating-Point Numbers

Floating-point numbers represent real numbers and consist of:
- A **sign** (positive or negative)
- A **decimal value** for significant digits
- An **optional exponent** (scientific notation)

#### Characteristics of Floating-Point Numbers:
- They have a limited number of significant digits.
- Floating-point numbers are often approximations, which can lead to rounding errors or precision issues.

### Examples of Floating-Point Numbers

```python
positive_float = 21.5         # a positive float value
negative_float = -124.82      # a negative float value
scientific_notation = -3.7e-9 # equivalent to -0.0000000037 (using scientific notation)
```

### Using Scientific Notation in Python
Scientific notation is useful for expressing very large or very small numbers concisely.

```python
value1 = 2.38E+5    # 2.38 * 10**5 = 238000.0
value2 = 3.25E-8    # 3.25 * 10**(-8) = 0.0000000325
print(value1, value2)
# Output: 238000.0 3.25e-08
```

## Common Floating-Point Errors
Floating-point numbers can sometimes lead to unexpected results due to precision limitations:

```python
>>> balance = 100.10
>>> balance += 100.10
>>> balance += 100.10
>>> balance
300.29999999999995
```

**Explanation**: The expected value was `300.3`, but due to floating-point precision, we get a slightly different result.

### Fixing Floating-Point Errors Using `round()`
To mitigate floating-point errors, you can round the result to a specified number of decimal places:

```python
balance = round(balance, 2)
print(balance)
# Output: 300.3
```

## The `math` Module
Python's `math` module provides several functions for mathematical operations.

### Common Functions in the `math` Module

1. `pow(num, power)`: Raises the number to the specified power.
2. `sqrt(num)`: Returns the square root of the number.
3. `ceil(num)`: Rounds the number up to the nearest integer.
4. `floor(num)`: Rounds the number down to the nearest integer.
5. `fabs(num)`: Returns the absolute value of a floating-point number.

### Example: Using `pow()` and `sqrt()`

```python
import math as m

result1 = m.pow(2, 3)        # 8.0 (2 raised to the power of 3)
result2 = m.sqrt(16)         # 4.0 (square root of 16)
result3 = m.pow(125, 1/3)    # ~4.999999999999999 (cube root of 125)
print(result1, result2, result3)
# Output: 8.0 4.0 4.999999999999999
```

### Using Constants in math Module

The `math` module also includes useful constants like `pi`:

```python
radius = 12
circumference = m.pi * radius * 2   # 75.39822368615503
area = m.pi * radius**2             # 452.3893421169302
print(circumference, area)
```

### Using `ceil()` and `floor()` for Decimal Precision

```python
result = m.ceil(2.0083 * 100) / 100      # 2.01
result2 = m.floor(2.0083 * 100) / 100    # 2.0
print(result, result2)
```

## Formatting Numbers with `format()`

Python provides the `format()` method for formatting numbers and strings.

### Syntax for `format()`

```python
"{:format_spec}".format(value)
```

### Common Type Codes for Formatting
- `d`: Integer (no decimal places allowed)
- `f`: Floating-point number (decimal places can be specified)
- `%`: Percent (multiplies by 100 and appends a '%' symbol)
- `e`: Scientific notation

### Examples of Formatting Numbers

```python
a = 12345.6789

# Formatting with floating-point type
print("{:15,.4f}".format(a))   # '    12,345.6789'
print("{:15.2f}".format(a))    # '       12345.68'
print("{:.2e}".format(a))      # '1.23e+04'

# Formatting integers with thousands separator
b = 12345
print("{:8,d}".format(b))      # '  12,345'

# Formatting percentages
c = 0.12345
print("{:.2%}".format(c))      # '12.35%'
```

### Aligning Text and Numbers

By default, numbers are right-aligned, and strings are left-aligned. You can adjust alignment using `<`, `>`, and `^`:

```python
print("{:<15} {:>10} {:^5}".format("Item", "Price", "Qty"))
print("{:<15} {:>10.2f} {:^5d}".format("Mobile", 15000.0, 3))
```

### Output:

```mathematica
Item               Price   Qty 
Mobile          15000.00   3  
```

## Using the locale Module for Number Formatting

Python's `locale` module allows formatting numbers according to different regional settings.

### Setting Up Locale

```python
import locale as lc

# Set to US English locale
lc.setlocale(lc.LC_ALL, 'en_US.UTF-8')

# Format numbers as currency
print(lc.currency(12345.67, grouping=True))  # Output: $12,345.67
```

### Using `locale.format()` for Numbers

```python
print(lc.format("%d", 12345, grouping=True))     # 12,345
print(lc.format("%.2f", 12345.67, grouping=True)) # 12,345.67
```

## Fixing Rounding Errors in Financial Calculations

When dealing with financial calculations, ensure accurate results by rounding to two decimal places.

### Incorrect Code Example

```python
order_total = float(input("Enter order total: "))
if order_total > 0 and order_total < 100:
    discount_percent = 0
elif order_total >= 100 and order_total < 250:
    discount_percent = 0.1
elif order_total >= 250:
    discount_percent = 0.2

discount = order_total * discount_percent
subtotal = order_total - discount
sales_tax = subtotal * 0.05
invoice_total = subtotal + sales_tax
```

### Corrected Code with Rounding
```python
discount = round(order_total * discount_percent, 2)
subtotal = round(order_total - discount, 2)
sales_tax = round(subtotal * 0.05, 2)
invoice_total = round(subtotal + sales_tax, 2)

print(f"Subtotal: ${subtotal:.2f}, Sales Tax: ${sales_tax:.2f}, Total: ${invoice_total:.2f}")
```
