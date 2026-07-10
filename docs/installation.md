# Installation

## Requirements

- Raspberry Pi or another ARM64 Linux machine
- Debian-based operating system
- Internet connection
- A ChatGPT account with access to Codex
- SSH access, monitor and keyboard, or another terminal

## Install Codex CLI

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

The installer may add Codex to your shell PATH. Open a new terminal after installation.

Confirm:

```bash
codex --version
```

## Install Bubblewrap

Codex can use its bundled Bubblewrap, but installing the operating system package removes the warning and provides the expected sandbox dependency.

```bash
sudo apt update
sudo apt install bubblewrap
```

Confirm:

```bash
bwrap --version
```

## Start Codex

```bash
codex
```

Inside Codex, try:

```text
What is the current operating system?
```

Codex should be able to run commands such as `uname -a` and read `/etc/os-release`.
