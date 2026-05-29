# Craton Project: Build Standards

This document defines the mandatory build procedures for packaging Craton Project modules into standalone executables.

## 1. Distribution Mode: `onedir`

All Craton modules **must** be built in "one-directory" mode (`--onedir`). This is required for:
*   Faster application startup (no decompression overhead).
*   Clean separation of dependencies via the `libs` folder, contents directory should be explicityly stated into each exe, not in collect_all.
*   Reliable resolution of relative assets (config, models, images).

## 2. Dependency Isolation (`libs` folder)

To prevent clutter in the root application folder, all collected binaries, zipfiles, and datas must be moved to a `libs` subdirectory using the `contents_directory` parameter in the PyInstaller `EXE` section.

### Required Spec Configuration:
```python
exe = EXE(
    pyz,
    a.scripts,
    [],
    [],
    [],
    exclude_binaries=True,
    name='CratonModule',
    # ... other params
    contents_directory='libs',
)

coll = COLLECT(
    exe,
    a.binaries,
    a.zipfiles,
    a.datas,
    # ...
)
```

## 3. Mandatory Build Inclusions

### Metadata
Streamlit and scientific packages rely on package metadata. You **must** include metadata collection in the `Analysis` datas:
```python
from PyInstaller.utils.hooks import copy_metadata
datas += copy_metadata("streamlit")
```

### Submodule Collection
This section only applies for workbench. Please double check the module capabilies before collection of submodule to prevent unnesessary bundle of modules inside assembly
Do not list submodules manually. Use `collect_submodules` for:
*   `streamlit`
*   `pandas`
*   `numpy`
*   `scipy`
*   `sklearn`
*   `plotly`

## 4. Platform Specifics

### Windows
*   **Architecture**: Must target `x64`.
*   **Manifest**: A `manifest.xml` must be provided to ensure `asInvoker` execution level and Windows 10/11 compatibility.
*   **Icon**: The unified `[module].ico` must be embedded.
*   **Installer**: Distribution must be handled via **Inno Setup** (.iss) to create a single-file setup wizard.

### Linux
*   **Architecture**: Must target `x64`.

## 5. Build Commands

Builders must use the following commands from the root of the repository:

**Windows Build:**
```bash
pyinstaller --clean tools/windows/build.spec
```

**Linux Build:**
```bash
pyinstaller --clean tools/linux/build.spec
```
