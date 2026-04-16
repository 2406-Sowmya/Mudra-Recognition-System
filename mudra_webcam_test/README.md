# Mudra Webcam Test

This project contains two webcam inference scripts for mudra recognition:

- `original.py`: the original hand-crop prediction pipeline
- `skin_segmenation.py`: hand detection followed by skin segmentation with a gray background and a 3-panel preview

## Default paths

The scripts use project-relative defaults:

- Model: `models\mudra_mobilenetv2_final.keras`
- Class names: `models\class_names.json`
- Hand detector: `hand_landmarker.task`

You only need to pass `--model` and `--class-names` if you want custom files.

## Setup

Run these commands from:

`C:\Users\RISHITHA\OneDrive\Desktop\mudra_webcam_test`

```powershell
python -m venv .venv
.\.venv\Scripts\python -m pip install --upgrade pip
.\.venv\Scripts\python -m pip install -r .\mudra_webcam_test\requirements.txt
```

Important: always run scripts with `.venv\Scripts\python` so global packages do not interfere.

## Run Original Predictor

```powershell
cd C:\Users\RISHITHA\OneDrive\Desktop\mudra_webcam_test
.\.venv\Scripts\python .\mudra_webcam_test\original.py --camera 0
```

Useful options:

```powershell
.\.venv\Scripts\python .\mudra_webcam_test\original.py --min-confidence 0.60
.\.venv\Scripts\python .\mudra_webcam_test\original.py --model "C:\path\to\model.keras" --class-names "C:\path\to\class_names.json"
```

## Run Skin Segmentation Predictor

YCrCb skin segmentation:

```powershell
cd C:\Users\RISHITHA\OneDrive\Desktop\mudra_webcam_test
.\.venv\Scripts\python .\mudra_webcam_test\skin_segmenation.py --camera 0 --method ycrcb
```

HSV skin segmentation:

```powershell
.\.venv\Scripts\python .\mudra_webcam_test\skin_segmenation.py --camera 0 --method hsv
```

Useful options:

```powershell
.\.venv\Scripts\python .\mudra_webcam_test\skin_segmenation.py --min-confidence 0.60 --method ycrcb
.\.venv\Scripts\python .\mudra_webcam_test\skin_segmenation.py --model "C:\path\to\model.keras" --class-names "C:\path\to\class_names.json" --method hsv
```

## Notes

- Press `Q` to close the webcam window.
- The app uses MediaPipe Hands for hand detection.
- `skin_segmenation.py` shows the original frame, segmented hand preview, and model input preview.
- The oneDNN TensorFlow message is informational. To suppress it in the current terminal:

```powershell
$env:TF_ENABLE_ONEDNN_OPTS = "0"
```
