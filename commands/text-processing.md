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
<details>
 <summary>sort</summary>
 
## `sort` Command (One-Liner)

**`sort`** is a Linux command used to arrange lines of text files in alphabetical, numerical, or custom order.

---

# Example 1: Basic Alphabetical Sort

### File: `names.txt`

```
John
Alex
David
Mary
```

### Command:

```bash
sort names.txt
```

### Output:

```
Alex
David
John
Mary
```

Default sorting is alphabetical (A–Z).

---

# Example 2: Numeric Sort

### File: `numbers.txt`

```
50
5
100
20
```

### Command:

```bash
sort -n numbers.txt
```

### Output:

```
5
20
50
100
```

`-n` sorts numerically (not alphabetically).

---

# Example 3: Reverse Sort

### File: `names.txt`

```
John
Alex
David
Mary
```

### Command:

```bash
sort -r names.txt
```

### Output:

```
Mary
John
David
Alex
```

`-r` sorts in reverse order (Z–A).

---

# Example 4: Sort by Column

### File: `marks.txt`

```
John 85
Mary 92
David 78
Alex 88
```

### Command (Sort by 2nd column numerically):

```bash
sort -k2 -n marks.txt
```

### Output:

```
David 78
John 85
Alex 88
Mary 92
```

`-k2` → sort by 2nd column
`-n` → numeric sorting

---

## Remove Duplicates Using `sort` Command

We use the `-u` option with `sort` to remove duplicate lines.

---

# Example File: `fruits.txt`

```
apple
banana
orange
apple
banana
grapes
```

---

# Command

```bash
sort -u fruits.txt
```

---

# Output

```
apple
banana
grapes
orange
```

`-u` = **unique** (removes duplicate lines)
It also sorts the output alphabetically.

---

# Example with Unsorted File

### File: `numbers.txt`

```
5
2
8
5
2
1
```

### Command:

```bash
sort -u numbers.txt
```

### Output:

```
1
2
5
8
```
</details>
<details>
 <summary>uniq</summary>

`uniq` is a Linux command used to **filter out or report consecutive duplicate lines** from a file or input.

---

# Example 1: Remove Adjacent Duplicates

### File: `fruits.txt`

```
apple
apple
banana
orange
orange
banana
grapes
```

### Command:

```bash
uniq fruits.txt
```

### Output:

```
apple
banana
orange
banana
grapes
```

> Note: Only **adjacent duplicates** are removed.

---

# Example 2: Count Occurrences of Each Line

### File: `fruits.txt` (same as above)

### Command:

```bash
uniq -c fruits.txt
```

### Output:

```
      2 apple
      1 banana
      2 orange
      1 banana
      1 grapes
```

> `-c` prints the number of occurrences for each line.

---

# Example 3: Remove Duplicates After Sorting

### File: `numbers.txt`

```
5
2
8
5
2
1
```

### Command:

```bash
sort numbers.txt | uniq
```

### Output:

```
1
2
5
8
```

> `uniq` alone only works on adjacent duplicates; `sort` ensures duplicates are together.

---

# Example 4: Show Only Duplicate Lines

### File: `fruits.txt` (same as above)

### Command:

```bash
uniq -d fruits.txt
```

### Output:

```
apple
orange
```

> `-d` shows only lines that are repeated **consecutively**.

---

# Example 5: Show Only Unique Lines

### File: `fruits.txt` (same as above)

### Command:

```bash
uniq -u fruits.txt
```

### Output:

```
banana
banana
grapes
```

> `-u` prints only lines that appear **once consecutively**.
</details>
<details>
 <summary>paste</summary>

The `paste` command in Linux is used to **merge lines of files horizontally**, joining corresponding lines from multiple files with a delimiter (default is a tab).

---

# Example 1: Merge Two Files Side by Side

### File 1: `names.txt`

```
John
Mary
David
Alex
```

### File 2: `marks.txt`

```
85
92
78
88
```

### Command:

```bash
paste names.txt marks.txt
```

### Output:

```
John    85
Mary    92
David   78
Alex    88
```

> Default delimiter is a **tab**.

---

# Example 2: Merge with Custom Delimiter

### Command:

```bash
paste -d "," names.txt marks.txt
```

### Output:

