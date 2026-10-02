# 🛡️ PhishShield AI

### Multimodal AI-Based Phishing Detection System

<p align="center">
  <b>Detect phishing using URL intelligence + visual webpage analysis.</b> 
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-blue?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/TensorFlow-Keras-orange?style=for-the-badge&logo=tensorflow&logoColor=white" />
  <img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi&logoColor=white" />
  <img src="https://img.shields.io/badge/Gradio-Demo-FF7C00?style=for-the-badge&logo=gradio&logoColor=white" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Deep%20Learning-CNN%20%7C%20BiLSTM-purple?style=flat-square" />
  <img src="https://img.shields.io/badge/Detection-Multimodal-red?style=flat-square" />
  <img src="https://img.shields.io/badge/Project-Computer%20Security-black?style=flat-square" />
</p>

---

## 🚀 Overview

**PhishShield AI** is a multimodal phishing detection system designed to analyze suspicious websites using two complementary sources of information:

* 🔗 **URL-based intelligence**
* 🖼️ **Website screenshot / visual intelligence**

Instead of depending on a single prediction source, the system combines multiple deep-learning outputs through a **Fusion Engine** to produce a final phishing probability and classification.

The complete system is exposed through a **FastAPI backend** and demonstrated through a modern **Gradio web interface**.

---

## 🎯 Project Objective

The primary objective of PhishShield AI is to build an intelligent security system capable of identifying potentially malicious websites by learning both:

> **What the URL looks like**

and

> **What the webpage visually looks like**

This multimodal approach is designed to provide a broader view of phishing characteristics than relying on URL analysis alone.

---

## 🧠 System Architecture

```text
                    ┌──────────────────────┐
                    │      Website URL     │
                    └──────────┬───────────┘
                               │
                     ┌─────────┴─────────┐
                     │                   │
                     ▼                   ▼
              ┌─────────────┐     ┌─────────────┐
              │   URL CNN   │     │ URL BiLSTM   │
              └──────┬──────┘     └──────┬──────┘
                     │                   │
                     └─────────┬─────────┘
                               │
                         URL Intelligence
                               │
                               ▼
                    ┌────────────────────┐
                    │   URL Probability  │
                    └─────────┬──────────┘
                              │
                              │
      ┌───────────────────────┘
      │
      │
      ▼
┌──────────────────────┐
│ Website Screenshot   │
└──────────┬───────────┘
           │
           ▼
   ┌─────────────────┐
   │ Screenshot CNN  │
   └────────┬────────┘
            │
            ▼
   Visual Probability
            │
            │
            └───────────────┐
                            ▼
                  ┌──────────────────┐
                  │  FUSION ENGINE   │
                  │                  │
                  │ URL: 60%         │
                  │ Visual: 40%      │
                  └────────┬─────────┘
                           │
                           ▼
                 ┌────────────────────┐
                 │ Final Probability   │
                 │ + Classification    │
                 └────────────────────┘
```

---

## ✨ Key Features

### 🔗 URL Intelligence

The URL branch uses two deep-learning architectures:

* **1D CNN**
* **BiLSTM**

These models analyze sequential patterns and structural characteristics present in URLs.

---

### 🖼️ Visual Intelligence

A dedicated **Screenshot CNN** analyzes the visual representation of a webpage.

The visual branch can capture webpage-level patterns that may not be obvious from the URL alone.

---

### ⚡ Multimodal Fusion

The project combines:

```text
URL Probability
       +
Visual Probability
       ↓
Fusion Engine
       ↓
Final Prediction
```

Current fusion configuration:

| Component           | Weight |
| ------------------- | -----: |
| URL Intelligence    |    60% |
| Visual Intelligence |    40% |

The final decision uses a tuned classification threshold of **0.30**.

---

## 📊 Evaluation

On the verified URL + visual evaluation subset used during development:

| Metric             |     Result |
| ------------------ | ---------: |
| Fusion Accuracy    | **84.09%** |
| ROC-AUC            | **80.83%** |
| Evaluation Samples |     **44** |
| Fusion Threshold   |   **0.30** |

