# Gait Analysis IoT Solution

A complete IoT system for collecting and analyzing human gait patterns using wearable sensors and machine learning for person identification.

📄 **[Full Project Report](docs/COMP6733_Final_Report.pdf)**

## Project Overview

This project combines:
- **IoT Sensors**: TI SensorTag with MPU-9250 IMU (accelerometer + gyroscope)
- **Communication**: CoAP over 6LoWPAN for low-power wireless data collection
- **Machine Learning**: KNN classifier for gait-based person identification

The system can identify individuals based on their unique walking patterns with ~93% accuracy.

## Repository Structure

```
Gait-Analysis-IoT-Solution/
├── iot/                    # IoT/Embedded systems code
│   ├── firmware/           # Contiki OS firmware for sensor nodes
│   └── data-collection/    # Python CoAP client for data collection
│
├── ml/                     # Machine Learning components
│   ├── notebooks/          # Jupyter notebooks for training and inference
│   ├── models/             # Trained model data (X_train.npy, y_train.npy)
│   └── src/                # Reusable ML code (future)
│
├── data/                   # Sensor data organized by user
│   └── raw/                # Raw accelerometer/gyroscope readings
│
├── scripts/                # Utility scripts
│   └── data_conversion/    # Data format conversion tools
│
├── docs/                   # Documentation
│
└── archive/                # Old/experimental code
```

## Quick Start

### Machine Learning

1. **Training:**
   ```bash
   cd ml/notebooks
   jupyter notebook 01_exploration_and_training.ipynb
   ```
   - Loads raw gait data
   - Applies bandpass filtering (0.5-20 Hz)
   - Detects gait peaks
   - Extracts features from windows
   - Trains and compares classifiers (SVM, KNN, Random Forest, etc.)

2. **Inference:**
   ```bash
   jupyter notebook 02_inference_demo.ipynb
   ```
   - Uses pre-trained KNN model (k=4)
   - Classifies new gait samples
   - Returns user identification

## System Architecture

1. **Data Collection Layer**
   - TI SensorTag with MPU-9250 IMU collects accelerometer/gyroscope data at 50 Hz
   - Firmware (`iot/firmware/sensor-node/send.c`) built on Contiki OS
   - CoAP protocol over 6LoWPAN for low-power wireless communication
   - Python client (`iot/data-collection/observe.py`) collects and stores data

2. **Data Processing Layer**
   - Bandpass filtering (0.5-20 Hz) to remove noise
   - Peak detection to identify gait cycles
   - Feature extraction from windows around peaks

3. **Classification Layer**
   - K-Nearest Neighbors (k=4) classifier
   - Trained on labeled gait data from multiple users
   - Achieves ~93% accuracy in cross-validation

> **Note**: The IoT hardware setup requires TI SensorTag, Contiki OS development environment, and a 6LoWPAN border router. The collected data is already available in `data/raw/` for ML experimentation.

## Data Format

Sensor readings are stored as JSON arrays in text files:
- `ax_array.txt`, `ay_array.txt`, `az_array.txt` - Accelerometer (3 axes)
- `gx_array.txt`, `gy_array.txt`, `gz_array.txt` - Gyroscope (3 axes)
- `total_array.txt` - Combined magnitude

Each reading is timestamped at 20ms intervals (50 Hz).

## Requirements

### Machine Learning (to run notebooks)
- Python 3.x
- NumPy
- SciPy
- scikit-learn
- matplotlib
- pandas
- Jupyter

## Project Info

Group project for COMP6733 (IoT course)

📄 **[Full Project Report](docs/COMP6733_Final_Report.pdf)** - Detailed documentation of system design, implementation, and evaluation
