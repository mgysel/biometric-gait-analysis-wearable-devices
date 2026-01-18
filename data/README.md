# Gait Analysis Data

This directory contains all sensor data collected for the gait analysis project.

## Directory Structure

```
data/
├── raw/
│   ├── user1_otto/          # User 1 (Otto) gait data
│   ├── user2_has/           # User 2 (Has) gait data
│   ├── user3_mum/           # User 3 (Mum) gait data
│   └── other_sessions/      # Earlier test sessions and packet data
```

## Data Format

Each user's directory contains multiple sessions (numbered 1-9), with each session containing:

- `ax_arrayN.txt` - X-axis accelerometer readings
- `ay_arrayN.txt` - Y-axis accelerometer readings
- `az_arrayN.txt` - Z-axis accelerometer readings
- `gx_arrayN.txt` - X-axis gyroscope readings
- `gy_arrayN.txt` - Y-axis gyroscope readings
- `gz_arrayN.txt` - Z-axis gyroscope readings
- `total_arrayN.txt` or `totalsqr_arrayN.txt` - Combined magnitude

Where N is the session number (1-9).

## Data Collection

- **Sampling Rate**: 50 Hz (one reading every 20ms)
- **Hardware**: TI SensorTag with MPU-9250 IMU
- **Protocol**: CoAP over 6LoWPAN
- **Collection Method**: Sensors attached to subjects while walking

## Users

- **User 1 (Otto)**: Primary test subject - used for training
- **User 2 (Has)**: Secondary test subject - used for training
- **User 3 (Mum)**: Additional test subject - available for validation

## Usage

The ML training notebook loads this data, applies filtering, and extracts features for gait classification.

See `ml/notebooks/01_exploration_and_training.ipynb` for data processing pipeline.