```
John,85
Mary,92
David,78
Alex,88
```

> `-d ","` sets the delimiter to a comma.

---

# Example 3: Merge More Than Two Files

### File 3: `grades.txt`

```
A
A
B
B
```

### Command:

```bash
paste names.txt marks.txt grades.txt
```

### Output:

```
John    85  A
Mary    92  A
David   78  B
Alex    88  B
```

---

# Example 4: Use Multiple Delimiters

### Command:

```bash
paste -d ",:" names.txt marks.txt grades.txt
```

### Output:

```
John,85:A
Mary,92:A
David,78:B
Alex,88:B
```

> Delimiters cycle through the list `, :` for each file column.

---

# Example 5: Merge Files Line by Line (Serial Mode)

### Command:

```bash
paste -s names.txt
```

### Output:

```
John    Mary    David   Alex
```

> `-s` merges all lines of a single file **serially** instead of column-wise.
</details>
<details>
 <summary>join</summary>

The `join` command in Linux is used to **combine lines from two files based on a common field (key column)**, similar to SQL joins.

---

# Example 1: Basic Join on First Column

### File 1: `students.txt`

```
1 John
2 Mary
3 David
4 Alex
```

### File 2: `marks.txt`

```
1 85
2 92
3 78
4 88
```

### Command:

```bash
join students.txt marks.txt
```

### Output:

```
1 John 85
2 Mary 92
3 David 78
4 Alex 88
```

> Default join is on **first column** of both files.

---

# Example 2: Join on a Different Column

### File 1: `students.txt`

```
John 1
Mary 2
David 3
Alex 4
```

### File 2: `marks.txt`

```
1 85
2 92
3 78
4 88
```

### Command:

```bash
join -1 2 -2 1 students.txt marks.txt
```

### Output:

```
1 John 85
2 Mary 92
3 David 78
4 Alex 88
```

> `-1 2` → use 2nd column of file1 as key
> `-2 1` → use 1st column of file2 as key

---

# Example 3: Join with a Custom Delimiter

### File 1: `students.csv`

```
1,John
2,Mary
3,David
4,Alex
```

### File 2: `marks.csv`

```
1,85
2,92
3,78
4,88
```

### Command:

```bash
join -t ',' students.csv marks.csv
```

### Output:

```
1,John,85
2,Mary,92
3,David,78
4,Alex,88
```

> `-t ','` sets the delimiter to a comma.

---

# Example 4: Include All Lines from First File

### Command:

```bash
join -a 1 students.txt marks.txt
```

> `-a 1` prints lines from **file1** even if there’s no matching key in file2.

---

# Example 5: Output Only Selected Fields

### Command:

```bash
join -o 1.2,2.2 students.txt marks.txt
```

### Output:

```
John 85
Mary 92
David 78
Alex 88
```

> `-o 1.2,2.2` prints 2nd field from file1 and 2nd field from file2.
</details>
<details>
 <summary>fold</summary>

The `fold` command in Linux is used to **wrap long lines of text to a specified width**, breaking lines at a set number of characters.

---

# Example 1: Wrap Lines at Default Width (80 characters)

### File: `text.txt`

```
This is a very long line of text that goes beyond the typical terminal width and needs to be wrapped properly.
```

### Command:

```bash
fold text.txt
```

### Output:

```
This is a very long line of text that goes beyond the typical terminal width and
needs to be wrapped properly.
```

> Default width is 80 characters.

---

# Example 2: Wrap Lines at 20 Characters

### Command:

```bash
fold -w 20 text.txt
```

### Output:

```
This is a very long
line of text that
goes beyond the
typical terminal
width and needs to
be wrapped properly.
```

> `-w 20` sets the line width to 20 characters.

---

# Example 3: Wrap Lines Without Breaking Words

### Command:

```bash
fold -s -w 20 text.txt
```

### Output:

```
This is a very long
line of text that
goes beyond the
typical terminal
width and needs to
be wrapped properly.
```

> `-s` breaks lines at **spaces** instead of mid-word.

---

# Example 4: Wrap a File and Save Output

### Command:

```bash
fold -w 30 text.txt > wrapped.txt
```

### File `wrapped.txt` Output:

