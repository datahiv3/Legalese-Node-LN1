# IDE Setup Guide

Configuring your Integrated Development Environment (IDE) is crucial for efficient development and management of your DataHive node. This guide covers recommended IDEs, extensions, and configurations for a streamlined workflow.

---

## Recommended IDEs

### 1. **Visual Studio Code (VS Code)**
- **Why?**
  - Lightweight yet powerful.
  - Extensive ecosystem of extensions.
  - Cross-platform support (Windows, macOS, Linux).

### 2. **JetBrains WebStorm**
- **Why?**
  - Advanced features for JavaScript/TypeScript development.
  - Integrated tools for debugging and testing.

### 3. **PyCharm (for Python)**
- **Why?**
  - Specialized for Python development.
  - Excellent support for virtual environments and linting.

### 4. **IntelliJ IDEA**
- **Why?**
  - Comprehensive support for multiple languages, including Java, Kotlin, and Go.

---

## Prerequisites

1. **Install Node.js and npm**:
   - Ensure Node.js (v16 or higher) and npm are installed. See the [environment setup guide](/docs/setup/ENVIRONMENT.md).

2. **Clone the Repository**:
   - Download the DataHive source code:
   ```bash
   git clone https://github.com/datahiv3/Legalese-Node-LN1.git
   cd Legalese-Node-LN1
   ```

3. **Install Dependencies**:
   ```bash
   npm install
   ```

---

## Setting Up VS Code

1. **Install VS Code**:
   - Download and install from [code.visualstudio.com](https://code.visualstudio.com/).

2. **Recommended Extensions**:
   - **ESLint**: Ensure code follows JavaScript/TypeScript standards.
   - **Prettier**: Automatically format your code.
   - **Docker**: Manage and interact with Docker containers.
   - **REST Client**: Test API endpoints.
   - **GitLens**: Advanced Git capabilities for tracking changes.

3. **Workspace Configuration**:
   - Create a `.vscode/settings.json` file with the following:
     ```json
     {
       "editor.formatOnSave": true,
       "eslint.enable": true,
       "files.exclude": {
         "node_modules": true,
         ".env": true
       },
       "editor.tabSize": 2
     }
     ```

4. **Debugging Configuration**:
   - Add a `launch.json` file for debugging:
     ```json
     {
       "version": "0.2.0",
       "configurations": [
         {
           "type": "node",
           "request": "launch",
           "name": "Launch Program",
           "skipFiles": ["<node_internals>/**"],
           "program": "${workspaceFolder}/index.js"
         }
       ]
     }
     ```

---

## Setting Up JetBrains IDEs

1. **Install WebStorm or IntelliJ IDEA**:
   - Download from [jetbrains.com](https://www.jetbrains.com/).

2. **Configure Project**:
   - Open the cloned repository as a new project.
   - Install npm dependencies through the built-in terminal.

3. **Enable ESLint and Prettier**:
   - Navigate to `Settings > Languages & Frameworks > JavaScript > Code Quality Tools`.
   - Enable ESLint and set Prettier as the default formatter.

4. **Run/Debug Configurations**:
   - Add a Node.js configuration with the entry point set to `index.js`.

---

## Setting Up PyCharm (Optional)

1. **Install PyCharm**:
   - Download from [jetbrains.com/pycharm](https://www.jetbrains.com/pycharm/).

2. **Configure Python Interpreter**:
   - Navigate to `File > Settings > Project > Python Interpreter`.
   - Add a virtual environment or select the system interpreter.

3. **Install Python Extensions**:
   - **Black**: Code formatter.
   - **Flake8**: Linting tool.

---

## Best Practices

1. **Use Git Integration**:
   - Ensure your IDE is configured for Git to track changes and collaborate efficiently.

2. **Automate Formatting and Linting**:
   - Enable Prettier and ESLint to maintain consistent code quality.

3. **Leverage Debugging Tools**:
   - Configure breakpoints and logs for efficient debugging.

4. **Optimize Performance**:
   - Disable unused extensions and plugins to improve IDE speed.

---

## Troubleshooting

| **Issue**                | **Solution**                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| Extensions not working   | Restart the IDE or reinstall the extensions.                                |
| Debugger not attaching   | Verify the entry point in `launch.json` or IDE debug configuration.         |
| Linting errors           | Run `npm run lint` in the terminal to identify and fix issues.              |

---

Setting up your IDE properly can significantly improve your productivity and ensure seamless development within the DataHive network. For additional assistance, visit the [support portal](/docs/onboarding/support/tickets.md) or join the [community forums](/docs/onboarding/community/forums.md).
