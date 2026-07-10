# Automatic startup with systemd

The repository includes:

```text
systemd/codex-remote.service
```

## Edit the service

Replace every occurrence of `YOUR_USER` with your Linux username.

Find the Codex binary if needed:

```bash
command -v codex
readlink -f "$(command -v codex)"
```

Update `ExecStart` if your path differs.

## Install

From the repository directory:

```bash
sudo cp systemd/codex-remote.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable --now codex-remote.service
```

## Check status

```bash
systemctl status codex-remote.service
```

## View logs

```bash
journalctl -u codex-remote.service -f
```

## Restart

```bash
sudo systemctl restart codex-remote.service
```

## Disable

```bash
sudo systemctl disable --now codex-remote.service
```

## Note about daemon mode

The included unit starts `codex remote-control` in the foreground and lets systemd manage the process. This is usually cleaner than launching the internal background daemon from another service manager.
