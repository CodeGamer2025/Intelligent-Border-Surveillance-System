# 🦚 Project MORPANKH: Intelligent Border Surveillance System

**An Autonomous, Multi-Modal AI Defense Architecture for Real-Time Threat Detection**

![Python](https://img.shields.io/badge/Python-3.12-blue?style=flat-square&logo=python)
![TensorFlow](https://img.shields.io/badge/TensorFlow-CNN-orange?style=flat-square&logo=tensorflow)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer%20Vision-green?style=flat-square&logo=opencv)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Random%20Forest-yellow?style=flat-square&logo=scikit-learn)

---

## 👁️ The "Morpankh" Philosophy: The Ultimate Shield
According to the epic Mahabharata, when a desperate Ashwatthama unleashed a devastating, stealthy weapon (*Brahmashirsha astra*) aimed at the unborn child in Uttara's womb, Lord Krishna immediately sensed the invisible danger. With his divine vision and protective grace—universally symbolized by his *Morpankh* (peacock feather)—he formed an impenetrable, microscopic shield around the womb, neutralizing the hidden threat before it could strike.

**Project MORPANKH** derives its core engineering philosophy from this legendary act of ultimate protection. Just as the divine shield neutralized an unseen danger, this Intelligent Border Surveillance System acts as a proactive protective barrier for the nation. By fusing an all-seeing Vision AI with highly sensitive seismic ground sensors, the system is designed to detect stealthy, hidden threats attempting to breach the border. It autonomously triggers defensive protocols and logs evidence—safeguarding the perimeter before harm can cross it.

---

## 📖 Table of Contents
1. [Project Abstract](#-project-abstract)
2. [Key Features](#-key-features)
3. [System Architecture](#-system-architecture)
4. [Technical Stack](#-technical-stack)
5. [Repository Structure](#-repository-structure)
6. [Execution & Usage](#-execution--usage)
7. [Future Scope](#-future-scope)
8. [Author](#-author)

---

## 🎯 Project Abstract
Traditional border security relies heavily on manual human monitoring and standalone visual cameras, which suffer from human fatigue, low-visibility errors, and high false-alarm rates triggered by environmental factors. 

**MORPANKH** is an automated, multi-modal AI defense net. It drastically reduces false positives through **Data Fusion**—correlating real-time visual anomaly detection (via a Convolutional Neural Network) with physical ground-vibration analysis (via a Random Forest Classifier). When a visual threat is verified by seismic activity, the system autonomously triggers hardware alarms and securely logs timestamped photographic evidence without requiring human intervention.

---

## ✨ Key Features
* **Multi-Modal Data Fusion:** Cross-references visual frame data with physical ground-sensor telemetry to eliminate visual "ghost" false alarms (e.g., shadows, animals).
* **High-Speed Vision AI:** Downsamples HD video feeds to `64x64` pixels to achieve true real-time processing without severe latency or reliance on massive external GPUs.
* **14-Class Threat Recognition:** Trained on the UCF Crime dataset to detect specific events including *Shooting, Fighting, Explosion, Arson, Assault,* and *Burglary*.
* **Automated Evidence Logging:** Captures the exact frame of a breach, permanently embeds the system timestamp/confidence score, and saves it locally.
* **Hardware Alarm Trigger:** Automatically executes a 1000Hz acoustic alarm (`winsound`) upon a verified >70% confidence threat, complete with a 5-second cooldown to prevent log spamming.
* **Predictive Deployment Mapping:** Utilizes EDA on ACLED and Border Crossing data to map geographical "Smart Zones" for optimal camera/sensor placement.

---

## 🧠 System Architecture

The project is divided into four integrated engineering phases:

### Phase 1: Risk Zone EDA (The Strategy)
Analyzed ACLED and Border Crossing Entry datasets to find geographical conflict clusters. Engineered features to visualize timeline trends using Pandas and Seaborn, dictating where the system should be theoretically deployed.

### Phase 2: Vision AI (The Eyes)
A custom Convolutional Neural Network (CNN) built with Keras.
* **Input:** Real-time video feeds (`.mp4`, `.webm`).
* **Processing:** Frames are extracted via OpenCV, resized to `(64, 64, 3)`, and normalized.
* **Output:** A classification probability across 14 categories. A prediction buffer (`deque`) smooths transient frame flickering.

### Phase 3: Sensor AI (The Nerves)
A Random Forest Classifier trained on the Human Activity Recognition (HAR) dataset.
* **Processing:** Extracts feature data from X, Y, and Z-axis vibration telemetry to distinguish ambient environmental noise from specific human movement signatures.

### Phase 4: Integration & Response Protocol
The final execution loop that acts as the Command Center.
* **Logic:** `IF` Visual Threat > 70% `AND` Sensor registers anomaly `THEN` execute Response.
* **Response:** Trigger localized alarm → Capture Frame → Apply Timestamp Overlay → Save to `Threat_Logs/`.

---

## 🛠️ Technical Stack

| Category | Tools & Libraries |
| :--- | :--- |
| **Core Language** | Python 3.12 |
| **Deep Learning (Vision)** | TensorFlow, Keras |
| **Machine Learning (Sensor)** | Scikit-Learn |
| **Computer Vision** | OpenCV (`cv2`) |
| **Data Analytics & EDA** | Pandas, NumPy, Matplotlib, Seaborn |
| **System Integrations** | `winsound`, `joblib`, `datetime`, `os`, `collections.deque` |

---

## 📁 Repository Structure

```text
Datasets/                              # Core datasets (ACLED, UCF Crime, HAR)
Threat_Logs/                           # Auto-populated with timestamped .jpg evidence
1_Risk_Zone_EDA.ipynb                  # Geolocation data analysis
2_Surveillance_Video_Processing.ipynb  # CNN training & live inference loop
3_Sensor_Data_Analysis.ipynb           # Random Forest training
best_border_defense_model.keras        # Trained Vision AI weights
sensor_defense_model.pkl               # Trained Sensor AI weights
sensor_label_encoder.pkl               # Label encoder for sensor data
Raw Media Files                        # .mp4 and .webm test videos