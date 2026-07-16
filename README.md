# SENTINEL – AI Video Surveillance & Behavioral Analysis System

SENTINEL is an AI-powered video surveillance system. The system utilizes YOLOv8, computer vision, and behavioral analysis techniques to automate surveillance tasks including traffic monitoring, weapon detection, and theft detection through a user-friendly Gradio interface.

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

### Traffic Monitoring
- Vehicle detection
- Vehicle counting
- Class-wise statistics

### Speed Estimation
- Track vehicle movement
- Estimate vehicle speed
- Overspeed alerts

### Weapon Detection
- Custom YOLOv8 model support
- Real-time threat alerts

### Theft Detection
- Person tracking
- Behavior classification
- Theft alert generation

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
