---
title: Task Prioritization Recommender Feature
---

## 1. Introduction

The Task Prioritization feature is designed to help students identify which tasks to focus on next
within OnTrack. The system evaluates multiple factors to generate a priority score for each task,
enabling students to manage their workload more effectively and reduce the risk of missed deadlines.

---

## 2. Purpose

The purpose of this feature is to:

- Recommend tasks based on urgency and workload
- Support better time management
- Integrate with AI-based effort prediction for smarter prioritisation

---

## 3. Approach

Tasks are ranked using a **weighted priority scoring system** based on:

- Deadline urgency
- Estimated effort required
- Current student workload

---

## 4. Prioritization Logic

### 4.1 Deadline Urgency

Tasks with closer due dates receive higher priority.

### 4.2 Estimated Effort

Tasks requiring more effort are prioritised earlier to allow sufficient time for completion.  
This will integrate with the AI-based effort prediction feature.

### 4.3 Workload

Tasks are prioritised higher when a student has multiple competing tasks.

Workload is determined by:

- Number of tasks due within a short timeframe
- Total estimated effort required for upcoming tasks

---

## 5. Scoring Model

### 5.1 Priority Score Formula

Priority Score = (0.5 × Deadline Score) + (0.3 × Effort Score) + (0.2 × Workload Score)

Each factor is converted into a score between **0–100**.

---

### 5.2 Deadline Score

| Time Remaining | Score |
| -------------- | ----- |
| ≤ 1 day        | 100   |
| ≤ 3 days       | 80    |
| ≤ 7 days       | 60    |
| ≤ 14 days      | 40    |
| > 14 days      | 20    |

---

### 5.3 Effort Score (AI-Based)

| Estimated Effort | Score |
| ---------------- | ----- |
| > 10 hours       | 90    |
| 5–10 hours       | 70    |
| 2–5 hours        | 50    |
| < 2 hours        | 30    |

---

### 5.4 Workload Score

| Workload Level | Score |
| -------------- | ----- |
| Low            | 30    |
| Medium         | 60    |
| High           | 90    |

---

## 6. Example Calculation

### Task A

- Due in 2 days → Deadline Score = 80
- Effort = 8 hours → Effort Score = 70
- Workload = Medium → Workload Score = 60  
  Priority Score = (0.5 × 80) + (0.3 × 70) + (0.2 × 60) = 40 + 21 + 12 = 73

---

### Task B

- Due in 10 days → Deadline Score = 40
- Effort = 2 hours → Effort Score = 30
- Workload = Low → Workload Score = 30

Priority Score = (0.5 × 40) + (0.3 × 30) + (0.2 × 30) = 20 + 9 + 6 = 35

---

### Result

Task A is prioritised higher than Task B due to a higher overall score.

---

## 7. System Flow

1. Retrieve all tasks for the student
2. Calculate:
   - Deadline score
   - Effort score (from AI prediction)
   - Workload score
3. Compute total priority score
4. Rank tasks in descending order
5. Recommend highest priority tasks to the user

---

## 8. Integration

- Effort scores will be derived from the **AI-Based Effort Prediction feature**
- The system will consume predicted effort (in hours) and map it to scoring ranges
- Designed to integrate seamlessly with backend APIs

---

## 9. Design Rationale

- **Deadline urgency (50%)**  
  Highest weight to reduce missed submissions

- **Effort (30%)**  
  Encourages early start on complex tasks

- **Workload (20%)**  
  Balances tasks across multiple units

---

## 10. Outcome

Tasks with higher priority scores will be recommended first, helping students:

- Stay on track
- Reduce stress
- Improve task planning

---

## 11. Dependencies

- AI-based effort prediction feature (external team)
- Task metadata (deadlines, units, etc.)
- Backend API integration

---

## 12. Conclusion

The Task Prioritization feature enhances OnTrack by providing a structured and intelligent way to
manage student tasks. By combining urgency, effort, and workload, the system delivers meaningful
recommendations that improve productivity and academic outcomes.


