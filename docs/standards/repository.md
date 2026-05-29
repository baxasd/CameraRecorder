# Craton Project: Repository Standards

This document defines the mandatory repository structure and naming conventions for all Craton Project modules (`vision`, `radar`, `workbench`).

## 1. Directory Hierarchy

Every repository must adhere to the following tree structure:

```text
craton-[module]/
├── core/                   # Internal Logic & UI
├── docs/                   # Documentation
├── tools/                  # Build & Deployment Tools
│   ├── windows/            # Windows-specific build assets
│   │   ├── build.spec      # PyInstaller Specification
│   │   └── manifest.xml    # Windows Assembly Manifest
│   │   └── installer.iss   # Inno Installer
│   ├── linux/              # Linux-specific build assets
│   │   └── build.spec      # PyInstaller Specification
│   ├── workbench.ico       # Unified Branding Icon
├── Root files              # Default root files, entrypoint applications

```

## 2. Naming Conventions

*   **Repository Name**: `craton-[purpose]` (e.g., `craton-vision`).
*   **Executable Name**: `[Purpose]` (PascalCase, e.g., `Workbench.exe`).
*   **Subdirectory for Libs**: Always named `libs`.

## 3. Path Resolution Standard

All internal path resolutions must use the following logic to ensure compatibility between `onedir` mode and development mode:

```python
if getattr(sys, 'frozen', False):
    root_base = sys._MEIPASS
    libs_path = os.path.join(root_base, 'libs')
    ROOT_DIR = libs_path if os.path.exists(libs_path) else root_base
else:
    ROOT_DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))
```

## 4. Standardized README Structure

Every repository must follow a consistent `README.md` layout to ensure professional and uniform documentation across the ecosystem.

### Required Sections:

1.  **Header & Badges**: 
    *   Project Title (H1).
    *   Projct version - Currently standard version on all modules is 0.1.0: e.g: Version: v0.1.0
    *   Badges for Python Version, Primary Frameworks (e.g., Streamlit, MediaPipe), and License.
2.  **Project Description**: A short, concise paragraph explaining the module's purpose and how it fits into the Craton pipeline.
3.  **Architecture**: 
    *   A bulleted list mapping files in `core/` to their specific responsibilities.
    *   Description of the applications in the root
4.  **Analysis Capabilities / Features**: 
    *   Breakdown of the processing logic provided by the module.
5.  **Installation & Usage**:
    *   **Setup**: Virtual environment and `pip install -r requirements.txt`.
    *   **Execution**: Command to run the local version (`python app.py`).
    *   **Build**: Standardized PyInstaller commands for Windows and Linux.
6.  **Contribution & License**: 
    *   Reference to the License. Keep in mind License is Apache and file itself should be without extension
    *   AI-Content Policy: "PRs containing unreviewed, generated AI content will be closed."
