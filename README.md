#  ENTERPRISE KNOWLEDGE ASSISTANT
## Fine-Tuned an Open-Source LLM for Internal Policy & IT Q&A
---

## Project Overview

This project demonstrates the **complete lifecycle of building a production-style GenAI system**, starting from **problem definition and dataset creation** to **model fine-tuning, evaluation, safety controls, UI deployment, and API exposure**.

The objective was **not** to build a generic chatbot, but to design a **reliable enterprise-grade internal knowledge assistant** that prioritizes:

- Factual correctness  
- Deterministic behavior  
- Hallucination mitigation  
- Production-readiness  

This mirrors how **GenAI systems are built and deployed in real organizations**.

---

##  Problem Definition

Enterprises maintain large volumes of internal documentation such as:

- HR policies  
- IT support procedures  
- Security guidelines  
- Engineering workflows  

These documents are often scattered across portals and wikis, making information retrieval slow and inconsistent.

### Goal

Build a **GenAI-powered assistant** that can:

- Answer internal policy and IT questions  
- Avoid hallucinations  
- Respond in a professional, policy-aligned tone  
- Behave deterministically and safely  

---

## Dataset Design & Creation

### Why a Custom Dataset?

Generic datasets (e.g., Dolly, Alpaca) result in **generic and unreliable answers**.  
Enterprise use cases require **authoritative, structured, and policy-driven responses**.

### Dataset Characteristics

- Instruction-following (Alpaca-style format)
- Clear, authoritative answers
- Explicit approvals, restrictions, and escalation paths
- Focus on enterprise tone (not conversational chat)

## 🗂️ Domains Covered

The dataset spans multiple enterprise-relevant domains to ensure broad internal coverage:

- **HR Policies**
- **IT Support**
- **Security & Compliance**
- **Engineering Processes**

This dataset design ensures the model learns **enterprise language and decision boundaries**, rather than producing generic or conversational explanations.

---

## 🧠 Model Selection Strategy

### Base Model

- **EleutherAI / GPT-Neo-125M**

### Why a Small Model?

The choice of a smaller open-source model was a **deliberate engineering decision**, driven by real-world enterprise constraints:

- Faster experimentation and iteration
- Lower compute and inference cost
- More realistic deployment scenarios
- Emphasis on **model adaptation quality**, not raw parameter count

> This project demonstrates that **reliability and controllability matter more than scale** in enterprise GenAI systems.

---

## 🔧 Fine-Tuning Approach (LoRA)

### Technique Used

- **LoRA (Low-Rank Adaptation)** using HuggingFace PEFT

### Why LoRA?

- Parameter-efficient fine-tuning
- Faster training cycles
- Easy updates when policies change
- Widely adopted in production GenAI systems

### Training Configuration

- LoRA Rank (`r`): 16
- LoRA Alpha: 32
- Epochs: 3
- Learning Rate: 1e-4
- FP16 training
- Prompt masking (loss computed only on responses)

This approach allowed the model to **internalize policy tone and structure without overfitting**.

---

## 📉 Training Monitoring & Loss Analysis

- Training loss was logged using the HuggingFace `Trainer`
- Loss curves were plotted to verify:
  - Stable convergence
  - Meaningful learning
  - No divergence or collapse

This validated that **learning actually occurred**, rather than merely executing training code.

---

## 🧪 Evaluation Framework (Before vs After)

Rather than relying solely on training loss, the model was evaluated on **unseen and paraphrased policy questions** to test generalization.

### Evaluation Methodology

- Base model vs fine-tuned model
- Identical prompts and decoding settings
- Manual correctness assessment

### Evaluation Criteria

- **Correct**
- **Partially Correct**
- **Hallucinated**

### Results

- Improved factual accuracy
- Stronger policy alignment
- Significant reduction in hallucinations

Evaluation outputs are saved in:


---

## 🛡️ Hallucination Mitigation & Safety Controls

Enterprise GenAI systems must **fail safely**.

### Techniques Applied

- Deterministic decoding (`do_sample=False`)
- Low temperature (`0.1`)
- Repetition penalty
- N-gram repetition blocking
- Output quality heuristics

### Fallback Logic

If the model response is:

- Too short
- Vague
- Repetitive
- Out-of-domain

The system returns a safe fallback message:

> “This information is not clearly defined in the current company policy. Please contact HR or IT support.”

This mirrors **real-world enterprise AI safety practices**.

---

## 🏷️ Domain-Aware Responses

Each query is automatically classified into one of the following domains:

- **HR Policy**
- **IT Support**
- **Security Policy**
- **Engineering Process**

Responses are tagged accordingly to improve **clarity, trust, and interpretability**.

---

## 🖥️ User Interface (Gradio)

A **clean, enterprise-style UI** was built using Gradio.

### UI Design Principles

- Professional (non-chatty)
- Clear question input
- Domain-tagged responses
- Example prompts for demos

📸 Screenshots of the **Gradio UI** are included in the repository  
🎥 A **Loom demo video** will be added later

This UI reflects how **internal enterprise tools are typically presented**.

---
## ⚠️ Limitations

- No real-time policy updates
- Ambiguous queries may trigger fallback
- Requires retraining when policies change
- Not suitable for legal or financial advice

Limitations are **explicitly documented** for responsible GenAI usage.

---

## 🔮 Future Improvements

- Retrieval-Augmented Generation (RAG)
- Confidence scoring
- Monitoring and logging
- Access control and authentication
- Policy versioning

---

## 🏆 Why This Project Matters

This project demonstrates **GenAI engineering maturity**:

- Dataset ownership
- Efficient fine-tuning
- Hallucination control
- Evaluation-driven iteration
- Production-style deployment
- Enterprise-focused UX design

It reflects how **GenAI systems are built in real enterprise environments**, not academic demos!






