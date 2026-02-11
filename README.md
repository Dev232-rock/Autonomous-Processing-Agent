```
Autonomous Insurance Claims Processing Agent
```
🚀 Project Summary

This project implements an AI-powered FNOL (First Notice of Loss) claims processing agent using Gemini LLM. The system automatically extracts key claim information from insurance PDFs, identifies missing or unreliable data, and routes claims to the correct workflow with clear reasoning.

The primary focus of this implementation is accurate decision-making and safe automation, ensuring that incomplete or ambiguous claims are correctly flagged for Manual Review instead of risking incorrect auto-processing.

🧠 Approach

Extract raw text from FNOL PDF

Use Gemini LLM as the primary extractor

Apply regex-based fallback for robustness

Filter out headers/labels to avoid false values

Assign confidence scores to extracted fields

Detect missing mandatory fields

Route the claim using deterministic business rules

🧾 Actual Result
```
{
  "extractedFields": {
    "claim_type": {
      "value": "vehicle_damage",
      "confidence": 0.9
    }
  },
  "missingFields": [
    "policy_number",
    "policyholder_name",
    "date",
    "location",
    "description",
    "estimated_damage"
  ],
  "recommendedRoute": "Manual Review",
  "reasoning": "Mandatory fields are missing"
}
```
```
Architecture Overview

FNOL PDF
   ↓
PDF Text Extraction
   ↓
Gemini LLM Extraction  ──┐
                         ├─→ Field Merge + Confidence Scoring
Regex Fallback Extraction ─┘
   ↓
Missing Field Detection
   ↓
Rule-Based Claim Routing
   ↓
JSON Result
```
▶️ How to Run
```
pip install pdfplumber google-generativeai
python run.py
```
🎯 Key Design Decision
Confidence scores and label filtering were added as optional enhancements to improve trust and explainability, without changing the assessment-required output structure.
```
🛠️ Tech Stack
LLM: Gemini 1.5
Runtime: Google Colab / Python
PDF Parsing: pdfplumber
Design: LLM-first, rule-backed
```
Model Confidence Scores (Reported)
```
| Field Source                               | Confidence Score |
| ------------------------------------------ | ---------------- |
| Gemini LLM (clean value)                   | **0.88 – 0.95**  |
| Regex fallback                             | **0.70 – 0.80**  |
| Structured fields (policy #, date, amount) | **+0.03 boost**  |
| Header / label-like values                 | **≤ 0.30**       |
| Missing or empty fields                    | **0.00**         |
```
