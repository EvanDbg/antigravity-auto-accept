# API Reference

This document describes all commands, settings, and keybindings exposed by the **Antigravity Auto Accept** extension.

---

## 🎯 Commands

All commands are accessible via the Command Palette (`Ctrl+Shift+P` or `Cmd+Shift+P`).

### `unlimited.toggle`

**Title:** Toggle Unlimited Auto-Accept

**Description:** Toggles the auto-accept feature on or off. When enabled, the extension automatically accepts all pending agent steps.

**Usage:**
- Command Palette: "Toggle Unlimited Auto-Accept"
- Keyboard: `Ctrl+Alt+Shift+U` (Windows/Linux) or `Cmd+Alt+Shift+U` (Mac)
- Status Bar: Click the Auto-Accept indicator

---

### `unlimited.toggleRetry`

**Title:** Toggle Unlimited Auto-Retry (CDP)

**Description:** Toggles the auto-retry feature on or off. When enabled, the extension automatically clicks the "Retry" button when the agent encounters an error.

**Usage:**
- Command Palette: "Toggle Unlimited Auto-Retry (CDP)"
- Keyboard: `Ctrl+Alt+Shift+R` (Windows/Linux) or `Cmd+Alt+Shift+R` (Mac)
- Status Bar: Click the Auto-Retry indicator

**Requirements:** Antigravity must be started with `--remote-debugging-port` flag.

---

### `unlimited.setCdpPort`

**Title:** Set CDP Port for Auto-Retry

**Description:** Opens an input dialog to set the Chrome DevTools Protocol port. This port is used to communicate with Antigravity for the auto-retry feature.

**Usage:**
- Command Palette: "Set CDP Port for Auto-Retry"

**Input:** A number between 1 and 65535 (default: 9222)

**Persistence:** The new port is saved to user settings.

---

### `unlimited.listCommands`

**Title:** List Antigravity Commands (Debug)

**Description:** Lists all registered VS Code commands related to Antigravity, Agent, Retry, Allow, Confirm, and Cockpit. Useful for debugging and discovering available commands.

**Usage:**
- Command Palette: "List Antigravity Commands (Debug)"

**Output:** Results are displayed in a new Output channel panel.

---

## ⚙️ Settings

All settings are prefixed with `antigravity-auto-accept.`

### `cdpPort`

| Property | Value |
|----------|-------|
| Type | `number` |
| Default | `9222` |
| Minimum | `1` |
| Maximum | `65535` |

The Chrome DevTools Protocol port for Antigravity remote debugging.

**JSON Example:**
```json
{
  "antigravity-auto-accept.cdpPort": 9222
}
```

---

### `autoRetryEnabled`

| Property | Value |
|----------|-------|
| Type | `boolean` |
| Default | `true` |

Enable or disable auto-retry via CDP when the agent encounters an error.

**JSON Example:**
```json
{
  "antigravity-auto-accept.autoRetryEnabled": true
}
```

---

## ⌨️ Keybindings

| Command | Windows/Linux | Mac |
|---------|---------------|-----|
| `unlimited.toggle` | `Ctrl+Alt+Shift+U` | `Cmd+Alt+Shift+U` |
| `unlimited.toggleRetry` | `Ctrl+Alt+Shift+R` | `Cmd+Alt+Shift+R` |

### Customizing Keybindings

You can customize these keybindings in your `keybindings.json`:

```json
[
  {
    "key": "ctrl+alt+a",
    "command": "unlimited.toggle"
  },
  {
    "key": "ctrl+alt+r",
    "command": "unlimited.toggleRetry"
  }
]
```

---

## 📊 Status Bar Items

### Auto-Accept Indicator

| State | Display | Tooltip |
|-------|---------|---------|
| ON | `✅ Auto-Accept: ON` | Click to pause |
| OFF | `🛑 Auto-Accept: OFF` | Click to resume |

**Position:** Right side, priority 10000

**Click Action:** Executes `unlimited.toggle`

---

### Auto-Retry Indicator

| State | Display | Tooltip |
|-------|---------|---------|
| ON | `🔄 Retry: ON (9222)` | Shows current port, click to disable |
| OFF | `⏸️ Retry: OFF` | Click to enable |

**Position:** Right side, priority 9999

**Click Action:** Executes `unlimited.toggleRetry`

---

## 📡 Output Channels

### Antigravity Auto-Accept

**ID:** `Antigravity Auto-Accept`

**Description:** Logs retry button click attempts and other extension activities.

**Sample Output:**
```
[14:32:15] ✅ Retry button clicked via CDP (target: Antigravity Agent)
```

---

### Antigravity Commands

**ID:** `Antigravity Commands`

**Description:** Created by the debug command to list all Antigravity-related commands.

**Usage:** Run `List Antigravity Commands (Debug)` command.

---

## 🔌 Activation Events

The extension activates on:

```json
{
  "activationEvents": ["onStartupFinished"]
}
```

This means the extension loads after VS Code/Antigravity has fully started.

---

## 🔗 Internal Commands (Consumed)

The extension calls these internal Antigravity commands:

| Command | Description |
|---------|-------------|
| `antigravity.agent.acceptAgentStep` | Accept pending agent step |
| `antigravity.terminal.accept` | Accept terminal command |
| `antigravity.terminalCommand.accept` | Accept terminal command (alternate) |
| `antigravity.command.accept` | Accept general command |
| `antigravity.agent.confirmStep` | Confirm step execution |
| `agCockpit.confirm` | Cockpit confirmation |
| `antigravity.confirm` | General confirmation |
| `antigravity.agent.allowOnce` | Allow permission once |
| `antigravity.agent.allowConversation` | Allow for entire conversation |
| `agCockpit.allowOnce` | Cockpit allow once |
| `agCockpit.allowConversation` | Cockpit allow conversation |
| `antigravity.allow` | General allow |

> **Note:** These commands may fail silently if there's nothing to accept, which is expected behavior.
