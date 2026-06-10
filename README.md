# Real-Time Crop Disease Detection Bot (Cauliflower & General Crops)

This repository contains the Python Flask backend for the **Real-Time Crop Disease Detection Bot**, an intelligent system powered by Google Gemini Flash to perform rapid visual diagnosis of plant and crop diseases. 

## 🚀 Project Overview

The system is designed to empower farmers and agriculturalists by providing immediate diagnostic feedback on crop health through images. Using advanced Multimodal Generative AI, it detects symptoms of various diseases (specifically targeting Cauliflower pathogens like Downy Mildew, Clubroot, or Black Rot) and suggests remediation methods instantly.

### Key Features
- **AI-Powered Visual Diagnosis**: Leveraging Google Gemini-2.5 Flash for rapid processing.
- **Comprehensive API Structure**: Scalable Flask endpoints for integration with mobile apps or IoT sensors.
- **Automated Reporting**: Generates polished PDF diagnostic reports (via FPDF2) for farm records.
- **CORS-Enabled**: Ready to interact with cross-origin web/mobile clients seamlessly.

---

## 🏗 Architecture & API Reference

### Base URL
`http://your-deployed-url.com` (or `http://localhost:5000` locally)

#### 1. Health Check
Verify server status.
- **Method**: `GET`
- **Endpoint**: `/`
- **Response**: `{"status": "online", "message": "Botany AI Pro Backend is live"}`

#### 2. Crop Disease Prediction
Upload an image for instant diagnostic.
- **Method**: `POST`
- **Endpoint**: `/predict`
- **Payload**: Multipart Form Data containing a file with key `'file'`.
- **Response**:
```json
{
  "status": "success",
  "data": {
    "v": "Cauliflower",
    "d": "Black Rot",
    "t": "Remove infected leaves immediately. Use clean tools and proper crop rotation. Consider copper-based fungicide if spreading persists."
  }
}
```

#### 3. Generate PDF Report
Download a professional PDF summary of the diagnosis.
- **Method**: `POST`
- **Endpoint**: `/generate_pdf`
- **Payload**: `application/json`
```json
{
  "v": "Cauliflower",
  "d": "Black Rot",
  "t": "Treatment steps..."
}
```
- **Response**: `Content-Type: application/pdf` (Binary stream downloads as `Botany_Report_Cauliflower.pdf`)

---

## 🛠 Setup & Local Deployment

### Prerequisites
- Python 3.8+
- A Gemini API Key from [Google AI Studio](https://aistudio.google.com/)

### Installation
1. **Clone Repository** (or navigate to project folder)
2. **Install Dependencies**:
   ```bash
   pip install -r requirements.txt
   ```
3. **Set Environment Variable**:
   On Windows (Command Prompt):
   ```cmd
   set GEMINI_API_KEY=your_api_key_here
   ```
   On macOS/Linux/Powershell:
   ```bash
   export GEMINI_API_KEY=your_api_key_here
   ```
4. **Run the Server**:
   ```bash
   python app.py
   ```
   Server will run on port `5000`.

---

## 🚢 Deployment (Heroku/Render)
Ensure your environment variable `GEMINI_API_KEY` is securely configured in the dashboard of your hosting provider. The repository contains a `Procfile` configured for dynamic scaling via Gunicorn.

```text
web: gunicorn app:app
```
