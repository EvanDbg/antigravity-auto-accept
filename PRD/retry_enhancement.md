# Antigravity Auto-Retry via CDP 需求文档

## 需求背景

当 Antigravity Agent 出现错误时，会弹出 "Agent terminated due to error" 对话框，用户需要手动点击 "Retry" 按钮才能重试。这影响了自动化工作流的连续性。

## 需求目标

实现自动点击 Retry 按钮，使 Antigravity Agent 能够在出错后自动重试，无需人工干预。

## 技术方案

### 方案选择

采用 **Chrome DevTools Protocol (CDP)** 远程调试方案：

| 方案 | 可行性 | 说明 |
|------|--------|------|
| ❌ Webview DOM 注入 | 不可行 | VS Code 安全限制 |
| ❌ 读取 Webview DOM | 不可行 | VS Code 安全限制 |
| ✅ CDP 远程调试 | **采用** | 通过 `--remote-debugging-port` 控制 |

### 实现方式

1. **启动 Antigravity**：使用 `--remote-debugging-port=<port>` 参数
2. **扩展连接 CDP**：通过 HTTP 获取调试目标，通过 WebSocket 执行脚本
3. **自动点击 Retry**：查找并点击 Retry 按钮

### 配置项

| 配置项 | 类型 | 默认值 | 说明 |
|--------|------|--------|------|
| `antigravity-auto-accept.cdpPort` | number | 9222 | CDP 远程调试端口 |
| `antigravity-auto-accept.autoRetryEnabled` | boolean | true | 是否启用自动重试 |

## 使用方法

1. **启动 Antigravity**（需添加参数）：
   ```bash
   antigravity.exe --remote-debugging-port=9222
   ```

2. **查看状态栏**：
   - `🔄 Retry: ON (9222)` - 已启用，显示当前端口
   - `⏸️ Retry: OFF` - 已禁用

3. **修改端口**：
   - 命令面板：`Set CDP Port for Auto-Retry`
   - 或修改设置：`antigravity-auto-accept.cdpPort`

## 验收标准

1. ✅ 端口可配置，避免与 Chrome 冲突
2. ✅ 状态栏显示当前端口号
3. ✅ 开关切换保存到配置文件
4. ✅ 通过 CDP 自动点击 Retry 按钮
