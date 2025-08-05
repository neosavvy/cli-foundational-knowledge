# CLI Command Cheat Sheet

## 📁 File System Management

### Navigation & Listing
```bash
ls -la                    # List all files with details
ls -lh                    # List with human-readable sizes
ls -t                     # Sort by modification time
tree                      # Show directory structure
tree -L 2                 # Limit depth to 2 levels
pwd                       # Show current directory
cd directory/             # Change directory
cd ~                      # Go to home directory
cd ..                     # Go to parent directory
```

### File Operations
```bash
touch file.txt            # Create empty file
cp source.txt dest.txt    # Copy file
cp -r src/ dest/          # Copy directory recursively
mv old.txt new.txt        # Move/rename file
rm file.txt               # Remove file
rm -rf directory/         # Remove directory (careful!)
mkdir directory/          # Create directory
mkdir -p path/to/dir/    # Create nested directories
```

### File Searching
```bash
find . -name "*.txt"      # Find files by name
find . -type f -name "*.py"  # Find Python files only
find . -mtime -7          # Files modified in last 7 days
find . -size +1M          # Files larger than 1MB
grep "pattern" file.txt   # Search for pattern in file
grep -r "pattern" .       # Recursive search
grep -i "pattern" file.txt # Case-insensitive search
grep -n "pattern" file.txt # Show line numbers
```

### Symbolic Links
```bash
ln -s target link         # Create symbolic link
readlink link             # Show link target
ls -la link               # View link details
```

## 🔒 Permissions & Security

### Permission Management
```bash
chmod 755 file.txt        # rwxr-xr-x (common for executables)
chmod 644 file.txt        # rw-r--r-- (common for files)
chmod 600 file.txt        # rw------- (owner only)
chmod u+x file.txt        # Add execute for user
chmod -R 755 directory/   # Recursive permission change
ls -la                    # List with permissions
stat file.txt             # Detailed file info
```

### Ownership
```bash
chown user file.txt       # Change owner
chown user:group file.txt # Change owner and group
chown -R user:group dir/  # Recursive ownership change
```

### Elevated Privileges
```bash
sudo command              # Run command as root
sudo -u user command      # Run as specific user
sudo -i                   # Interactive root shell
sudo -s                   # Root shell with current env
sudo !!                   # Previous command with sudo
su username               # Switch user
su - username             # Switch with login environment
```

## 📊 Text Processing & Scripting

### JSON Processing (jq)
```bash
jq '.' file.json          # Pretty print JSON
jq '.field' file.json     # Extract field
jq '.array[]' file.json   # Iterate array
jq 'select(.condition)' file.json  # Filter
jq 'map(.field)' file.json # Transform array
jq '.users[].name' file.json  # Extract all names
jq '.users | length' file.json  # Count array length
```

### Text Extraction (cut)
```bash
cut -d',' -f1,3 file.csv # Extract fields 1,3 (comma-delimited)
cut -f1-3 file.txt        # Extract fields 1-3 (tab-delimited)
cut -c1-10 file.txt       # Extract characters 1-10
cut -d'|' -f2 file.txt    # Pipe-delimited, field 2
```

### Text Transformation (sed)
```bash
sed 's/old/new/g' file.txt        # Global substitution
sed '/pattern/d' file.txt          # Delete matching lines
sed -n '1,3p' file.txt            # Print lines 1-3
sed -i 's/old/new/g' file.txt     # In-place edit
sed -i.bak 's/old/new/g' file.txt # Edit with backup
```

### Data Processing (awk)
```bash
awk '{print $1}' file.txt         # Print first field
awk -F',' '{print $1}' file.txt   # Comma-separated
awk '$2 > 10 {print $1}' file.txt # Conditional print
awk '{sum += $2} END {print sum}' file.txt  # Sum field 2
awk 'BEGIN {print "Start"} {print $0} END {print "End"}' file.txt
```

## 🌐 Networking

