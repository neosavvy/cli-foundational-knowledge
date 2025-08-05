# Module 03: Bash Scripting and Text Processing

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Process and manipulate text data using command-line tools
- Parse JSON data with `jq`
- Extract specific fields from text using `cut`
- Perform text transformations with `sed`
- Process structured data with `awk`
- Combine tools in pipelines for complex data processing
- Write basic bash scripts for automation

## 📚 Core Tools

### `jq` - JSON Processor

`jq` is a lightweight command-line JSON processor that allows you to slice, filter, map, and transform JSON data.

#### Basic Usage
```bash
# Pretty print JSON
echo '{"name":"John","age":30}' | jq '.'

# Extract specific field
echo '{"name":"John","age":30}' | jq '.name'

# Extract multiple fields
echo '{"name":"John","age":30,"city":"NYC"}' | jq '{name: .name, age: .age}'

# Filter arrays
echo '[{"name":"John","age":30},{"name":"Jane","age":25}]' | jq '.[] | select(.age > 25)'

# Transform data
echo '{"name":"John","age":30}' | jq '{name: .name, isAdult: (.age >= 18)}'
```

#### Advanced Features
```bash
# Working with arrays
echo '[1,2,3,4,5]' | jq '.[0:3]'           # Slice array
echo '[1,2,3,4,5]' | jq 'map(. * 2)'        # Transform each element

# Working with objects
echo '{"users":[{"name":"John"},{"name":"Jane"}]}' | jq '.users[].name'

# Conditional logic
echo '{"age":25}' | jq 'if .age >= 18 then "adult" else "minor" end'
```

### `cut` - Extract Sections from Lines

`cut` extracts portions of each line from files or standard input.

#### Basic Usage
```bash
# Extract specific fields (comma-separated)
echo "name,age,city" | cut -d',' -f1        # Extract first field
echo "name,age,city" | cut -d',' -f1,3      # Extract first and third fields
echo "name,age,city" | cut -d',' -f2-       # Extract from second field to end

# Extract by character position
echo "Hello World" | cut -c1-5               # Extract first 5 characters
echo "Hello World" | cut -c7-                # Extract from 7th character to end

# Extract by delimiter (tab-separated)
echo -e "name\tage\tcity" | cut -f1,3       # Extract first and third fields
```

#### Common Options
```bash
cut -d',' -f1,3 file.csv     # Comma-delimited, fields 1 and 3
cut -f1-3 file.txt           # Tab-delimited, fields 1-3
cut -c1-10 file.txt          # Characters 1-10
cut -d'|' -f2 file.txt       # Pipe-delimited, field 2
```

### `sed` - Stream Editor

`sed` is a stream editor for filtering and transforming text.

#### Basic Substitution
```bash
# Simple substitution
echo "Hello World" | sed 's/World/Unix/'

# Global substitution (all occurrences)
echo "Hello Hello Hello" | sed 's/Hello/Hi/g'

# Case-insensitive substitution
echo "Hello HELLO hello" | sed 's/hello/hi/gi'

# Substitute with regex
echo "file1.txt file2.txt" | sed 's/\.txt$/.log/g'
```

#### Advanced Features
```bash
# Delete lines
sed '1d' file.txt            # Delete first line
sed '1,3d' file.txt          # Delete lines 1-3
sed '/pattern/d' file.txt     # Delete lines matching pattern

# Add/insert lines
sed '1i\New line' file.txt   # Insert before line 1
sed '1a\New line' file.txt   # Append after line 1

# Print specific lines
sed -n '1,3p' file.txt       # Print lines 1-3 only
sed -n '/pattern/p' file.txt  # Print lines matching pattern
```

#### In-place Editing
```bash
sed -i 's/old/new/g' file.txt        # Edit file in place
sed -i.bak 's/old/new/g' file.txt    # Create backup with .bak extension
```

### `awk` - Pattern Scanning and Processing

`awk` is a powerful programming language for processing text files.

#### Basic Usage
```bash
# Print specific fields
echo "John 30 NYC" | awk '{print $1, $3}'    # Print first and third fields
echo "John 30 NYC" | awk '{print $1}'        # Print first field only

# Print with custom separator
echo "John,30,NYC" | awk -F',' '{print $1, $3}'

# Conditional printing
echo "John 30 NYC" | awk '$2 > 25 {print $1, "is old"}'
```

#### Advanced Features
```bash
# BEGIN and END blocks
awk 'BEGIN {print "Starting..."} {print $0} END {print "Finished"}' file.txt

# Variables and calculations
echo "John 30 NYC" | awk '{age = $2; print $1, "is", age, "years old"}'

# Pattern matching
awk '/pattern/ {print $0}' file.txt           # Print lines matching pattern
awk '$1 ~ /^J/ {print $0}' file.txt          # Print lines where first field starts with J

# Built-in functions
echo "hello world" | awk '{print toupper($0)}'    # Convert to uppercase
echo "HELLO WORLD" | awk '{print tolower($0)}'    # Convert to lowercase
```

## 🏋️ Practice Exercises

### Exercise 1: JSON Processing with `jq`
```bash
# Create a JSON file
cat > users.json << 'EOF'
{
  "users": [
    {"name": "John", "age": 30, "city": "NYC", "active": true},
    {"name": "Jane", "age": 25, "city": "LA", "active": false},
    {"name": "Bob", "age": 35, "city": "Chicago", "active": true}
  ]
}
EOF

# Extract all names
jq '.users[].name' users.json

# Find active users
jq '.users[] | select(.active == true)' users.json

# Create summary
jq '{total_users: (.users | length), active_users: ([.users[] | select(.active)] | length)}' users.json
```

