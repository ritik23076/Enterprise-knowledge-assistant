🧠 Enterprise Knowledge Assistant
GenAI System for Internal Policy & IT Q&A (LoRA Fine-Tuned LLM)
📌 Overview

This project demonstrates the end-to-end design of a production-style GenAI system for answering internal enterprise policy and IT support questions.

An open-source Large Language Model (LLM) is fine-tuned using Parameter-Efficient Fine-Tuning (LoRA) on a custom internal knowledge dataset. The system is designed with hallucination mitigation, response controllability, evaluation, and deployment readiness in mind.

Unlike generic chatbots, this assistant prioritizes:

Accuracy over creativity

Reliability over verbosity

Enterprise constraints over scale

🎯 Problem Statement

Internal teams often rely on:

HR portals

IT tickets

Documentation wikis

These are slow to navigate and inconsistent.
This project builds a GenAI-powered internal assistant that can answer policy and IT questions safely and reliably, while minimizing hallucinations.

🏗️ System Architecture
User Query
   ↓
Prompt Engineering (Instruction Format)
   ↓
LoRA Fine-Tuned LLM (GPT-Neo-125M)
   ↓
Decoding Controls + Safety Guardrails
   ↓
Domain Tagging + Fallback Logic
   ↓
Response (UI / API)

🧠 Model & Training Details
Base Model

Model: EleutherAI/gpt-neo-125M

Chosen intentionally for:

Low inference cost

Fast iteration

Realistic enterprise constraints

This project focuses on model adaptation quality, not model size.

Fine-Tuning Strategy

Technique: LoRA (Low-Rank Adaptation)

Framework: HuggingFace Transformers + PEFT

LoRA Configuration:

Rank (r): 16

Alpha: 32

Target modules: q_proj, k_proj, v_proj, out_proj

Training Setup:

Epochs: 3

Learning Rate: 1e-4

FP16 training

Custom data collator with prompt masking

📊 Dataset Design
Dataset Type

Instruction-following, enterprise-style Q&A

Alpaca-style JSONL format

Domains Covered

HR Policies

IT Support

Security & Compliance

Engineering Processes

Design Principles

Authoritative, policy-aligned tone

Explicit approvals / denials

Escalation paths (HR / IT / Security)

No conversational fluff

This ensures the model learns enterprise language, not generic explanations.

🛡️ Hallucination Mitigation & Safety

To ensure reliability, the system includes multiple guardrails:

Decoding Controls

Deterministic decoding (do_sample=False)

Low temperature (0.1)

Repetition penalty

N-gram repetition blocking

Fallback Logic

If a response is:

Too short

Vague

Repetitive

Out-of-domain

The system returns a safe fallback:

“This information is not clearly defined in the current company policy. Please contact HR or IT support.”

Domain Awareness

Responses are tagged as:

HR Policy

IT Support

Security Policy

Engineering Process

This improves clarity and trust.

📈 Evaluation Framework

The model was evaluated using unseen, paraphrased policy questions to test generalization rather than memorization.

Evaluation Method

Side-by-side comparison:

Base model vs Fine-tuned model

Manual labeling:

Correct

Partially correct

Hallucinated

Results

Significant improvement in:

Policy alignment

Factual tone

Reduction in hallucinations

Evaluation results are available in:

evaluation_results.csv

🖥️ User Interface (Gradio)

The project includes a clean enterprise-style UI built using Gradio.

UI Features

Professional layout (non-chatty)

Example question prompts

Domain-tagged responses

Crisp, policy-focused answers

The UI is designed to resemble a real internal company tool, not a chatbot demo.

🚀 API Deployment (FastAPI)

To simulate production deployment, the model is exposed via a FastAPI inference endpoint.

Endpoint
POST /ask

Example Request
{
  "question": "What is the company password policy?"
}

Why This Matters

Separates training from serving

Demonstrates production thinking

Enables future scaling and monitoring

⚠️ Limitations

No real-time policy updates

Ambiguous queries may trigger fallback

Requires retraining when policies change

Not intended for legal or financial advice

These limitations are explicitly documented to ensure responsible GenAI usage.

🔮 Future Improvements

Retrieval-Augmented Generation (RAG)

Confidence scoring

Access control & authentication

Logging and monitoring

Policy versioning

🧩 Why This Project is GenAI-Focused

This project emphasizes GenAI engineering principles:

Model controllability

Safety & reliability

Evaluation-driven iteration

Production-oriented design

Enterprise realism

It goes beyond “fine-tuning a model” and treats the system as a deployable GenAI application.

🧑‍💻 Tech Stack

Python

HuggingFace Transformers

PEFT (LoRA)

PyTorch

Gradio

FastAPI

Google Colab

📌 Conclusion

This project demonstrates how open-source LLMs can be adapted for enterprise use cases using efficient fine-tuning techniques, strong safety controls, and production-aware design.

It reflects the kind of decision-making, iteration, and responsibility expected from a GenAI / Applied AI Engineer.

⭐ If you like this project, feel free to star the repository!
