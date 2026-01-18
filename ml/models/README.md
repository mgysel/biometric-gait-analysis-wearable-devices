# ML Models

This directory contains trained model data for the gait analysis classifier.

## Files

- `X_train.npy`: Training feature vectors (numpy array)
  - Shape: (241, 60) - 241 samples with 60 features each
  - Features are extracted from accelerometer data windows centered around gait peaks
  - Each window contains 20 readings × 3 axes (ax, ay, az)

- `y_train.npy`: Training labels (numpy array)
  - Labels: "u1" (User 1 - Otto) or "u2" (User 2 - Has)

## How These Were Generated

These files were generated from the training notebook (`01_exploration_and_training.ipynb`) using:
1. Raw gait data from `data/raw/user1_otto/` and `data/raw/user2_has/`
2. Bandpass filtering (0.5-20 Hz)
3. Peak detection in accelerometer data
4. Window extraction (20 readings centered on each peak)
5. Feature extraction from windows

## Model

The inference notebook (`02_inference_demo.ipynb`) uses:
- **Algorithm**: K-Nearest Neighbors (KNN)
- **Parameters**: k=4 neighbors
- **Performance**: ~93% cross-validation accuracy (from hyperparameter tuning)

## Usage

Load in Python:
```python
import numpy as np
X_train = np.load('X_train.npy')
y_train = np.load('y_train.npy')
```

## Note

To regenerate these files, run the training notebook and manually save the final X and y arrays using `np.save()`.
