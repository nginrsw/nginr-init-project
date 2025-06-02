# Basic Project Setup Guide

This guide explains the steps to create a basic project structure.

## 1. Directory Structure

```
myproject/
├── requirements.txt
├── docs/
│   └── *.md
├── src/
│   ├── __init__.py
│   └── main.xr
└── tests/
    └── test_*.xr
```

* **requirements.txt**: A list of dependencies required by the project.
* **docs/**: Folder for project documentation (in Markdown format).
* **src/**: Folder containing the main source code.

  * `__init__.py`: Marks the folder as a Python package.
  * `main.xr`: The main file that contains the core logic of the program.
* **tests/**: Folder for test files.

## 2. Creating a New Project

1. **Create the folder structure** as shown above.
2. **Create a `requirements.txt` file** to list any dependencies (e.g., `math`, `time`, `random`, `os`, `sys`, or anything else your project needs).
3. **Create a `main.xr` file** inside the `src/` folder as the program’s entry point.
4. **Create test files** inside the `tests/` folder (e.g., `test_*.xr`).
5. **Run the project** using a suitable command or task (e.g., the `nginr` task).

## 3. Running the Project

* Make sure all dependencies are installed.
* Run the main file (`main.xr`) using the `nginr` preprocessor or a predefined task (especially if you're using VS Code).

## 4. Tips

* Always separate main code and test code into different folders.
* Use the `docs/` folder for any additional documentation.
* Save dependency lists in `requirements.txt` for easy reinstallation.

## 5. VS Code Configuration: Settings and Tasks

### a. Syntax Highlighting

To make `.xr` files recognized as Python (for syntax highlighting and integration with other tools), add the following configuration to your `settings.json`.

**How to Open `settings.json` (User Settings):**

* Open VS Code.
* Go to **File → Preferences → Settings** (or press `Ctrl + ,`).
* Click the `{}` icon at the top right corner to open the JSON view.

Then add this to your JSON:

```json
"files.associations": {
  "*.xr": "python"
}
```

> If you already have a `files.associations` section, simply add `"*.xr": "python"` inside it.

### b. Disabling the Python Extension (Recommended)

To avoid constant linting errors from the Python extension (e.g., marking `fn` as an invalid function declaration), it’s **recommended to disable the Python extension** for this workspace.

#### Steps:

1. Open the **Command Palette** (`Ctrl+Shift+P`).
2. Search for and select: `Extensions: Disable (Workspace)`
3. Find **Python**, then choose to disable it.
4. VS Code may prompt you to **also disable related extensions** (like Jupyter, Pylance, etc.).
   → **Choose "Yes" or "Disable All"** to avoid interference.

> This only disables Python extensions for the current project. They remain active for other workspaces.

### c. Running Files with a Task

Create a `tasks.json` file inside the `.vscode/` folder with the following content:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // Replace PATH/TO with your actual nginr path
      "args": [
        "${file}"
      ],
      "problemMatcher": [],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

* Make sure the path in `command` matches your system's location for `nginr`.
* Use `${HOME}` for portability.
* Save this as `.vscode/tasks.json` in the project root.

### d. Note for ErrorLens Users

If you use the **ErrorLens** extension, be aware that it will still highlight errors reported by linters such as Python or Pylance. Therefore:

* **Disable the Python extension as shown above** to prevent false errors.
* Alternatively, you can **temporarily disable ErrorLens** if it becomes too noisy.
