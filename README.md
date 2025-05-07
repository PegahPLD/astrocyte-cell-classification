# Astrocyte Cell Classification & Full FOV Detection Pipeline

This project includes two connected components:

1. A deep learning model that classifies individual astrocyte cells as live or dead.
2. A pipeline that processes full microscopy field-of-view (FOV) images to segment, extract, and classify cells using the trained model.

---

## Part 1: Astrocyte Live/Dead Cell Classifier

Goal:
Train a CNN to classify cropped images of single astrocyte cells as either live or dead.

Dataset structure:

data/
├── dead/
└── live/

- Live cells: ~2430 images
- Dead cells: ~630 images

To handle class imbalance:
- Applied data augmentation (rotation, flipping, brightness)
- Used class weighting during training

Model architecture:

Input → Conv → Pool → Conv → Pool → Flatten → Dense → Dropout → Dense → Sigmoid

- Loss: Binary crossentropy
- Optimizer: Adam
- Accuracy: ~88% on validation set

Training details:
- Images resized to 128x128
- Normalized pixel values to [0, 1]
- Model saved as: astrocyte_live_dead_model.keras

Trained using: model_training.ipynb


---

## Part 2: Full FOV Microscopy Image Classification

Goal:
Detect and classify multiple astrocyte cells in large microscopy images using the trained CNN.

Pipeline steps:

1. Load a full FOV `.tif` image
2. Enhance contrast using CLAHE
3. Apply adaptive thresholding or Otsu + morphological filtering
4. Segment cells using contours or watershed
5. Filter objects by area and aspect ratio
6. Crop each cell region and classify it
7. Draw boxes and labels for predicted class and confidence

Classification:
- Each region resized to 128x128
- Converted to RGB if needed
- Normalized to [0, 1]
- Passed into the saved CNN model
- Threshold set at 0.4 to improve prediction balance

Outputs:
- Annotated image with bounding boxes
  - Green box = live
  - Red box = dead
- Live/dead count summary
- Optional: Save annotated image



---

## Future Directions

- Replace thresholding with deep segmentation (Cellpose, StarDist)
- Export detected cells in YOLO format for training object detectors
- Build a GUI for drag-and-drop FOV classification

---

## Credits

Developed using TensorFlow, OpenCV, NumPy, and Jupyter Notebook.
Created to assist with astrocyte cell viability classification from microscopy images.
