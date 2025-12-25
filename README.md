# University Helpdesk Assistant – LoRA Fine-Tuning (FLAN-T5-Small)

## Overview
This project demonstrates the fine-tuning of a **small instruction-following language model** using **Parameter-Efficient Fine-Tuning (LoRA / PEFT)** to build a **University Helpdesk Assistant**.  
The assistant is designed to answer common student and staff queries related to admissions, academics, IT support, and administrative services in a concise, safe, and domain-specific manner.

The project was completed as part of the **OXZON AI – AI/ML Internship Assessment** and focuses on **clarity of design, reasoning, and correctness**, rather than model size or computational complexity.

---

## Domain
**Education / University Helpdesk Assistant**

The assistant handles:
- Admissions and enrollment queries  
- Academic procedures (exams, results, grading)  
- IT and LMS support  
- Student services and campus facilities  

The model does **not** provide medical, legal, or confidential advice.

---

## Model Choice

- **Base Model:** `google/flan-t5-small` (~80M parameters)
- **Fine-Tuning Method:** LoRA (Low-Rank Adaptation) using HuggingFace PEFT

### Why FLAN-T5-Small?
- Already instruction-tuned
- Lightweight and suitable for free Google Colab
- Strong performance on short, task-oriented prompts
- Well-documented and stable

### Why LoRA / PEFT?
- Trains only a small subset of parameters
- Reduces GPU memory usage
- Faster training
- Prevents catastrophic forgetting
- Ideal for small, domain-specific datasets

---

## Dataset

### Structure
Each record follows the required instruction–response format:

```json
{
  "instruction": "How can I reset my student portal password?",
  "response": "You can reset your password using the 'Forgot Password' option on the student portal or by contacting IT support."
}
