# FAQ

## Does Raspberry Pi appear directly in ChatGPT Remote?

Yes, when the experimental Remote Control feature is enabled and the remote daemon is running.

## Do I need to open a router port?

Normally no. The connection is outbound and does not require exposing the Raspberry Pi directly to the internet.

## Does it work on ARM64?

It was tested successfully on an ARM64 Raspberry Pi system.

## Is Remote Control stable?

It is marked experimental. Commands and behavior may change.

## Can I copy `auth.json`?

Only between devices that you own and trust. Treat it like a password and never publish it.

## Can I copy Codex chat history too?

Codex stores local state under `~/.codex`, including a `sessions` directory in some versions. Back up the destination first and copy only while Codex is stopped. Storage formats may change between versions.

## Why does `pair` fail?

The app-server daemon must be running first:

```bash
codex remote-control start
codex remote-control pair
```

## How do I see the hostname?

```bash
hostname
```

That hostname is normally the name shown in ChatGPT Remote.
