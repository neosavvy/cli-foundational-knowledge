# Module 04: Networking

## 🎯 Learning Objectives

By the end of this module, you will be able to:
- Understand basic networking concepts and protocols
- Configure and view network interfaces using `ifconfig`
- Perform DNS lookups and troubleshoot name resolution with `nslookup`
- Trace network routes using `traceroute`
- Perform network discovery and security scanning with `nmap`
- Diagnose common network connectivity issues
- Understand network security implications

## 📚 Core Concepts

### Network Fundamentals

**IP Addresses:**
- IPv4: 192.168.1.1 (32-bit addresses)
- IPv6: 2001:db8::1 (128-bit addresses)
- Private ranges: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16

**Common Ports:**
- 22: SSH
- 80: HTTP
- 443: HTTPS
- 53: DNS
- 25: SMTP
- 110: POP3
- 143: IMAP

**Network Layers:**
- Physical (cables, wireless)
- Data Link (MAC addresses)
- Network (IP addresses)
- Transport (TCP/UDP)
- Application (HTTP, FTP, SSH)

## 📚 Core Commands

### `ifconfig` - Network Interface Configuration

`ifconfig` displays and configures network interfaces.

#### Basic Usage
```bash
ifconfig                    # Show all interfaces
ifconfig eth0              # Show specific interface
ifconfig eth0 up           # Enable interface
ifconfig eth0 down         # Disable interface
ifconfig eth0 192.168.1.100  # Set IP address
```

#### Modern Alternative: `ip`
```bash
ip addr show               # Show all interfaces
ip addr show eth0          # Show specific interface
ip link set eth0 up        # Enable interface
ip addr add 192.168.1.100/24 dev eth0  # Add IP address
```

#### Interface Information
```bash
# View detailed interface info
ifconfig eth0

# Output includes:
# - IP address and netmask
# - MAC address
# - Interface status (UP/DOWN)
# - Packet statistics
# - MTU size
```

### `nslookup` - DNS Lookup Tool

`nslookup` queries DNS servers to resolve domain names to IP addresses.

#### Basic Usage
```bash
nslookup google.com        # Lookup domain
nslookup 8.8.8.8          # Reverse lookup IP
nslookup -type=mx google.com  # Lookup MX records
nslookup -type=ns google.com  # Lookup NS records
```

#### Interactive Mode
```bash
nslookup
> google.com              # Lookup domain
> set type=mx             # Set record type
> google.com              # Lookup MX records
> server 8.8.8.8         # Use specific DNS server
> google.com              # Query using new server
> exit                    # Exit nslookup
```

#### Record Types
```bash
nslookup -type=A google.com      # A record (IPv4)
nslookup -type=AAAA google.com   # AAAA record (IPv6)
nslookup -type=CNAME www.google.com  # CNAME record
nslookup -type=MX google.com     # Mail exchange
nslookup -type=NS google.com     # Name servers
nslookup -type=TXT google.com    # TXT records
```

### `traceroute` - Network Path Tracing

`traceroute` shows the network path packets take to reach a destination.

#### Basic Usage
```bash
traceroute google.com      # Trace route to domain
traceroute 8.8.8.8        # Trace route to IP
traceroute -n google.com   # Don't resolve hostnames
traceroute -I google.com   # Use ICMP instead of UDP
```

#### Understanding Output
```bash
traceroute google.com
# Output shows:
# 1. Hop number
# 2. Router/host name and IP
# 3. Response times (3 probes)
# 4. * indicates no response
```

#### Advanced Options
```bash
traceroute -m 15 google.com      # Max 15 hops
traceroute -w 1 google.com       # Wait 1 second
traceroute -q 5 google.com       # Send 5 probes per hop
traceroute -p 80 google.com      # Use port 80
```

### `nmap` - Network Discovery and Security Scanner

`nmap` is a powerful network scanner for discovering hosts and services.

#### Basic Scanning
```bash
nmap localhost              # Scan localhost
nmap 192.168.1.0/24        # Scan entire subnet
nmap -sn 192.168.1.0/24    # Ping scan (host discovery only)
nmap -p 80,443 google.com   # Scan specific ports
```

#### Port Scanning
```bash
nmap -p- localhost          # Scan all ports (1-65535)
nmap -p 22,80,443 google.com  # Scan specific ports
nmap --top-ports 10 localhost  # Scan top 10 most common ports
nmap -sS localhost          # SYN scan (stealth)
nmap -sU localhost          # UDP scan
```

#### Service Detection
```bash
nmap -sV localhost          # Version detection
nmap -sC localhost          # Default script scan
nmap -A localhost           # Aggressive scan (all features)
nmap --script=vuln localhost  # Vulnerability scan
```

#### Network Discovery
```bash
nmap -sn 192.168.1.0/24    # Find live hosts
nmap -PR 192.168.1.0/24    # ARP ping scan
nmap -PE 192.168.1.0/24    # ICMP echo scan
nmap -PS 192.168.1.0/24    # TCP SYN ping scan
```

## 🏋️ Practice Exercises

