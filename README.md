# Mental Health Meme Classification

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This project presents a novel **multimodal framework** to classify mental health memes by integrating figurative reasoning and commonsense knowledge into visual and textual models. Memes often express complex mental health symptoms like depression and anxiety through a blend of humor, sarcasm, and imagery. Our approach leverages state-of-the-art transformers and fusion techniques to improve automatic detection of these symptoms.

---

## Motivation

Memes have become a popular form of communication expressing personal struggles, especially around mental health issues such as anxiety and depression. Traditional text-based mental health detection methods struggle with memes due to their multimodal nature and figurative language. This project aims to build an AI system capable of interpreting both visual and textual cues to detect mental health symptoms early, which can support researchers and practitioners.

---

## Key Features

- **Multimodal Input:** Combines image features (using CLIP) with OCR-extracted meme text embeddings.
- **Figurative Reasoning:** Integrates commonsense knowledge for better interpretation of figurative language (ongoing/future work).
- **Multi-Label & Single-Label Classification:**
  - Multi-label classification of depression symptoms.
  - Single-label classification of anxiety symptoms.
- **Text Encoders:** Experiments with multiple text encoders including Sentence-BERT, MentalBERT (mental health domain-specific), and RoBERTa.
- **Fusion Techniques:** Early fusion of visual and textual embeddings for classification.
- **Performance Evaluation:** Models evaluated on curated depression and anxiety meme datasets.

---

## Methodology

1. **OCR Text Extraction:**  
   Extract meme text using Tesseract OCR.

2. **Text Embedding:**  
   Encode extracted text with Sentence-BERT, MentalBERT, or RoBERTa.

3. **Image Embedding:**  
   Extract visual features using the CLIP ViT-B/32 model.

4. **Fusion:**  
   Concatenate textual and visual embeddings to form multimodal representations.

5. **Classification:**  
   - Multi-label classifier with sigmoid activation for depression symptoms.  
   - Single-label classifier with softmax activation for anxiety symptoms.

6. **Training Details:**  
   - Optimizer: Adam  
   - Learning rate: 5e-5  
   - Batch size: 4  
   - Epochs: 10  
   - Loss: Binary Cross-Entropy for multi-label, Cross-Entropy for single-label.

---

## Datasets

- **Depression Dataset (Multi-label):** Memes labeled with multiple depressive symptoms like Hopelessness, Anhedonia, Fatigue, Social Withdrawal.
- **Anxiety Dataset (Single-label):** Memes labeled with a single anxiety symptom such as Excessive Worry, Nervousness, or Restlessness.

---

## Results Summary

| Model              | Dataset       | Accuracy (%) | Macro-F1 (%) | Weighted-F1 (%) |
|--------------------|---------------|--------------|--------------|-----------------|
| **CLIP + Sentence-BERT** | Anxiety       | 56.81        | 52.76        | 55.48           |
| **CLIP + MentalBERT**    | Anxiety       | 53.67        | 48.35        | 51.74           |
| **CLIP + RoBERTa**       | Anxiety       | 38.81        | 31.87        | 35.30           |
| **CLIP + RoBERTa**       | Depression    | 48.67        | 45.42        | 46.12           |
| **CLIP + MentalBERT**    | Depression    | 49.21        | 43.42        | 41.22           |
| **CLIP + Sentence-BERT** | Depression    | 10.58        | 1.77         | 7.76            |

- Sentence-BERT performs well on anxiety (simpler task) but poorly on multi-label depression.
- RoBERTa excels in multi-label depression classification.
- MentalBERT shows moderate performance due to domain-specific pretraining.

---

## Challenges & Observations

- Figurative and sarcastic language in memes poses difficulty for models.
- OCR quality critically impacts performance.
- Multi-label depression classification is more complex than single-label anxiety classification.
- Early fusion may miss nuanced interactions between modalities — future work to explore attention-based fusion.
- Dataset size and diversity limit generalization; augmentation and commonsense knowledge integration planned.

---

## Future Work

- Incorporate emotion recognition from visuals.
- Develop cross-attention fusion models for better inter-modal understanding.
- Integrate advanced figurative reasoning modules using large language models.
- Extend classification to predict severity levels of symptoms.
- Expand datasets and improve OCR robustness.

---

## Installation

```bash
# Clone the repository
git clone https://github.com/Anand23111/mental-health-meme-classification.git
cd mental-health-meme-classification

# Create and activate a Python virtual environment (optional)
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
