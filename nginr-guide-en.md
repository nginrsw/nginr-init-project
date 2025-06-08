# Basic Project Setup Guide

This guide explains the steps to create a basic project structure.

## 1. Directory Structure

```project_name/
├── README.md
├── requirements.txt
├── nginr_config.yaml
├── docs/
│   ├── architecture.md
│   ├── api.md
│   └── dev-notes.md
├── src/
│   ├── __init__.py  # Main source code (nginr file)
│   └── main.xr
├── tests/
│   └── test_main.xr # Tests for main.xr
└── .gitignore
```

* **requirements.txt**: A text file listing the Python dependencies needed for the project. It helps to easily install all required packages using tools like `pip`.

* **docs/**: A directory containing additional project documentation written in Markdown (`.md`) files, such as:

  * `architecture.md`: Describes the overall architecture of the project.
  * `api.md`: Contains API documentation, if applicable.
  * `dev-notes.md`: Developer notes and important information for contributors.

* **src/**: The folder containing the main source code files with `.xr` extension, written in the `nginr` syntax.

  * `main.xr`: The primary source code file which contains the core logic of the application.

  > **Note:** This folder does not include `__init__.py` because it is not a Python package but rather a folder for scripts using a custom syntax.

* **tests/**: A directory for test files that verify the correctness of the source code in `src/`.

  * `test_main.xr`: A test script designed to test the functionality in `main.xr`.

## 2. Creating a New Project

Nginr can also help you quickly set up a new project structure. Use the init command:

```
nginr init your_project_name
```

And you will get the project structure as shown above.

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

**How to open `settings.json` (User Settings):**

1. Open VS Code.
2. Go to **File → Preferences → Settings** (or press `Ctrl + ,`).
3. In the top right corner of the Settings panel, click the `{}` icon (Open Settings (JSON)).
4. Add the following to the JSON:

```json
"files.associations": {
  "*.xr": "python"
}
```

> If the `files.associations` section already exists, just add `"*.xr": "python"` inside it.

---

### b. Disabling the Python Extension (Recommended)

To avoid syntax errors or warnings from the Python linter (e.g., `fn` being flagged because it's not a standard Python keyword), it’s **recommended to disable the Python extension for this project only**.

#### How to disable the Python extension for a single workspace/project:

1. Open the **Extensions sidebar** (click the box icon or press `Ctrl+Shift+X`).

2. Search for **Python** in the search bar.

3. Find the **Python** extension (usually by Microsoft).

4. Click the **⚙️ gear icon** next to the extension, then choose:

   > **"Disable (Workspace)"**

5. If prompted with something like:

   > *"This extension depends on other extensions. Do you want to disable them too?"*

   Select **"Yes" or "Disable All"**.

💡 This will automatically disable additional extensions such as:

* **Pylance**
* **Jupyter**
* **Python Debugger**, etc.

> When you want to use Python again, please remember to re-enable the extensions that were disabled in order to restore linting and other functionalities provided by the Python extension and any related extensions.

---

### c. Task to Run Files

Create a `tasks.json` file inside the `.vscode/` folder with the following content:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "nginr",
      "type": "shell",
      "command": "${HOME}/PATH/TO/nginr", // Replace PATH/TO with your actual nginr location
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

* Make sure the `command` path points to the correct location of `nginr` on your system.
* Use `${HOME}` for better portability.
* Save this file as `.vscode/tasks.json` at the root of your project.

---

### d. Note for ErrorLens Extension Users

If you're using the **ErrorLens** extension, keep in mind that it only displays messages from other extensions (such as Python or Pylance). Therefore:

* **It’s recommended to disable the Python extension** as described above to prevent persistent error messages.
* If ErrorLens is still too distracting, you can **temporarily disable it** via the gear icon in the Extensions sidebar.
