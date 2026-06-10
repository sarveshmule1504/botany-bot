# 🌾 Botany-Bot: AI-Powered Crop Disease Detection

[![Python](https://img.shields.io/badge/Language-Python%203.8%2B-blue?style=flat-square&logo=python)](https://www.python.org/)
[![Flask](https://img.shields.io/badge/Framework-Flask-lightgrey?style=flat-square&logo=flask)](https://flask.palletsprojects.com/)
[![Google Gemini](https://img.shields.io/badge/AI-Google%20Gemini%202.5%20Flash-orange?style=flat-square&logo=google)](https://ai.google.dev/)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

## 📋 Overview

Botany-Bot is an intelligent **Real-Time Crop Disease Detection System** powered by Google Gemini 2.5 Flash. It empowers farmers and agriculturalists with **instant diagnostic feedback** on crop health through AI-powered visual analysis of plant images.

Whether you're managing cauliflower fields, general crops, or implementing IoT-based monitoring systems, Botany-Bot provides:
- ⚡ **Rapid diagnosis** using advanced multimodal generative AI
- 📄 **Professional PDF reports** for farm records
- 🔗 **Scalable API** ready for mobile and IoT integration
- 🌐 **CORS-enabled** for seamless cross-origin requests

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 🤖 **AI-Powered Diagnosis** | Google Gemini 2.5 Flash for rapid and accurate disease detection |
| 📸 **Visual Analysis** | Upload crop images for instant diagnostic results |
| 📊 **Comprehensive Reports** | Auto-generated PDF reports with treatment recommendations |
| 🔄 **RESTful API** | Easy-to-integrate endpoints for mobile apps and IoT sensors |
| 🛡️ **CORS Support** | Ready for cross-origin web and mobile client integration |
| 🚀 **Production-Ready** | Gunicorn + Procfile configured for cloud deployment |
| 📝 **Actionable Insights** | Treatment recommendations and preventive measures |

## 🛠️ Tech Stack

- **Backend Framework:** Python Flask
- **AI Engine:** Google Gemini 2.5 Flash API
- **Report Generation:** FPDF2
- **Server:** Gunicorn (production)
- **Deployment:** Heroku / Render / Any Python-compatible host

## 🏗️ System Architecture

```
┌─────────────────────┐
│  Client             │
│  (Mobile/Web/IoT)   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────────────────────┐
│  Flask Backend (Port 5000)          │
│  ├─ Health Check Endpoint           │
│  ├─ Prediction Endpoint             │
│  └─ PDF Report Generation           │
└──────────┬──────────────────────────┘
           │
           ▼
┌─────────────────────────────────────┐
│  Google Gemini 2.5 Flash API        │
│  (Multimodal AI Analysis)           │
└─────────────────────────────────────┘
```

## 📡 API Reference

### Base URL
```
http://localhost:5000  (local development)
http://your-deployed-url.com  (production)
```

### 1. Health Check
Verify the server is running and ready.

```http
GET /
```

**Response:**
```json
{
  "status": "online",
  "message": "Botany AI Pro Backend is live"
}
```

---

### 2. Predict Crop Disease
Upload an image to receive instant disease diagnosis with treatment recommendations.

```http
POST /predict
Content-Type: multipart/form-data

file: <image_file>
```

**Parameters:**
- `file` (required): Image file containing crop/plant (JPEG, PNG, etc.)

**Response:**
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

**Response Fields:**
- `v` - Vegetable/Crop type detected
- `d` - Disease name
- `t` - Treatment recommendations

---

### 3. Generate PDF Report
Create a professional PDF report from diagnosis results.

```http
POST /generate_pdf
Content-Type: application/json

{
  "v": "Cauliflower",
  "d": "Black Rot",
  "t": "Treatment steps..."
}
```

**Response:**
- Binary PDF file (downloads as `Botany_Report_Cauliflower.pdf`)
- Content-Type: `application/pdf`

---

## 💻 Local Setup & Installation

### Prerequisites
- Python 3.8 or higher
- pip (Python package manager)
- Google Gemini API Key ([Get one free here](https://aistudio.google.com/))
- Git

### Step-by-Step Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/sarveshmule1504/botany-bot.git
   cd botany-bot
   ```

2. **Create and activate a virtual environment (Recommended):**
   ```bash
   python -m venv venv
   
   # On Windows:
   venv\Scripts\activate
   
   # On macOS/Linux:
   source venv/bin/activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set your Gemini API Key:**
   
   **On Windows (Command Prompt):**
   ```cmd
   set GEMINI_API_KEY=your_api_key_here
   ```

   **On Windows (PowerShell):**
   ```powershell
   $env:GEMINI_API_KEY='your_api_key_here'
   ```

   **On macOS/Linux (Bash/Zsh):**
   ```bash
   export GEMINI_API_KEY=your_api_key_here
   ```

5. **Run the application:**
   ```bash
   python app.py
   ```

   Your server will start at: **`http://localhost:5000`**

## 🚢 Deployment

### Heroku / Render Deployment

The repository includes a `Procfile` pre-configured for production deployment.

1. **Create account** on [Heroku](https://heroku.com) or [Render](https://render.com)

2. **Connect repository** to your hosting platform

3. **Set environment variable:**
   - Add `GEMINI_API_KEY` to your platform's environment variables/secrets

4. **Deploy:**
   - The platform will automatically use the `Procfile` with Gunicorn
   - Your app will be live in minutes!

### Docker Deployment (Optional)

```dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["gunicorn", "app:app"]
```

## 📂 Project Structure

```
botany-bot/
├── app.py                 # Main Flask application
├── requirements.txt       # Python dependencies
├── Procfile              # Heroku/Render configuration
├── .env.example          # Environment variables template
├── templates/            # HTML templates (if applicable)
├── static/               # Static assets
└── README.md             # This file
```

## 🔧 Configuration

### Required Environment Variables
```env
GEMINI_API_KEY=your_api_key_here
```

### Optional Environment Variables
```env
FLASK_ENV=development  # or production
FLASK_DEBUG=True       # Set to False in production
PORT=5000
```

## 📖 Usage Examples

### Python (Requests Library)
```python
import requests

# Predict disease
files = {'file': open('cauliflower.jpg', 'rb')}
response = requests.post('http://localhost:5000/predict', files=files)
diagnosis = response.json()

print(f"Crop: {diagnosis['data']['v']}")
print(f"Disease: {diagnosis['data']['d']}")
print(f"Treatment: {diagnosis['data']['t']}")

# Generate PDF
pdf_data = requests.post('http://localhost:5000/generate_pdf', json=diagnosis['data'])
with open('report.pdf', 'wb') as f:
    f.write(pdf_data.content)
```

### cURL
```bash
# Test health check
curl http://localhost:5000/

# Predict from image
curl -X POST -F "file=@cauliflower.jpg" http://localhost:5000/predict

# Generate PDF report
curl -X POST -H "Content-Type: application/json" \
  -d '{"v":"Cauliflower","d":"Black Rot","t":"Remove infected leaves..."}' \
  http://localhost:5000/generate_pdf --output report.pdf
```

### JavaScript (Fetch API)
```javascript
// Predict disease
const formData = new FormData();
formData.append('file', fileInput.files[0]);

const response = await fetch('http://localhost:5000/predict', {
  method: 'POST',
  body: formData
});

const diagnosis = await response.json();
console.log(`Disease: ${diagnosis.data.d}`);
console.log(`Treatment: ${diagnosis.data.t}`);
```

## 🤝 Contributing

We welcome contributions! Here's how to get started:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes and commit (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow PEP 8 code style
- Add docstrings to new functions
- Test your changes locally before submitting
- Update this README if adding new features

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| `GEMINI_API_KEY not found` | Ensure the environment variable is set correctly |
| `ModuleNotFoundError` | Run `pip install -r requirements.txt` |
| `Port 5000 already in use` | Change port: `python app.py --port 8000` or kill the process using the port |
| `CORS errors` | CORS is already enabled; check that your frontend is making requests correctly |

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support & Issues

- **Found a bug?** Open an [issue](https://github.com/sarveshmule1504/botany-bot/issues)
- **Have questions?** Check existing issues or start a discussion
- **Want to contribute?** Check [open issues](https://github.com/sarveshmule1504/botany-bot/issues) for ways to help

## 🔗 Resources

- [Google Gemini API Docs](https://ai.google.dev/)
- [Flask Documentation](https://flask.palletsprojects.com/)
- [FPDF2 Documentation](https://py-pdf.github.io/fpdf2/)
- [Deploy to Heroku Guide](https://devcenter.heroku.com/articles/getting-started-with-python)

## 🎯 Roadmap

- [ ] Mobile app integration (React Native/Flutter)
- [ ] Multi-language support for treatment recommendations
- [ ] Advanced analytics dashboard
- [ ] Crop rotation recommendations
- [ ] Historical disease tracking
- [ ] Offline image processing capability

---

<div align="center">

**Made with 🌾 by [Sarvesh Mule](https://github.com/sarveshmule1504)**

*Empowering farmers with AI-powered crop disease detection*

</div>
