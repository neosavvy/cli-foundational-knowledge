# Final Assessment: CLI Mastery Test

## 🎯 Assessment Overview

This final assessment will test your mastery of all five CLI modules. Complete each section to validate your understanding and practical skills.

## 📋 Assessment Structure

- **Part 1:** File System Management (25 points)
- **Part 2:** Permissions and Security (20 points)
- **Part 3:** Text Processing and Scripting (25 points)
- **Part 4:** Networking (15 points)
- **Part 5:** File Editing (15 points)

**Total: 100 points**

## 🏆 Part 1: File System Management (25 points)

### Exercise 1.1: Directory Structure Creation (10 points)
```bash
# Create this directory structure:
# cli_assessment/
# ├── docs/
# │   ├── README.md
# │   └── config.txt
# ├── src/
# │   ├── main.py
# │   └── utils.py
# ├── data/
# │   ├── users.csv
# │   └── logs/
# │       ├── app.log
# │       └── error.log
# └── backup/

# Your commands here:
mkdir -p cli_assessment/{docs,src,data/logs,backup}
touch cli_assessment/docs/{README.md,config.txt}
touch cli_assessment/src/{main.py,utils.py}
touch cli_assessment/data/users.csv
touch cli_assessment/data/logs/{app.log,error.log}

# Verify with tree
tree cli_assessment/
```

### Exercise 1.2: File Operations (8 points)
```bash
# Navigate to the assessment directory
cd cli_assessment/

# 1. Copy the main.py file to backup/
cp src/main.py backup/

# 2. Move config.txt to the root directory
mv docs/config.txt ./

# 3. Create a symbolic link from backup/main.py to src/main_backup.py
ln -s backup/main.py src/main_backup.py

# 4. Find all Python files in the directory
find . -name "*.py"
```

### Exercise 1.3: Content Search (7 points)
```bash
# Add some content to files
echo "This is a Python application" > src/main.py
echo "Utility functions" > src/utils.py
echo "user1,admin,active" > data/users.csv
echo "user2,user,inactive" >> data/users.csv
echo "ERROR: Connection failed" > data/logs/error.log
echo "INFO: System started" > data/logs/app.log

# 1. Find all files containing "Python"
grep -r "Python" .

# 2. Find all files containing "ERROR"
grep -r "ERROR" .

# 3. Count lines in users.csv
wc -l data/users.csv
```

## 🔒 Part 2: Permissions and Security (20 points)

### Exercise 2.1: Permission Management (10 points)
```bash
# 1. Set appropriate permissions for different files
chmod 644 docs/README.md          # Regular file
chmod 755 src/                    # Directory
chmod 600 data/users.csv          # Private data
chmod 750 backup/                 # Group access directory

# 2. Verify permissions
ls -la docs/README.md
ls -la src/
ls -la data/users.csv
ls -la backup/
```

### Exercise 2.2: Ownership and Security (10 points)
```bash
# 1. Check current ownership
ls -la src/main.py

# 2. Create a test file and change its group
echo "Test content" > test_file.txt
sudo chown :staff test_file.txt

# 3. Set restrictive permissions on sensitive file
chmod 600 test_file.txt

# 4. Verify the changes
ls -la test_file.txt
```

## 📊 Part 3: Text Processing and Scripting (25 points)

### Exercise 3.1: JSON Processing (8 points)
```bash
# Create a JSON file with user data
cat > users.json << 'EOF'
{
  "users": [
    {"id": 1, "name": "Alice", "role": "admin", "active": true},
    {"id": 2, "name": "Bob", "role": "user", "active": false},
    {"id": 3, "name": "Charlie", "role": "user", "active": true}
  ]
}
EOF

# 1. Extract all names
jq '.users[].name' users.json

# 2. Find active users
jq '.users[] | select(.active == true)' users.json

# 3. Count total users
jq '.users | length' users.json
```

### Exercise 3.2: Text Processing (8 points)
```bash
# Create a CSV file
cat > employees.csv << 'EOF'
name,department,salary,start_date
John,IT,50000,2020-01-15
Jane,HR,45000,2019-03-20
Bob,IT,55000,2021-06-10
EOF

# 1. Extract names and departments
cut -d',' -f1,2 employees.csv

# 2. Find IT employees
grep "IT" employees.csv

# 3. Replace "IT" with "Technology"
sed 's/IT/Technology/g' employees.csv
```

### Exercise 3.3: Data Analysis (9 points)
```bash
# Create a log file
cat > system.log << 'EOF'
2024-01-01 10:00:00 INFO User login successful
2024-01-01 10:05:00 ERROR Database connection failed
2024-01-01 10:10:00 INFO User logout
2024-01-01 10:15:00 ERROR File not found
2024-01-01 10:20:00 INFO Backup completed
EOF

# 1. Extract all ERROR messages
grep "ERROR" system.log

# 2. Count different log levels
grep -o "ERROR\|INFO" system.log | sort | uniq -c

# 3. Extract timestamps of errors
grep "ERROR" system.log | cut -d' ' -f1,2
```

