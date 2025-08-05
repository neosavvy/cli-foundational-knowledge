# Module 05: File Editing

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Edit files using command-line text editors (`nano`, `vim`, `emacs`)
- View file contents using `cat`, `head`, `tail`, and `less`
- Navigate and edit files efficiently in terminal-based editors
- Use search and replace functions in text editors
- Understand the differences between various text editors
- Survive and thrive when working on remote servers with only CLI access

## 📚 Core Concepts

### Text Editor Types

**Simple Editors:**
- `nano` - Beginner-friendly, easy to use
- `pico` - Similar to nano (legacy)

**Advanced Editors:**
- `vim` - Powerful, highly customizable
- `emacs` - Extensible, feature-rich
- `ed` - Line editor (very basic)

**File Viewers:**
- `cat` - Display entire file
- `head` - Show beginning of file
- `tail` - Show end of file
- `less` - Interactive file viewer
- `more` - Simple pager

## 📚 Core Commands

### `nano` - Beginner-Friendly Text Editor

`nano` is a simple, easy-to-use text editor perfect for beginners.

#### Basic Usage
```bash
nano filename.txt           # Open file for editing
nano -w filename.txt        # Disable word wrap
nano +10 filename.txt       # Open at line 10
nano -T 4 filename.txt      # Set tab size to 4 spaces
```

#### Navigation and Editing
```bash
# Navigation
Ctrl + G                  # Get help
Ctrl + X                  # Exit
Ctrl + O                  # Save (Write Out)
Ctrl + W                  # Search
Ctrl + K                  # Cut line
Ctrl + U                  # Paste
Ctrl + A                  # Go to beginning of line
Ctrl + E                  # Go to end of line
Ctrl + Y                  # Go to previous page
Ctrl + V                  # Go to next page

# Editing
Ctrl + K                  # Cut from cursor to end of line
Ctrl + U                  # Paste
Ctrl + 6                  # Set mark (for selection)
Alt + A                   # Mark text (select)
Alt + 6                   # Copy marked text
```

#### Search and Replace
```bash
Ctrl + W                  # Search forward
Ctrl + Q                  # Search backward
Alt + R                   # Replace
Alt + A                   # Replace all
```

### `vim` - Powerful Text Editor

`vim` is a highly efficient text editor with a steep learning curve but powerful capabilities.

#### Modes
- **Normal mode** - Default mode for navigation and commands
- **Insert mode** - For typing text
- **Visual mode** - For selecting text
- **Command mode** - For executing commands

#### Basic Usage
```bash
vim filename.txt           # Open file
vim +10 filename.txt       # Open at line 10
vim -R filename.txt        # Read-only mode
vim -o file1.txt file2.txt # Open multiple files in horizontal split
```

#### Essential Commands

**Navigation (Normal mode):**
```bash
h, j, k, l                # Move left, down, up, right
w, b                      # Move word forward/backward
0, $                      # Go to beginning/end of line
gg, G                     # Go to beginning/end of file
:n                        # Go to line n
Ctrl + f, Ctrl + b        # Page down/up
```

**Editing (Normal mode):**
```bash
i                         # Enter insert mode
a                         # Append after cursor
o                         # Open new line below
O                         # Open new line above
x                         # Delete character under cursor
dd                        # Delete line
yy                        # Yank (copy) line
p                         # Paste after cursor
P                         # Paste before cursor
u                         # Undo
Ctrl + r                  # Redo
```

**Search and Replace:**
```bash
/pattern                  # Search forward for pattern
?pattern                  # Search backward for pattern
n                         # Next search result
N                         # Previous search result
:%s/old/new/g            # Replace all occurrences
:%s/old/new/gc           # Replace with confirmation
```

**File Operations:**
```bash
:w                        # Save file
:w filename.txt           # Save as
:q                        # Quit
:q!                       # Quit without saving
:wq                       # Save and quit
:x                        # Save and quit
ZZ                        # Save and quit
ZQ                        # Quit without saving
```

#### Visual Mode
```bash
v                         # Enter visual mode
V                         # Enter visual line mode
Ctrl + v                  # Enter visual block mode
y                         # Yank selected text
d                         # Delete selected text
```

### `emacs` - Extensible Text Editor

`emacs` is a highly extensible text editor with many features.

