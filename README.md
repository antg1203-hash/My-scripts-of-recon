# My Scripts of Recon and Tinkering

Just experimenting and doing recon (and pretty much everything) on my phone with Termux.

## Table of Contents

- [Initial Setup](#initial-setup)
- [Basic Recon](#basic-recon)
- [Network Recon](#network-recon)
- [Termux Environments](#termux-environments)
- [Testing and Benchmarks](#testing-and-benchmarks)
- [Bypassing Cloudflare](#bypassing-cloudflare)

---

## Initial Setup

Before starting any recon activities, make sure your system is up to date:

```bash
pkg update && pkg upgrade -y
```

This ensures that all tools are running the latest versions.

---

## Basic Recon

Collection of basic reconnaissance commands for information gathering.

### Robots.txt Enumeration

Extract disallowed paths from Google's robots.txt:

```bash
curl -s https://www.google.com/robots.txt | grep "Disallow" > google.txt
```

### Wayback Machine Enumeration

Retrieve historical URLs from Wayback Machine:

```bash
timeout 60s waybackurls tesla.com > tesla_total.txt
```

### Grep for Sensitive Keywords

Search for common sensitive paths and keywords:

```bash
grep -i "api\|debug\|internal\|admin\|backup\|config\|env\|db" tesla_total.txt | head -n 30
```

### File Information

Check file size and details:

```bash
ls -lh tesla_total.txt
```

### CTF Practice (OverTheWire)

Connect to OverTheWire labs for practice:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

---

## Network Recon

Network reconnaissance tools - no root privileges required (proot is optional).

### Basic Nmap Scan

Scan localhost:

```bash
nmap localhost --unprivileged
```

### Network Range Scan

Scan a subnet (CIDR notation):

```bash
nmap (example IP)/24
```

---

## Termux Environments

### Using Proot Distributions

Termux allows you to run full Linux distributions using proot.

#### Debian

```bash
proot-distro login debian
```

#### Ubuntu

```bash
proot-distro login ubuntu
```

### ⚠️ VERY IMPORTANT

When using proot, use `apt` instead of `pkg`:

```bash
# Inside proot (use apt)
apt update && apt upgrade

# Outside proot (use pkg)
pkg update && pkg upgrade
```

This applies to all package installations as well:
- **proot**: `apt install <package>`
- **Termux**: `pkg install <package>`

---

## Testing and Benchmarks

### CPU Benchmarking with Sysbench

#### Single-thread Test

```bash
sysbench cpu --cpu-max-prime=10000 run
```

#### Multi-thread Test

Replace `8` with your device's actual thread count:

```bash
sysbench cpu --cpu-max-prime=10000 --threads=8 run
```

### Password Cracking Benchmarks with John

Test your device's password cracking capability:

```bash
john --test
```

---

## Bypassing Cloudflare

Techniques to bypass or work around Cloudflare protection.

### Method 1: User-Agent Spoofing with Curl

#### Simple User-Agent

```bash
curl -s -L -A "Mozilla/5.0 ..." https://www.carsdirect.com/robots.txt | grep -i disallow
```

#### Full User-Agent String

```bash
curl -s -A "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36" https://www.carsdirect.com/robots.txt | grep -i disallow
```

### Method 2: Python with fake_useragent

```python
from fake_useragent import UserAgent
import requests

ua = UserAgent()
headers = {'User-Agent': ua.random}
response = requests.get(url, headers=headers)
```

### Method 3: Seleniumbase with UC Mode (Undetected Chromium)

This method uses undetected browser automation to bypass Cloudflare:

```python
# pip3 install seleniumbase

from seleniumbase import Driver

# Initialize driver with UC mode enabled
driver = Driver(uc=True)

# Set target URL
url = "https://www.scrapingcourse.com/cloudflare-challenge"

# Open URL using UC mode with reconnect
driver.uc_open_with_reconnect(url, reconnect_time=4)

driver.sleep(10)

# Attempt to click the CAPTCHA checkbox
driver.uc_gui_click_captcha()

# Wait for CAPTCHA solving
driver.sleep(10)

# ... scraping logic here ...

# Close the browser and end the session
driver.quit()
```

---

## Notes

- These techniques are for educational and authorized testing purposes only
- Always ensure you have permission before performing recon on any target
- Cloudflare bypass methods may not work reliably and are constantly being updated