## 🌐 Part 4: Networking (15 points)

### Exercise 4.1: Network Interface Analysis (5 points)
```bash
# 1. Display network interfaces
ifconfig

# 2. Find your IP address
ifconfig | grep "inet " | grep -v "127.0.0.1"

# 3. Check interface status
ip link show
```

### Exercise 4.2: DNS and Connectivity (5 points)
```bash
# 1. Test DNS resolution
nslookup google.com

# 2. Test connectivity
ping -c 3 google.com

# 3. Check route to a website
traceroute -m 5 google.com
```

### Exercise 4.3: Network Discovery (5 points)
```bash
# 1. Scan localhost for open ports
nmap localhost

# 2. Check specific ports
nmap -p 22,80,443 localhost

# 3. Discover hosts on your network (replace with your subnet)
# nmap -sn 192.168.1.0/24
```

## 📝 Part 5: File Editing (15 points)

### Exercise 5.1: Basic Editing (8 points)
```bash
# 1. Create and edit a file with nano
echo "Original content" > edit_test.txt
nano edit_test.txt
# Add a new line and save

# 2. Edit the same file with vim
vim edit_test.txt
# Add another line and save

# 3. View the final result
cat edit_test.txt
```

### Exercise 5.2: File Viewing and Processing (7 points)
```bash
# Create a large file
for i in {1..50}; do
    echo "Line $i: This is test content for line number $i" >> large_file.txt
done

# 1. View first 10 lines
head -10 large_file.txt

# 2. View last 10 lines
tail -10 large_file.txt

# 3. View lines 20-30
head -30 large_file.txt | tail -10

# 4. Search for specific content
grep "line number 25" large_file.txt
```

## 🧪 Knowledge Check Questions

### Multiple Choice (20 points - 2 points each)

1. **What command creates a symbolic link?**
   - a) `ln -s target link`
   - b) `link -s target link`
   - c) `symlink target link`
   - d) `ln target link`

2. **What does `chmod 755` set?**
   - a) Read/write for owner, read for group/others
   - b) Read/write/execute for owner, read/execute for group/others
   - c) Read/write/execute for all
   - d) Read/write for owner, read for group, nothing for others

3. **What does `jq '.users[].name'` do?**
   - a) Extracts all names from a users array
   - b) Extracts the first user's name
   - c) Extracts the last user's name
   - d) Creates a new users array

4. **What does `nslookup -type=mx google.com` do?**
   - a) Looks up the IP address of google.com
   - b) Looks up the mail exchange servers for google.com
   - c) Looks up the name servers for google.com
   - d) Performs a reverse DNS lookup

5. **How do you save and quit in vim?**
   - a) `:wq`
   - b) `Ctrl+X`
   - c) `:quit`
   - d) `Ctrl+S`

6. **What does `tail -f` do?**
   - a) Shows the last 10 lines
   - b) Follows a file for changes
   - c) Shows the first 10 lines
   - d) Formats the file

7. **What does `traceroute` show?**
   - a) Network bandwidth
   - b) Network path packets take
   - c) Open ports
   - d) DNS records

8. **What does `sed 's/old/new/g'` do?**
   - a) Replaces all occurrences of "old" with "new"
   - b) Replaces only the first occurrence
   - c) Deletes lines containing "old"
   - d) Adds "new" after "old"

9. **What does `nmap -sn` do?**
   - a) Performs a stealth scan
   - b) Scans for open ports
   - c) Performs host discovery only
   - d) Scans for vulnerabilities

10. **How do you search in nano?**
    - a) `/pattern`
    - b) `Ctrl+W`
    - c) `Ctrl+F`
    - d) `Ctrl+S`

## 📊 Scoring Guide

### Practical Exercises (80 points)
- **Part 1:** File System Management - 25 points
- **Part 2:** Permissions and Security - 20 points
- **Part 3:** Text Processing and Scripting - 25 points
- **Part 4:** Networking - 15 points
- **Part 5:** File Editing - 15 points

### Knowledge Check (20 points)
- 10 multiple choice questions × 2 points each = 20 points

### Grading Scale
- **90-100 points:** CLI Master
- **80-89 points:** CLI Expert
- **70-79 points:** CLI Proficient
- **60-69 points:** CLI Intermediate
- **Below 60 points:** Needs more practice

## 🎯 Completion Checklist

- [ ] Completed all practical exercises
- [ ] Answered all knowledge check questions
- [ ] Verified all commands work correctly
- [ ] Understood the concepts behind each command
- [ ] Can explain the purpose of each tool used

## 🏆 Next Steps After Assessment

1. **Review any missed concepts**
2. **Practice with real-world scenarios**
3. **Explore advanced features of each tool**
4. **Build automation scripts combining multiple tools**
5. **Share knowledge with team members**

---

**Congratulations on completing the CLI Study Guide!** 🎉

You now have a solid foundation in Unix/Linux command-line tools and can confidently navigate, manage, and troubleshoot systems using the terminal. 