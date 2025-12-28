### Lead Qualifier - A virtual Pre-sales team
Tool for identifying leads with potential and separate from  junk.

<img width="968" height="286" alt="LeadQualifier" src="https://github.com/user-attachments/assets/7b597322-50a8-4bac-908b-b1d3dfa9f55a" />

---

## 1. Introduction

### 1.1 Problem Statement
In the real estate industry, sales teams are often overwhelmed by a high volume of raw leads. Manual qualification is time-consuming, inconsistent, and prone to human error. Approximately 40-60% of sales time is wasted chasing low-intent prospects, while high-value leads may turn cold due to delayed response times.

### 1.2 Solution Overview
The **Lead Qualification System** is an automated CRM tool designed to solve this inefficiency. It acts as a first-line filter, instantly analyzing, scoring, and tagging incoming leads. By leveraging a multi-tiered intelligence engine, the system ensures that sales teams can prioritize their efforts on the top 20% of leads that are most likely to convert.

### Key Features
   *   **Smart Tagging**: Automatic classification into 🔥Hot, ✨Warm, ❄️Low Intent, or 🗑️Junk.
   *   **Adaptive Intelligence**: Three distinct scoring modes to suit different needs.
   *   **Dashboard**: Visual overview of lead quality and distribution.
   *   **Bulk Processing**: Support for uploading and processing large datasets (CSV/Excel).

## 2. Technology Stack
*   **Data Science**: Scikit-Learn, Pandas, NumPy, Joblib.
*   **Persistence**:  PKL (Model Artifacts).

## 3. The Intelligence Engine (Core Logic)

The system's unique value proposition is its **Adaptive Intelligence Engine**, which operates in three distinct modes to cater to different stages of business maturity.
<img width="828" height="294" alt="LeadQualifier2" src="https://github.com/user-attachments/assets/b27edf60-7981-400d-974c-f127275121d2" />

### Mode 1: Standard Rules (Deterministic)
**Best for:** Teams starting out with no historical data.

This mode uses a fixed, rule-based algorithm based on industry best practices.
*   **Logic**: Linear Weighted Sum.
*   **Scoring Factors**:
    *   **Budget (30%)**: Favors high-value brackets (> ₹1 Cr).
    *   **Timeline (25%)**: Rewards urgency (< 1 month).
    *   **Purpose (15%)**: Prioritizes investors over end-users.
    *   **Loan Eligibility (20%)**: Rewards pre-approved buyers.
    *   **Location (10%)**: Specific location interest adds value.

### Mode 2: Custom Model (Adaptive )
**Best for:** Teams with historical data who want tailored scoring.

This mode runs entirely in the browser. It analyzes your uploaded past data to learn what actually converts *for you*.
*   **Logic**: Statistical Correlation Analysis.
*   **Mechanism**:
    1.  Calculates the **Conversion Rate (CR)** for every attribute value.
    2.  Compares local CR to global CR to generate a **Multiplier**.
    3.  'Multiplier' Penalizes those attribute values that dont convert and pumps those that convert.
    4.  Example: If "Low Budget" leads convert surprisingly well, the model assigns a high multiplier(e.g. 1.5x) to that category, boosting their scores significantly compared to the Standard mode.

### Mode 3: External ML Model (Predictive)
**Best for:** Enterprise use cases-having historic data & requiring complex, non-linear logic.

This mode offloads decision-making to the pre-traied ML model.
*   **Logic**: Non-linear Machine Learning (Decision Tree / Random Forest).
*   **Mechanism**:
    1.  Accepts a custom pre trained '.pkl' file that's trained on historic data.
    2.  Ttransforms features of test leads (One-Hot Encoding, Scaling).
    3.  Predicts conversion potential (Hot/Warm/Cold) and Confidence Score using ML model.
    4.  Supports dynamic model updates via `.pkl` file upload.

---

## 4. User Guide

### 4.1 Dashboard
The central hub providing a visual overview.
*   **Lead Cards**: Displays individual lead details with color-coded tags (Hot/Warm/Junk).
*   **Agent Analysis**: Explains *why* a lead got a specific score (e.g., "+30 High Budget").

### 4.2 Model Training
Allows users to customize the intelligence.
*   **Browser Training**: Upload a CSV to generate custom weights instantly.
*   **External Upload**: Upload a pre-trained `.pkl` file for advanced logic.

### 4.3 Settings
*   **Scoring Mode**: Toggle between Standard, Custom, and External modes.
*   **Visual Themes**: Switch between "Futuristic" (Dark) and "Clean" (Light) themes.

---

## 5. Future Enhancements
*   **CRM Integration**: Direct connectors for Salesforce/HubSpot.
*   **NLP Analysis**: Sentiment analysis of lead comments/notes.
*   **User Auth**: Multi-user role-based access control.

---

## 6 Additional Tech stack 
*   **Frontend**: React 18, Vite, CSS Modules (Glassmorphism Design).
*   **Backend**: Python 3.9+, Flask, Flask-CORS,JSON.






