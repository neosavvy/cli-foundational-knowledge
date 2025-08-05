# Module 01: File System Management

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Navigate and explore the file system effectively
- Create, copy, move, and delete files and directories
- Search for files and content within files
- Use symbolic links for file organization
- Understand file system structure and hierarchy

## 📚 Core Commands

### File Listing and Navigation

#### `ls` - List Directory Contents
```bash
ls                    # List files in current directory
ls -la               # List all files (including hidden) with details
ls -lh               # List with human-readable file sizes
ls -t                # Sort by modification time (newest first)
ls -R                # Recursive listing (include subdirectories)
```

#### `tree` - Display Directory Structure
```bash
tree                  # Show directory structure
tree -L 2            # Limit depth to 2 levels
tree -a               # Include hidden files
tree -I "node_modules|.git"  # Exclude specific patterns
```

### File Operations

#### `touch` - Create Empty Files
```bash
touch filename.txt    # Create empty file
touch -a filename.txt # Update access time only
touch -m filename.txt # Update modification time only
```

#### `cp` - Copy Files and Directories
```bash
cp source.txt dest.txt           # Copy file
cp -r source_dir/ dest_dir/     # Copy directory recursively
cp -v source.txt dest.txt        # Verbose output
cp -i source.txt dest.txt        # Interactive (prompt before overwrite)
cp -p source.txt dest.txt        # Preserve permissions and timestamps
```

#### `mv` - Move/Rename Files
```bash
mv oldname.txt newname.txt       # Rename file
mv file.txt directory/           # Move file to directory
mv -i file.txt directory/        # Interactive mode
mv -v file.txt directory/        # Verbose output
```

#### `rm` - Remove Files
```bash
rm filename.txt                  # Remove file
rm -r directory/                 # Remove directory recursively
rm -f filename.txt               # Force remove (no prompts)
rm -i filename.txt               # Interactive mode
rm -v filename.txt               # Verbose output
```

### File Searching

#### `find` - Search for Files
```bash
find . -name "*.txt"            # Find all .txt files
find . -type f -name "*.py"     # Find Python files only
find . -mtime -7                # Files modified in last 7 days
find . -size +1M                # Files larger than 1MB
find . -user username           # Files owned by specific user
find . -exec grep -l "pattern" {} \;  # Find files containing pattern
```

#### `grep` - Search File Contents
```bash
grep "pattern" file.txt          # Search for pattern in file
grep -r "pattern" directory/     # Recursive search
grep -i "pattern" file.txt       # Case-insensitive search
grep -n "pattern" file.txt       # Show line numbers
grep -v "pattern" file.txt       # Invert match (show lines without pattern)
grep -A 3 "pattern" file.txt     # Show 3 lines after match
grep -B 3 "pattern" file.txt     # Show 3 lines before match
```

### Symbolic Links

#### `ln -s` - Create Symbolic Links
```bash
ln -s target_file link_name     # Create symbolic link
ln -s /path/to/target link_name # Create link to absolute path
ln -sf target_file link_name    # Force overwrite existing link
```

## 🏋️ Practice Exercises

### Exercise 1: Basic File Operations
```bash
# Create a practice directory
mkdir cli_practice
cd cli_practice

# Create some test files
touch file1.txt file2.txt file3.txt
echo "Hello World" > hello.txt
echo "This is a test file" > test.txt

# List all files
ls -la

# Create a subdirectory and move files
mkdir backup
mv file1.txt file2.txt backup/

# Copy a file
cp hello.txt hello_backup.txt

# Remove a file
rm file3.txt
```

### Exercise 2: File Searching
```bash
# Create files with different extensions
touch document.pdf image.jpg script.py data.json

# Find all image files
find . -name "*.jpg" -o -name "*.png" -o -name "*.gif"

# Find files modified today
find . -mtime -1

# Search for content in files
echo "TODO: Complete this task" > todo.txt
echo "DONE: Task completed" > done.txt
grep -r "TODO" .
```

### Exercise 3: Symbolic Links
```bash
# Create a symbolic link
ln -s /usr/bin/python3 python_link

# Verify the link
ls -la python_link

# Follow the link
readlink python_link
```

## 🧪 Knowledge Check

### Multiple Choice Questions

1. **What command lists all files including hidden ones?**
   - a) `ls -a`
   - b) `ls -h`
   - c) `ls -l`
   - d) `ls -R`

2. **How do you copy a directory recursively?**
   - a) `cp -r source dest`
   - b) `cp source dest`
   - c) `cp -v source dest`
   - d) `cp -i source dest`

3. **What does `grep -i` do?**
   - a) Show line numbers
   - b) Case-insensitive search
   - c) Invert match
   - d) Recursive search

4. **Which command creates a symbolic link?**
   - a) `ln -s target link`
   - b) `link -s target link`
   - c) `symlink target link`
   - d) `ln target link`

### Practical Test

Complete these tasks in your terminal:

1. **File Management Test:**
   ```bash
   # Create a test directory structure
   mkdir -p test_project/{src,docs,backup}
   cd test_project
   
   # Create files
   touch src/main.py src/utils.py
   echo "# Documentation" > docs/README.md
   
   # List the structure
   tree
   
   # Copy files to backup
   cp -r src backup/
   
   # Find all Python files
   find . -name "*.py"
   ```

2. **Search Test:**
   ```bash
   # Create test files with content
   echo "ERROR: Connection failed" > log1.txt
   echo "INFO: System started" > log2.txt
   echo "ERROR: Timeout occurred" > log3.txt
   
   # Find all files containing "ERROR"
   grep -l "ERROR" *.txt
   
   # Count lines with "ERROR"
   grep -c "ERROR" *.txt
   ```

## 📋 Cheat Sheet

### Essential Commands
```bash
# Navigation
ls -la              # List all files with details
tree -L 2           # Show directory structure (2 levels)
pwd                 # Show current directory

# File Operations
touch file.txt      # Create empty file
cp -r src/ dest/    # Copy directory
mv old new          # Move/rename
rm -rf dir/         # Remove directory (careful!)

# Searching
find . -name "*.txt"    # Find files by name
grep -r "text" .        # Search content recursively
grep -i "text" file.txt # Case-insensitive search

# Links
ln -s target link       # Create symbolic link
readlink link           # Show link target
```

### Common Options
- `-r` or `-R`: Recursive
- `-f`: Force (no prompts)
- `-i`: Interactive (prompt before overwrite)
- `-v`: Verbose output
- `-a`: All files (including hidden)
- `-l`: Long format (detailed listing)

## 🎯 Next Steps

Once you've completed this module:
1. Take the knowledge check
2. Complete the practical tests
3. Practice with your own files
4. Move to [Module 02: Permissions and Elevated Privileges](../02-permissions/README.md)

---

**Remember:** Always be careful with `rm` commands, especially with `-rf` flags. When in doubt, use `-i` for interactive mode! 