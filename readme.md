# 7-Day Postdoctoral Technical Challenge  
## AI Medical Imaging, Visual Language Models, and Semantic Retrieval

**AlfaisalX: Cognitive Robotics and Autonomous Agents**  
**MedX Research Unit – Medical Robotics & AI in Healthcare**  
**College of Engineering and Advanced Computing**  
**Alfaisal University, Riyadh, Saudi Arabia**

---

## Challenge Overview

This repository contains my submission for the **7-Day Postdoctoral Technical Challenge** focused on building end-to-end AI systems for medical imaging applications. The challenge evaluates the ability to design, implement, and analyze interconnected AI components involving:

- Medical image classification
- Visual language models for report generation
- Semantic image retrieval using embedding-based search

All tasks are implemented using the **PneumoniaMNIST dataset (MedMNIST v2)** and are designed to be reproducible via **Google Colab notebooks**.

---

## Repository Contents

This repository includes:

- Complete Python implementations for all three tasks
- Google Colab notebooks for online execution and demonstration
- Detailed Markdown reports documenting methodology, evaluation, and analysis

---

## Dataset

All tasks use the **PneumoniaMNIST** dataset from **MedMNIST v2**, a lightweight benchmark for chest X-ray analysis.

**Dataset characteristics:**
- Task: Binary classification (Normal vs. Pneumonia)
- Training set: ~4,700 images
- Validation set: ~500 images
- Test set: ~600 images
- Image format: 28 × 28 grayscale chest X-rays

The dataset can be installed using:
```bash
pip install medmnist
