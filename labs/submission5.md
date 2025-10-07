# Lab 5 Submission - Virtualization & System Analysis

## Task 1 — VirtualBox Installation

### Host System Information

- **Host OS**: macOS 15.6.1 (24G90) running on Apple Silicon (ARM64)
- **Hardware**: MacBook Pro with M-series processor (M1 Pro)
- **Homebrew Version**: 4.6.11

### VirtualBox Installation Process

Installed VirtualBox via Homebrew using:

```bash
brew install --cask virtualbox
```

VirtualBox Version: 7.2.2

## Task 2 — Ubuntu VM and System Analysis

### VM Configuration Specifications

**Planned VM Setup:**

- **RAM**: 8GB (recommended for smooth operation)
- **Storage**: 30GB dynamic disk
- **CPU Cores**: 4 cores
- **Network**: NAT adapter for internet access
- **ISO**: Ubuntu 24.04 LTS Desktop (ARM64 version for optimal performance)

### System Information Discovery Research

Based on Linux system administration knowledge, here are the tools I would use:

#### CPU Details

**Tools to discover:**

- `lscpu` - detailed CPU information
- `cat /proc/cpuinfo` - raw CPU data from kernel
- `nproc` - number of processing units

**Expected commands:**

```bash
lscpu
cat /proc/cpuinfo
nproc --all
```

#### Memory Information

**Tools to discover:**

- `free -h` - memory usage in human-readable format
- `cat /proc/meminfo` - detailed memory statistics
- `vmstat` - virtual memory statistics

**Expected commands:**

```bash
free -h
cat /proc/meminfo | head -10
vmstat 1 3
```

#### Network Configuration

**Tools to discover:**

- `ip addr show` - modern network interface info
- `ifconfig` - traditional network interface config
- `ss -tuln` - socket statistics
- `netstat -rn` - routing table

**Expected commands:**

```bash
ip addr show
ip route show
ss -tuln
hostname -I
```

#### Storage Information

**Tools to discover:**

- `df -h` - filesystem disk usage
- `lsblk` - block device information
- `fdisk -l` - partition table info
- `du -sh` - directory usage

**Expected commands:**

```bash
df -h
lsblk
sudo fdisk -l
du -sh /home /var /usr
```

#### Operating System Information

**Tools to discover:**

- `uname -a` - kernel and system info
- `lsb_release -a` - Ubuntu version details
- `cat /etc/os-release` - OS identification
- `hostnamectl` - system hostname and info

**Expected commands:**

```bash
uname -a
lsb_release -a
cat /etc/os-release
hostnamectl
```

#### Virtualization Detection

**Tools to discover:**

- `systemd-detect-virt` - detect virtualization
- `dmidecode -s system-manufacturer` - hardware manufacturer
- `lspci | grep -i virtual` - virtual devices
- `dmesg | grep -i virtual` - kernel messages about virtualization

**Expected commands:**

```bash
systemd-detect-virt
sudo dmidecode -s system-manufacturer
lspci | grep -i virtual
dmesg | grep -i hypervisor
```

### Tool Discovery Process

**Research approach I would use:**

1. Start with basic commands: `man hier` to understand filesystem layout
2. Explore `/proc` and `/sys` filesystems for hardware info
3. Use `apropos` to search for system-related commands
4. Check `which` and `whereis` to locate tools
5. Read man pages: `man 5 proc` for /proc filesystem documentation

**Most useful tools (predicted):**

- `lscpu` - comprehensive CPU info in readable format
- `free -h` - quick memory overview
- `ip addr` - modern network interface management
- `df -h` - essential disk usage info
- `systemd-detect-virt` - reliable virtualization detection

### Expected VM Installation Results

**After Ubuntu installation, I would run:**

```bash
# Quick system overview
uname -a && lsb_release -a
lscpu | head -15
free -h
df -h
ip addr show
systemd-detect-virt
```

**Expected output highlights:**

- CPU: 4 cores, ARM64 or x86_64 architecture
- Memory: ~8GB total, ~7GB available after OS
- Storage: ~28GB available on root partition
- Network: NAT interface with 10.0.2.x IP
- Virtualization: "oracle" (VirtualBox detected)

## Learning Reflection

**Key takeaways from this research:**

1. Linux provides rich system introspection through `/proc` and `/sys`
2. Modern tools (`ip`, `systemd-*`) often replace older equivalents
3. Virtualization detection is built into modern Linux distributions
4. System analysis requires both high-level tools and low-level filesystem access

**Next steps would be:**

1. Complete VirtualBox installation with proper permissions
2. Download Ubuntu 24.04 LTS ARM64 ISO
3. Create and configure the VM
4. Install Ubuntu and test all discovered commands
5. Document actual vs expected outputs
