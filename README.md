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

## ✨ Recent Features

### 📋 Practice vs Exam Modes
- **Practice Mode**: No time limit with "Show Answer" feature to reveal correct answers and explanations immediately.
- **Exam Mode**: Timed mode with no answer reveal button. Navigate using Previous/Next buttons only.

### ⏱️ Timer Functionality
- **Practice Mode**: Count-up timer showing elapsed time during the exam.
- **Exam Mode**: Countdown timer with automatic submission when time expires.
- **Default Duration**: Calculated as `total_questions × 90 seconds` (customizable before exam start).
- **Time Tracking**: Final results display total time taken in the elegant Orbitron monospace font.

### 🎬 Scenario Support
- Questions can now reference reusable scenarios via `scenario_id` to reduce JSON file repetition.
- Scenarios are displayed in a modal overlay accessible via the **"View Scenario"** button.
- Each question independently manages scenario visibility based on its content.
- Legacy exam files without scenarios continue to work seamlessly.

### 🎨 Enhanced UI/UX
- Sticky header with live question counter, attendance tracker, and timer display.
- Progress bar showing exam completion percentage.
- Responsive design optimized for desktop and mobile devices.
- Orbitron Google Font applied to timer displays for visual emphasis.

---

## 🚀 How to Use the Exam Engine

### 📌 Option 1: Online Exams (Cloud Mode)
1. Open **`exam-engine.html`** in any modern web browser.
2. By default, the **"Online Exams"** tab is active.
3. Choose an exam group from the first dropdown. The options are shown as `<code> - <name>`.
4. After selecting the exam group, choose a specific test from the second dropdown.
5. Click **START EXAM** to fetch the chosen question set directly from the GitHub repository.

> The online exam engine loads exam metadata from `available-exams.json`, which must contain a top-level `exams` array.

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
- `questions`: Array of question objects.

**Question Fields:**
- `id`: Unique identifier for the question.
- `Question`: The question text (supports line breaks with `\n`).
- `Options`: Array of answer choices with `id`, `text`, and `reason` fields.
- `MaxAnswerSelection`: Determines if the question is Single-Select (1) or Multi-Select (2+).
- `CorrectAnswers`: Array of IDs of correct answer options.
- `CorrectAnswerExplanation`: Overall justification text shown after answer reveal.
- `scenario_id` (optional): Reference to a scenario object by ID. Only shown if the question has this field.

**Scenario Support (Optional):**
```json
{
  "scenarios": [
    {
      "id": 1,
      "text": "A detailed scenario description\nwith multiple lines\nof context."
    }
  ],
  "questions": [
    {
      "id": 1,
      "scenario_id": 1,
      "Question": "Question that references the scenario...",
      ...
    }
  ]
}
```
Scenarios reduce JSON file size by eliminating repeated context across multiple questions.

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
├── available-exams.json       # Online exam config with top-level exams array
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

