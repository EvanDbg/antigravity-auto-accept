# Publishing to VS Code Marketplace

This guide explains how to package and publish the **Antigravity Auto Accept** extension.

---

## Prerequisites

- Node.js installed
- npm installed
- A Microsoft account for the VS Code Marketplace

---

## 1. Install VSCE

VSCE (Visual Studio Code Extensions) is the command-line tool for packaging and publishing.

```bash
npm install -g @vscode/vsce
```

---

## 2. Navigate to the Extension Folder

Open a terminal and navigate to the extension directory:

```bash
cd path/to/antigravity-auto-accept
```

---

## 3. Package the Extension

Create a `.vsix` file:

```bash
npx vsce package
```

If prompted about missing fields, type `y` to continue.

This creates a file like `antigravity-auto-accept-1.1.0.vsix`.

---

## 4. Publish to Marketplace

### Option A: Web Upload (Recommended for First-Time)

1. Go to [marketplace.visualstudio.com/manage](https://marketplace.visualstudio.com/manage)
2. Log in with your Microsoft account
3. Click **"New Extension"** → **"Visual Studio Code"**
4. Upload the `.vsix` file
5. Fill in the required metadata
6. Click **Publish**

### Option B: Command Line

1. Create a Personal Access Token (PAT) from [Azure DevOps](https://dev.azure.com)
   - Scopes needed: `Marketplace (Manage)`

2. Publish:
   ```bash
   npx vsce publish -p <YOUR_PAT_TOKEN>
   ```

---

## 5. Pre-Publish Checklist

Before publishing, verify:

- [ ] `package.json` version is updated
- [ ] `CHANGELOG.md` includes the new version
- [ ] `publisher` field matches your Marketplace Publisher ID
- [ ] `repository` field points to your GitHub repo
- [ ] `icon.png` is present and valid (128x128 recommended)
- [ ] README renders correctly

---

## 6. Update the Version

When publishing a new version:

1. Update `version` in `package.json`
2. Add entry to `CHANGELOG.md`
3. Package and publish

```bash
# Update version
npm version patch  # or minor, or major

# Package
npx vsce package

# Publish
npx vsce publish -p <YOUR_PAT_TOKEN>
```

---

## Troubleshooting

### "Missing publisher"
Add your publisher ID to `package.json`:
```json
{
  "publisher": "your-publisher-id"
}
```

### "Missing repository"
Add repository info to `package.json`:
```json
{
  "repository": {
    "type": "git",
    "url": "https://github.com/your-username/antigravity-auto-accept"
  }
}
```

### PowerShell Execution Errors
Use Command Prompt (cmd) instead of PowerShell, or set the execution policy:
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```