```
This is a very long line of
text that goes beyond the
typical terminal width and
needs to be wrapped
properly.
```

> Output is redirected to a new file.

---

# Example 5: Wrap Multiple Files Together

### Files:

`file1.txt`

```
First file has some long text that needs wrapping.
```

`file2.txt`

```
Second file also has long text that should be folded.
```

### Command:

```bash
fold -w 25 file1.txt file2.txt
```

### Output:

```
First file has some long
text that needs wrapping.
Second file also has long
text that should be folded.
```

> `fold` can process multiple files at once.
</details>
<details>
 <summary>tee</summary>

The `tee` command in Linux **reads standard input and writes it simultaneously to standard output and one or more files**, allowing you to view and save output at the same time.

# Example 1: Write Output to a File

### Command:

```bash
echo "Hello World" | tee output.txt
```

### File `output.txt` Content:

```
Hello World
```

### Output to Terminal:

```
Hello World
```

> `tee` saves the output to `output.txt` and also displays it on the terminal.

---

# Example 2: Append to a File

### Command:

```bash
echo "New Line" | tee -a output.txt
```

### File `output.txt` After Append:

```
Hello World
New Line
```

> `-a` appends instead of overwriting.

---

# Example 3: Write Output to Multiple Files

### Command:

```bash
echo "Multi Save" | tee file1.txt file2.txt
```

### File Contents:

* `file1.txt` → `Multi Save`
* `file2.txt` → `Multi Save`

> `tee` can write to multiple files at once.

---

# Example 4: Use `tee` with Command Output

### File: `fruits.txt`

```
apple
banana
orange
apple
grapes
banana
```

### Command:

```bash
cat fruits.txt | tee fruits_copy.txt | sort
```

### Output to Terminal:

```
apple
banana
orange
apple
grapes
banana
```

### File `fruits_copy.txt` Content:

```
apple
banana
orange
apple
grapes
banana
```

> Output is **saved** to a file and **still sent to `sort`**.

---

# Example 5: Combine with `sudo` to Write to Protected File

```bash
echo "System Log Entry" | sudo tee /var/log/custom.log
```

> Normally, `>` redirection would fail without sudo; `tee` allows writing as superuser.

---

# Example 6: Monitor a Log File in Real-Time

### Command:

```bash
tail -f /var/log/syslog | tee syslog_copy.log
```

### How It Works:

1. `tail -f /var/log/syslog` → shows new log entries as they appear.
2. `tee syslog_copy.log` → writes the same output to `syslog_copy.log`.
3. You can **watch live output** while saving a copy for later.

---

# Example 7: Save and Monitor Script Output

### Command:

```bash
./long_script.sh | tee script_output.log
```

* All output from `long_script.sh` is **displayed on screen** and **saved** to `script_output.log`.
* Helpful if you want to **debug while logging**.

---

# Example 8: Append Instead of Overwriting

```bash
ping google.com | tee -a ping_log.txt
```

* `-a` ensures each run **appends** to the file instead of overwriting.
* You can **see live ping results** and save them for records.

---

# Example 9: Monitor and Filter Simultaneously

```bash
tail -f /var/log/apache2/access.log | grep "404" | tee errors.log
```

* Filters only **404 errors** in real-time.
* Displays them **live** and saves to `errors.log`.

---

# Example 10: Multiple Files at Once

```bash
top -b -n 1 | tee top_snapshot1.txt top_snapshot2.txt
```

* `top -b -n 1` runs `top` in batch mode once.
* `tee` writes the output to **multiple files simultaneously**.
</details>
<details>
 <summary>comm</summary>

The `comm` command in Linux **compares two sorted files line by line** and outputs lines that are unique to each file or common to both.

> **Important:** Files must be **sorted** before using `comm`.

# Example 1: Basic Comparison

### File 1: `file1.txt`

```
apple
banana
grapes
orange
```

### File 2: `file2.txt`

```
banana
kiwi
orange
pear
```

### Command:

```bash
comm file1.txt file2.txt
```

### Output:

```
apple
        banana
grapes
        kiwi
        orange
        pear
```

* Column 1 → lines only in file1
* Column 2 → lines only in file2
* Column 3 → lines common to both

---

# Example 2: Show Only Lines Unique to File1

