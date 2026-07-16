# Brain Tumor Detection from MRI Images using Digital Image Processing

A desktop application that uses a Convolutional Neural Network (CNN) to classify brain MRI scans as **Tumor** or **Normal**, built with Keras/TensorFlow and wrapped in a Tkinter GUI for end-to-end use (data import → training → inference).

## Overview

This project provides a simple GUI-driven pipeline for brain tumor detection from MRI images. Instead of running scripts from the command line, users can import a dataset, train a CNN model, and test it on new MRI images — all through a single desktop interface.

## Features

- **Data Import** — Load MRI image dataset from a structured directory (`xray/train`, `xray/val`, `xray/test`)
- **Model Training** — Train a CNN classifier directly from the GUI with live progress and accuracy feedback
- **Inference / Testing** — Upload a single MRI image and get an instant Tumor / Normal prediction
- **Visual Feedback** — Displays the selected MRI image and shows accuracy via popup dialogs

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python |
| Deep Learning | Keras, TensorFlow |
| Image Processing | OpenCV, PIL (Pillow) |
| GUI | Tkinter |
| Data Handling | NumPy, Pandas |
| Visualization | Matplotlib |

## Model Architecture

A sequential CNN with 3 convolution + max-pooling blocks:

```
Input (64x64x3)
   ↓
Conv2D(32, 3x3, ReLU) → MaxPooling2D(2x2)
   ↓
Conv2D(32, 3x3, ReLU) → MaxPooling2D(2x2)
   ↓
Conv2D(32, 3x3, ReLU) → MaxPooling2D(2x2)
   ↓
Flatten
   ↓
Dense(128, ReLU)
   ↓
Dense(1, Sigmoid)   →  Tumor / Normal
```

- **Optimizer:** Adam
- **Loss:** Binary Crossentropy
- **Metric:** Accuracy
- **Data Augmentation:** Rescaling, shear, zoom, and horizontal flip via `ImageDataGenerator`

## Results

- **Accuracy:** 90–96% on the test set
- **Dataset:** 600+ MRI images (Tumor / Normal classes)

## Project Structure

```
Brain-Tumor-Detection-from-MRI-Image-Using-Digital-Image-Processing/
│
├── main.py                # GUI application + CNN pipeline
├── xray/
│   ├── train/
│   │   ├── Tumor/
│   │   └── Normal/
│   ├── val/
│   │   ├── Tumor/
│   │   └── Normal/
│   └── test/
│       ├── Tumor/
│       └── Normal/
└── README.md
```

## Installation

1. Clone the repository
   ```bash
   git clone https://github.com/AB0823/Brain-Tumor-Detection-from-MRI-Image-Using-Digital-Image-Processing.git
   cd Brain-Tumor-Detection-from-MRI-Image-Using-Digital-Image-Processing
   ```

2. Install dependencies
   ```bash
   pip install numpy pandas pydicom opencv-python matplotlib pillow keras tensorflow scikit-learn
   ```

3. Organize your dataset into the `xray/train`, `xray/val`, and `xray/test` folders, each containing `Tumor` and `Normal` subfolders.

## Usage

1. Run the application
   ```bash
   python main.py
   ```
2. Click **Import Data** to load the dataset from the `xray/` directory.
3. Click **Train Data** to train the CNN. Training progress and final test accuracy will be shown in a popup.
4. Click **Test Data** to select an MRI image and get a Tumor/Normal prediction.

## Future Improvements

- Package as a standalone `.exe` (PyInstaller) for easier distribution
- Add a web-based version (e.g., Streamlit) for browser-based access without local setup
- Expand beyond binary classification to tumor subtype/grade classification
- Add model persistence (save/load trained weights instead of retraining each session)
- Replace deprecated `Image.ANTIALIAS` with `Image.LANCZOS` for compatibility with newer Pillow versions
