# Antigravity Auto Accept

[![Version](https://img.shields.io/badge/version-1.1.0-blue.svg)](https://github.com/pesoszpesosz/antigravity-auto-accept)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Finally, true hands-free automation for your Antigravity Agent.**

This extension automatically accepts **ALL** pending steps from the Antigravity Agent and auto-retries on errors:

- ✅ **Run Command** requests (Terminal)
- ✅ **Save File** requests  
- ✅ **Code Edits**
- ✅ **Auto-Retry** on agent errors (via CDP)

It bypasses the limitations of external scripts by running directly inside the IDE process, ensuring 100% reliability even when the window is minimized or unfocused.

---

## 🚀 Installation

### Option 1: Install from VSIX (Recommended)

1. Download the latest `.vsix` file from [Releases](https://github.com/pesoszpesosz/antigravity-auto-accept/releases)
2. Open Antigravity IDE
3. Go to **Extensions** → Click `...` menu → **Install from VSIX...**
4. Select the downloaded `.vsix` file
5. Restart the IDE

### Option 2: Build from Source

```bash
git clone https://github.com/pesoszpesosz/antigravity-auto-accept.git
cd antigravity-auto-accept
npm install -g @vscode/vsce
vsce package
```

Then install the generated `.vsix` file as described above.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| **Zero-Interference** | Runs silently in the background |
| **Toggle Control** | Click status bar or use keyboard shortcut |
| **Visual Status** | Green (ON) / Red (OFF) indicators |
| **Deep Integration** | Calls internal Antigravity commands directly |
| **Auto-Retry (CDP)** | Automatically clicks Retry button on errors |
| **Configurable Port** | Customize CDP port to avoid conflicts |

---

## 🔄 Auto-Retry via CDP (v1.1.0+)

When the Antigravity Agent encounters an error, it displays a dialog with a "Retry" button. This extension can automatically click that button using Chrome DevTools Protocol (CDP).

### Setup

1. **Start Antigravity with remote debugging enabled:**
   ```bash
   antigravity.exe --remote-debugging-port=9222
   ```

2. **Verify the status bar shows:**
   - `✅ Auto-Retry: ON (9222)` - Auto-Retry is enabled

### Configuration

| Setting | Default | Description |
|---------|---------|-------------|
| `antigravity-auto-accept.cdpPort` | `9222` | CDP remote debugging port |
| `antigravity-auto-accept.autoRetryEnabled` | `true` | Enable/disable auto-retry |

> **Note:** If you're also running Chrome with remote debugging, use a different port to avoid conflicts.

---

## ⌨️ Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl+Alt+Shift+U` | Toggle Auto-Accept ON/OFF |
| `Cmd+Alt+Shift+U` (Mac) | Toggle Auto-Accept ON/OFF |
| `Ctrl+Alt+Shift+R` | Toggle Auto-Retry ON/OFF |
| `Cmd+Alt+Shift+R` (Mac) | Toggle Auto-Retry ON/OFF |

---

## 📖 Usage

1. Install the extension
2. Restart Antigravity IDE
3. (Optional) Start Antigravity with `--remote-debugging-port=9222` for auto-retry
4. The extension activates automatically (`✅ Auto-Accept: ON`)
5. Launch an Agent task and sit back!

### Status Bar Indicators

| Indicator | Meaning |
|-----------|---------|
| `✅ Auto-Accept: ON` | All agent steps are being auto-accepted |
| `🛑 Auto-Accept: OFF` | Manual approval required |
| `✅ Retry: ON (9222)` | Auto-retry enabled on port 9222 |
| `🛑 Retry: OFF` | Auto-retry disabled |

---

## 🛠️ Commands

| Command | Description |
|---------|-------------|
| `Toggle Unlimited Auto-Accept` | Turn auto-accept on/off |
| `Toggle Unlimited Auto-Retry (CDP)` | Turn auto-retry on/off |
| `Set CDP Port for Auto-Retry` | Change the CDP port |
| `List Antigravity Commands (Debug)` | Show all Antigravity-related commands |

---

## 🔧 Requirements

- Antigravity IDE (VS Code based)
- For Auto-Retry: Launch with `--remote-debugging-port` flag

---

## ❓ FAQ

**Q: Is this safe to use?**  
A: The extension only accepts steps that Antigravity Agent proposes. Review agent behavior periodically.

**Q: Can I pause it temporarily?**  
A: Yes! Click the status bar item or press `Ctrl+Alt+Shift+U`.

**Q: Does it work when the window is minimized?**  
A: Yes, that's the main advantage over external automation scripts.

**Q: Auto-Retry is not working?**  
A: Make sure you started Antigravity with `--remote-debugging-port=9222` flag. Check the Output panel (Antigravity Auto-Accept) for logs.

**Q: CDP port conflict with Chrome?**  
A: Use a different port, e.g., `--remote-debugging-port=9333`, and update the extension setting accordingly.

---

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📜 License

MIT - See [LICENSE](LICENSE) for details.

---

## ⭐ Support

If you find this useful, consider giving it a star on GitHub!
