# Mkraftman Fision Numpad

Custom HACS Lovelace card for Hotwire Fision numeric channel entry, sending through the `script.fision_send` script (Global Caché iTach → Cisco ISB IPTV box).

## Features

- Dialpad icon that opens a custom numpad overlay
- Sends `exit` before the first digit so an open banner or menu doesn't swallow the digits
- Sends digits 0-9 as `digit_0` … `digit_9` via `script.fision_send`, which alternates the IR toggle bit so repeated digits (e.g. `11`) register as separate presses
- Auto-closes after 4 digits, or 3 seconds after the last digit (the box tunes on its own)
- Backspace sends `left`
- Tap outside numpad to dismiss
- iOS-style keyboard appearance with rounded corners

## Prerequisites

A script that takes a `command` field and sends it to the box — `script.fision_send` from the Fision HA package, with commands `exit`, `left` and `digit_0` … `digit_9`.

## Installation

1. Add this repository to HACS as a custom repository
2. Install the card
3. Add to your dashboard

## Configuration

```yaml
type: custom:mkraftman-fision-numpad
```

All options are optional:

| Option | Default | Description |
| --- | --- | --- |
| `script` | `fision_send` | Script to call (with or without the `script.` prefix) |
| `max_digits` | `4` | Close once this many digits are entered |
| `idle_close` | `3000` | Milliseconds after the last digit before closing; `0` disables |
| `clear_command` | `exit` | Sent before the first digit; empty string disables |
| `backspace_command` | `left` | Sent on backspace |

## Releasing

Bump the version in `VERSION` (e.g. `1.0.1`) and push to `main`. The release workflow creates the matching `vX.Y.Z` tag and GitHub release with `dist/mkraftman-fision-numpad.js` attached. Pushing a `vX.Y.Z` tag directly also still works.
