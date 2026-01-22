# Changelog

All notable changes to the **Antigravity Auto Accept** extension will be documented in this file.

## [1.1.0] - 2026-01-22

### Added
- **Auto-Retry via CDP**: Automatically click the "Retry" button when agent encounters an error
- New status bar indicator showing Retry status and CDP port (`🔄 Retry: ON (9222)`)
- New keyboard shortcut `Ctrl+Alt+Shift+R` to toggle Auto-Retry
- New command `Toggle Unlimited Auto-Retry (CDP)`
- New command `Set CDP Port for Auto-Retry` to configure the debugging port
- New command `List Antigravity Commands (Debug)` for troubleshooting
- Configurable CDP port via `antigravity-auto-accept.cdpPort` setting (default: 9222)
- Configurable auto-retry toggle via `antigravity-auto-accept.autoRetryEnabled` setting
- Output Channel logging for retry actions (`Antigravity Auto-Accept`)
- WebSocket-based CDP communication for reliable script execution

### Changed
- Refactored extension architecture to support CDP integration
- Enhanced status bar with dual indicators (Accept + Retry)

## [1.0.3] - 2025-12-10

### Fixed
- Improved status bar item visibility and positioning

## [1.0.2] - 2025-12-10

### Added
- Status bar toggle with visual indicators (Green ON / Red OFF)
- Keyboard shortcut `Ctrl+Alt+Shift+U` to toggle auto-accept

### Changed
- Optimized polling interval for better performance

## [1.0.1] - 2025-12-10

### Added
- Terminal command acceptance (`antigravity.terminal.accept`)

## [1.0.0] - 2025-12-10

### Added
- Initial release
- Automatic acceptance of Antigravity agent steps
- Background polling every 500ms
- Zero-interference operation (works when minimized/unfocused)
