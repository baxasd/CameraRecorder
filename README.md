# Craton Vision

Version: v0.1.0

[![Python](https://img.shields.io/badge/Python-3.12-3776AB.svg?style=flat&logo=python&logoColor=white)](https://www.python.org/) 
[![Intel RealSense](https://img.shields.io/badge/PyRealsense-2.58+-0071C5.svg?style=flat&logo=intel&logoColor=white)](https://github.com/IntelRealSense/librealsense)
[![MediaPipe](https://img.shields.io/badge/Mediapipe-0.10.21-00C0FF.svg?style=flat&logo=google&logoColor=white)](https://mediapipe.dev/)
[![License](https://img.shields.io/badge/License-Apache_2.0-blueviolet.svg?style=flat)](LICENSE)

Craton Vision is a high-performance module for 3D human pose estimation and recording using Intel RealSense depth cameras and MediaPipe. It serves as the primary visual acquisition layer for the Craton Project pipeline, providing low-latency spatial tracking of human motion.

## Architecture

### Core Modules (`core/`)
- **`core/camera.py`**: Manages Intel RealSense pipeline, alignment, and hardware filters.
- **`core/pose.py`**: Handles MediaPipe Pose estimation and 2D coordinate extraction.
- **`core/depth.py`**: Performs 3D deprojection math for pixel-to-point translation.
- **`core/config.py`**: Auto-generates and manages `settings.ini` with standard path resolution.

### Root Applications
- **`recorder.py`**: Main CLI interface for high-speed data acquisition and binary serialization.
- **`calibrator.py`**: GUI tool for visual camera configuration and filter tuning.
- **`viewer.py`**: Playback and inspection tool for captured `.bin` data.

## Analysis Capabilities / Features

- **3D Pose Estimation**: Real-time extraction of 33 human skeletal landmarks in metric space.
- **Depth Integration**: Seamless deprojection of 2D MediaPipe landmarks to 3D points using synchronized depth frames.
- **Optimized Serialization**: Custom binary format (`.bin`) for minimal I/O overhead during recording.
- **Hardware Acceleration**: Support for Intel RealSense on-chip processing and MediaPipe GPU/CPU delegation.

## Installation & Usage

### Setup
1. **Create Virtual Environment**:
   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux
   # or
   .\venv\Scripts\activate  # Windows
   ```
2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

### Execution
Run the recorder to start the CLI menu:
```bash
python recorder.py
```

For camera calibration:
```bash
python calibrator.py
```

For data inspection:
```bash
python viewer.py
```

### Build
Standardized PyInstaller commands for generating standalone executables:

**Windows Build:**
```bash
pyinstaller --clean tools/windows/build.spec
```

**Linux Build:**
```bash
pyinstaller --clean tools/linux/build.spec
```

## Contribution & License

- **License**: Distributed under the Apache 2.0 License. See `LICENSE` for details.
- **AI-Content Policy**: PRs containing unreviewed, generated AI content will be closed.
