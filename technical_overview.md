# Lead Qualification Agent - Technical Overview

## 1. Application Overview
The **Lead Qualification Agent** is an intelligent CRM tool designed to automate the process of scoring and classifying real estate leads. It helps sales teams prioritize high-value prospects by analyzing key attributes like budget, timeline, and purpose.

### Key Features
-   **Instant Scoring**: Real-time analysis of lead data.
-   **Smart Tagging**: Automatic classification into Hot, Warm, Low Intent, or Junk.
-   **Dashboard**: Visual overview of lead quality and distribution.
-   **Bulk Processing**: Support for uploading and processing large datasets (CSV/Excel).
-   **Adaptive Intelligence**: Three distinct scoring modes to suit different needs.

---

## 2. Intelligence Engine Logic
The core of the application is the "Intelligence Engine," which drives the scoring and tagging decisions. It operates in three modes:

### Mode A: Standard Rules (Deterministic)
**Best for:** Teams starting out with no historical data.
This mode uses a fixed, rule-based algorithm based on industry best practices.

**Scoring Logic (Max 100 Points):**
*   **Budget (30 pts)**: Higher budgets get more points (> ₹1 Cr = 30, < ₹20 L = 0).
*   **Timeline (25 pts)**: Urgency is rewarded (Immediate = 25, > 6 months = 5).
*   **Purpose (15 pts)**: Investors are scored higher (15) than end-users (10).
*   **Loan Eligibility (20 pts)**: Pre-approved/Cash buyers get max points.
*   **Location (10 pts)**: Specific location interest adds value.

**Tagging Thresholds:**
*   🔥 **Hot**: Score ≥ 80
*   ✨ **Warm**: Score ≥ 50
*   ❄️ **Low Intent**: Score < 50
*   🗑️ **Junk**: Invalid contact info.

### Mode B: Custom AI Model (Adaptive)
**Best for:** Teams with historical data who want tailored scoring.
This mode runs entirely in the browser. It analyzes your uploaded past data to learn what actually converts *for you*.

**How it Works:**
1.  **Training**: You upload a CSV of past leads with outcomes (Converted/Lost).
2.  **Correlation Analysis**: The system calculates conversion rates for each attribute (e.g., "Do 'Short Term' leads convert better than average?").
3.  **Dynamic Weights**: It generates multipliers (0.5x - 2.5x) for each attribute.
    *   *Example*: If "Low Budget" leads convert surprisingly well, the model assigns a high multiplier (e.g., 1.5x) to that category, boosting their scores significantly compared to the Standard mode.

### Mode C: External ML Model (Advanced)
**Best for:** Enterprise use cases requiring complex, non-linear logic.
This mode connects to a local Python backend running a Scikit-Learn machine learning model.

**Technical Flow:**
1.  **Request**: Frontend sends JSON data to `http://localhost:5000/predict`.
2.  **Inference**: The Python Flask server uses a pre-trained **Decision Tree Classifier** (`model.pkl`) to evaluate the lead.
3.  **Response**: Returns a predicted Tag and Confidence Score.
4.  **Fallback**: If the server is offline, the system seamlessly reverts to Standard Rules.

---

## 3. Technical Architecture

### Frontend (Client-Side)
-   **Framework**: React (v18) with Vite for fast development.
-   **Styling**: Vanilla CSS with a custom "Futuristic/Glassmorphism" design system.
-   **State Management**: React `useState` and `localStorage` for persistence.
-   **Data Processing**: `src/lib/agent.js` handles the business logic and scoring algorithms.

### Backend (Server-Side)
-   **Runtime**: Python 3.9+
-   **Framework**: Flask (Lightweight WSGI web application framework).
-   **ML Library**: Scikit-learn (for the Decision Tree model).
-   **Serialization**: Joblib (for loading the `.pkl` model).
-   **API**: RESTful endpoints (`/health`, `/predict`).

### Directory Structure
```
g:/Lead Qualifier/
├── src/
│   ├── components/     # React UI components (LeadCard, Dashboard, etc.)
│   ├── lib/            # Logic (agent.js, api.js, trainingAgent.js)
│   └── App.jsx         # Main application controller
├── backend/
│   ├── app.py          # Flask server entry point
│   ├── model.pkl       # Trained ML model artifact
│   └── requirements.txt # Python dependencies
└── README.md           # Setup instructions
```

## 4. Running the Application
The system requires two concurrent processes:
1.  **Backend**: `python backend/app.py` (Runs on port 5000)
2.  **Frontend**: `npm run dev` (Runs on port 5173)
