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

### a. Syntax Highlighting Setup

To make `.xr` files recognized as Python (for syntax highlighting and better tool integration), add the following configuration to your `settings.json`.

#### How to Open `settings.json` (User Settings):

1. Open VS Code.
2. Go to **File → Preferences → Settings** (or press `Ctrl + ,`).
3. Click the **{} icon** (Open Settings (JSON)) in the top right corner of the settings panel.
4. Add the following code:

```json
"files.associations": {
  "*.xr": "python"
}
```

> If a `files.associations` section already exists, just add `"*.xr": "python"` inside it.

### b. Task to Run the File

Create a `tasks.json` file inside the `.vscode/` folder with the following content:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // Replace PATH/TO with the actual location of nginr
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

* Make sure the path in `command` points to where `nginr` is installed on your system. Use `${HOME}` to make it more portable.
* Save this file as `.vscode/tasks.json` in your project root.

### c. Note for ErrorLens Users

If you're using the `ErrorLens` extension, make sure the Python interpreter is **not set to any specific version**. This avoids persistent warnings on lines that use `fn` or other custom syntax, because the project doesn't use the Python interpreter directly—instead, it uses the `nginr` preprocessor.
