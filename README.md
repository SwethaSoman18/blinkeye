# 👁️ BlinkEye — Real-Time Blink Detection

A real-time eye blink detection and counter application built with Python, OpenCV, and MediaPipe FaceMesh. It tracks facial landmarks around the eye, calculates an eye-openness ratio, and counts blinks live with a dynamic plot.

---

## 🎯 Features

- 📷 **Live webcam feed** processed in real time
- 👁️ **Eye landmark tracking** using FaceMesh (12 key points around the left eye)
- 📊 **Live ratio plot** showing eye openness over time
- 🔢 **Blink counter** displayed on screen with color feedback
- 🧠 **Smoothing** via a rolling average of the last 3 frames to reduce false positives

---

## 🖥️ Demo

| Webcam View + Blink Counter | Live Eye Ratio Plot |
|:---------------------------:|:-------------------:|
| Blink landmarks drawn on face | Real-time graph of vertical/horizontal eye ratio |

---

## 🛠️ Tech Stack

| Library | Purpose |
|---------|---------|
| `opencv-python` | Webcam capture & image rendering |
| `cvzone` | FaceMesh detection & UI utilities |
| `mediapipe` | Underlying face landmark model (via cvzone) |

---

## 📁 Project Structure

```
blinkeye/
├── blink_eye.py          # Main blink detection script
├── main.py               # Entry point (PyCharm default)
├── face_landmarker.task  # MediaPipe face landmark model
├── .gitignore
└── README.md
```

---

## ⚙️ How It Works

1. **Capture** — Reads frames from the default webcam (`cv2.VideoCapture(0)`).
2. **Detect** — `FaceMeshDetector` locates 468 facial landmarks on the face.
3. **Measure** — Calculates the **vertical** (top–bottom eyelid) and **horizontal** (left–right eye corner) distances for the left eye.
4. **Ratio** — Computes `ratio = (vertical / horizontal) × 100`. A lower ratio means the eye is more closed.
5. **Blink** — If the smoothed ratio drops below **35**, a blink is registered (with a cooldown of 10 frames to avoid double-counting).
6. **Visualize** — Displays the webcam feed side-by-side with a live ratio plot.

```
Eye Openness Ratio = (Vertical Distance / Horizontal Distance) x 100
Blink threshold: ratio < 35
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- A webcam

### Installation

```bash
# Clone the repository
git clone https://github.com/SwethaSoman18/blinkeye.git
cd blinkeye

# Create and activate a virtual environment
python -m venv .venv
.venv\Scripts\activate      # Windows
# source .venv/bin/activate  # macOS/Linux

# Install dependencies
pip install opencv-python cvzone mediapipe
```

### Run

```bash
python blink_eye.py
```

Press **`Q`** to quit the application.

---

## 🔑 Key Landmark IDs (Left Eye)

```
idList = [22, 23, 24, 26, 110, 157, 158, 159, 160, 161, 130, 243]

Vertical reference  : face[159] (top)  <-> face[23]  (bottom)
Horizontal reference: face[130] (left) <-> face[243] (right)
```

---

## 📌 Notes

- The model currently tracks the **left eye** only.
- The blink threshold (`< 35`) may need tuning depending on lighting and camera distance.
- `face_landmarker.task` is the MediaPipe model binary included in the repo (~3.6 MB).

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---
