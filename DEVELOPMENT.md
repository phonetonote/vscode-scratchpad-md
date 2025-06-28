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

# Or for one-time build
npm run vscode:prepublish
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

## Development Workflow

### Making Changes

1. **Edit source code** in `src/extension.ts`
2. **Compile changes:**
   ```bash
   npm run compile
   ```
3. **Restart the Extension Development Host** (if using F5 method)
4. **Test your changes**

### Key Files to Modify

- **`src/extension.ts`** - Main extension logic
- **`package.json`** - Extension metadata, commands, activation events
- **`README.md`** - User documentation

### Debugging

- Use `console.log()` statements in your code
- Check the Debug Console in VS Code
- Use VS Code's built-in debugging features

## Publishing to VS Code Marketplace

### 1. Prepare for Publishing

#### Update package.json
```json
{
    "name": "your-unique-extension-name",
    "displayName": "Your Extension Display Name",
    "description": "Your extension description",
    "version": "1.0.0",
    "publisher": "your-publisher-name",
    "repository": {
        "type": "git",
        "url": "https://github.com/yourusername/your-repo.git"
    },
    "keywords": ["scratchpad", "notes", "markdown"],
    "icon": "icon.png",  // Add a 128x128 PNG icon
    "galleryBanner": {
        "color": "#C80000",
        "theme": "dark"
    }
}
```

#### Create Required Assets
- **`icon.png`** (128x128 pixels)
- **`README.md`** (detailed documentation)
- **`CHANGELOG.md`** (version history)
- **`LICENSE`** (if applicable)

### 2. Create a Publisher Account

1. Go to [Visual Studio Marketplace](https://marketplace.visualstudio.com/)
2. Sign in with your Microsoft account
3. Click "Publish extensions"
4. Create a publisher account

### 3. Get a Personal Access Token (PAT)

1. Go to [Azure DevOps](https://dev.azure.com/)
2. Create an organization (if you don't have one)
3. Go to User Settings → Personal Access Tokens
4. Create a new token with "Marketplace (Publish)" scope
5. Copy the token (you'll need it for publishing)

### 4. Login and Publish

```bash
# Login with your PAT
vsce login your-publisher-name

# Package and publish
vsce publish

# Or package first, then publish
vsce package
vsce publish
```

### 5. Update Versions

For subsequent updates:
```bash
# Patch version (0.0.1 → 0.0.2)
vsce publish patch

# Minor version (0.0.1 → 0.1.0)
vsce publish minor

# Major version (0.0.1 → 1.0.0)
vsce publish major
```

## Common Issues and Solutions

### Extension Not Loading
- Check the Developer Tools console for errors
- Verify `package.json` syntax
- Ensure all required fields are present

### Command Not Found
- Check command registration in `package.json`
- Verify activation events
- Restart the Extension Development Host

### Build Errors
- Check TypeScript compilation errors
- Verify all imports are correct
- Ensure `out/` directory exists

## Useful Commands

```bash
# Development
npm run compile          # Compile TypeScript
npm run vscode:prepublish # Build for publishing

# Publishing
vsce package             # Create .vsix file
vsce publish             # Publish to marketplace
vsce login <publisher>   # Login to marketplace

# Testing
code --install-extension <file>.vsix  # Install local package
code --uninstall-extension <extension-id>  # Uninstall extension
```

## Best Practices

1. **Version Control:**
   - Use semantic versioning
   - Keep a detailed changelog
   - Tag releases in Git

2. **Testing:**
   - Test on different platforms
   - Test with different VS Code versions
   - Get feedback from users

3. **Documentation:**
   - Write clear README
   - Include screenshots/GIFs
   - Document all commands and features

4. **Performance:**
   - Lazy load when possible
   - Minimize bundle size
   - Use efficient algorithms

## Resources

- [VS Code Extension API](https://code.visualstudio.com/api)
- [Extension Marketplace](https://marketplace.visualstudio.com/)
- [VS Code Extension Samples](https://github.com/microsoft/vscode-extension-samples)
- [Extension Guidelines](https://code.visualstudio.com/api/references/extension-guidelines)

## Troubleshooting

### Extension Development Host Issues
- Close all VS Code windows
- Delete `out/` directory and rebuild
- Check for conflicting extensions

### Publishing Issues
- Verify PAT has correct permissions
- Check publisher name matches exactly
- Ensure version number is unique

### Performance Issues
- Profile extension performance
- Check for memory leaks
- Optimize file operations
