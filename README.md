# Real_Time_Virtual_Tryon
# Virtual Try-On Application 👕💇♂️

A real-time virtual try-on application that allows users to try different hairstyles and shirts using augmented reality. Leverages semantic segmentation and facial landmarks for precise overlays.

## Features ✨
- **Dual Mode Selection**: Switch between hairstyle and shirt try-on modes
- **Hand Gesture Control**: Navigate UI using hand movements
- **Real-Time Overlay**: Dynamically overlays hairstyles/shirts on webcam feed
- **Perspective Correction**: Adjusts clothing items to match body posture
- **Interactive Carousel**: Scroll through available styles with left/right buttons

## Technical Overview 🛠️

### Core Technologies
- **Clothing Segmentation**: 
  - `SegFormer-B2` model ([mattmdjaga/segformer_b2_clothes](https://huggingface.co/mattmdjaga/segformer_b2_clothes))
  - Semantic segmentation for shirt area detection (class 4)
  
- **Hair & Face Processing**:
  - MediaPipe `ImageSegmenter` with custom TFLite model
  - MediaPipe `FaceMesh` for facial landmarks
  - Adaptive hairstyle scaling based on head dimensions

- **Hand Tracking**:
  - `cvzone.HandTrackingModule` for gesture recognition
  - Contour-based UI interaction system

### Key Processes
**Shirt Try-On Pipeline**:
1. Body segmentation using SegFormer
2. Bounding box detection with perspective warping
3. KDTree-based edge filling for seamless blending
4. Alpha compositing with background extraction

**Hairstyle Try-On Pipeline**:
1. Hair region segmentation using MediaPipe
2. Facial landmark detection (468 points)
3. Perspective transformation matrix calculation
4. Alpha channel blending with warping

## Installation 📦

### Requirements
- Python 3.8+
- Webcam
- CUDA-enabled GPU (recommended)

```bash
# Install dependencies
pip install torch torchvision transformers mediapipe opencv-python cvzone Pillow numpy scipy

# Directory structure setup
mkdir Shirts Hairstyles

Asset Preparation

Download hair_segmenter.tflite (place in root)
Add UI elements in root directory:
button.png (arrow buttons)
shirt_button.png (shirt mode selector)
hair_button.png (hair mode selector)
Usage 🚀

Add try-on items:
Shirt PNGs (with transparency) → /Shirts
Hairstyle PNGs (with transparency) → /Hairstyles
Launch application:
python segformer_final.py

Controls:

✋ Hover over mode buttons (1s) to switch between shirt/hair
👈👉 Use left/right buttons to browse styles
✊ Close hand to select current item
