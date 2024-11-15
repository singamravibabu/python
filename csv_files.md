# Working with CSV Files in Python

A **Comma-Separated Values (CSV)** file is a common text file format used to store tabular data. Each line in a CSV file represents a row of data, and each row consists of one or more columns separated by commas. The CSV format is widely used due to its simplicity and compatibility with various applications like Microsoft Excel, Google Sheets, and database systems.

#### Key Concepts:
- **Rows** (or **Records**): Each line in the file, representing a single entry or record.
- **Columns** (or **Fields**): Values within a row, separated by commas.

Python provides a built-in `csv` module that makes working with CSV files straightforward, offering functionality to both read from and write to CSV files.

## Writing Data to a CSV File

To write data into a CSV file, we use the `csv.writer()` function from the `csv` module. This function returns a **CSV writer object** that is used to convert Python data into the CSV format.

### Importing the CSV Module

Before we can write or read CSV files, we need to import the `csv` module:

```python
import csv
```

### The `writer()` Function

```python
csv.writer(file)
```

- **Purpose**: Creates a CSV writer object for the specified file.
- **Returns**: A writer object that converts data into comma-separated values for writing.

### Writing Data using the `writerows()` Method

Once we have a writer object, we can use the `writerows()` method to write multiple rows of data at once.

```python
writerows(rows)
```

- **Purpose**: Writes all specified rows to the file using the CSV format.
- **Parameters**: `rows` - A list of rows to be written, where each row is a list of column values.

#### Example: Writing a 2D List to a CSV File

Let's create a 2-dimensional list containing book details (title, price, and quantity):

```python
books = [
    ["Attitude", 150.00, 130],
    ["One Minute Manager", 199.00, 90],
    ["Leader", 300.00, 240],
    ["Manager's Manual", 1500.00, 900],
    ["Word Smart", 750.00, 400]
]

# Writing the list to a CSV file
with open("C:\\Sample\\books.csv", "w", newline="") as file:
    writer_obj = csv.writer(file)
    writer_obj.writerows(books)
```

#### Explanation:

- We used the `open()` function with the `"w"` mode to open the file for writing.
- The `newline=""` argument prevents adding extra blank lines between rows on Windows systems.
- The `writerows()` method writes all the rows from our `books` list into the file.

### Writing Data Row by Row using `writerow()`

If you want to write rows one at a time, use the `writerow()` method:

```python
with open("C:\\Sample\\books.csv", "w", newline="") as file:
    writer_obj = csv.writer(file)
    writer_obj.writerow(["Title", "Price", "Quantity"])  # Writing header
    for book in books:
        writer_obj.writerow(book)
```

## Reading Data from a CSV File

To read data from a CSV file, we use the `csv.reader()` function. This returns a **CSV reader object**, which we can iterate over to access each row of data.

### The reader() Function

```python
csv.reader(file)
```

- **Purpose**: Creates a CSV reader object for the specified file.
- **Returns**: A reader object that retrieves data from the CSV file.

### Example: Reading Data from a CSV File

```python
with open("C:\\Sample\\books.csv", newline="") as file:
    reader_obj = csv.reader(file)
    for row in reader_obj:
        print(row)
```

#### Output:

```css
['Attitude', '150.0', '130']
['One Minute Manager', '199.0', '90']
['Leader', '300.0', '240']
['Manager's Manual', '1500.0', '900']
['Word Smart', '750.0', '400']
```

### Accessing Specific Columns

To read specific columns from each row, you can index into the list:

```python
with open("C:\\Sample\\books.csv", newline="") as file:
    reader_obj = csv.reader(file)
    for row in reader_obj:
        print(f"{row[0]} ({row[2]} copies)")
```

#### Output:

```scss
Attitude (130 copies)
One Minute Manager (90 copies)
Leader (240 copies)
Manager's Manual (900 copies)
Word Smart (400 copies)
```

## CSV Format Specifications

By default, the CSV module uses commas to separate columns and only quotes columns when necessary. However, you can customize this behavior using optional parameters.

### Optional Parameters for `csv.reader()` and `csv.writer()`

| Parameter	| Description	| Default	|
|---------------|---------------|---------------|
| `delimiter`	| Character used to separate fields.	| `,` (comma) |
| `quotechar`	| Character used to quote fields containing special characters (like `,` or `\n`).	| `"` (double-quote) |
| `quoting`	| Controls when quotes are used. Options include `csv.QUOTE_MINIMAL`, `csv.QUOTE_ALL`, `csv.QUOTE_NONNUMERIC`, and `csv.QUOTE_NONE`.	| `csv.QUOTE_MINIMAL` |

### Example: Changing the Delimiter to a Tab Character

```python
with open("C:\\Sample\\books_tab.csv", "w", newline="") as file:
    writer_obj = csv.writer(file, delimiter="\t")
    writer_obj.writerows(books)
```

### Reading a CSV File with a Custom Delimiter

```python
with open("C:\\Sample\\books_tab.csv", newline="") as file:
    reader_obj = csv.reader(file, delimiter="\t")
    for row in reader_obj:
        print(row)
```

## Notes on Working with CSV Files

- **Universal Newlines Mode**: When opening a CSV file, always include `newline=""` to handle different newline characters across platforms.
- **Data Type Handling**: The `csv.reader()` reads all values as strings by default. You may need to convert data types explicitly, e.g., `int(row[2])` for numerical data.

By using Python's `csv` module, you can efficiently read and write CSV files, making it easier to work with tabular data in various applications.