# 🔎 Classifying Cells in Full FOV Microscopy Images

## 🧠 Goal
Apply a trained CNN model to **microscopy images** (FOVs) to classify individual astrocyte cells as **live** or **dead**.

---

## ⚙️ Pipeline Overview
1. Load `.tif` FOV images  
2. Enhance contrast (CLAHE)  
3. Segment cells using adaptive thresholding or watershed  
4. Filter valid cell-like regions (contour area, aspect ratio)  
5. Extract, normalize, resize and classify each cell using the CNN model  
6. Overlay predicted labels (green = live, red = dead) on original image  

---

## 🌐 Preprocessing
- CLAHE: local contrast enhancement  
- Adaptive thresholding: detects cells even with variable lighting  
- Morphological opening/closing: removes noise  

---

## ⚡ Segmentation
- **Contour-based** detection using OpenCV `findContours`  
- **Watershed** segmentation to split overlapping cells  
- Area filtering: exclude very small or large blobs  
- Aspect ratio filtering: remove long or irregular shapes  

---

## 🧪 Classification
- Each valid region is:
  - Cropped from original image  
  - Resized to 128x128  
  - Converted to RGB  
  - Normalized to [0, 1]  
- Predictions made using `astrocyte_live_dead_model.keras`  

**Thresholds**:
- Default: 0.5  
- Tuned threshold: 0.25 (to reduce false dead calls)  

---

## 🖼️ Output
- Annotated image with predictions  
- Count of predicted live/dead cells  
- Optionally saved image using `cv2.imwrite()`  

---

## 📘 Example Notebook
Run `Classifying Cells in Full FOV Microscopy Images.ipynb`

---

## 🔧 Requirements
```bash
pip install opencv-python matplotlib numpy tifffile tensorflow