```bash
comm -23 file1.txt file2.txt
```

### Output:

```
apple
grapes
```

> `-2 -3` hides columns 2 and 3.

---

# Example 3: Show Only Lines Unique to File2

```bash
comm -13 file1.txt file2.txt
```

### Output:

```
kiwi
pear
```

> `-1 -3` hides columns 1 and 3.

---

# Example 4: Show Only Common Lines

```bash
comm -12 file1.txt file2.txt
```

### Output:

```
banana
orange
```

> `-1 -2` hides columns 1 and 2, leaving only lines present in both files.

---

# Example 5: Ignore Case Differences

### Files:

`file1.txt`

```
Apple
Banana
Grapes
Orange
```

`file2.txt`

```
apple
banana
Kiwi
Orange
```

### Command:

```bash
comm -i file1.txt file2.txt
```

> `-i` ignores case differences (available in some versions of `comm`).

---

**Tip:** Always **sort files** first:

```bash
sort file1.txt -o file1.txt
sort file2.txt -o file2.txt
```

before using `comm`.
</details>
<details>
 <summary>cmp</summary>

The `cmp` command in Linux **compares two files byte by byte** and reports the first difference; it is mainly used for **binary or text file comparison**.

# Example 1: Basic Comparison

### File 1: `file1.txt`

```
Hello
World
```

### File 2: `file2.txt`

```
Hello
Linux
```

### Command:

```bash
cmp file1.txt file2.txt
```

### Output:

```
file1.txt file2.txt differ: byte 7, line 2
```

> Reports the **first differing byte and line**.

---

# Example 2: Silent Comparison (Check Only If Files Differ)

```bash
cmp -s file1.txt file2.txt
echo $?
```

### Output:

```
1
```

> `-s` suppresses output; `$?` returns `0` if files are identical, `1` if different.

---

# Example 3: Compare Binary Files

### Files:

`image1.png`
`image2.png`

### Command:

```bash
cmp image1.png image2.png
```

### Output (example):

```
image1.png image2.png differ: byte 1024, line 1
```

> `cmp` works on **text and binary files**.

---

# Example 4: Show All Differences with `-l`

```bash
cmp -l file1.txt file2.txt
```

### Output (example):

```
7 157 154
```

* Shows **byte position**, **octal value in file1**, **octal value in file2** for all differences.

---

# Example 5: Use in Scripts to Check File Integrity

```bash
if cmp -s backup.txt original.txt; then
    echo "Files are identical"
else
    echo "Files differ"
fi
```

### Output (if files differ):

```
Files differ
```

> Useful for automated verification or checksum comparisons.
</details>
<details>
 <summary>diff</summary>

The `diff` command in Linux **compares two files line by line** and outputs the differences between them, showing what needs to be changed to make the files identical.

# Example 1: Basic Comparison

### File 1: `file1.txt`

```
Hello
World
Linux
```

### File 2: `file2.txt`

```
Hello
World
Unix
```

### Command:

```bash
diff file1.txt file2.txt
```

### Output:

```
3c3
< Linux
---
> Unix
```

> `3c3` → line 3 changed, `<` = file1, `>` = file2.

---

# Example 2: Ignore Case Differences

```bash
diff -i file1.txt file2.txt
```

> `-i` ignores uppercase/lowercase differences.

---

# Example 3: Ignore White Spaces

```bash
diff -w file1.txt file2.txt
```

> `-w` ignores all whitespace differences.

---

# Example 4: Side-by-Side Comparison

```bash
diff -y file1.txt file2.txt
```

### Output:

```
Hello                   Hello
World                   World
Linux                  | Unix
```

> `-y` displays differences **side by side** for easier visual comparison.

---

# Example 5: Only Show Differences, Suppress Common Lines

```bash
diff --suppress-common-lines -y file1.txt file2.txt
```

### Output:

```
Linux                  | Unix
```

> Shows **only the differing lines**, ignoring lines that are the same.

---

**Tip:** For scripts, you can combine with `wc -l` or check exit codes:

```bash
diff file1.txt file2.txt > diff_output.txt
if [ $? -eq 0 ]; then
    echo "Files are identical"
else
    echo "Files differ"
fi
```
</details>
<details>
 <summary>sdiff</summary>

