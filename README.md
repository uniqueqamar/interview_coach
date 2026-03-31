# 🎯 AI Interview Coach

Real-time facial emotion analysis during mock interviews.  
Built with **Streamlit · OpenCV · FER · Plotly**.

---

## ✨ Features

| Feature | Detail |
|---|---|
| Live webcam feed | Annotated with bounding boxes + emotion labels |
| Emotion detection | 7 emotions via FER (happy, neutral, surprise, fear, sad, angry, disgust) |
| Confidence Score | 0–100, derived from positive vs negative emotion ratios |
| Real-time graph | Rolling 120-frame confidence trend |
| Contextual tips | Emotion-specific coaching advice |
| Session summary | Duration, avg score, % confident vs nervous, donut chart, timeline |

---

## ⚙️ Installation

### 1. Clone / download
```bash
# Place app.py and requirements.txt in the same folder
cd ai_interview_coach
```

### 2. Create a virtual environment (recommended)
```bash
python -m venv venv

# macOS / Linux
source venv/bin/activate

# Windows
venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

> **Note on TensorFlow:** FER uses TensorFlow internally.  
> For CPU-only machines use `pip install tensorflow-cpu` instead.  
> On Apple Silicon (M1/M2/M3): `pip install tensorflow-macos tensorflow-metal`

### 4. Run the app
```bash
streamlit run app.py
```

The browser will open automatically at `http://localhost:8501`.

---

## 🖥️ Usage

1. Click **▶ Start Interview** — your webcam activates.
2. Speak your answers aloud while facing the camera.
3. Watch the **Live Emotion** label and **Confidence Score** update in real time.
4. Click **⏹ Stop Interview** when done.
5. Review the **Session Summary** — emotion distribution, feedback tips, and a confidence timeline.

---

## 🔧 Performance Tips

| Tip | Details |
|---|---|
| Good lighting | Bright, even frontal light gives best face detection |
| Frame distance | Sit ~50–80 cm from the camera |
| Background | Plain/dark backgrounds reduce false detections |
| GPU | TensorFlow with CUDA will significantly improve FPS |
| mtcnn | Change `FER(mtcnn=True)` in `load_detector()` for higher accuracy (slower) |

---

## 📁 Project Structure

```
ai_interview_coach/
├── app.py            ← Main Streamlit application
├── requirements.txt  ← Python dependencies
└── README.md         ← This file
```

---

## 🧠 How Confidence Score Works

```
Positive emotions: happy, neutral
Negative emotions: fear, sad, angry, disgust

score = positive_mass / (positive_mass + negative_mass) × 100
```

A score of **65+** is considered confident, **35–** is nervous, **35–65** is neutral.

---

## 📦 Key Dependencies

| Library | Version | Purpose |
|---|---|---|
| streamlit | ≥1.35 | Web UI framework |
| opencv-python | ≥4.9 | Webcam capture + annotation |
| fer | ≥22.5 | Facial emotion recognition |
| tensorflow | ≥2.13 | FER inference backend |
| plotly | ≥5.18 | Interactive charts |
| numpy | ≥1.24 | Array operations |

---

## 🐛 Troubleshooting

**Webcam not detected:**  
→ Grant browser/terminal camera permissions. Try `cv2.VideoCapture(1)` for external webcams.

**`ModuleNotFoundError: fer`:**  
→ Run `pip install fer` inside your activated virtual environment.

**TensorFlow warnings on startup:**  
→ These are normal informational logs and don't affect functionality.

**Low FPS / lag:**  
→ Detection runs every 2 frames by default. Increase `frame_skip % 2` to `% 3` in `app.py` for lighter CPU usage.
