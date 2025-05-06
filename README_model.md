# 🔬 Astrocyte Live/Dead Cell Classifier

## 🧠 Goal
Train a convolutional neural network (CNN) to classify individual astrocyte cell images as **live** or **dead**, using microscopy image data.

---

## 📁 Dataset Structure
Images were sorted into two labeled folders:

data/
├── dead/
└── live/

- Live cells: ~2430
- Dead cells: ~630

To mitigate class imbalance:
- Data augmentation (rotations, flips, brightness, zoom)
- Class weights were used during training

---

## 🏗️ Model Architecture
A simple CNN built with TensorFlow/Keras:

Input → Conv → Pool → Conv → Pool → Flatten → Dense → Dropout → Dense → Sigmoid

- **Loss**: Binary crossentropy  
- **Optimizer**: Adam  
- **Final accuracy**: ~88% on validation data

The final model is saved as:

astrocyte_live_dead_model.keras

---

## 🔄 Training Details
- Images resized to 128x128  
- Normalized to [0, 1]  
- Binary labels: 0 = dead, 1 = live  

Example training notebook: `astrocyte_live_dead_model.ipynb`

---

## ✨ Improvements to Explore
- Balance dataset using more dead cell samples  
- Add focal loss to penalize misclassification of minority class  
- Try deeper CNN or transfer learning (e.g., MobileNet)

---

## 📄 Output
- `.keras` model for prediction  
- Classification report with precision, recall, F1-score  
- Visualization of training history and predictions

---

## 📍 Location
Place this model in `models/astrocyte_live_dead_model.keras` and call it from the FOV analysis notebook.
