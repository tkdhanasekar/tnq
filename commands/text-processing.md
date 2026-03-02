<details>
 <summary>sed</summary>
 
sed (Stream EDitor) is a powerful Linux command-line tool used to search, filter, transform, and edit text in files or input streams.

It works line-by-line and is commonly used for:

Text replacement

Deleting lines

Inserting text

Filtering logs

Batch file editing

Basic Syntax
```
sed [options] 'command' filename
```
**`sed` command examples**

## Replace Text in a File

```bash
sed 's/apple/orange/' hello.txt
```

**What it does:**
Replaces the **first occurrence** of `apple` with `orange` on each line.

Replace **all occurrences** in each line:

```bash
sed 's/apple/orange/g' file.txt
```

---

## Replace Text and Save Changes (In-Place Editing)

```bash
sed -i 's/foo/bar/g' hello.txt
```

**What it does:**
Replaces all `foo` with `bar` directly inside `file.txt`.

Create a backup before editing:

```bash
sed -i.bak 's/foo/bar/g' hello.txt
```

This creates `hello.txt.bak`.

---

## Delete Specific Lines

Delete line 3:

```bash
sed '3d' hello.txt
```

Delete lines 2 to 4:

```bash
sed '2,4d' hello.txt
```

Delete lines containing a word:

```bash
sed '/error/d' hello.txt
```

---

## Print Specific Lines

Print only line 4:

```bash
sed -n '4p' hello.txt
```

Print lines 2 through 6:

```bash
sed -n '2,6p' hello.txt
```

> `-n` suppresses automatic printing.

---

## Insert or Append Text

Insert text before line 3:

```bash
sed '3i\New Line Inserted' hello.txt
```

Append text after line 3:

```bash
sed '3a\New Line Added After' hello.txt
```

Replace an entire line:

```bash
sed '3c\This is the new line content' hello.txt
```
</details>
<details>
 <summary>awk</summary>
 
## `awk` Command in Linux

`awk` is a powerful **text-processing and pattern-scanning** tool in Linux.
It is mainly used for:

* Processing structured text (like logs, CSV, tables)
* Searching for patterns
* Performing calculations
* Generating reports

`awk` works **column-wise** (field-based processing), which makes it very powerful for handling tabular data.

---

# Basic Syntax

```bash
awk 'pattern { action }' filename
```

Example:

```bash
awk '{print $1}' hello.txt
```

Prints the **first column** of each line.

---

# 🔹 Important Built-in Variables

| Variable        | Meaning                          |
| --------------- | -------------------------------- |
| `$1, $2, $3...` | Field (column) numbers           |
| `$0`            | Entire line                      |
| `NR`            | Current line number              |
| `NF`            | Number of fields in current line |
| `FS`            | Field separator                  |
| `OFS`           | Output field separator           |

**`awk` command examples** 

## Print a Specific Column

Print the first column from a file:

```bash
awk '{print $1}' file.txt
```

`$1` = first field (column)
`$0` = entire line

---

## Print Multiple Columns

Print first and third columns:

```bash
awk '{print $1, $3}' file.txt
```

Change output separator:

```bash
awk 'BEGIN {OFS=" - "} {print $1, $3}' file.txt
```

---

## Use Custom Field Separator (CSV Example)

For comma-separated file:

```bash
awk -F ',' '{print $1, $2}' file.csv
```

 `-F ','` sets field separator to comma.

---

## Filter Rows Based on Condition

Print rows where 3rd column is greater than 100:

```bash
awk '$3 > 100' file.txt
```

Print rows where first column equals "admin":

```bash
awk '$1 == "admin"' file.txt
```

---

## Calculate Sum of a Column

Sum of second column:

```bash
awk '{sum += $2} END {print "Total:", sum}' file.txt
```

---

# Example File (`sales.txt`)

```
John 100
Mary 200
David 150
Alex 250
```

Here:

* Column 1 → Name
* Column 2 → Sales amount

---

# Run the Command

```bash
awk '{sum += $2} END {print "Total:", sum}' sales.txt
```

---

# 🔍 How It Works

### Step 1: `{sum += $2}`

* `$2` → second column (sales amount)
* `sum += $2` → adds each value to variable `sum`

Processing line by line:

| Line      | $2 Value | Running Total |
| --------- | -------- | ------------- |
| John 100  | 100      | 100           |
| Mary 200  | 200      | 300           |
| David 150 | 150      | 450           |
| Alex 250  | 250      | 700           |

---

### Step 2: `END {print "Total:", sum}`

* `END` block runs **after all lines are processed**
* Prints the final total

---

# Output

```
Total: 700
```

---

# 💡 Bonus: With CSV File

If file is comma-separated:

```
John,100
Mary,200
David,150
Alex,250
```

Use:

```bash
awk -F ',' '{sum += $2} END {print "Total:", sum}' sales.csv
```

---

# Why This Is Useful

* Calculate total salary
* Add sales amounts
* Sum CPU usage from logs
* Count totals in reports

---

## Print Line Numbers

```bash
awk '{print NR, $0}' hello.txt
```

`NR` = current record (line) number.

---

# Use with Pipe

Example with `ps` command:

```bash
ps aux | awk '{print $1, $3}'
```

Prints user and CPU usage.

---

# `awk` vs `sed`

| `awk`                   | `sed`                    |
| ----------------------- | ------------------------ |
| Column-based processing | Line-based processing    |
| Supports arithmetic     | Mainly text replacement  |
| Better for reports      | Better for substitutions |

---

# Why `awk` is Important?

* Powerful for log analysis
* Great for CSV processing
* Used in DevOps & automation
</details>
