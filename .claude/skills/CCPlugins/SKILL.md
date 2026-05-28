```markdown
# CCPlugins Development Patterns

> Auto-generated skill from repository analysis

## Overview

This skill teaches the core development patterns, workflows, and coding conventions used in the CCPlugins repository. CCPlugins is a Python-based suite of CLI commands designed for extensibility and modularity, with a strong focus on maintainable documentation, quality checks, and session management. The repository is framework-agnostic and uses a combination of markdown-driven command definitions and Python scripts for installation and management.

## Coding Conventions

- **File Naming:**  
  Use camelCase for Python files and command markdown files.  
  _Example:_  
  ```
  fixImports.py
  implementCommand.md
  ```

- **Import Style:**  
  Use relative imports within modules.  
  _Example:_  
  ```python
  from .utils import parse_args
  ```

- **Export Style:**  
  Use named exports (explicit function/class definitions, not wildcard `*`).  
  _Example:_  
  ```python
  def run_command():
      pass

  __all__ = ["run_command"]
  ```

- **Commit Messages:**  
  Use prefixes: `feat`, `fix`, `add`, `chore`.  
  _Example:_  
  ```
  feat: add session persistence to scaffold command
  fix: correct folder path resolution in implement
  ```

## Workflows

### Add or Enhance Command
**Trigger:** When introducing a new CLI command or significantly updating an existing one  
**Command:** `/add-command`

1. Create or update the command markdown file under `commands/`
2. Update `README.md` to document the new/changed command
3. Update `CHANGELOG.md` to record the addition/change
4. Update `install.sh`, `uninstall.py`, and `uninstall.sh` to include or remove the command
5. Optionally update `CONTRIBUTING.md` if developer workflow changes

_Example:_  
```bash
touch commands/myNewCommand.md
# Edit README.md, CHANGELOG.md, and installer scripts as needed
```

---

### Refactor or Enhance Existing Command
**Trigger:** When improving, refactoring, or extending the logic of an existing command  
**Command:** `/refactor-command`

1. Edit the relevant command markdown file(s) under `commands/`
2. Update `README.md` and/or `CHANGELOG.md` to reflect the change
3. If session or folder logic changes, update related command files in batch
4. If installer/uninstaller scripts are affected, update them

---

### Session or Folder Path Update
**Trigger:** When fixing or improving how commands store session data or handle working directories  
**Command:** `/update-session-paths`

1. Edit multiple command files to update path/session logic (e.g., `.claude/` → visible folders)
2. Update `README.md` and/or `CHANGELOG.md` to document the change
3. Batch update affected commands for consistency

_Example:_  
```python
# Before
session_path = ".claude/session.json"

# After
session_path = "sessions/session.json"
```

---

### Quality Checks and Validation Enhancement
**Trigger:** When enforcing or enhancing pre-commit/pre-push quality gates or adding validation to commands  
**Command:** `/add-quality-checks`

1. Edit commands to add or update validation/quality check logic (e.g., `commands/commit.md`, `commands/contributing.md`, `commands/test.md`)
2. Update `README.md` and/or `CHANGELOG.md` to document the new requirements
3. Update `CONTRIBUTING.md` if developer workflow changes

_Example:_  
```python
def validate_command_input(args):
    if not args:
        raise ValueError("Arguments required")
```

---

### Documentation Overhaul or Update
**Trigger:** When updating documentation to match new features, commands, or architecture  
**Command:** `/update-docs`

1. Edit `README.md` and/or `CHANGELOG.md` with new sections or updates
2. Edit or add relevant command markdown files under `commands/`
3. Update `CONTRIBUTING.md` if developer workflow changes
4. If a docs command exists, update `commands/docs.md`

---

## Testing Patterns

- **Test Files:**  
  Test files follow the `*.test.*` naming pattern (e.g., `scaffold.test.py`).
- **Framework:**  
  No specific test framework detected; likely uses standard Python testing (e.g., `unittest` or `pytest`).
- **Test Placement:**  
  Tests are placed alongside or near the code they test.

_Example:_  
```python
# scaffold.test.py
import unittest
from .scaffold import run_scaffold

class TestScaffold(unittest.TestCase):
    def test_run_scaffold(self):
        self.assertTrue(run_scaffold())
```

## Commands

| Command              | Purpose                                                                 |
|----------------------|-------------------------------------------------------------------------|
| /add-command         | Add a new CLI command or significantly enhance an existing one           |
| /refactor-command    | Refactor or extend the logic of an existing command                      |
| /update-session-paths| Update session or folder path logic for commands                         |
| /add-quality-checks  | Add or improve validation and quality checks to commands and workflows   |
| /update-docs         | Overhaul or update project documentation                                 |
```
