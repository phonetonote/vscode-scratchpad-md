# VS Code Scratchpad Extension - Development Guide

This guide covers how to build, test, and publish your VS Code extension locally.

## Prerequisites

- **Node.js** (v16.0.0 or higher)
- **VS Code** (for development and testing)
- **Git** (for version control)

## Project Structure

```
vscode-scratchpad-md/
├── src/
│   └── extension.ts          # Main extension code
├── out/                      # Compiled JavaScript (generated)
├── package.json              # Extension manifest
├── tsconfig.json             # TypeScript configuration
├── typings/
│   └── node.d.ts             # Node.js type definitions
└── README.md                 # User documentation
```

## Local Development Setup

### 1. Install Dependencies

```bash
# Install all dependencies
npm install

# Or if you prefer bun (faster)
bun install
```

### 2. Build the Extension

```bash
# Compile TypeScript to JavaScript
npm run compile
```

The compiled code will be output to the `out/` directory.

### 3. Test Locally

#### Method 1: Using VS Code Extension Development Host

1. **Open the project in VS Code:**
   ```bash
   code .
   ```

2. **Press `F5` or go to Run → Start Debugging**
   - This opens a new VS Code window (Extension Development Host)
   - Your extension is loaded in this window
   - Any changes require restarting the debug session

3. **Test the extension:**
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
   - Search for "Open Scratchpad"
   - Execute the command

#### Method 2: Package and Install Locally

1. **Install vsce (VS Code Extension Manager):**
   ```bash
   npm install -g @vscode/vsce
   ```

2. **Package the extension:**
   ```bash
   vsce package
   ```
   This creates a `.vsix` file.

3. **Install the package:**
   ```bash
   code --install-extension scratchpad-0.0.1.vsix
   ```

4. **Test in regular VS Code:**
   - Open VS Code
   - Press `Ctrl+Shift+P`
   - Search for "Open Scratchpad"
