difying fields doesn't auto-update $0
awk '{ $1 = "NEW"; print }' file.txt  # Recalculates $0

# ✅ EXPLICIT: Force recalculation
awk '{ $1 = "NEW"; $0 = $0; print }' file.txt
```

### **Mistake 4: Integer Division**

```bash
# ❌ WRONG: Integer division
awk '{ print 5/2 }'  # Output: 2.5 (actually works in awk!)

# But be careful:
awk '{ print int(5/2) }'  # Output: 2
```

---

## 🎯 **16. ULTIMATE CHEAT SHEET KHIDIR!**

```bash
# BASIC SYNTAX
awk '{ print $1 }' file.txt              # Print column 1
awk '{ print $1, $3 }' file.txt          # Print columns 1 & 3
awk '{ print $NF }' file.txt             # Print last column
awk -F',' '{ print $1 }' file.csv        # CSV (comma separator)

# PATTERN MATCHING
awk '/pattern/ { print }' file.txt       # Match pattern (like grep)
awk '$2 > 100' file.txt                  # Column 2 > 100
awk '$3 == "active"' file.txt            # Column 3 equals "active"
awk '$1 ~ /^[A-Z]/' file.txt            # Column 1 starts with uppercase

# CALCULATIONS
awk '{ sum += $2 } END { print sum }' file.txt             # Sum column 2
awk '{ sum += $2; n++ } END { print sum/n }' file.txt     # Average
awk 'BEGIN { max=0 } { if ($1>max) max=$1 } END { print max }' file.txt  # Max

# BUILT-IN VARIABLES
NR      # Line number (current record)
NF      # Number of fields (columns)
$0      # Entire line
$1,$2   # Column 1, column 2
FS      # Field separator (input)
OFS     # Output field separator
FNR     # File record number
FILENAME # Current filename

# COMMON PATTERNS
# Count lines
awk 'END { print NR }' file.txt

# Remove duplicates
awk '!seen[$0]++' file.txt

# Print specific lines (5-10)
awk 'NR >= 5 && NR <= 10' file.txt

# Sum by group
awk '{ sum[$1] += $2 } END { for (key in sum) print key, sum[key] }' file.txt

# CSV to TSV
awk -F',' '{ print $1 "\t" $2 "\t" $3 }' file.csv

# Add line numbers
awk '{ print NR, $0 }' file.txt

# Print lines longer than 80 chars
awk 'length > 80' file.txt

# Remove blank lines
awk 'NF > 0' file.txt

# PRACTICAL EXAMPLES
# Top 10 IPs from access log
awk '{ print $1 }' access.log | sort | uniq -c | sort -rn | head -10

# Calculate total salary
awk -F',' '{ sum += $4 } END { print "Total:", sum }' employees.csv

# Filter and format
awk '$3 > 25 { printf "%-10s %5d\n", $1, $3 }' data.txt

# Count by category
awk '{ count[$2]++ } END { for (cat in count) print cat, count[cat] }' data.txt

# Generate SQL
awk -F',' '{ print "INSERT INTO users VALUES (" $1 ", '\''" $2 "'\'');" }' data.csv
```

---

## 📝 **17. LATIHAN PRAKTIS**

### **Exercise 1: Sales Report**

```bash
# File: sales.csv (Product,Quantity,Price)
# Task: Calculate total revenue per product

# Solution:
awk -F',' 'NR > 1 { revenue[$1] += $2 * $3 } 
           END { for (product in revenue) 
                   printf "%s: $%.2f\n", product, revenue[product] }' sales.csv
```

### **Exercise 2: Log Analysis**

```bash
# File: access.log
# Task: Find top 5 IPs with most 404 errors

# Solution:
awk '$9 == 404 { print $1 }' access.log | \
  sort | uniq -c | sort -rn | head -5
```

### **Exercise 3: System Resource**

```bash
# Task: Find processes using more than 5% memory

# Solution:
ps aux | awk 'NR > 1 && $4 > 5 { printf "%-20s %5.1f%%\n", $11, $4 }'
```

---

## ✅ **KESIMPULAN ULTIMATE KHIDIR!**

**AWK = Programmable Text Processing!**

**Core Concepts:**
```
$1, $2, $3  → Columns
NR          → Line number  
NF          → Field count
BEGIN/END   → Before/After processing
```

**Most Common Pattern (90%):**
```bash
awk -F'delimiter' 'condition { action }' file.txt
```

**Top 10 Use Cases:**
1. ✅ Extract columns: `awk '{ print $1, $3 }'`
2. ✅ Sum/Average: `awk '{ sum += $2 } END { print sum }'`
3. ✅ Filter rows: `awk '$2 > 100'`
4. ✅ Count occurrences: `awk '{ count[$1]++ } END { ... }'`
5. ✅ Format output: `awk '{ printf "%-10s %5d\n", $1, $2 }'`
6. ✅ Log analysis: `awk '{ print $1 }' | sort | uniq -c`
7. ✅ CSV processing: `awk -F',' '{ print $1 }'`
8. ✅ Generate reports with BEGIN/END
9. ✅ Data validation
10. ✅ Complex calculations

