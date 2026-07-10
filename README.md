# OpenAI Codex on Raspberry Pi

> Run OpenAI Codex on Raspberry Pi with Remote Control support and manage it directly from the ChatGPT mobile app.

![GitHub stars](https://img.shields.io/github/stars/YOUR_USERNAME/codex-remote-raspberry-pi?style=flat-square)
![Platform](https://img.shields.io/badge/Platform-Raspberry%20Pi-green?style=flat-square)
![OS](https://img.shields.io/badge/Debian-13-red?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

---

## Features

- ✅ Install OpenAI Codex CLI on Raspberry Pi
- ✅ Enable Remote Control
- ✅ Use Raspberry Pi directly from the ChatGPT mobile app
- ✅ Automatic startup using systemd
- ✅ Bubblewrap configuration
- ✅ Troubleshooting guide

---

## Tested Environment

| Component | Version |
|------------|---------|
| Raspberry Pi 4 | ✅ |
| Raspberry Pi OS | Debian 13 (Trixie) |
| Codex CLI | v0.144.1 |
| ChatGPT Mobile | Latest |

---

# Installation

## Install Codex

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Verify installation:

```bash
codex --version
```

---

# Login

Authenticate using your ChatGPT account.

```bash
codex login
```

Verify:

```bash
codex login status
```

Expected:

```text
Logged in using ChatGPT
```

---

# Install Bubblewrap

Although Codex can run without it, Bubblewrap is recommended.

```bash
sudo apt update
sudo apt install bubblewrap
```

---

# Enable Remote Control

Enable the experimental feature:

```bash
codex features enable remote_control
```

---

# Start Remote Control

Foreground mode

```bash
codex remote-control
```

Background daemon

```bash
codex remote-control start
```

Expected output:

```text
Starting app-server daemon with remote control enabled...
This machine is available for remote control as <hostname>
```

---

# Pairing

Generate a temporary pairing code:

```bash
codex remote-control pair
```

Example:

```text
Pairing code:
ABCD-EFGH
```

---

# ChatGPT Mobile

Open

```
ChatGPT
        ↓
      Remote
        ↓
 Raspberry Pi
```

Your Raspberry Pi should appear automatically.

---

# Auto Start

Create

```
/etc/systemd/system/codex-remote.service
```

```ini
[Unit]
Description=OpenAI Codex Remote Control
After=network-online.target

[Service]
Type=simple
User=YOUR_USER
WorkingDirectory=/home/YOUR_USER
ExecStart=/home/YOUR_USER/.codex/packages/standalone/current/codex remote-control start
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Reload systemd

```bash
sudo systemctl daemon-reload
```

Enable service

```bash
sudo systemctl enable codex-remote
```

Start service

```bash
sudo systemctl start codex-remote
```

Check status

```bash
systemctl status codex-remote
```

---

# Troubleshooting

## Bubblewrap warning

Install Bubblewrap

```bash
sudo apt install bubblewrap
```

---

## Connection refused

```
failed to connect to app-server-control.sock
```

Solution

```bash
codex remote-control start
```

---

## Pair command fails

Make sure the daemon is running:

```bash
codex remote-control start
```

Then run:

```bash
codex remote-control pair
```

---

## Raspberry Pi does not appear inside ChatGPT

Verify Remote Control is enabled

```bash
codex features enable remote_control
```

Verify daemon

```bash
codex remote-control start
```

Expected

```text
This machine is available for remote control as <hostname>
```

Restart the ChatGPT mobile app if necessary.

---

# Example

Create a Python file

```
Create hello.py that prints "Hello from Codex"
```

Codex creates

```python
print("Hello from Codex")
```

Run

```bash
python3 hello.py
```

Output

```
Hello from Codex
```

---

# Project Structure

```
Raspberry Pi
│
├── Codex CLI
├── Remote Control
├── ChatGPT Account
└── systemd
      │
      ▼
ChatGPT Mobile
      │
      ▼
 Remote
      │
      ▼
 Raspberry Pi
```

---

# Contributing

Contributions, improvements and testing on additional Raspberry Pi models are welcome.

Feel free to open Issues or Pull Requests.

---

# License

MIT
