# 📘 MS Certification Preparation – Practice Exams

This repository contains **practice exam samples** for Microsoft certification exams, designed to help learners **assess readiness, understand concepts, and practice exam-style questions**.

Hosted Link for Exam Engine - https://kashyapmak.github.io/ms-certification-preparation/ 

## 🎯 What This Repository Offers

- 🚀 **Centralized Exam Engine**: A single HTML interface (`exam-engine.html`) to run all practice tests.
- 🌐 **Online Exam Library**: Fetch the latest question sets directly from GitHub.
- 📂 **Local JSON Support**: Ability to upload and take exams from your own local JSON files.
- 🧠 **Scenario-based Questions**: Detailed explanations and justification for every answer.
- 🛠️ **Validation & Error Handling**: The engine automatically checks local files for correct formatting before starting.

---

## 🚀 How to Use the Exam Engine

### 📌 Option 1: Online Exams (Cloud Mode)
1. Open **`exam-engine.html`** in any modern web browser.
2. By default, the **"Online Exams"** tab is active.
3. Select an exam set from the dropdown menu (e.g., *GH-300 - GitHub Copilot*).
4. Click **START EXAM** to fetch the questions directly from the GitHub repository.

### 📌 Option 2: Local JSON Upload (Offline Mode)
1. Open **`exam-engine.html`**.
2. Switch to the **"Local Upload"** tab.
3. Click the file input area to upload a compatible `.json` question set from your machine.
4. The engine will validate your file:
   - ✅ If valid, the **START EXAM** button will enable.
   - ❌ If the JSON is malformed or missing required fields, a red error alert will describe the issue.

---

## 🛠️ Question Set JSON Schema

All practice exams are stored in a standardized JSON format to ensure they work with the central engine. Refer to `question-set-schema.json` for technical details.


**Key Fields Required:**
- `quizName`: The name displayed in the exam header.
- `passingScore`: The minimum score needed to trigger a "PASSED" status.
- `MaxAnswerSelection`: Determines if the question is Single-Select (1) or Multi-Select (2+).
- `CorrectAnswerExplanation`: The justification text shown during the "Show Answer" or "Review" phase.

---

## ⚠️ Disclaimer
* This repository contains **unofficial practice questions**.
* It does **not** contain real Microsoft certification

---

## 📂 Repository Structure

The repository is organized to separate the exam logic (engine) from the question data (JSON sets).

```text
ms-certification-preparation/
│
├── exam-engine.html           # The central engine (open this in your browser)
├── question-set-schema.json    # Standard JSON schema for all question sets
├── README.md                   # Repository documentation
│
├── AI-102/                     # Azure AI Engineer Question Sets
│   ├── ai-102-Set-1.json
│   ├── ai-102-Set-2.json
│   └── ai-102-Set-3-Comprehensive.json
│
├── GH-300/                     # GitHub Copilot Question Sets
│   └── gh-300.json
│
└── Sample/                     # Dummy/Tutorial Question Sets
    └── sample.json

