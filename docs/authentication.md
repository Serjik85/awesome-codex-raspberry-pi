# Authentication migration

## Normal sign-in

Use one of the official login flows:

```bash
codex login
```

For a remote or headless machine:

```bash
codex login --device-auth
```

Check status:

```bash
codex login status
```

## Migrating an existing login between your own devices

This method is useful when:

- Codex is already signed in on one trusted computer
- You are adding another device that you own
- The normal login flow cannot be completed on the new device

The source device must already have a valid Codex login.

### Security warning

`auth.json` contains sensitive tokens. Never publish it, commit it, attach it to an issue, or display its contents.

### Windows source device

The usual file location is:

```text
%USERPROFILE%\.codex\auth.json
```

Copy it to the Raspberry Pi:

```powershell
scp $env:USERPROFILE\.codex\auth.json YOUR_USER@RASPBERRY_PI_IP:/home/YOUR_USER/auth.json
```

### Linux or macOS source device

```bash
scp ~/.codex/auth.json YOUR_USER@RASPBERRY_PI_IP:/home/YOUR_USER/auth.json
```

### On the Raspberry Pi

```bash
mkdir -p ~/.codex
mv ~/auth.json ~/.codex/auth.json
chmod 600 ~/.codex/auth.json
```

Confirm:

```bash
codex login status
```

Expected:

```text
Logged in using ChatGPT
```

## Backup

Store a backup only on an encrypted or otherwise trusted device.

Linux:

```bash
cp ~/.codex/auth.json ~/codex-auth-backup.json
chmod 600 ~/codex-auth-backup.json
```

Windows PowerShell:

```powershell
New-Item -ItemType Directory -Path E:\Backup -Force
Copy-Item $env:USERPROFILE\.codex\auth.json E:\Backup\codex-auth.json
```

Do not add this file to Git.
