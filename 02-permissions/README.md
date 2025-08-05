# Module 02: Permissions and Elevated Privileges

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Understand Unix/Linux file permissions and ownership
- Modify file and directory permissions using `chmod`
- Change file ownership using `chown`
- Use `sudo` and `su` for elevated privileges
- Understand the difference between root and user privileges
- Implement proper security practices

## 📚 Core Concepts

### File Permissions Overview

Unix/Linux uses a permission system with three levels:
- **Owner** (user who created the file)
- **Group** (group that owns the file)
- **Others** (everyone else)

Each level has three permissions:
- **Read (r)** - Can view file contents
- **Write (w)** - Can modify file contents
- **Execute (x)** - Can run file as program

### Permission Representation

Permissions are displayed as: `rwxrwxrwx`
- First `rwx`: Owner permissions
- Second `rwx`: Group permissions  
- Third `rwx`: Others permissions

Numeric representation (octal):
- Read = 4
- Write = 2
- Execute = 1
- Example: `rwxr-xr--` = 754

## 📚 Core Commands

### `chmod` - Change File Permissions

#### Symbolic Mode
```bash
chmod u+x file.txt        # Add execute for owner
chmod g-w file.txt        # Remove write for group
chmod o=r file.txt        # Set others to read-only
chmod a+x file.txt        # Add execute for all (a=all)
chmod u+rw,g+r,o-rwx file.txt  # Complex permission change
```

#### Numeric Mode
```bash
chmod 755 file.txt        # rwxr-xr-x (common for executables)
chmod 644 file.txt        # rw-r--r-- (common for files)
chmod 600 file.txt        # rw------- (owner only)
chmod 750 directory/      # rwxr-x--- (owner/group access)
chmod 777 file.txt        # rwxrwxrwx (everyone can everything - DANGEROUS!)
```

#### Recursive Changes
```bash
chmod -R 755 directory/   # Apply to directory and all contents
chmod -R u+w directory/   # Add write for owner recursively
```

### `chown` - Change File Ownership

```bash
chown newuser file.txt     # Change owner
chown newuser:newgroup file.txt  # Change owner and group
chown :newgroup file.txt   # Change group only
chown -R user:group directory/  # Recursive ownership change
```

### `sudo` - Execute Commands with Elevated Privileges

```bash
sudo command              # Run command as root
sudo -u username command  # Run command as specific user
sudo -i                   # Start interactive root shell
sudo -s                   # Start root shell with current environment
sudo !!                   # Run previous command with sudo
```

### `su` - Switch User

```bash
su username               # Switch to specific user
su - username             # Switch with login environment
su                        # Switch to root
su -                      # Switch to root with login environment
exit                      # Return to original user
```

## 🔒 Security Concepts

### Root vs User Privileges

**Root (Superuser):**
- Has complete system access
- Can modify any file
- Can install software
- Can change system settings
- Dangerous if misused

**Regular User:**
- Limited to their home directory
- Cannot modify system files
- Cannot install system software
- Safer for daily use

### Best Practices

1. **Never run as root for daily tasks**
2. **Use `sudo` for specific commands that need elevation**
3. **Set appropriate file permissions**
4. **Regularly audit file permissions**
5. **Use groups for shared access**

## 🏋️ Practice Exercises

### Exercise 1: Understanding Permissions
```bash
# Create test files
touch test1.txt test2.txt test3.txt

# Check current permissions
ls -la test*.txt

# Change permissions using symbolic mode
chmod u+rw test1.txt
chmod g+r test1.txt
chmod o-rwx test1.txt

# Check the result
ls -la test1.txt

# Change permissions using numeric mode
chmod 644 test2.txt
chmod 755 test3.txt

# Compare all files
ls -la test*.txt
```

### Exercise 2: Ownership Changes
```bash
# Create a test file
echo "Test content" > ownership_test.txt

# Check current ownership
ls -la ownership_test.txt

# Change ownership (if you have another user)
# sudo chown otheruser ownership_test.txt

# Change group
sudo chown :staff ownership_test.txt

# Verify changes
ls -la ownership_test.txt
```

