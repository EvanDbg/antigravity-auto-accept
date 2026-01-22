# Publishing to Open VSX Registry

Antigravity uses the **Open VSX Registry** (open-vsx.org) instead of the Microsoft Marketplace.

---

## Prerequisites

- Node.js and npm installed
- A GitHub account (for Open VSX login)

---

## 1. Create a Namespace

1. Go to [open-vsx.org](https://open-vsx.org)
2. Log in with your GitHub account
3. Go to **Settings** → **Namespaces**
4. Click **Create New Namespace**
   - Use your GitHub username or organization name

---

## 2. Update package.json (CRITICAL)

Your `package.json` **must** match your Open VSX namespace.

1. Open `package.json`
2. Find the `"publisher"` field
3. Change it to your **actual namespace**
4. Save the file

```json
{
  "publisher": "your-namespace"
}
```

---

## 3. Package the Extension

Create a new `.vsix` file with the correct publisher name:

```bash
cd path/to/antigravity-auto-accept
npx vsce package
```

This creates a file like `your-namespace.antigravity-auto-accept-1.1.0.vsix`.

---

## 4. Upload to Open VSX

### Option A: Web Upload

1. Go to [open-vsx.org/publish](https://open-vsx.org/publish)
2. Log in with GitHub
3. Drag and drop your `.vsix` file
4. Click **Publish**

### Option B: Command Line

1. Get an access token from Open VSX settings
2. Publish:
   ```bash
   npx ovsx publish -p <YOUR_TOKEN> path/to/extension.vsix
   ```

---

## 5. Verify Publication

After publishing:

1. Wait a few minutes for processing
2. Search for your extension on [open-vsx.org](https://open-vsx.org)
3. Verify it appears in the Antigravity Extensions view

---

## 6. Updating the Extension

When publishing updates:

1. Update `version` in `package.json`
2. Add entry to `CHANGELOG.md`
3. Repackage: `npx vsce package`
4. Upload the new `.vsix` file

---

## Troubleshooting

### "Namespace not found"
Make sure you've created a namespace matching your `publisher` field.

### "Already exists"
You cannot republish the same version. Increment the version number.

### "Invalid VSIX"
Ensure your `package.json` has all required fields:
- `name`
- `version`
- `publisher`
- `engines.vscode`
