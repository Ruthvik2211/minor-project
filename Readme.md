# Mask Detection using ResNet50 v2 
# Face Mask Detection

This repository contains scripts and a small Streamlit UI for detecting face masks in images and video, plus training and model-conversion utilities.

Quick links:

- Image detection: `detect_mask_image.py`
- Video / webcam detection: `detect_mask_video.py`
- Streamlit UI: `app.py` (run with `streamlit run app.py`)
- Training: `train_mask_detector.py` (MobileNetV2) and ResNet50 example in `ResNet50_v2/`
- Convert to ONNX: `model2onnx.py`

**Requirements (Windows)**

1. Create a Python venv and activate it:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1    # or .\.venv\Scripts\activate.bat
```

2. Install dependencies:

```powershell
pip install -r requirements.txt
```

Usage
-----

- Detect masks in a single image (opens a window):

```powershell
python detect_mask_image.py --image images/pic1.jpeg --model mask_detector.model
```

- Run real-time webcam mask detection:

```powershell
python detect_mask_video.py --model mask_detector.model
```

- Run the Streamlit app (browser UI):

```powershell
streamlit run app.py
```

In the Streamlit UI you can upload a JPG (it saves to `images/out.jpg`) and press *Process* to run detection. The webcam option is listed but currently marked "available soon" in the UI.

Training
--------

- Train a MobileNetV2-based mask detector using the provided `train_mask_detector.py`:

```powershell
python train_mask_detector.py --dataset dataset --model mask_detector.model --plot plot.png
```

- There is also an example ResNet50 training notebook and script under `ResNet50_v2/`:

```powershell
python ResNet50_v2/mask_with_resnet.py --dataset dataset --model "ResNet50_v2/ResNet50_mask_detector.model"
```

Model conversion
----------------

Convert a saved Keras `.h5` model to ONNX:

```powershell
python model2onnx.py --model mask_detector.model --output mask_detector.onnx
```

Notes and file layout
---------------------

- `mask_detector.model` — default trained model (Keras HDF5) loaded by scripts and `app.py`.
- `face_detector/` — OpenCV DNN face detector files (`deploy.prototxt` and `.caffemodel`) used by detection scripts.
- `dataset/` — training images organized as `dataset/with_mask` and `dataset/without_mask`.
- `images/` — sample images and the app's temporary `out.jpg`.

Implementation notes
--------------------

- Scripts set environment variables to prefer CPU and a Python protobuf implementation; remove or modify these if you want GPU support.
- The Streamlit app uses `mask_detector.model` by default. Replace the filename or retrain if you want improved accuracy.

Troubleshooting
---------------

- If OpenCV cannot access your webcam, try running your terminal as Administrator or use a different `src` index in `detect_mask_video.py`.
- If TensorFlow/Keras versions mismatch when loading a saved model, install the package versions from `requirements.txt`.

Want changes?
-------------
If you'd like I can:

- add example images and a small GIF demonstrating the app
- update `requirements.txt` to pin exact package versions
- add a `Makefile` or PowerShell script with the common commands

---
Updated README to include usage, run commands, and brief notes.

