
## 🎯 **16. ULTIMATE CHEAT SHEET AWK**

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

