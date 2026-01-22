# Troubleshooting Guide

This guide helps you diagnose and resolve common issues with the **Antigravity Auto Accept** extension.

---

## 🔴 Auto-Retry Not Working

### Symptom
The `🔄 Retry: ON` indicator is shown, but the Retry button is not being clicked automatically.

### Solutions

#### 1. Verify CDP is Enabled
Make sure Antigravity was started with remote debugging:

```bash
antigravity.exe --remote-debugging-port=9222
```

#### 2. Check Port Matching
The extension's `cdpPort` setting must match the launch parameter:

| Launch Parameter | Extension Setting |
|-----------------|-------------------|
| `--remote-debugging-port=9222` | `"antigravity-auto-accept.cdpPort": 9222` |

#### 3. Test CDP Connection
Open a browser and navigate to:
```
http://localhost:9222/json
```

You should see a JSON array of debugging targets. If not, CDP is not running.

#### 4. Check for Port Conflicts
Another application (like Chrome) may be using port 9222. Try a different port:

```bash
antigravity.exe --remote-debugging-port=9333
```

Then update the extension setting accordingly.

---

## 🔴 CDP Connection Refused

### Symptom
Error messages or no response when trying to connect to CDP.

### Solutions

1. **Restart Antigravity** with the correct flag
2. **Check Windows Firewall** - ensure localhost connections are allowed
3. **Try a different port** - some ports may be reserved

---

## 🔴 Retry Button Not Found

### Symptom
CDP is connected but the Output panel shows "not_found" for retry attempts.

### Possible Causes

1. **No error dialog present** - The retry button only appears when there's an error
2. **Different dialog structure** - The error dialog may have changed in a new version

### Debugging Steps

1. Open the Output panel: `View` → `Output`
2. Select `Antigravity Auto-Accept` from the dropdown
3. Look for retry attempt logs

---

## 🔴 WebSocket Timeout

### Symptom
Output shows "WebSocket timeout" errors.

### Solutions

1. **Network latency** - The extension has a 3-second timeout
2. **Too many targets** - Close unnecessary browser tabs/windows
3. **Restart Antigravity** - CDP may be in a bad state

---

## 🔴 Auto-Accept Not Working

### Symptom
Agent steps are not being auto-accepted.

### Solutions

1. **Check status bar** - Ensure it shows `✅ Auto-Accept: ON`
2. **Toggle off and on** - Press `Ctrl+Alt+Shift+U` twice
3. **Restart extension** - Reload the window (`Ctrl+Shift+P` → `Reload Window`)

---

## 🔴 Status Bar Not Visible

### Symptom
The Auto-Accept and Auto-Retry indicators are not shown in the status bar.

### Solutions

1. **Check if extension is active** - Open Extensions panel and verify it's enabled
2. **Restart Antigravity** - The extension activates on startup
3. **Check error console** - `Help` → `Toggle Developer Tools` → `Console`

---

## 📋 Diagnostic Checklist

| Check | How to Verify |
|-------|---------------|
| Extension installed | Extensions panel shows "Antigravity Auto Accept" |
| Extension active | Status bar shows accept/retry indicators |
| CDP enabled | `http://localhost:9222/json` returns data |
| Port matching | Extension setting equals launch parameter |
| No port conflicts | Only one app using the CDP port |

---

## 🔍 Viewing Logs

The extension logs retry attempts to an Output channel:

1. Open `View` → `Output`
2. Select `Antigravity Auto-Accept` from the dropdown
3. Look for messages like:
   - `✅ Retry button clicked via CDP (target: ...)`

---

## 🐛 Debug Mode

To list all Antigravity-related commands for debugging:

1. Open Command Palette (`Ctrl+Shift+P`)
2. Run `List Antigravity Commands (Debug)`
3. Check the Output panel for the command list

---

## 📞 Still Having Issues?

1. Check [GitHub Issues](https://github.com/pesoszpesosz/antigravity-auto-accept/issues) for similar problems
2. Create a new issue with:
   - Your Antigravity version
   - Extension version
   - Steps to reproduce
   - Output panel logs
