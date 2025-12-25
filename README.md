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
```

---

## Setup Instructions

### Environment
- Python 3.9 or higher  
- Google Colab (Free Tier) or a local machine with GPU (optional)

### Install Dependencies
```bash
pip install transformers datasets peft accelerate sentencepiece torch
```
## Training Details

### LoRA Configuration
- **Rank (r):** 88  
- **LoRA Alpha:** 16  
- **LoRA Dropout:** 0.05  
- **Target Modules:** Query and Value projection layers  

Only approximately **0.5% of the model parameters** are trainable, which makes the fine-tuning process **memory-efficient, faster, and suitable for limited compute environments** such as Google Colab Free Tier.

---

### Training Hyperparameters
- **Batch Size:** 8  
- **Learning Rate:** 2e-4  
- **Epochs:** 3  
- **Maximum Sequence Length:** 256  


---

### Training Process
1. Load the base **FLAN-T5-Small** model and tokenizer  
2. Apply **LoRA adapters** using HuggingFace PEFT  
3. Tokenize the dataset using instruction-style prompts  
4. Fine-tune the model using the HuggingFace `Trainer` API  
5. Save the trained **LoRA adapters** for inference  

---

## Evaluation

### Training Loss
- Training loss decreases steadily across epochs  
- Indicates stable convergence without signs of overfitting  

A **training loss curve** was plotted and captured as part of the submission to demonstrate training stability.

---

### Base Model vs Fine-Tuned Model Comparison

The same evaluation prompts were tested on:
- Base **FLAN-T5-Small** model  
- **LoRA fine-tuned** model  

#### Observed Improvements
- Fine-tuned model produces **domain-specific answers**
- Clear references to **student portals, academic offices, and IT support**
- More consistent **institutional and professional tone**
- Significant reduction in **vague or generic responses**

#### Limitations
- Cannot answer questions outside the trained domain
- Response quality depends heavily on dataset coverage
- No access to real-time or dynamic university information

---

### Sample Prompts Used for Evaluation
- How can I reset my student portal password?
- Where can I find the exam timetable?
- How do I apply for hostel accommodation?
- Who should I contact for LMS technical issues?
- How can I request an academic transcript?

---

## Observations & Learnings
- Small instruction-tuned models can be highly effective when combined with **high-quality, domain-specific fine-tuning**
- LoRA enables efficient training even with **limited computational resources**
- Dataset quality and response consistency significantly influence final model behavior
- Fine-tuning is more reliable than **zero-shot prompting** for repetitive, domain-specific helpdesk tasks

---

## Future Improvements
- Expand the dataset with more phrasing variations and edge cases
- Add automated evaluation metrics such as **ROUGE** and **BLEU**
- Integrate **Retrieval-Augmented Generation (RAG)** for dynamic university information
- Deploy the assistant as a **web-based or CLI helpdesk application**

