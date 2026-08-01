---markdown
# 🌲 Intelligent Poaching Detection and Response System

An AI-powered computer vision system designed to assist forest authorities in detecting potential poaching-related activity from images and videos.

The system uses **YOLOv8** for object detection, **FastAPI** for the backend API, **MongoDB** for storing detection information, and **React (Vite)** for the monitoring dashboard.

---

## 📌 Overview

Illegal poaching is difficult to monitor continuously across large forest areas. This project aims to support forest monitoring by automatically analyzing uploaded images and videos using an object detection model.

The detection pipeline identifies objects of interest, records their confidence scores and detection information, and makes the results available through a web-based monitoring application.

### System Flow

---text
Image / Video
      ↓
YOLOv8 Object Detection
      ↓
Detected Objects + Confidence Scores
      ↓
FastAPI Backend
      ↓
MongoDB
      ↓
React Monitoring Dashboard
      ↓
Detection / Alert Information
---

---

## ✨ Key Features

* 🎯 YOLOv8-based object detection
* 🎥 Image and video analysis
* 🧠 Custom object-detection model integration
* ⚡ FastAPI backend
* 🗄️ MongoDB database integration
* 🖥️ React + Vite monitoring dashboard
* 🔐 JWT-based authentication
* 📧 Email-based alert functionality
* 📊 Detection confidence and threat information
* 📁 Storage and retrieval of detection results

---

## 🧠 Machine Learning

The project uses **Ultralytics YOLOv8** for object detection.

A custom-trained model can be loaded by the detection pipeline for identifying domain-specific objects from uploaded media.

The detection pipeline works with:

* Bounding boxes
* Class labels
* Confidence scores
* Processed image/video frames

The project architecture includes domain-specific detection classes such as:

* `poacher`
* `weapon`
* `animal`
* `ranger`

---

## 🏗️ System Architecture

```text
                    ┌──────────────────┐
                    │   Image / Video  │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │     YOLOv8       │
                    │ Object Detection │
                    └────────┬─────────┘
                             │
                  Detection Results
                             │
                             ▼
                    ┌──────────────────┐
                    │  FastAPI Backend │
                    └────────┬─────────┘
                             │
                ┌────────────┴────────────┐
                │                         │
                ▼                         ▼
        ┌──────────────┐          ┌──────────────┐
        │   MongoDB    │          │ Alert System │
        └──────┬───────┘          └──────────────┘
               │
               ▼
        ┌──────────────────┐
        │ React Dashboard  │
        └──────────────────┘
```

---

## 🛠️ Technology Stack

### Machine Learning & Computer Vision

* Python
* Ultralytics YOLOv8
* OpenCV

### Backend

* FastAPI
* Python
* MongoDB
* Motor / MongoDB integration
* JWT authentication

### Frontend

* React
* Vite
* JavaScript
* Tailwind CSS

### Development Tools

* Git
* GitHub
* VS Code

---

## 📂 Project Structure

```text
poaching-detection-system/
│
├── backend/
│   ├── api/
│   ├── core/
│   ├── db/
│   ├── schemas/
│   ├── services/
│   ├── main.py
│   ├── requirements.txt
│   └── .env.example
│
├── frontend/
│   ├── public/
│   ├── src/
│   ├── package.json
│   └── vite.config.js
│
├── model/
│   ├── detector.py
│   └── __init__.py
│
├── .gitignore
├── README.md
└── run.sh
```

---

# 🚀 Getting Started

## Prerequisites

Make sure the following are installed:

* Python 3.10+
* Node.js 18+
* MongoDB running locally or a reachable MongoDB URI

---

## 1. Clone the Repository

```bash
git clone https://github.com/Sravyasree-080905/poaching-detection-system.git
cd poaching-detection-system
```

---

## 2. Configure Environment Variables

The backend provides an environment template:

```text
backend/.env.example
```

Create your local environment file from the template.

### Windows

```powershell
copy backend\.env.example backend\.env
```

### Linux / macOS

```bash
cp backend/.env.example backend/.env
```

Configure the required values, including:

```text
MONGO_URI
JWT_SECRET
```

Additional configuration options are documented in `backend/.env.example`.

> ⚠️ Never commit your actual `.env` file or credentials to GitHub.

---

## 3. Install Backend Dependencies

Navigate to the backend directory:

```bash
cd backend
```

Create a virtual environment:

```bash
python -m venv .venv
```

### Windows

```powershell
.venv\Scripts\activate
```

### Linux / macOS

```bash
source .venv/bin/activate
```

Install the required Python packages:

```bash
pip install -r requirements.txt
```

---

## 4. Install Frontend Dependencies

Open a new terminal and navigate to the frontend:

```bash
cd frontend
```

Install the required Node.js packages:

```bash
npm install
```

---

# ▶️ Running the Application

## Option 1: Unified Runner

The repository contains a `run.sh` script intended to start the backend and frontend together.

