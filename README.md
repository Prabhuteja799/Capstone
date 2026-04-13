# Capstone — Face Recognition Attendance System

An automated attendance marking system that uses real-time face recognition to identify students and log their attendance — no manual sign-ins, no proxy marking.

Built as a final-year capstone project using OpenCV and the face_recognition library.

---

## What it does

- Trains on a set of labeled student photos stored in `Training_images/`
- Opens a live webcam feed and identifies faces in real time
- Matches detected faces against the trained model
- Marks attendance with a timestamp in `Attendance.csv`
- Unknown or unrecognized faces are flagged and skipped

---

## How it works

```
Training phase
──────────────
Training_images/ (labeled photos)
    │
    ▼
face_recognition encodes each face → stored in memory

Live detection phase
────────────────────
Webcam feed → OpenCV frame capture
    │
    ▼
face_recognition.compare_faces()
    │
    ├── match → log name + timestamp to Attendance.csv
    └── no match → display "Unknown"
```

---

## Project structure

```
Capstone/
├── Code                   ← Main Python script
├── Training_images/       ← Labeled student photos (one folder per student)
└── Attendance.csv         ← Auto-generated attendance log
```

---

## Setup

### Prerequisites

- Python 3.8+
- Webcam
- `cmake` (required by dlib, which face_recognition depends on)

### Install

```bash
# Install system dependencies (Mac)
brew install cmake

# Install Python packages
pip install face_recognition opencv-python numpy pandas
```

### Add training images

Create one folder per person inside `Training_images/`, named exactly as you want them identified:

```
Training_images/
├── John_Smith/
│   ├── photo1.jpg
│   └── photo2.jpg
└── Jane_Doe/
    └── photo1.jpg
```

### Run

```bash
python Code
```

The webcam opens. Detected and recognized faces are outlined with their name. Attendance is written to `Attendance.csv` automatically.

---

## Tech stack

| Component | Tech |
|---|---|
| Language | Python 3 |
| Face recognition | `face_recognition` (dlib) |
| Computer vision | OpenCV (`cv2`) |
| Data logging | pandas / CSV |

---

## Limitations

- Designed for controlled lighting and single-camera setups
- Recognition accuracy drops with significant changes in lighting or angle
- Not intended for large-scale or production deployment without further hardening

---

## Future improvements

- Web UI for viewing attendance logs
- Multi-camera support
- Liveness detection to prevent photo spoofing
- Database backend instead of CSV
