# Basic Project Creation Guide

This guide explains the steps to create a basic `project` structure.

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

- **requirements.txt**: List of project dependencies.
- **docs/**: Project documentation (markdown format).
- **src/**: Main source code of the project.
    - `__init__.py`: Marks the folder as a Python package.
    - `main.xr`: Main file containing the program's main function.
- **tests/**: Folder for test files.

## 2. Creating a New Project
1. **Create the folder structure** as shown above.
2. **Create a `requirements.txt` file** to list dependencies (e.g., `math`, `time`, `random`, `os`, `sys` or any others needed).
3. **Create the main file** in `src/main.xr` with your main code.
4. **Create test files** in the `tests/` folder (e.g., `test_*.xr`).
5. **Run the project** using the appropriate command or task (e.g., the `nginr` task).

## 3. Running the Project
- Make sure all dependencies are installed.
- Run the main file (`main.xr`) using the nginr preprocessor or the provided task (see below for VS Code setup).

## 4. Tips
- Always separate main code and test code.
- Use the `docs/` folder for additional documentation.
- Save dependencies in `requirements.txt` for easy reinstallation.

## 5. Example VS Code Task Configuration
To run `.xr` files with a task in VS Code, create a `tasks.json` file in the `.vscode/` folder with the following content:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // change this path to where nginr is installed
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

- Make sure the `command` path matches the location of `nginr` on your system. Use `${HOME}` for portability.
- Save this file as `.vscode/tasks.json` in your project root.
- If you use the `errorlens` extension, make sure the Python interpreter is **not set to any version** so `errorlens` does not keep warning about lines with `fn` declarations. This is because you are not running Python directly, but using the `nginr` preprocessor.