### Network Interfaces
```bash
ifconfig                  # Show all interfaces
ifconfig eth0             # Show specific interface
ip addr show              # Modern interface command
ip link show              # Show interface status
```

### DNS & Connectivity
```bash
nslookup domain.com       # Basic DNS lookup
nslookup -type=mx domain.com  # Mail records
nslookup -type=ns domain.com  # Name servers
dig domain.com            # Alternative DNS tool
ping domain.com           # Test connectivity
ping -c 4 domain.com      # Ping 4 times
```

### Network Path
```bash
traceroute domain.com     # Trace network path
traceroute -n domain.com  # No hostname resolution
traceroute -m 10 domain.com # Limit to 10 hops
```

### Network Discovery
```bash
nmap localhost            # Scan localhost
nmap -sn 192.168.1.0/24  # Host discovery
nmap -p 80,443 domain.com # Port scan
nmap -sV localhost        # Version detection
nmap -A localhost         # Aggressive scan
```

## 📝 File Editing

### nano (Beginner-Friendly)
```bash
nano file.txt             # Open file
Ctrl + X                  # Exit
Ctrl + O                  # Save
Ctrl + W                  # Search
Ctrl + K                  # Cut line
Ctrl + U                  # Paste
Ctrl + G                  # Help
```

### vim (Powerful Editor)
```bash
vim file.txt              # Open file
i                         # Enter insert mode
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

### File Viewing
```bash
cat file.txt              # Display entire file
cat -n file.txt           # With line numbers
head -10 file.txt         # First 10 lines
tail -10 file.txt         # Last 10 lines
tail -f file.txt          # Follow file (watch changes)
less file.txt             # Interactive viewer
more file.txt             # Simple pager
```

### less Navigation
```bash
Space, b                  # Page down/up
j, k                      # Line down/up
g, G                      # Go to beginning/end
/pattern                  # Search forward
?pattern                  # Search backward
n, N                      # Next/previous search
q                         # Quit
```

## 🔧 Common Options

### Universal Options
```bash
-r, -R                   # Recursive
-f                        # Force (no prompts)
-i                        # Interactive (prompt before overwrite)
-v                        # Verbose output
-a                        # All files (including hidden)
-l                        # Long format (detailed listing)
-n                        # Number lines
```

### File Patterns
```bash
*                         # Any characters
?                         # Single character
[abc]                     # Any of a, b, or c
[!abc]                    # Not a, b, or c
{file1,file2}             # Either file1 or file2
```

## 🚨 Important Warnings

### Dangerous Commands
```bash
rm -rf /                  # NEVER run this!
chmod 777 file.txt        # Very permissive (dangerous)
sudo rm -rf /             # NEVER run this!
```

### Safe Alternatives
```bash
rm -i file.txt            # Interactive remove
rm -rf directory/         # Only if you're sure
chmod 755 file.txt        # Safe permissions
sudo command              # Only when necessary
```

## 🎯 Quick Reference by Task

### File Management
- **Create file:** `touch file.txt`
- **Copy file:** `cp source.txt dest.txt`
- **Move file:** `mv old.txt new.txt`
- **Delete file:** `rm file.txt`
- **List files:** `ls -la`

### Text Processing
- **View file:** `cat file.txt`
- **Search content:** `grep "pattern" file.txt`
- **Extract fields:** `cut -d',' -f1,3 file.csv`
- **Replace text:** `sed 's/old/new/g' file.txt`
- **Process data:** `awk '{print $1}' file.txt`

### Network Troubleshooting
- **Check connectivity:** `ping domain.com`
- **DNS lookup:** `nslookup domain.com`
- **Trace route:** `traceroute domain.com`
- **Scan ports:** `nmap localhost`

### File Editing
- **Simple edit:** `nano file.txt`
- **Advanced edit:** `vim file.txt`
- **View file:** `less file.txt`
- **Follow changes:** `tail -f file.txt`

---

**Remember:** Practice makes perfect! Use these commands regularly to build muscle memory and confidence with the command line. 