# Project Report: Lead Qualification System

**Version:** 1.0
**Date:** December 2025

---

## 1. Introduction

### 1.1 Problem Statement
In the real estate industry, sales teams are often overwhelmed by a high volume of raw leads. Manual qualification is time-consuming, inconsistent, and prone to human error. Approximately 40-60% of sales time is wasted chasing low-intent prospects, while high-value leads may turn cold due to delayed response times.

### 1.2 Solution Overview
The **Lead Qualification System** is an automated CRM tool designed to solve this inefficiency. It acts as a first-line filter, instantly analyzing, scoring, and tagging incoming leads. By leveraging a multi-tiered intelligence engine, the system ensures that sales teams can prioritize their efforts on the top 20% of leads that are most likely to convert.

---

### 2 Technology Stack
*   **Frontend**: React 18, Vite, CSS Modules (Glassmorphism Design).
*   **Backend**: Python 3.9+, Flask, Flask-CORS.
*   **Data Science**: Scikit-Learn, Pandas, NumPy, Joblib.
*   **Persistence**: JSON (Lead Storage), PKL (Model Artifacts).

---

## 3. The Intelligence Engine (Core Logic)

The system's unique value proposition is its **Adaptive Intelligence Engine**, which operates in three distinct modes to cater to different stages of business maturity.

### Tier 1: Standard Rules (Deterministic)
*Best for: Cold Start (No Historical Data)*

This mode uses a weighted attribute model based on industry best practices.
*   **Logic**: Linear Weighted Sum.
*   **Scoring Factors**:
    *   **Budget (30%)**: Favors high-value brackets (> ₹1 Cr).
    *   **Timeline (25%)**: Rewards urgency (< 1 month).
    *   **Purpose (15%)**: Prioritizes investors over end-users.
    *   **Loan Eligibility (20%)**: Rewards pre-approved buyers.

### Tier 2: Custom AI Model (Adaptive Inference)
*Best for: Growth Phase (Moderate Data)*

This mode runs entirely in the browser. It analyzes uploaded historical data (CSV) to "learn" specific conversion patterns.
*   **Logic**: Statistical Correlation Analysis.
*   **Mechanism**:
    1.  Calculates the **Conversion Rate (CR)** for every attribute value.
    2.  Compares local CR to global CR to generate a **Multiplier**.
    3.  Example: If "Low Budget" leads convert 2x better than average, they get a 2.0x score boost.

### Tier 3: External ML Model (Predictive)
*Best for: Enterprise (Sufficient Data)*

This mode offloads decision-making to the Python backend.
*   **Logic**: Non-linear Machine Learning (Decision Tree / Random Forest).
*   **Mechanism**:
    1.  Frontend sends raw JSON to `/predict`.
    2.  Backend transforms features (One-Hot Encoding, Scaling).
    3.  Model predicts class (Hot/Warm/Cold) and Confidence Score.
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