> **Note:** These measurements come from the verified evaluation subset used for the multimodal fusion experiment, not from the entire dataset. They should therefore be interpreted as experimental evaluation results rather than a universal real-world accuracy guarantee.

---

## 🔬 Why Multimodal Detection?

Traditional URL-only detection mainly focuses on the structure of the URL.

However, phishing pages can sometimes use:

* Familiar-looking page layouts
* Brand-like visual elements
* Login interfaces
* Suspicious visual patterns
* Deceptive webpage designs

PhishShield AI therefore combines **URL-level** and **visual-level** signals.

```text
Traditional approach

URL ───────────────► Prediction


PhishShield AI

URL ────────────────┐
                    ├──► Fusion ───► Prediction
Screenshot ─────────┘
```

---

## 🧩 Technology Stack

| Layer                   | Technology         |
| ----------------------- | ------------------ |
| Programming Language    | Python             |
| Deep Learning           | TensorFlow / Keras |
| URL Model 1             | CNN                |
| URL Model 2             | BiLSTM             |
| Visual Model            | CNN                |
| Backend                 | FastAPI            |
| Frontend / Demo         | Gradio             |
| Image Processing        | Pillow             |
| Development Environment | Google Colab       |
| Storage / Backup        | Google Drive       |

---

## 🏗️ Project Structure

```text
PhishShield_AI/
│
├── main.py
│
├── models/
│   ├── phishshield_url_cnn.keras
│   ├── phishshield_url_bilstm.keras
│   ├── phishshield_screenshot_cnn_improved.keras
│   │
│   └── phishshield_html_nn.keras
│
├── preprocessing/
│   ├── phishshield_url_tokenizer.pkl
│   ├── phishshield_html_scaler.pkl
│   ├── phishshield_html_features.pkl
│   └── phishshield_html_branch_info.pkl
│
├── config/
│   ├── phishshield_project_config.json
│   └── phishshield_fusion_config.json
│
├── demo/
│   └── gradio_demo
│
└── README.md
```

---

## 🔌 API Endpoints

The FastAPI backend exposes the following endpoints:

### Health Check

```http
GET /health
```

Example response:

```json
{
  "status": "healthy",
  "url_cnn": true,
  "url_bilstm": true,
  "screenshot_cnn": true
}
```

---

### URL Prediction

```http
POST /predict/url
```

Used for URL-based phishing analysis.

---

### Multimodal Prediction

```http
POST /predict/multimodal
```

Accepts:

* Website URL
* Website screenshot

and returns the multimodal prediction.

---

## 🖥️ Demo Interface

The final demonstration interface provides:

* 🔗 Website URL input
* 🖼️ Screenshot upload
* 🚀 One-click analysis
* 🎯 Final prediction
* 📊 Fusion probability
* 🔗 URL probability
* 🖼️ Visual probability
* ⚡ System status

Example output:

```text
FINAL PREDICTION
🛡️ LEGITIMATE

FUSION PROBABILITY
28.77%

URL PROBABILITY
0.09%

VISUAL PROBABILITY
71.78%
```

---

## ⚙️ Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_USERNAME/PhishShield-AI.git
cd PhishShield-AI
```

Install dependencies:

```bash
pip install fastapi uvicorn python-multipart pillow tensorflow gradio requests
```

---

## ▶️ Running the Backend

Start the FastAPI server:

```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

Then open:

```text
http://127.0.0.1:8000
```

Health endpoint:

```text
http://127.0.0.1:8000/health
```

---

## 🎨 Running the Demo

The project includes a Gradio-based demonstration interface.

The demo workflow is:

```text
Enter URL
     ↓
Upload Screenshot
     ↓
Analyze Website
     ↓
URL CNN + BiLSTM
     ↓
Screenshot CNN
     ↓
Fusion Engine
     ↓
Final Prediction
```

---

## 🔐 HTML Analysis Branch

An HTML neural-network branch was also developed as part of the project.

However, during the verified integration stage, exact URL-to-HTML alignment was unavailable for the available samples.