### Exercise 2: Text Processing with `cut`
```bash
# Create a CSV file
cat > data.csv << 'EOF'
name,age,city,occupation
John,30,NYC,Engineer
Jane,25,LA,Designer
Bob,35,Chicago,Manager
EOF

# Extract names and cities
cut -d',' -f1,3 data.csv

# Extract ages only
cut -d',' -f2 data.csv

# Extract first 10 characters of each line
cut -c1-10 data.csv
```

### Exercise 3: Text Transformation with `sed`
```bash
# Create a text file
cat > sample.txt << 'EOF'
Hello World
This is a test file
Hello again
Goodbye World
EOF

# Replace "Hello" with "Hi"
sed 's/Hello/Hi/g' sample.txt

# Delete lines containing "test"
sed '/test/d' sample.txt

# Add line numbers
sed '=' sample.txt | sed 'N;s/\n/ /'

# Convert to uppercase
sed 's/.*/\U&/' sample.txt
```

### Exercise 4: Data Processing with `awk`
```bash
# Create a space-separated file
cat > scores.txt << 'EOF'
John 85 90 78
Jane 92 88 95
Bob 78 82 80
EOF

# Calculate averages
awk '{avg = ($2 + $3 + $4) / 3; print $1, avg}' scores.txt

# Find highest scorer
awk '{sum = $2 + $3 + $4; print $1, sum}' scores.txt | sort -k2 -nr | head -1

# Print formatted output
awk '{printf "%-10s: %d, %d, %d (Avg: %.1f)\n", $1, $2, $3, $4, ($2+$3+$4)/3}' scores.txt
```

### Exercise 5: Combining Tools
```bash
# Process log file
cat > app.log << 'EOF'
2024-01-01 10:00:00 INFO User login successful
2024-01-01 10:05:00 ERROR Database connection failed
2024-01-01 10:10:00 INFO User logout
2024-01-01 10:15:00 ERROR File not found
EOF

# Extract error messages with timestamps
grep "ERROR" app.log | cut -d' ' -f1,2,4-

# Count error types
grep "ERROR" app.log | cut -d' ' -f4 | sort | uniq -c

# Extract timestamps and convert format
grep "ERROR" app.log | cut -d' ' -f1,2 | sed 's/ /T/' | sed 's/$/Z/'
```

## 🧪 Knowledge Check

### Multiple Choice Questions

1. **What does `jq '.users[].name'` do?**
   - a) Extracts all names from a users array
   - b) Extracts the first user's name
   - c) Extracts the last user's name
   - d) Creates a new users array

2. **How do you extract the 3rd field from a comma-separated line?**
   - a) `cut -d',' -f3`
   - b) `cut -f3`
   - c) `cut -d',' -c3`
   - d) `cut -f3 -d','`

3. **What does `sed 's/old/new/g'` do?**
   - a) Replaces all occurrences of "old" with "new"
   - b) Replaces only the first occurrence
   - c) Deletes lines containing "old"
   - d) Adds "new" after "old"

4. **In awk, what does `$1` refer to?**
   - a) The first character
   - b) The first field
   - c) The first line
   - d) The first file

### Practical Test

Complete these tasks in your terminal:

1. **JSON Processing Test:**
   ```bash
   # Create test JSON
   cat > test.json << 'EOF'
   {
     "employees": [
       {"id": 1, "name": "Alice", "salary": 50000, "department": "IT"},
       {"id": 2, "name": "Bob", "salary": 60000, "department": "HR"},
       {"id": 3, "name": "Charlie", "salary": 55000, "department": "IT"}
     ]
   }
   EOF
   
   # Extract all names
   jq '.employees[].name' test.json
   
   # Find IT department employees
   jq '.employees[] | select(.department == "IT")' test.json
   
   # Calculate total salary
   jq '.employees | map(.salary) | add' test.json
   ```

2. **Text Processing Test:**
   ```bash
   # Create test data
   cat > data.txt << 'EOF'
   apple,red,fruit
   banana,yellow,fruit
   carrot,orange,vegetable
   EOF
   
   # Extract colors only
   cut -d',' -f2 data.txt
   
   # Replace "fruit" with "produce"
   sed 's/fruit/produce/g' data.txt
   
   # Print items with their colors
   awk -F',' '{print $1, "is", $2}' data.txt
   ```

## 📋 Cheat Sheet

### jq Commands
```bash
jq '.' file.json                    # Pretty print
jq '.field' file.json              # Extract field
jq '.array[]' file.json            # Iterate array
jq 'select(.condition)' file.json  # Filter
jq 'map(.field)' file.json         # Transform array
```

### cut Commands
```bash
cut -d',' -f1,3 file.csv          # Extract fields 1,3
cut -f1-3 file.txt                 # Extract fields 1-3
cut -c1-10 file.txt                # Extract characters 1-10
cut -d'|' -f2 file.txt             # Pipe-delimited, field 2
```

### sed Commands
```bash
sed 's/old/new/g' file.txt         # Global substitution
sed '/pattern/d' file.txt           # Delete matching lines
sed -n '1,3p' file.txt             # Print lines 1-3
sed -i 's/old/new/g' file.txt      # In-place edit
```

### awk Commands
```bash
awk '{print $1}' file.txt          # Print first field
awk -F',' '{print $1}' file.txt    # Comma-separated
awk '$2 > 10 {print $1}' file.txt  # Conditional print
awk '{sum += $2} END {print sum}' file.txt  # Sum field 2
```

## 🎯 Next Steps

Once you've completed this module:
1. Take the knowledge check
2. Complete the practical tests
3. Practice with your own data files
4. Move to [Module 04: Networking](../04-networking/README.md)

---

**Remember:** These tools are incredibly powerful when combined. Practice building pipelines that use multiple tools together! 