#### Basic Usage
```bash
emacs filename.txt         # Open file
emacs -nw filename.txt     # No window (terminal only)
emacs +10 filename.txt     # Open at line 10
```

#### Essential Commands
```bash
# File operations
Ctrl + x, Ctrl + s        # Save file
Ctrl + x, Ctrl + w        # Save as
Ctrl + x, Ctrl + c        # Exit emacs

# Navigation
Ctrl + p, Ctrl + n        # Previous/next line
Ctrl + b, Ctrl + f        # Backward/forward character
Ctrl + a, Ctrl + e        # Beginning/end of line
Ctrl + v, Alt + v         # Page down/up
Ctrl + x, Ctrl + x        # Go to line

# Editing
Ctrl + space              # Set mark
Ctrl + w                  # Kill region (cut)
Alt + w                   # Copy region
Ctrl + y                  # Yank (paste)
Ctrl + x, u               # Undo
Ctrl + g                  # Cancel current command

# Search
Ctrl + s                  # Search forward
Ctrl + r                  # Search backward
Alt + %                   # Query replace
```

### File Viewing Commands

#### `cat` - Concatenate and Display Files
```bash
cat filename.txt           # Display entire file
cat -n filename.txt        # Display with line numbers
cat -A filename.txt        # Show non-printing characters
cat file1.txt file2.txt    # Display multiple files
cat > newfile.txt          # Create new file (Ctrl+D to end)
cat >> existing.txt        # Append to existing file
```

#### `head` - Display Beginning of Files
```bash
head filename.txt          # Show first 10 lines
head -n 20 filename.txt    # Show first 20 lines
head -c 100 filename.txt   # Show first 100 characters
head -q file1.txt file2.txt # Show multiple files without headers
```

#### `tail` - Display End of Files
```bash
tail filename.txt          # Show last 10 lines
tail -n 20 filename.txt    # Show last 20 lines
tail -f filename.txt       # Follow file (watch for changes)
tail -c 100 filename.txt   # Show last 100 characters
tail +10 filename.txt      # Show from line 10 to end
```

#### `less` - Interactive File Viewer
```bash
less filename.txt          # View file interactively
less -N filename.txt       # Show line numbers
less -R filename.txt       # Display ANSI color codes
less +10 filename.txt      # Start at line 10
less +/pattern filename.txt # Start at first match of pattern
```

**Less Navigation:**
```bash
Space, b                  # Page down/up
j, k                      # Line down/up
g, G                      # Go to beginning/end
/pattern                  # Search forward
?pattern                  # Search backward
n, N                      # Next/previous search
q                         # Quit
```

## 🏋️ Practice Exercises

### Exercise 1: Basic File Editing with nano
```bash
# Create a test file
echo "This is a test file" > test.txt

# Open with nano
nano test.txt

# Practice these operations:
# 1. Navigate to the end of the line
# 2. Add some text
# 3. Save the file (Ctrl+O, then Enter)
# 4. Exit nano (Ctrl+X)

# View the result
cat test.txt
```

### Exercise 2: vim Basics
```bash
# Create a test file
cat > vimtest.txt << 'EOF'
Line 1: This is the first line
Line 2: This is the second line
Line 3: This is the third line
EOF

# Open with vim
vim vimtest.txt

# Practice these operations:
# 1. Navigate to line 2 (2G)
# 2. Enter insert mode (i)
# 3. Add some text
# 4. Exit insert mode (Esc)
# 5. Save and quit (:wq)

# View the result
cat vimtest.txt
```

### Exercise 3: File Viewing Commands
```bash
# Create a large test file
for i in {1..50}; do
    echo "This is line number $i" >> largefile.txt
done

# Practice viewing commands
head -5 largefile.txt      # Show first 5 lines
tail -5 largefile.txt      # Show last 5 lines
head -10 largefile.txt | tail -5  # Show lines 6-10
cat -n largefile.txt | head -10   # Show first 10 lines with numbers
less largefile.txt         # Interactive viewing
```

### Exercise 4: Search and Replace
```bash
# Create a file with repeated text
cat > searchtest.txt << 'EOF'
Hello World
Hello Universe
Hello Galaxy
Goodbye World
Hello Again
EOF

# Use nano to search and replace
nano searchtest.txt
# Press Ctrl+W to search for "Hello"
# Press Alt+R to replace "Hello" with "Hi"

# Or use vim
vim searchtest.txt
# Use :%s/Hello/Hi/g to replace all occurrences
```