Therefore:

> **The HTML branch is preserved in the project package but is not included in the active final URL + Visual fusion pipeline.**

This design choice avoids introducing unreliable data alignment into the final prediction system.

---

## 💡 Project Novelty

The main contribution of PhishShield AI is its **multimodal phishing detection architecture**.

Instead of relying on only one signal, the system combines:

```text
URL Deep Learning
       +
Visual Deep Learning
       ↓
Multimodal Fusion
       ↓
Final Phishing Assessment
```

The system also uses a development-time threshold analysis to select the final fusion decision threshold.

---

## 🧪 Development Workflow

```text
Dataset Collection
        ↓
Data Cleaning
        ↓
Preprocessing
        ↓
URL Model Development
        ↓
CNN + BiLSTM
        ↓
Screenshot Model Development
        ↓
CNN
        ↓
Model Evaluation
        ↓
Fusion Experiments
        ↓
Threshold Analysis
        ↓
FastAPI Backend
        ↓
Gradio Interface
        ↓
Final Demonstration
```

---

## 📦 Model Files

The project package contains the trained model artifacts used by the system:

```text
phishshield_url_cnn.keras
phishshield_url_bilstm.keras
phishshield_screenshot_cnn_improved.keras
phishshield_html_nn.keras
```

Supporting preprocessing/configuration files include:

```text
phishshield_url_tokenizer.pkl
phishshield_html_scaler.pkl
phishshield_html_features.pkl
phishshield_html_branch_info.pkl
phishshield_project_config.json
phishshield_fusion_config.json
```

---

## 🛡️ Security & Privacy

PhishShield AI is intended as an academic/research project for phishing detection.

It should **not** be treated as a replacement for:

* Browser security systems
* Enterprise security products
* Threat intelligence platforms
* Professional security analysis

Predictions are model outputs and may contain false positives or false negatives.

---

## ⚠️ Important

Do **not** commit sensitive files such as:

```text
.env
API keys
passwords
private tokens
credentials
personal datasets
private Google Drive files
```

For large model files, consider using **Git LFS** or an external artifact-storage solution rather than committing oversized binaries directly to Git. GitHub recommends Git LFS for large files.

---

## 📸 Demo Screenshots

Add your project screenshots here:

```markdown
![PhishShield AI Demo](docs/images/demo.png)
```

Recommended screenshots:

1. 🖥️ Final Gradio interface
2. 🔍 URL analysis result
3. 🎯 Multimodal prediction result
4. 📊 Fusion evaluation
5. 🧠 System architecture

GitHub supports relative image paths, so keeping screenshots inside the repository makes the README portable when the repository is cloned.

---

## 📚 Research Context

PhishShield AI was developed as an academic Computer Security / Machine Learning project focusing on:

* Phishing detection
* Deep learning
* URL classification
* Computer vision
* Multimodal learning
* Model fusion
* Cybersecurity automation

---

## 👨‍💻 Project Team

**PhishShield AI**

Academic Project
Computer Security / Machine Learning

> Add your team members, university, department, course code, and supervisor information here.

---

## 📌 Future Improvements

Potential future extensions include:

* 🌐 Live webpage HTML analysis
* 🔍 DOM-based phishing detection
* 🔗 External threat-intelligence integration
* 🧠 Transformer-based URL modeling
* 🖼️ Improved visual feature extraction
* 🔄 Dynamic multimodal calibration
* 📱 Mobile-friendly interface
* 🚀 Cloud deployment
* 📈 Larger-scale evaluation
* 🛡️ Real-time browser integration

---

## ⭐ Acknowledgement

This project was developed for academic and educational purposes to explore the application of deep learning and multimodal analysis in cybersecurity.

---

## 📄 License

This project is intended primarily for academic and educational use.

If you plan to distribute the project as open-source software, add an appropriate license such as MIT, Apache-2.0, or another license that matches your intended usage.

---

<p align="center">

### 🛡️ PhishShield AI

**URL Intelligence × Visual Intelligence × Fusion**

*Building smarter approaches to phishing detection.*

</p>
