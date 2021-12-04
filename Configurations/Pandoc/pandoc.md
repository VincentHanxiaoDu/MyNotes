---
title: Pandoc
listings-disable-line-numbers: true
---

# Pandoc Configurations

## Using Pandoc in Visual Studio Code

### Prerequisites

1. Install [VScode Insiders](https://code.visualstudio.com/insiders/) or [VScode](https://code.visualstudio.com/).
2. Install [Pandoc](https://pandoc.org/).
3. Install [LaTeX](https://www.latex-project.org/).
4. Install [LaTeX language support](https://marketplace.visualstudio.com/items?itemName=mathematic.vscode-latex) VScode extension. (Recommended)
5. Install [vscode-pdf](https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf) VScode extension. (Recommended)

### Configurations

- Pandoc Templates
  1. Templates can be found from online websites and repositories like [pandoc-templates](https://github.com/kjhealy/pandoc-templates).
  2. Use `pandoc --data-dir <data directory>` to specify the location of the templates, template files should be placed in `<data directory>/templates`. Use `pandoc --template <template name>` to specify which template to use. For more details, see [Pandoc User’s Guide](https://pandoc.org/MANUAL.html#option--data-dir).
  3. Use `pandoc <markdown_file.md> -o <pdf_file.pdf>` to generate a pdf file `<pdf_file.pdf>` from a markdown file `<markdown_file.md>`.

- VScode
  1. Open the Command Palette (Ctrl+Shift+P on Windows or Command+Shift+P on Mac), search for "Preference: Configure User Snippets" and click "markdown.json".
  2. Add a custom header. For example:
  ```json
  "header": {
      "prefix": "header",
      "body": [
          "---",
          "title: $TM_FILENAME_BASE",
          "date: $CURRENT_YEAR-$CURRENT_MONTH-$CURRENT_DATE",
          "author: <author>",
          "geometry: \"left=3cm,right=3cm,top=2cm,bottom=2cm\"",
          "---"
      ]
  }
  ```
  Open the Command Palette (Ctrl+Shift+P on Windows or Command+Shift+P on Mac), search for "Preference: Open Settings (JSON)" and click it. Add configurations:
  ```json
  "[markdown]": {
      "editor.quickSuggestions": true
  }
  ```
  Then, when editing any markdown file in the editor, type "header"+Enter to generate the header automatically.
  3. Add customized tasks, open the Command Palette (Ctrl+Shift+P on Windows or Command+Shift+P on Mac), search and click "Tasks: Configure Task", add tasks into the json file. For example:
  ```json
  "tasks": [
      {
          "label": "pandoc-md-pdf",
          "type": "shell",
          "command": "pandoc",
          "args": [
              "${file}",
              "-o",
              "${fileDirname}/${fileBasenameNoExtension}.pdf",
              "--from",
              "markdown",
              "--listings",
              "--template",
              "<template path>"
          ]
      },
      {
          "label": "pandoc-md-pdf-open",
          "type": "shell",
          "command": "open",
          "args": [
              "${fileDirname}/${fileBasenameNoExtension}.pdf"
          ],
          "dependsOn": [
              "pandoc-md-pdf"
          ],
          "group": {
              "kind": "build",
              "isDefault": true
          },
          "problemMatcher": []
      }
  ]
  ```
  4. Run the task by opening the Command Palette (Ctrl+Shift+P on Windows or Command+Shift+P on Mac), search for "Task: Run Task" and click the task created.