### Exercise 5: Advanced File Operations
```bash
# Create multiple files
echo "File 1 content" > file1.txt
echo "File 2 content" > file2.txt
echo "File 3 content" > file3.txt

# View all files at once
cat file*.txt

# Create a combined file
cat file1.txt file2.txt file3.txt > combined.txt

# View the combined file
cat combined.txt

# Use less to view the combined file
less combined.txt
```

## 🧪 Knowledge Check

### Multiple Choice Questions

1. **What is the easiest text editor for beginners?**
   - a) vim
   - b) nano
   - c) emacs
   - d) ed

2. **How do you save and quit in vim?**
   - a) `:wq`
   - b) `Ctrl+X`
   - c) `:quit`
   - d) `Ctrl+S`

3. **What does `tail -f` do?**
   - a) Shows the last 10 lines
   - b) Follows a file for changes
   - c) Shows the first 10 lines
   - d) Formats the file

4. **How do you search in nano?**
   - a) `/pattern`
   - b) `Ctrl+W`
   - c) `Ctrl+F`
   - d) `Ctrl+S`

### Practical Test

Complete these tasks in your terminal:

1. **Basic Editing Test:**
   ```bash
   # Create a test file
   echo "Original content" > edit_test.txt
   
   # Edit with nano
   nano edit_test.txt
   # Add a new line and save
   
   # Edit with vim
   vim edit_test.txt
   # Add another line and save
   
   # View the final result
   cat edit_test.txt
   ```

2. **File Viewing Test:**
   ```bash
   # Create a large file
   for i in {1..100}; do
       echo "Line $i: Some content here" >> view_test.txt
   done
   
   # Use different viewing commands
   head -10 view_test.txt
   tail -10 view_test.txt
   head -20 view_test.txt | tail -10
   less view_test.txt
   ```

3. **Search and Replace Test:**
   ```bash
   # Create a file with repeated words
   cat > replace_test.txt << 'EOF'
   apple apple apple
   banana banana
   apple orange apple
   EOF
   
   # Use nano to replace "apple" with "fruit"
   nano replace_test.txt
   
   # Or use vim
   vim replace_test.txt
   # Use :%s/apple/fruit/g
   ```

## 📋 Cheat Sheet

### nano Commands
```bash
Ctrl + X                  # Exit
Ctrl + O                  # Save
Ctrl + W                  # Search
Ctrl + K                  # Cut line
Ctrl + U                  # Paste
Ctrl + G                  # Help
```

### vim Commands
```bash
i                         # Insert mode
Esc                       # Normal mode
:w                        # Save
:q                        # Quit
:wq                       # Save and quit
dd                        # Delete line
yy                        # Copy line
p                         # Paste
/pattern                  # Search
:%s/old/new/g            # Replace all
```

### File Viewing Commands
```bash
cat file.txt              # Display entire file
head -10 file.txt         # First 10 lines
tail -10 file.txt         # Last 10 lines
tail -f file.txt          # Follow file
less file.txt             # Interactive viewer
```

### emacs Commands
```bash
Ctrl + x, Ctrl + s        # Save
Ctrl + x, Ctrl + c        # Exit
Ctrl + x, Ctrl + f        # Find file
Ctrl + s                  # Search
Ctrl + r                  # Search backward
```

## 🎯 Editor Selection Guide

**Choose nano if:**
- You're new to command-line editing
- You need something simple and fast
- You're editing small files
- You want to avoid learning complex commands

**Choose vim if:**
- You want powerful editing capabilities
- You work with large files
- You need advanced search and replace
- You want to be efficient with keyboard navigation

**Choose emacs if:**
- You want extensibility and customization
- You need integrated development features
- You want to use the same editor for everything
- You're comfortable with complex key combinations

## 🎯 Next Steps

Once you've completed this module:
1. Take the knowledge check
2. Complete the practical tests
3. Practice with your own files
4. You've completed the CLI study guide!

---

**Remember:** The key to mastering CLI editors is practice. Start with nano for simple edits, then graduate to vim for more complex tasks. The investment in learning vim will pay off with increased productivity! 