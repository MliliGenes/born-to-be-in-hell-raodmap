# Born2BeRoot Project 🖥️

## Project Overview

Born2BeRoot is an intricate system administration project designed to immerse students in the world of virtualization, server configuration, and cybersecurity principles. Through this project, you'll transform a virtual machine into a secured, minimalist server environment while demonstrating deep understanding of Linux system management.

## 🔍 Project Resources

### Official Documentation
- [42 School Born2BeRoot Subject](en.subject.pdf)

### Community Guides
1. **Project Bible**
   - [Miro Board - Project Bible by @zmoumen @mrian @aboubara](https://miro.com/app/board/uXjVPEVHTXk=/)
   
2. **Extended Project Guide**
   - [Miro Board - Extended Version](https://miro.com/app/board/uXjVP37UxCE=/)

### Repository References
1. **Comprehensive Implementation**
   - [Ayoub's Born2BeRoot Repository](https://github.com/ayoub0x1/born2beroot/tree/main)
   
2. **Step-by-Step Tutorial**
   - [Born2BeRoot Tutorial by gemartin99](https://github.com/gemartin99/Born2beroot-Tutorial/blob/main/README_EN.md)

## 💻 System Preparation and Installation

### Virtual Machine Setup
```bash
# Recommended Virtual Machine Tools
# - VirtualBox (Primary Recommendation)
# - UTM (Mac Alternative)

# Minimum System Requirements
# - RAM: 1024 MB
# - Storage: 10-12 GB
# - No Graphical Interface
```

### Operating System Selection
- **Recommended: Debian**
  - More beginner-friendly
  - Stable and well-documented
- **Alternative: Rocky Linux**
  - More advanced configuration
  - Enterprise-level security features

### Partitioning Strategy
```bash
# LVM with Encryption Requirements
# Minimum 2 Encrypted Partitions
# Example Partition Layout:
# - /boot (500 MB, unencrypted)
# - swap (2 GB)
# - / (root partition)
# - /home
# - /var

# Verification Commands
sudo lvdisplay   # List Logical Volumes
sudo vgdisplay   # Volume Group Details
sudo pvdisplay   # Physical Volume Information
```

## 🔒 Security Configuration

### SSH Configuration
```bash
# SSH Service Setup
sudo apt-get install openssh-server  # Debian
sudo systemctl start ssh
sudo systemctl enable ssh

# Modify SSH Configuration
sudo nano /etc/ssh/sshd_config
# Key Modifications:
# - Port 4242
# - PermitRootLogin no
# - PasswordAuthentication yes

sudo systemctl restart ssh
```

### Firewall Implementation
```bash
# UFW (Debian)
sudo apt-get install ufw
sudo ufw enable
sudo ufw allow 4242/tcp
sudo ufw status

# Firewalld (Rocky Linux)
sudo dnf install firewalld
sudo systemctl start firewalld
sudo firewall-cmd --permanent --add-port=4242/tcp
sudo firewall-cmd --reload
```

### Password Policy Enforcement
```bash
# Password Complexity Configuration
sudo nano /etc/login.defs
# Set Parameters:
# PASS_MAX_DAYS 30     # Password expires every 30 days
# PASS_MIN_DAYS 2      # Minimum 2 days before password change
# PASS_WARN_AGE 7      # Warning 7 days before expiration

# PAM Configuration for Complex Passwords
sudo nano /etc/pam.d/common-password
# Add Complexity Requirements:
# password requisite pam_pwquality.so \
#   minlen=10          # Minimum 10 characters
#   ucredit=-1         # At least one uppercase
#   lcredit=-1         # At least one lowercase
#   dcredit=-1         # At least one digit
#   maxrepeat=3        # Maximum 3 consecutive identical characters
#   reject_username    # Prevent username in password
```

### Sudo Configuration
```bash
# Sudo Installation
sudo apt-get install sudo

# Sudo Configuration
sudo visudo
# Add/Modify Configuration:
# Defaults	passwd_tries=3
# Defaults	badpass_message="Incorrect sudo password"
# Defaults	log_input
# Defaults	log_output
# Defaults	iolog_dir="/var/log/sudo/"
# Defaults	requiretty
```

### Monitoring Script Development
```bash
#!/bin/bash
# monitoring.sh
# Generates system information broadcast every 10 minutes

# System Architecture Details
ARCH=$(uname -a)
CPU_PHYSICAL=$(grep "physical id" /proc/cpuinfo | wc -l)
CPU_VIRTUAL=$(grep "processor" /proc/cpuinfo | wc -l)
# Additional metrics follow similar pattern
```

## 🚀 Bonus Opportunities
- WordPress website setup
- Additional service implementation
- Complex partitioning schemes

## 📋 Submission Requirements
- Generate `signature.txt`
```bash
# Generate Virtual Disk Signature
# Windows: certUtil -hashfile <vm_name>.vdi sha1
# Linux/Mac: sha1sum <vm_name>.vdi
```

## 🧠 Evaluation Preparation
- Understand differences between `apt` and `aptitude`
- Know SELinux/AppArmor configurations
- Explain monitoring script mechanics
- Demonstrate systematic configuration approach

## ⚠️ Critical Warnings
- Bonus part evaluated only if mandatory part is perfect
- Virtual machine signature must match `signature.txt`
- No graphical interface allowed

## 🤝 Community and Acknowledgments
Special thanks to 42 School and the open-source community for creating this transformative learning experience.

## 📚 Recommended Learning Path
1. Virtualization fundamentals
2. Linux system administration
3. Cybersecurity principles
4. Bash scripting
5. Network configuration strategies

---

**Pro Tip**: This project is not just about completing tasks, but understanding the "why" behind each configuration. Take time to research, experiment, and truly comprehend the security principles you're implementing.
