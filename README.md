# Garud-agri-uav
Garud Drone is an AI-powered unmanned aerial vehicle (UAV) designed to revolutionize crop health monitoring and agricultural intervention. This drone provides real-time, data-driven insights into plant health by detecting nutrient deficiencies, diseases, and weeds, helping farmers make timely and precise interventions.
# Garud Drone

An AI‑Powered Precision Crop Monitoring UAV for real‑time detection of nutrient deficiencies, diseases, and weeds — enabling targeted interventions and higher yields.

---

## Motivation & Problem Statement

Traditional manual spraying of fertilizers and pesticides is:
- **Uneven**: causes up to 15–20% yield loss due to under‑ or over‑treatment  
- **Hazardous**: exposes workers to toxic chemicals  
- **Inefficient**: lacks continuous monitoring; issues often go undetected until severe  

No commercial agricultural drone in India integrates onboard AI for fully automated crop scouting and spraying. **Garud Drone** fills this gap by delivering an end‑to‑end aerial platform for precision crop care.

---

## Key Features

- **Onboard AI Inference**  
  Runs on a Raspberry Pi 5 companion computer for true offline operation.

- **Nutrient & Disease Detection**  
  Lightweight CNN (≈0.5 M parameters) classifies N, P, K deficiencies and common diseases (leaf spot, blight) with ~92% lab accuracy.

- **Weed Detection**  
  YOLOv8s object detector (mAP@0.5 ≈ 0.77) segments weeds vs. crops in real time.

- **Autonomous Flight Controls**  
  Pixhawk 2.4.8 running ArduPilot handles stabilization, geofencing, failsafes, and MAVLink telemetry at 921600 baud.

- **Live Dashboard**  
  Streamlit‑based interface shows annotated video feed and time‑series charts of detections.

## Software & AI Pipeline

1. **ArduPilot Trigger**  
   A Lua script on Pixhawk emits a MAVLink “armed” event → Pi listener script launches vision pipeline.

2. **Frame Capture & Preprocessing**  
   − Acquire 1920×1200 frames via CSI → resize to 224×224, normalize to [0,1].

3. **CNN Inference**  
   − Three Conv‑MaxPool blocks (32→64→128 filters) + Dense(512) + Dropout → Softmax(5 classes).

4. **YOLOv8 Inference**  
   − Process 640×640 frames to detect “weed” vs. “crop,” output bounding boxes + confidence.

5. **Dashboard & Logging**  
   − Streamlit app overlays detections on video, logs counts over time, and provides download links.

---

## Field Test Results

- **Flight Performance**  
  − Stable 21 min flights carrying full payload  
  − Smooth hover and manual maneuvers  

- **AI Accuracy**  
  − Weed detection: ~80% in real conditions  
  − Nutrient/disease classification: ~85%  

- **Safety & Reliability**  
  − Geofence and low‑battery auto‑landing tested successfully  
  − No structural failures; vibration dampening effective  



