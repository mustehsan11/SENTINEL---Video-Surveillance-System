# SENTINEL – AI Video Surveillance & Behavioral Analysis System

SENTINEL is an AI-powered video surveillance system. The system utilizes YOLOv8, computer vision, and behavioral analysis techniques to automate surveillance tasks including traffic monitoring, weapon detection, and theft detection through a user-friendly Gradio interface.

<img width="1597" height="718" alt="image" src="https://github.com/user-attachments/assets/4ade50f2-4e97-42cf-b553-340afd927f1e" />

## Features

- 🚗 Real-time Vehicle Detection & Counting
  - Detects and counts cars, motorcycles, buses, and trucks.
  - Uses YOLOv8 with multi-object tracking.

- ⚡ Vehicle Speed Estimation
  - Estimates vehicle speed from video.
  - Generates alerts for vehicles exceeding 90 km/h.

- 🔫 Weapon Detection
  - Supports custom-trained YOLOv8 weapon detection models.
  - Displays real-time critical alerts upon weapon detection.

- 🛒 Behavioral Theft Detection
  - Detects suspicious activities such as:
    - Loitering
    - Running
    - Item concealment
  - Uses a Finite State Machine (FSM) combined with object tracking to reduce false positives.

- 📊 Data Analysis & Reporting
  - Automatic preprocessing pipeline
  - Interactive charts and visualizations
  - HTML report generation
  - Annotated output videos

---

## Technologies Used

- Python
- YOLOv8 (Ultralytics)
- OpenCV
- Gradio
- Pandas
- NumPy
- Matplotlib
- Google Colab

---

## System Workflow

1. Upload a surveillance video.
2. Select the desired analysis module.
3. Process the video using YOLOv8 detection and tracking.
4. Generate:
   - Annotated output video
   - Detection statistics
   - Analysis charts
   - HTML report

---

## Project Modules

### 1. Traffic Monitoring
Detections are filtered to target COCO classes: car (2), motorcycle (3), bus (5), and truck (7). YOLOv8's BoT-SORT tracker (persist=True) assigns consistent IDs across frames. A vehicle is counted once when its track ID exits the speed zone for the first time. A speed outlier filter (speed > 200 km/h) discards physically impossible estimates caused by tracker ID flickers.

<img width="714" height="403" alt="image" src="https://github.com/user-attachments/assets/af2630dd-e83a-4461-868a-dbf1d9df07d0" />



### 2. Speed Estimation

A virtual speed zone is defined between 55% and 85% of frame height. The entry frame of each tracked vehicle is recorded on zone entry. On zone exit, elapsed time (seconds) = frames_elapsed / FPS. Speed (km/h) = (zone_distance_m / time_s) × 3.6. Vehicles exceeding 90 km/h are labelled SPEEDING! in red; compliant vehicles are labelled OK in green.

<img width="692" height="431" alt="image" src="https://github.com/user-attachments/assets/c7be6fa2-127c-46da-86eb-0c57e4ecf052" />

### Traffic & Speed Results

<img width="713" height="455" alt="image" src="https://github.com/user-attachments/assets/0a83f35d-0005-42e2-b1a4-2a4faa20a001" />


### 3. Weapon Detection

A user-supplied custom YOLOv8 weapon model is loaded at runtime. Each frame is processed by both the core model (person detection, class 0, confidence ≥ 0.6) and the weapon model (confidence ≥ 0.5). When a weapon is detected, a semi-transparent red overlay banner is rendered across the top of the frame with the label CRITICAL ALERT: WEAPON DETECTED.

<img width="714" height="396" alt="image" src="https://github.com/user-attachments/assets/e89a27d3-8dbc-4fb9-a43c-17c6857ef1fa" />

### Weapon Detection Results
<img width="713" height="519" alt="image" src="https://github.com/user-attachments/assets/b33c6690-0b0e-481b-9a55-8de893b9894b" />

### 4. Theft Detection

The theft detector implements a three-state **Finite State Machine (FSM)** for behavioral classification. Each tracked person maintains a **30-frame trajectory history**. The Euclidean displacement between the **15th-to-last** and the current centroid position determines the state:

| State | Trigger Condition | Box Colour | Risk Level |
|-------|-------------------|------------|------------|
| **LOITERING** | Displacement < 15 px / 15 frames | Cyan | Medium |
| **NORMAL** | 15 px ≤ displacement ≤ 60 px | Green | Low |
| **RUNNING** | Displacement > 60 px / 15 frames | Magenta | High |

The theft alarm fires only when:

- A previously handled item has been missing for **more than 20 consecutive frames**, **AND**
- The person who last handled that item is in the **RUNNING** state.

<img width="709" height="363" alt="image" src="https://github.com/user-attachments/assets/68f9bb91-1ad3-42a2-b225-8ec3f8294522" />

### Theft Detection Results
<img width="710" height="495" alt="image" src="https://github.com/user-attachments/assets/d2878747-7d25-4856-bfc8-aa08a9a57dfb" />



---

## Results

The project achieved:

- Vehicle counting accuracy of **92.3%**
- Speed estimation error of approximately **±7.8 km/h**
- Functional behavioral theft detection with reduced false positives
- Interactive Gradio dashboard with automated reporting

---

## Future Improvements

- Multi-camera surveillance support
- Homography-based speed calibration
- Deep learning action recognition models
- Person Re-Identification (ReID)
- Improved weapon detection through larger datasets
- Exportable PDF incident reports

---

## License

This project was developed for academic purposes as part of the **CT-356 Data Mining Complex Computing Problem (CCP)** at **NED University of Engineering & Technology**.