The `sdiff` command in Linux **displays differences between two files side by side**, showing which lines are unique to each file and which lines are common.

> Files should ideally be **sorted or aligned** for clear comparison.

---

# Example 1: Basic Side-by-Side Comparison

### File 1: `file1.txt`

```
apple
banana
grapes
orange
```

### File 2: `file2.txt`

```
banana
kiwi
orange
pear
```

### Command:

```bash
sdiff file1.txt file2.txt
```

### Output:

```
apple              | 
banana             banana
grapes             | kiwi
orange             orange
                   | pear
```

* `|` → line differs between files
* `<` → line only in left file
* `>` → line only in right file

---

# Example 2: Use Custom Column Width

```bash
sdiff -w 30 file1.txt file2.txt
```

* `-w 30` sets **maximum width** of the output columns for better readability.

---

# Example 3: Merge Interactively

```bash
sdiff -o merged.txt file1.txt file2.txt
```

* Opens an **interactive mode** allowing you to merge differences line by line.
* Result is saved to `merged.txt`.

---

# Example 4: Suppress Common Lines

```bash
sdiff -s file1.txt file2.txt
```

* `-s` suppresses lines that are identical in both files, showing **only differences**.

---

# Example 5: Compare Larger Files

### File 1: `students.txt`

```
1 John
2 Mary
3 David
4 Alex
```

### File 2: `marks.txt`

```
1 John
2 Mary
3 David
4 Alice
```

### Command:

```bash
sdiff students.txt marks.txt
```

### Output:

```
1 John           1 John
2 Mary           2 Mary
3 David          3 David
4 Alex           | 4 Alice
```

> Clearly shows that **line 4 differs** between the two files.

---

## **difference between `diff` and `sdiff`** in Linux:



## 1. Purpose

| Feature     | `diff`                                                                    | `sdiff`                                                                         |               |
| ----------- | ------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------- |
| Primary Use | Shows **line-by-line differences** between two files in a textual format. | Shows **differences side by side**, visually aligning the files for comparison. |               |
| Output Type | Textual instructions (e.g., `3c3` means line 3 changed).                  | Two columns showing left and right files with markers (`                        | `, `<`, `>`). |

---

## 2. Output Style

* **diff**:

```
3c3
< Linux
---
> Unix
```

* **sdiff**:

```
Linux         | Unix
```

> `diff` is more suitable for scripts or patch creation.
> `sdiff` is easier for humans to read and manually compare.

---

## 3. Interactivity

| Feature       | `diff` | `sdiff`                                      |
| ------------- | ------ | -------------------------------------------- |
| Merge Support |  No   | Can merge interactively using `-o` option. |

---

## 4. Use Cases

* **diff**:

  * Generate patches for version control.
  * Compare files in scripts.
  * Detect line differences programmatically.

* **sdiff**:

  * Manually inspect differences in files.
  * Merge files interactively.
  * Side-by-side comparison for reports.

---

## 5. Typical Commands

* `diff`:

```bash
diff file1.txt file2.txt
```

* `sdiff`:

```bash
sdiff file1.txt file2.txt
```

---

**Summary:**

* Use **`diff`** for scripting, automated comparison, or patch files.
* Use **`sdiff`** for **human-readable, side-by-side comparison** and interactive merging.

</details>
<details>
 <summary>fmt</summary>

The `fmt` command in Linux **formats text by adjusting line width**, wrapping long lines into neat, readable paragraphs.

> Unlike `fold`, `fmt` tries to break lines at **word boundaries** and maintains paragraph structure.

# Example 1: Basic Formatting

### File: `text.txt`

```
This is a very long line of text that should be wrapped properly to improve readability in a terminal.
```

### Command:

```bash
fmt text.txt
```

### Output:

```
This is a very long line of text that should be wrapped properly to
improve readability in a terminal.
```

> Default line width is 75 characters.

---

# Example 2: Set Custom Width

```bash
fmt -w 40 text.txt
```

### Output:

```
This is a very long line of text that
should be wrapped properly to improve
readability in a terminal.
```

> `-w 40` sets the maximum line width to 40 characters.

---

# Example 3: Format Multiple Files

### File 1: `para1.txt`

