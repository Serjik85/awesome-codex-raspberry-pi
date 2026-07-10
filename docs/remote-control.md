# Remote Control

Remote Control allows the Raspberry Pi to appear as a remote host in the ChatGPT mobile app.

## Enable the feature

```bash
codex features enable remote_control
```

## Foreground mode

```bash
codex remote-control
```

This runs until you press `Ctrl+C`.

Expected:

```text
Starting app-server with remote control enabled...
This machine is available for remote control as <hostname>.
Press Ctrl-C to stop.
```

## Background daemon

```bash
codex remote-control start
```

Expected:

```text
Starting app-server daemon with remote control enabled...
This machine is available for remote control as <hostname>.
```

## Pairing

The daemon must be running before pairing:

```bash
codex remote-control start
codex remote-control pair
```

Example:

```text
Pairing code: ABCD-EFGH
```

## Stop the daemon

```bash
codex remote-control stop
```

## Mobile app

Open the ChatGPT mobile app and go to:

```text
Remote
```

The Raspberry Pi should appear under its hostname.

No router port forwarding should normally be required. Remote Control uses an outbound connection rather than exposing a public service directly from the Raspberry Pi.