### Exercise 3: Directory Permissions
```bash
# Create test directory
mkdir test_dir
touch test_dir/file1.txt test_dir/file2.txt

# Set directory permissions
chmod 755 test_dir
chmod 644 test_dir/file1.txt
chmod 600 test_dir/file2.txt

# Test access
ls -la test_dir/
ls -la test_dir/file1.txt
ls -la test_dir/file2.txt
```

### Exercise 4: Sudo Usage
```bash
# Try to read a system file
cat /etc/shadow

# Use sudo to read it
sudo cat /etc/shadow

# Check who you are
whoami

# Switch to root temporarily
sudo -i
whoami
exit

# Run a command as another user (if available)
# sudo -u otheruser whoami
```

## 🧪 Knowledge Check

### Multiple Choice Questions

1. **What does `chmod 755` set?**
   - a) Read/write for owner, read for group/others
   - b) Read/write/execute for owner, read/execute for group/others
   - c) Read/write/execute for all
   - d) Read/write for owner, read for group, nothing for others

2. **What is the difference between `sudo` and `su`?**
   - a) `sudo` runs one command, `su` switches user
   - b) `sudo` is safer, `su` is dangerous
   - c) `sudo` requires password, `su` doesn't
   - d) There's no difference

3. **What does `chmod u+x` do?**
   - a) Adds execute permission for user
   - b) Adds execute permission for all users
   - c) Removes execute permission for user
   - d) Sets execute permission for user only

4. **Which permission is most secure for a private file?**
   - a) 777
   - b) 755
   - c) 644
   - d) 600

### Practical Test

Complete these tasks in your terminal:

1. **Permission Management Test:**
   ```bash
   # Create test files
   touch secure.txt public.txt private.txt
   
   # Set appropriate permissions
   chmod 600 private.txt    # Owner only
   chmod 644 public.txt     # Owner read/write, others read
   chmod 755 secure.txt     # Owner all, others read/execute
   
   # Verify permissions
   ls -la *.txt
   
   # Try to read each file as different users
   cat private.txt
   cat public.txt
   cat secure.txt
   ```

2. **Sudo Test:**
   ```bash
   # Check current user
   whoami
   
   # Try to access system directory
   ls /root
   
   # Use sudo to access
   sudo ls /root
   
   # Check what sudo privileges you have
   sudo -l
   ```

## 📋 Cheat Sheet

### Permission Commands
```bash
# Change permissions
chmod 755 file.txt        # rwxr-xr-x
chmod 644 file.txt        # rw-r--r--
chmod 600 file.txt        # rw-------
chmod u+x file.txt        # Add execute for user
chmod -R 755 directory/   # Recursive change

# Change ownership
chown user file.txt       # Change owner
chown user:group file.txt # Change owner and group
chown -R user:group dir/  # Recursive ownership

# Check permissions
ls -la                    # List with permissions
stat file.txt             # Detailed file info
```

### Sudo Commands
```bash
sudo command              # Run as root
sudo -u user command      # Run as specific user
sudo -i                   # Interactive root shell
sudo -s                   # Root shell with current env
sudo !!                   # Previous command with sudo
```

### Common Permission Patterns
- `755` - Directories (rwxr-xr-x)
- `644` - Regular files (rw-r--r--)
- `600` - Private files (rw-------)
- `750` - Group access (rwxr-x---)
- `777` - Everyone everything (DANGEROUS!)

## ⚠️ Security Warnings

1. **Never use `chmod 777`** - This gives everyone full access
2. **Be careful with `sudo`** - Only use when necessary
3. **Don't run as root** - Use regular user for daily tasks
4. **Audit permissions regularly** - Check for overly permissive files
5. **Use groups for shared access** - Don't give everyone access

## 🎯 Next Steps

Once you've completed this module:
1. Take the knowledge check
2. Complete the practical tests
3. Practice with your own files
4. Move to [Module 03: Bash Scripting](../03-bash-scripting/README.md)

---

**Remember:** With great power comes great responsibility! Always think twice before using elevated privileges. 