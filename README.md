# Custom VS Code Build with Wingman AI Integration

## 📌 Objective

This project is a custom, portable build of **Visual Studio Code** with the **Wingman AI** extension deeply integrated. It behaves as a **native feature** rather than a user-installed extension and is:

- Preloaded on first launch
- Hidden from the Extensions UI and Marketplace
- Not removable via the VS Code extension panel
- Fully functional as a standard VS Code build
- Easy to update or rebase with future upstream changes

---

## 🛠 Prerequisites

Ensure the following are installed before building:

- **Node.js** (>= 18.x)
- **Yarn** (classic version `1.x`)
- **Git**
- **Python** (v3.x)
- **C++ Build Tools** (Windows) / **Xcode Command Line Tools** (macOS)
- **VS Code Dev Dependencies**

```bash
git --version
node -v
yarn -v
python --version
```

---

## 🚀 Build Instructions

### 1. Clone the VS Code Repository

```bash
git clone https://github.com/microsoft/vscode.git
cd vscode
yarn
```

### 2. Clone and Embed Wingman AI

```bash
cd extensions
git clone https://github.com/RussellCanfield/wingman-ai.git
mv wingman-ai wingman-ai-built-in
```

### 3. Mark Wingman as Built-In

Edit the root file:  
`build/builtinExtensions.json`

Add the entry:
```json
{
  "name": "wingman-ai-built-in",
  "repo": "local",
  "enableProposedApi": true
}
```

### 4. Hide Wingman from Extensions View

Modify this in the extension’s `package.json`:
```json
"capabilities": {
  "uninstallable": false,
  "virtualWorkspaces": true,
  "hiddenFromExtensionsView": true
}
```

### 5. Build VS Code

```bash
yarn gulp vscode-win32-x64-archive   # For Windows
# OR
yarn gulp vscode-darwin              # For macOS
```

The build artifacts will be inside the `.\.build` folder.

---

## 💻 Run Instructions

Extract the generated zip or run the `.exe` / `.app` directly from the output folder:

```bash
./VSCode-win32-x64/Code.exe
# OR
./VSCode-darwin/Visual\ Studio\ Code.app
```

Wingman AI will auto-load at startup and is not shown in the Extensions tab.

---

## 🔁 Upgrade Guide

### To Update VS Code:
```bash
cd vscode
git pull origin main
yarn
```

### To Update Wingman AI:
```bash
cd extensions/wingman-ai-built-in
git pull origin main
```

### Rebuild:
```bash
yarn gulp vscode-win32-x64-archive
```

If Wingman's API or structure changes, update the integration logic accordingly in:
- `builtinExtensions.json`
- `package.json`
- `main.ts` or activation code, if modified

---

## 📽 Demo Video

See the attached screen recording for:
- First launch behavior
- Wingman AI functioning
- Its absence from the Extensions list

---

## 📁 Deliverables Summary

- ✅ Portable `.exe` / `.app` build
- ✅ Source with `README.md`
- ✅ Screen recording
- ✅ Upgrade instructions

---


## 🎥 Demo Video Link

Watch the demonstration here (recommended to watch at 2x speed):  
🔗 [Loom Recording – VS Code with Wingman AI](https://www.loom.com/share/c9f8e41214684ea3a1712409ea90410d?sid=64466e9c-55fe-4b63-aede-672df12f35e7)

---
