# 🅿️ Smart Parking — AI-Powered Parking Monitoring System

### Real-Time Parking Occupancy Detection Using Deep Learning and Computer Vision

**Author:** Leroy Makita Loubaki  
**Institution:** ESIGELEC — DARIA Engineering Program  
**Project Type:** Personal Project — Computer Vision & Artificial Intelligence

---

## 📖 1. Project Overview

This project focuses on the development of an intelligent parking monitoring system capable of identifying available and occupied parking spaces from video footage.

The system combines **Deep Learning, Computer Vision, and Image Processing** to analyze parking occupancy and display the results through a real-time visual dashboard.

The project was developed in three complementary phases:

1. **Parking Space Classification:** Training a ResNet-50 classifier using the PKLot dataset.
2. **Vehicle Detection:** Detecting and counting vehicles using a pre-trained YOLOv8 model.
3. **Real-Time Monitoring:** Developing a video-processing pipeline to classify predefined parking spaces and display occupancy statistics.

## 🎯 2. Project Objectives

- Automatically classify parking spaces as available or occupied.
- Explore transfer learning for parking occupancy classification.
- Detect and count vehicles using object detection.
- Process parking video footage.
- Develop an interactive parking-space selection tool.
- Visualize occupancy information in real time.

## 🛠️ 3. Technologies Used

| Category | Technologies |
|---|---|
| Programming Language | Python 3.14 |
| Deep Learning | PyTorch 2.9 |
| Image Processing | OpenCV 4.13 |
| Classification Model | ResNet-50 |
| Object Detection | YOLOv8n |
| Dataset | PKLot |
| Development Environment | VS Code, Jupyter Notebook |
| Hardware | Intel CPU, Windows 10 |

## 📊 4. Dataset — PKLot

The project uses the **PKLot dataset**, containing annotated parking lot images.

The dataset is provided in COCO detection format, with bounding-box annotations identifying individual parking spaces.

Two classes are considered:

- `space-empty`: Available parking space.
- `space-occupied`: Occupied parking space.

Individual parking-space images were extracted from the original images using their annotated bounding boxes.

### Dataset Distribution

| Split | Available | Occupied | Total |
|---|---:|---:|---:|
| Training | 265,908 | 231,948 | 497,856 |
| Validation | 73,629 | 69,687 | 143,316 |
| Testing | 36,584 | 34,100 | 70,684 |
| **Total** | **376,121** | **335,735** | **711,856** |

The extracted dataset contains approximately 53% available spaces and 47% occupied spaces.

## 🧠 5. Phase 1 — Parking Space Classification with ResNet-50

### Model Architecture

ResNet-50 is a convolutional neural network originally trained on the ImageNet dataset.

Transfer learning was used to adapt the model to binary parking occupancy classification.

The implementation involved:

1. Loading pre-trained ImageNet weights.
2. Freezing the backbone parameters.
3. Replacing the final classification layer.
4. Training the new classification layer for two output classes.

The final layer was configured as:

`Linear(2048, 2)`

Only the 4,098 parameters of the new classification layer were trained.

### Training Configuration

| Parameter | Value |
|---|---|
| Input Image Size | 224 × 224 pixels |
| Batch Size | 32 |
| Optimizer | Adam |
| Learning Rate | 0.001 |
| Scheduler | StepLR |
| Scheduler Step Size | 3 |
| Scheduler Gamma | 0.1 |
| Epochs | 5 |
| Loss Function | CrossEntropyLoss |

### Data Augmentation

To improve training robustness, the following transformations were applied to the training data:

- Random horizontal flipping
- Random rotation (±10°)
- Color jitter (brightness, contrast, saturation)
- ImageNet normalization

### Classification Results

**Approximately 99% accuracy on a sample of 100 test images.**

This preliminary result demonstrates promising classification performance using transfer learning.

However, it does not represent a full evaluation of the entire 70,684-image test set. A more comprehensive evaluation remains necessary.

## 🚗 6. Phase 2 — Vehicle Detection with YOLOv8

The second phase explores vehicle detection and counting using a pre-trained YOLOv8n model.

The model was loaded with pre-trained COCO weights without additional fine-tuning.

### Detection Configuration

- Model: `yolov8n.pt`
- Vehicle Classes: Car, Bus, Truck
- Confidence Threshold: 0.30
- Framework: Ultralytics YOLOv8

### Vehicle Counting

The number of vehicles is obtained from the detected bounding boxes.

To reduce frame-to-frame fluctuations, a moving average over the previous 10 frames was implemented.

### Limitations

The pre-trained model performs better on conventional horizontal or oblique surveillance views than on aerial parking footage.

Adapting YOLOv8 to aerial imagery through dedicated fine-tuning is identified as a future improvement.

## 📹 7. Phase 3 — Real-Time Parking Monitoring Dashboard

The final phase implements parking occupancy monitoring through video processing and ResNet-50 classification.

### Processing Pipeline

**Video Input → Frame Extraction → Parking Space Cropping → ResNet-50 Classification → Dashboard Visualization**

### Interactive Parking Space Selection

An interactive OpenCV tool was developed to define parking-space regions manually using mouse clicks.

A total of **42 parking spaces** were selected in the test video.

### Real-Time Classification

For each video frame:

1. Extract each predefined parking-space region.
2. Apply image preprocessing.
3. Run inference using the trained ResNet-50 classifier.
4. Classify the region as available or occupied.
5. Draw a colored rectangle around the parking space.
6. Update occupancy counters.

### Visualization

- 🟢 **Green:** Available parking space
- 🔴 **Red:** Occupied parking space

### Demonstration Results

| Metric | Value |
|---|---:|
| Monitored Parking Spaces | 42 |
| Available Spaces | 25 |
| Occupied Spaces | 17 |

These values correspond to the demonstration shown in the project report.

## 📈 8. Key Results

The project demonstrates:

- A ResNet-50 classification pipeline trained using transfer learning.
- Approximately 99% accuracy on a limited sample of 100 test images.
- Vehicle detection and counting using pre-trained YOLOv8.
- A manually configured 42-space parking monitoring system.
- A video dashboard displaying the number of available and occupied spaces.

## ⚠️ 9. Current Limitations

Several limitations were identified:

- The reported classification accuracy was evaluated on a limited sample.
- YOLOv8 was not fine-tuned for aerial parking imagery.
- Parking-space regions are defined manually.
- A comprehensive evaluation of real-time processing performance remains to be documented.

## 🚀 10. Future Improvements

Potential improvements include:

- Training and evaluating ResNet-50 on GPU using Google Colab.
- Evaluating the complete PKLot test set.
- Fine-tuning YOLOv8 for aerial vehicle detection.
- Automatically identifying parking spaces through image segmentation.
- Deploying the solution on a Raspberry Pi 4 for embedded monitoring.

## 📚 11. Project Documentation

The technical project report describes:

- Dataset preparation and crop extraction
- ResNet-50 architecture and training
- YOLOv8 vehicle detection
- Real-time monitoring implementation
- Experimental results
- Source code excerpts

Additional source files and demonstration images will be organized in this repository.

## 👨‍💻 12. About the Author

**Leroy Makita Loubaki**

Engineering student at **ESIGELEC**, specializing in **DARIA — Digitalization, Automation, Robotics and Artificial Intelligence for Industry**.


Interested in Artificial Intelligence, Computer Vision, Robotics, Industrial Automation and Intelligent Systems.

### Connect With Me

[LinkedIn — Leroy Makita Loubaki](https://www.linkedin.com/in/leroy-makita-loubaki-a78792290/)

---

*Personal engineering project — June 2026.*