### Exercise 1: Network Interface Analysis
```bash
# View all network interfaces
ifconfig

# Or use modern ip command
ip addr show

# Check specific interface (replace eth0 with your interface)
ifconfig eth0

# Check interface statistics
ifconfig eth0 | grep -E "(RX|TX)"

# Test interface connectivity
ping -c 4 8.8.8.8
```

### Exercise 2: DNS Troubleshooting
```bash
# Basic DNS lookup
nslookup google.com

# Check different record types
nslookup -type=A google.com
nslookup -type=MX google.com
nslookup -type=NS google.com

# Test with different DNS servers
nslookup google.com 8.8.8.8
nslookup google.com 1.1.1.1

# Reverse DNS lookup
nslookup 8.8.8.8
```

### Exercise 3: Network Path Analysis
```bash
# Trace route to a website
traceroute google.com

# Compare with different destinations
traceroute github.com
traceroute amazon.com

# Use different options
traceroute -n google.com    # No hostname resolution
traceroute -m 10 google.com # Limit to 10 hops
traceroute -I google.com    # Use ICMP
```

### Exercise 4: Network Discovery with nmap
```bash
# Scan localhost
nmap localhost

# Discover hosts on your network (replace with your subnet)
nmap -sn 192.168.1.0/24

# Scan specific ports
nmap -p 22,80,443,8080 localhost

# Service version detection
nmap -sV localhost

# Scan your own machine thoroughly
nmap -A localhost
```

### Exercise 5: Network Diagnostics
```bash
# Test basic connectivity
ping -c 4 google.com

# Check DNS resolution
dig google.com

# Test specific port connectivity
telnet google.com 80
# Or use nc (netcat)
nc -zv google.com 80

# Check routing table
route -n
# Or modern equivalent
ip route show
```

## 🧪 Knowledge Check

### Multiple Choice Questions

1. **What does `nslookup -type=mx google.com` do?**
   - a) Looks up the IP address of google.com
   - b) Looks up the mail exchange servers for google.com
   - c) Looks up the name servers for google.com
   - d) Performs a reverse DNS lookup

2. **What is the purpose of `traceroute`?**
   - a) To measure network bandwidth
   - b) To show the network path packets take
   - c) To configure network interfaces
   - d) To scan for open ports

3. **What does `nmap -sn` do?**
   - a) Performs a stealth scan
   - b) Scans for open ports
   - c) Performs host discovery only
   - d) Scans for vulnerabilities

4. **Which command shows network interface information?**
   - a) `netstat`
   - b) `ifconfig`
   - c) `ping`
   - d) `route`

### Practical Test

Complete these tasks in your terminal:

1. **Network Interface Test:**
   ```bash
   # View your network interfaces
   ifconfig
   
   # Find your IP address
   ifconfig | grep "inet "
   
   # Check if your interface is up
   ifconfig eth0  # or your interface name
   ```

2. **DNS Resolution Test:**
   ```bash
   # Test DNS resolution
   nslookup google.com
   
   # Test with different DNS servers
   nslookup google.com 8.8.8.8
   nslookup google.com 1.1.1.1
   
   # Check different record types
   nslookup -type=mx google.com
   nslookup -type=ns google.com
   ```

3. **Network Path Test:**
   ```bash
   # Trace route to a website
   traceroute google.com
   
   # Compare with a different site
   traceroute github.com
   
   # Use different options
   traceroute -n google.com
   ```

4. **Network Discovery Test:**
   ```bash
   # Scan localhost
   nmap localhost
   
   # Scan your own machine thoroughly
   nmap -A localhost
   
   # Discover hosts on your network (be careful!)
   nmap -sn 192.168.1.0/24  # Replace with your subnet
   ```

## 📋 Cheat Sheet

### Network Interface Commands
```bash
ifconfig                    # Show all interfaces
ifconfig eth0              # Show specific interface
ip addr show               # Modern interface command
ip link show               # Show interface status
```

### DNS Commands
```bash
nslookup domain.com        # Basic lookup
nslookup -type=mx domain.com  # Mail records
nslookup -type=ns domain.com  # Name servers
dig domain.com             # Alternative DNS tool
```

### Network Path Commands
```bash
traceroute domain.com      # Trace network path
traceroute -n domain.com   # No hostname resolution
traceroute -m 10 domain.com # Limit hops
```

### Network Scanning Commands
```bash
nmap localhost             # Scan localhost
nmap -sn 192.168.1.0/24   # Host discovery
nmap -p 80,443 domain.com  # Port scan
nmap -sV localhost         # Version detection
```

### Connectivity Testing
```bash
ping domain.com            # Test connectivity
telnet domain.com 80       # Test specific port
nc -zv domain.com 80       # Netcat port test
```

## ⚠️ Security and Legal Considerations

1. **Only scan networks you own or have permission to scan**
2. **Be aware that some network scanning may be detected as suspicious activity**
3. **Use nmap responsibly and ethically**
4. **Respect network policies and terms of service**
5. **Some tools may require elevated privileges (sudo)**

## 🎯 Next Steps

Once you've completed this module:
1. Take the knowledge check
2. Complete the practical tests
3. Practice with your own network
4. Move to [Module 05: File Editing](../05-file-editing/README.md)

---

**Remember:** Network tools can be powerful but also potentially disruptive. Always use them responsibly and only on networks you have permission to test! 