```
Linux is a free and open-source operating system that is widely used in servers, desktops, and embedded systems.
```

### File 2: `para2.txt`

```
It was originally created by Linus Torvalds and has since grown into a large collaborative project.
```

### Command:

```bash
fmt para1.txt para2.txt
```

### Output:

```
Linux is a free and open-source operating
system that is widely used in servers,
desktops, and embedded systems.

It was originally created by Linus Torvalds
and has since grown into a large
collaborative project.
```

---

# Example 4: Combine with Pipe

```bash
cat text.txt | fmt -w 50
```

* Reads from `cat` and formats text with width 50.
* Useful in **scripts** or pipelines.

---

# Example 5: Preserve Existing Paragraphs

### File: `story.txt`

```
This is the first paragraph. It contains several sentences that should be formatted properly.

This is the second paragraph. It also needs proper formatting.
```

### Command:

```bash
fmt -w 60 story.txt
```

### Output:

```
This is the first paragraph. It contains several sentences
that should be formatted properly.

This is the second paragraph. It also needs proper
formatting.
```

> `fmt` preserves **blank lines** between paragraphs.
</details>
<details>
 <summary>cut</summary>

The `cut` command in Linux is used to **extract specific columns or fields from a file or input**, based on delimiters or character positions.

# Example 1: Extract a Single Column

### File: `users.txt`

```
alice:1001:/home/alice
bob:1002:/home/bob
carol:1003:/home/carol
```

### Command:

```bash
cut -d ':' -f 1 users.txt
```

### Output:

```
alice
bob
carol
```

> `-d ':'` sets the delimiter, `-f 1` extracts the first field.

---

# Example 2: Extract Multiple Columns

### Command:

```bash
cut -d ':' -f 1,3 users.txt
```

### Output:

```
alice:/home/alice
bob:/home/bob
carol:/home/carol
```

> Extracts **first and third fields** separated by `:`.

---

# Example 3: Extract by Character Position

### File: `data.txt`

```
abcdef
ghijkl
mnopqr
```

### Command:

```bash
cut -c 2-4 data.txt
```

### Output:

```
bcd
hij
nop
```

> `-c 2-4` extracts **characters 2 to 4** from each line.

---

# Example 4: Use with Pipe

```bash
ps aux | cut -d ' ' -f 1
```

* Extracts the **first column (user)** from `ps aux` output.
* Useful for scripts or quick column filtering.

---

# Example 5: Extract Last Field from a File

### File: `marks.txt`

```
John,85,Math
Mary,92,Science
David,78,History
```

### Command:

```bash
cut -d ',' -f 3 marks.txt
```

### Output:

```
Math
Science
History
```

> Extracts the **third column** separated by a comma.
</details>
<details>
 <summary>tr</summary>

The `tr` command in Linux **translates, replaces, or deletes characters** from input text, usually used in pipelines.

---

# Example 1: Convert Lowercase to Uppercase

### File: `text.txt`

```
hello world
linux commands
```

### Command:

```bash
cat text.txt | tr 'a-z' 'A-Z'
```

### Output:

```
HELLO WORLD
LINUX COMMANDS
```

> Converts all lowercase letters to uppercase.

---

# Example 2: Replace Characters

### File: `file.txt`

```
2026-03-02
```

### Command:

```bash
cat file.txt | tr '-' '/'
```

### Output:

```
2026/03/02
```

> Replaces `-` with `/`.

---

# Example 3: Delete Specific Characters

### File: `numbers.txt`

```
1a2b3c4d5
```

### Command:

```bash
cat numbers.txt | tr -d 'a-d'
```

### Output:

```
12345
```

> `-d` deletes all characters `a` through `d`.

---

# Example 4: Squeeze Repeated Characters

### File: `text2.txt`

```
hellooo    world
```

### Command:

```bash
cat text2.txt | tr -s ' '
```

### Output:

```
hellooo world
```

> `-s` squeezes multiple spaces into a single space.

---

# Example 5: Replace Newlines with Spaces

### File: `list.txt`

```
apple
banana
orange
grapes
```

### Command:

```bash
cat list.txt | tr '\n' ' '
```

### Output:

```
apple banana orange grapes 
```

> Converts **line breaks to spaces**, useful for formatting output.
</details>

