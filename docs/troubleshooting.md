# Troubleshooting

## `codex: command not found`

Open a new terminal after installation.

Check:

```bash
echo "$PATH"
find ~/.codex -type f -name codex 2>/dev/null
```

## Bubblewrap warning

Message:

```text
Codex could not find bubblewrap on PATH
```

Fix:

```bash
sudo apt update
sudo apt install bubblewrap
```

## Pairing fails with connection refused

Message:

```text
failed to connect to ... app-server-control.sock
Connection refused (os error 111)
```

Cause:

The Remote Control daemon is not running.

Fix:

```bash
codex remote-control start
codex remote-control pair
```

## `ss -tulpn | grep codex` returns nothing

This does not necessarily mean Remote Control is broken. Codex can use Unix sockets and outbound connections instead of listening on a public TCP port.

Check the process:

```bash
ps aux | grep '[c]odex'
```

Check the local control directory:

```bash
ls -la ~/.codex/app-server-control/
```

## Raspberry Pi does not appear in ChatGPT Mobile

Run:

```bash
codex login status
codex features enable remote_control
codex remote-control start
```

Confirm the output contains:

```text
This machine is available for remote control as <hostname>.
```

Then:

- Fully close and reopen the ChatGPT mobile app
- Confirm the mobile app uses the same ChatGPT account
- Generate a new pairing code
- Confirm the Raspberry Pi has internet access
- Check system time and time zone

## Token expired or refresh token already used

If another trusted device still has a working Codex login, copy a fresh `auth.json` from that device.

Never paste token contents into chat, GitHub issues, or screenshots.

## The command was typed into Bash instead of Codex

This will fail:

```bash
Create a file hello.py
```

Bash treats `Create` as a command.

Start Codex first:

```bash
codex
```

Then enter the natural-language instruction inside the Codex interface.
