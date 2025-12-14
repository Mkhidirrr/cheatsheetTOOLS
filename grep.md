**CHEATSHEET TOOLS GREP**
# BASIC SEARCH
grep "pattern" file.txt              # Simple search
grep -i "pattern" file.txt           # Case-insensitive
grep -n "pattern" file.txt           # With line numbers
grep -c "pattern" file.txt           # Count matches
grep -v "pattern" file.txt           # Invert (non-matching)

# REGEX
grep "^start" file.txt               # Lines starting with
grep "end$" file.txt                 # Lines ending with
grep -E "pat1|pat2" file.txt         # OR pattern
grep -E "[0-9]+" file.txt            # Extended regex
grep -P "\d+" file.txt               # Perl regex

# RECURSIVE
grep -r "pattern" dir/               # Recursive
grep -rn "pattern" .                 # Recursive + line numbers
grep -r --include="*.py" "pattern" . # Specific files
grep -r --exclude-dir="node_modules" "pattern" .  # Exclude dir

# CONTEXT
grep -A 3 "pattern" file.txt         # 3 lines after
grep -B 3 "pattern" file.txt         # 3 lines before
grep -C 3 "pattern" file.txt         # 3 lines around

# FILES
grep -l "pattern" *.txt              # List matching files
grep -L "pattern" *.txt              # List non-matching files

# PRACTICAL EXAMPLES
# Find errors
grep -i "error" /var/log/syslog

# Top IPs
grep -oE "([0-9]{1,3}\.){3}[0-9]{1,3}" access.log | sort | uniq -c | sort -rn | head -10

# Find TODO
grep -rn "TODO" src/

# Extract emails
grep -oE "[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}" file.txt

# Find in code
grep -r --include="*.py" "def.*function" .

# Active config lines
grep -v "^#" config.conf | grep -v "^$"

# Check if exists (script)
if grep -q "pattern" file.txt; then
  echo "Found"
fi
