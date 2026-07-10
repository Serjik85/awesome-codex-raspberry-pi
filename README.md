# OpenAI Codex Remote on Raspberry Pi

Run OpenAI Codex CLI on a Raspberry Pi, enable experimental Remote Control, and access the Pi from the ChatGPT mobile app.

> Community guide based on a working Raspberry Pi setup. Remote Control is currently experimental and behavior may change between Codex versions.

## What this project covers

- Installing Codex CLI on Raspberry Pi
- Signing in with ChatGPT
- Migrating an existing Codex login between your own trusted devices
- Installing Bubblewrap
- Enabling experimental Remote Control
- Starting and pairing the remote host
- Showing the Raspberry Pi in ChatGPT Mobile
- Starting Remote Control automatically
- Fixing common errors

## Tested setup

| Component | Tested value |
|---|---|
| Device | Raspberry Pi |
| Architecture | ARM64 / aarch64 |
| Operating system | Debian GNU/Linux 13 Trixie |
| Codex CLI | 0.144.1 |
| Remote host | ChatGPT mobile app |

## Important security note

The file `~/.codex/auth.json` contains sensitive authentication tokens.

- Treat it like a password
- Never commit it to Git
- Never upload it to an issue, forum, screenshot, or public cloud folder
- Copy it only between devices that you own and trust
- Set file permissions to `600` on Linux

## Quick start

### 1. Install Codex CLI

```bash
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

Open a new terminal and confirm the installation:

```bash
codex --version
```

### 2. Sign in

For a normal interactive login:

```bash
codex login
```

For a headless device:

```bash
codex login --device-auth
```

Check the result:

```bash
codex login status
```

Expected output:

```text
Logged in using ChatGPT
```

If sign-in is blocked but Codex already works on another device that you own, see [Authentication migration](docs/authentication.md).

### 3. Install Bubblewrap

```bash
sudo apt update
sudo apt install bubblewrap
```

### 4. Enable Remote Control

```bash
codex features enable remote_control
```

Expected output:

```text
Enabled feature `remote_control` in config.toml.
```

### 5. Start the remote daemon

```bash
codex remote-control start
```

Expected output:

```text
Starting app-server daemon with remote control enabled...
This machine is available for remote control as <hostname>.
```

### 6. Generate a pairing code

```bash
codex remote-control pair
```

Example:

```text
Pairing code: ABCD-EFGH
```

### 7. Open ChatGPT Mobile

Open:

```text
ChatGPT -> Remote -> your Raspberry Pi hostname
```

The host should appear with a green online indicator.

## Test the connection

Open a Codex session and ask:

```text
Create a file named hello.py that prints "Hello from Codex"
```

Then verify:

```bash
cat hello.py
python3 hello.py
```

Expected output:

```text
Hello from Codex
```

## Automatic startup

A ready-to-use service file is included:

```text
systemd/codex-remote.service
```

Before installing it, replace `YOUR_USER` with your Linux username.

Install:

```bash
sudo cp systemd/codex-remote.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now codex-remote.service
```

Check status:

```bash
systemctl status codex-remote.service
```

See [Automatic startup](docs/systemd.md) for details.

## Documentation

- [Installation](docs/installation.md)
- [Authentication migration](docs/authentication.md)
- [Remote Control](docs/remote-control.md)
- [Automatic startup](docs/systemd.md)
- [Troubleshooting](docs/troubleshooting.md)
- [FAQ](docs/faq.md)

## Repository structure

```text
codex-remote-raspberry-pi/
├── README.md
├── LICENSE
├── .gitignore
├── docs/
│   ├── installation.md
│   ├── authentication.md
│   ├── remote-control.md
│   ├── systemd.md
│   ├── troubleshooting.md
│   └── faq.md
├── screenshots/
│   └── README.md
└── systemd/
    └── codex-remote.service
```

## Disclaimer

This is an independent community project. It is not affiliated with or endorsed by OpenAI.

Remote Control is experimental. Commands and configuration may change in future Codex releases.

## Contributing

Issues and pull requests are welcome. Please remove usernames, hostnames, email addresses, pairing codes, tokens, IP addresses, and other private information before posting logs or screenshots.

## License

MIT
