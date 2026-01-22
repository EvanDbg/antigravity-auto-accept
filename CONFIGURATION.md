# Configuration Guide

This document describes all configurable settings for the **Antigravity Auto Accept** extension.

---

## ⚙️ Extension Settings

All settings can be configured via:
- **Settings UI**: `File` → `Preferences` → `Settings` → Search "antigravity"
- **settings.json**: Add entries directly to your configuration file

### Available Settings

#### `antigravity-auto-accept.cdpPort`

| Property | Value |
|----------|-------|
| Type | `number` |
| Default | `9222` |
| Scope | User |

The Chrome DevTools Protocol (CDP) port for remote debugging. This port is used by the Auto-Retry feature to communicate with Antigravity.

**Example:**
```json
{
  "antigravity-auto-accept.cdpPort": 9333
}
```

> **Note:** This must match the `--remote-debugging-port` value used when launching Antigravity.

---

#### `antigravity-auto-accept.autoRetryEnabled`

| Property | Value |
|----------|-------|
| Type | `boolean` |
| Default | `true` |
| Scope | User |

Enable or disable the Auto-Retry feature. When enabled, the extension automatically clicks the "Retry" button when the agent encounters an error.

**Example:**
```json
{
  "antigravity-auto-accept.autoRetryEnabled": false
}
```

---

## 🚀 Launch Configuration

To use the Auto-Retry feature, Antigravity must be started with remote debugging enabled.

### Windows

```bash
antigravity.exe --remote-debugging-port=9222
```

### macOS / Linux

```bash
./antigravity --remote-debugging-port=9222
```

### Using a Custom Port

If port 9222 is already in use (e.g., by Chrome), use a different port:

```bash
antigravity.exe --remote-debugging-port=9333
```

Then update the extension setting:
```json
{
  "antigravity-auto-accept.cdpPort": 9333
}
```

---

## 📋 Quick Reference

| Setting | Default | CLI Equivalent |
|---------|---------|----------------|
| `cdpPort` | `9222` | `--remote-debugging-port=9222` |
| `autoRetryEnabled` | `true` | N/A |

---

## 🔄 Changing Settings at Runtime

You can also change settings via commands:

1. **Set CDP Port**: Open Command Palette (`Ctrl+Shift+P`) → `Set CDP Port for Auto-Retry`
2. **Toggle Auto-Retry**: Click the status bar item or press `Ctrl+Alt+Shift+R`

Settings changed via these methods are persisted to your user configuration.
