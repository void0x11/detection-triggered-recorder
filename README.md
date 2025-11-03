# Detection-Triggered Recorder

An **intelligent, event-driven surveillance system** that automatically captures video and screenshots when humans are detected in real time using AI-powered vision processing.

---

## 📖 Overview

**Detection-Triggered Recorder** is an advanced **security monitoring application** designed for research and autonomous surveillance scenarios.  
It continuously monitors a USB-connected camera feed, performs real-time **human detection** using **YOLOv8**, and **initiates recording only when persons are detected** in the scene.  

This **event-driven recording** approach minimizes storage usage compared to traditional continuous recording, while still maintaining full event coverage with timestamped video and image evidence.

---

## 🚀 Key Features

### 🎯 Core Functionality
- **Real-Time Human Detection** — Powered by the YOLOv8 neural network (up to 30 FPS)
- **Automatic Event-Driven Recording** — Records only when a person is detected
- **Smart Cooldown Logic** — 5-second cooldown after last detection to prevent fragmented clips
- **Timestamped Snapshots** — Captures screenshots every 2 seconds during detection
- **Efficient Standby Mode** — Minimal CPU usage while continuously monitoring

---

### 🎬 Recording Features
- **High-Quality Output** — 1920×1080 @ 30 FPS (MP4, H.264 codec)
- **Automatic Timestamping** — Filenames in `YYYYMMDD_HHMMSS` format
- **Organized Storage** — Videos stored in the `recordings/` directory
- **Efficient Compression** — H.264 codec for balance between quality and size

---

### 📸 Screenshot Features
- **Event Detection Snapshots** — Automatic image capture upon detection
- **Timestamp Overlay** — Each image annotated with detection time
- **Organized Storage** — Saved in `snapshots/` directory with millisecond precision
- **Smart Capture Frequency** — 2-second interval during ongoing detection
- **Evidence Redundancy** — Screenshots serve as backups if camera disconnects mid-recording

---

### 🖥️ User Interface
- **Modern PyQt5 GUI** — Clean, professional desktop interface
- **Live Feed Display** — Real-time camera view with detection bounding boxes
- **Dynamic Status Indicators**:
  - 🟩 **Person Detection**: Not Detected / **DETECTED**
  - 🟥 **Recording Status**: Standby / **RECORDING** / Cooldown
  - 🟧 **System Status**: Monitoring / Stopped / Error
- **Color-Coded Feedback** — Green (normal), Red (active), Orange (transition)
- **Camera Selection Dropdown** — Choose among available cameras
- **Resizable Window** — Adaptable layout for all screen sizes

---

### 🎥 Camera Support
- **USB and Built-in Camera Compatibility**
- Tested with **OBSBOT Tiny 2** and standard V4L2-compliant webcams
- **Auto Camera Detection** — Scans and identifies connected devices
- **1920×1080 Capture at 30 FPS**
- **Multi-Camera Adaptability** — Can be extended for simultaneous feeds

---

## 🧩 System Architecture

### ⚙️ Threading Model
- **CameraThread** — Captures frames at 30 FPS  
- **DetectionThread** — Performs YOLOv8 inference  
- **RecordingManager** — Manages recording lifecycle (Standby → Detected → Cooldown)  
- **ScreenshotManager** — Handles snapshot capture and annotation  
- **Main UI Thread** — Manages PyQt5 rendering and user interaction  

---

### 🔄 Data Flow
```text
USB Camera (1920×1080, 30 FPS)
    ↓
CameraThread (frame capture)
    ↓
DetectionThread (YOLOv8 inference)
    ↓ (detection_result signal)
    ├→ RecordingManager (starts/stops recording)
    ├→ ScreenshotManager (captures snapshots)
    └→ Main UI (updates status indicators)
    ↓
Video Output: recordings/*.mp4
Image Output: snapshots/*.jpg
```

---

## 🧰 Installation Guide

### ✅ Prerequisites
- **Python 3.8+**
- **pip** package manager
- **USB camera or built-in webcam**

---

### 🪜 Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/detection-triggered-recorder.git
cd detection-triggered-recorder
```

### ⚙️ Step 2: Install Dependencies
```bash
pip install -r requirements.txt
```

### ▶️ Step 3: Run the Application
```bash
python security_monitor.py
```

---

## 📂 Project Structure
```text
detection-triggered-recorder/
├── security_monitor.py          # Main application file
├── requirements.txt             # Dependencies list
├── recordings/                  # Saved video recordings
├── snapshots/                   # Saved detection snapshots
├── models/                      # YOLOv8 model weights
└── ui/                          # GUI resources and assets
```

---

## 🧠 Technical Notes
- Designed with **modular architecture** for research and customization.
- Compatible with **Windows**, **Linux**, and **macOS**.
- Can be extended for **multi-camera systems**, **remote alerts**, or **cloud storage**.

---

## 🛡️ License
This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

---

## 🤝 Contributing
Contributions, issues, and feature requests are welcome!  
Please open an issue or submit a pull request via GitHub.

---

## 🌟 Acknowledgements
- **YOLOv8** by [Ultralytics](https://github.com/ultralytics/ultralytics)
- **PyQt5** for the graphical interface
- **OpenCV** for image and video processing

---
