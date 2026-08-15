# LLM Hallucination Detection

## Overview

Large Language Models (LLMs) can generate fluent and coherent responses, 
but they may also produce hallucinations — information that is factually 
incorrect or unsupported.

This project investigates and compares two approaches for detecting 
hallucinations in LLM-generated answers.

The experiments are conducted using the TruthfulQA dataset, with Phi-3 
used to generate responses.

---

## Methods

### Method 1: Reference-Based Detection

The generated answer is compared with the reference answers provided by 
TruthfulQA.

The similarity between the generated response and the ground-truth 
reference is used to determine whether the response contains hallucinated 
information.

### Method 2: Retrieval-Based Verification

The second method verifies generated answers using external evidence.

Pipeline:

Question  
↓  
Phi-3 Response  
↓  
Claim Extraction  
↓  
Wikipedia Evidence Retrieval  
↓  
Claim Verification  
↓  
Hallucination Classification

The retrieval system uses Wikipedia as the knowledge source and FAISS for 
offline evidence retrieval.

Two verification approaches are investigated:

- Prompt-based LLM judge
- Fine-tuned DeBERTa judge trained using FEVER

---

## Repository Structure

    Code/
    ├── generate_phi_3_answer/
    ├── method_1_reference_based/
    │   └── Phi3_Hallucination_Detection.ipynb
    │
    └── method_2_retrieval_based/
        ├── building_procedures/
        |   ├── fine_tuned_judge_training/
        |   |   └── FEVER_DeBERTa_Judge_Training.ipynb
        |   |
        |   └── offline_FAISS_index_building/
        |   |   └── Wikipedia_Passage_FAISS.ipynb
        |   |
        |   └── 01_Prompt_Claim_Extraction.ipynb
        |   └── 02_Wikipedia_Evidence_retrieval_by_FAISS.ipynb
        |   └── 02_Wikipedia_Evidence_Retrieval_by_online_search.ipynb
        |   └── 03_Prompt_Judge_and_Aggregator.ipynb
        |
        └── final_pipeline/
            ├── fever_deberta_judge/
            |   └── model.safetensors
            ├── WIKI_resource/
            |   └── wiki_retrieval_output/
            |       └── wiki_passages.faiss
            └── Final_Pipeline.ipynb
    requirements.txt
    README.md

---

## Installation

Clone the repository:

    git clone <repository-url>
    cd ECE1508

Install the required packages:

    pip install -r requirements.txt

Python 3.10 or later is recommended.

---

## Usage

### 1. Generate Phi-3 Responses

Run the notebooks in:

    Code/generate_phi_3_answer/

These notebooks prepare the TruthfulQA data and generate responses using 
Phi-3 Mini.

### 2. Reference-Based Detection

Run:

    Code/method_1_reference_based/Phi3_Hallucination_Detection.ipynb

This evaluates hallucinations using reference-answer similarity.

### 3. Retrieval-Based Detection

The development notebooks are available in:

    Code/method_2_retrieval_based/building_procedures/

The complete retrieval-based pipeline can be run using:

    Code/method_2_retrieval_based/final_pipeline/Final_Pipeline.ipynb

The pipeline performs claim extraction, Wikipedia evidence retrieval, 
claim verification, and final hallucination classification.

---

## Models

The project uses:

- Phi-3 Mini — answer generation
- Qwen2.5-3B-Instruct — claim extraction
- Sentence Transformer — semantic evidence retrieval
- FAISS — offline Wikipedia retrieval
- DeBERTa — fine-tuned claim verification
- OpenAI API — prompt-based claim verification

The fine-tuned model weights are stored using Git LFS.

---

## Evaluation

The hallucination detectors are evaluated using:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

The ground-truth hallucination labels are compared against the predictions 
from each detection method.

---

## Results

Experimental outputs are available in:

    Results/

and

    Code/method_2_retrieval_based/final_pipeline/outputs/

The project compares reference-based detection with retrieval-based 
verification and investigates the effect of evidence retrieval quality on 
hallucination detection performance.

---

## Reproducibility

The required Python packages are listed in:

    requirements.txt

The main pipeline notebook provides sample input and output demonstrating 
the complete hallucination detection process.