From the project root:

```bash
./run.sh
```

> On Windows, the individual backend and frontend commands below can be used if the shell script is not directly supported.

---

## Option 2: Run Backend and Frontend Separately

### Start the Backend

Navigate to:

```bash
cd backend
```

Activate the virtual environment and start FastAPI:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend API will be available at:

```text
http://localhost:8000
```

FastAPI Swagger documentation:

```text
http://localhost:8000/docs
```

---

### Start the Frontend

In another terminal:

```bash
cd frontend
npm run dev
```

The React application will normally be available at:

```text
http://localhost:5173
```

---

# ⚙️ Configuration

Backend configuration is managed through:

```text
backend/.env
```

The available configuration variables are documented in:

```text
backend/.env.example
```

Common configuration includes:

```text
MONGO_URI
DATABASE_NAME
JWT_SECRET
BACKEND_CORS_ORIGINS
```

### MongoDB

The application requires MongoDB for storing application and detection information.

A local MongoDB instance can be used, or the application can be configured to connect to a remote MongoDB deployment through `MONGO_URI`.

---

# 🤖 Detection Pipeline

The detection workflow can be summarized as:

```text
1. User uploads image/video
              ↓
2. Backend receives the media
              ↓
3. YOLOv8 model processes the media
              ↓
4. Objects are detected
              ↓
5. Bounding boxes and confidence scores are generated
              ↓
6. Detection information is stored
              ↓
7. Results are displayed through the frontend
```

For video processing, frames are analyzed by the detection service and relevant detection information is recorded.

---

# 📊 Detection Information

For each detection, the system can work with information such as:

* Detected class
* Confidence score
* Bounding box information
* Associated video/image
* Detection timestamp
* Threat-related information

This information is used by the backend and frontend to provide a monitoring view of detected activity.

---

# 🔐 Authentication & Security

The backend includes authentication functionality using JWT-based authentication.

Sensitive configuration such as:

* Database credentials
* Secret keys
* Email credentials

should be stored using environment variables rather than being hard-coded in source code.

The repository provides:

```text
backend/.env.example
```

as a configuration template.

---

# 📧 Alert System

The application includes an email-based alert mechanism for relevant detection events.

Alert information can include details such as:

* Detected threat/object
* Confidence score
* Threat level
* Detection information
* Supporting image/frame

The actual email configuration should be provided through environment variables.

---

# 👩‍💻 My Contribution

This project was developed collaboratively as part of an AI/ML internship.

My primary contribution was focused on the **AI/ML and computer vision components**, including:

* Dataset preparation and preprocessing
* Working with object-detection datasets
* YOLOv8 model training
* Model inference and evaluation
* Integration of the trained detection model with the application
* Testing the detection pipeline

The overall application was developed as a team involving machine learning, backend, and frontend components.

---

# 🔮 Future Enhancements

Potential improvements identified during development include:

### 🎥 Live Camera Monitoring

Support for live RTSP/HLS camera streams for continuous forest surveillance.

### ⚡ Real-Time Dashboard Updates

WebSocket or Server-Sent Events integration for pushing detection updates to the frontend immediately.

### 📩 Alert Throttling

Aggregate multiple detections from the same video instead of generating excessive individual alerts.

### 🧠 Improved Spatial Reasoning

Use relationships between bounding boxes and detected objects to improve threat classification.

### 🔐 Enhanced Role-Based Access

Improve authorization for administrative settings and sensitive system operations.

### 📋 Incident Management

Add structured incident-resolution workflows and investigation notes for detected events.

---

# 🧪 Troubleshooting

## MongoDB Connection Error

Make sure MongoDB is running and that the `MONGO_URI` in `backend/.env` is correct.

For MongoDB Atlas, verify that:

* The connection string is correct.
* The database credentials are valid.
* Your IP address is allowed by the Atlas network configuration.

---

## CORS Error

If the frontend cannot communicate with the backend, verify the allowed frontend origin in:

```text
backend/.env
```

For local development, the frontend commonly runs on:

```text
http://localhost:5173
```

---

## FastAPI API Documentation

The interactive API documentation can be accessed at:

```text
http://localhost:8000/docs
```

This can also be used as a quick smoke test to verify that the backend is running.

---

# 📌 Disclaimer

This project was developed as an academic/internship project to demonstrate the application of computer vision, machine learning, backend development, and frontend technologies for wildlife protection.

It is intended as a decision-support system and should not replace professional field investigation or law-enforcement procedures.

---

# 📄 License

This project is available under the license included in this repository.

---

### After pasting

Just do:

**GitHub → `README.md` → ✏️ Edit → Ctrl+A → paste → Commit changes.**

Don't make any other changes to the repository right now. Once this is saved, **we'll move directly to the Seanergy preparation**, especially your **Poaching project explanation + likely AI/ML technical questions + HR questions**, because the drive is on August 3–4. 🚀
```
