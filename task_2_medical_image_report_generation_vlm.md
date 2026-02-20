# Task 2: Medical Image–Based Report Generation Using a Vision–Language Model

## 1. Overview

This task focuses on generating **clinically meaningful textual reports from chest X-ray images** by combining the **CNN classifier trained in Task 1** with a **medical Vision–Language Model (VLM)**. The objective is not only to classify images (normal vs pneumonia) but also to **explain model behavior** by generating structured, human-readable medical reports for:

- Correctly classified samples
- Misclassified samples

This bridges the gap between *pure classification* and *explainable, clinician-facing AI systems*.

---

## 2. Motivation

While Task 1 demonstrated strong performance in pneumonia classification using a ResNet-based CNN, raw predictions alone are insufficient in real clinical settings. Radiologists and clinicians require:

- Visual evidence
- Clear textual descriptions
- Contextual interpretation of findings

Therefore, Task 2 extends the pipeline by integrating a **medical-domain VLM** to generate reports directly from the X-ray images selected based on CNN predictions.

---

## 3. System Architecture

The complete pipeline consists of three major components:

### 3.1 CNN Classifier (Task 1)

- **Model**: ResNet-18
- **Training Dataset**: PneumoniaMNIST
- **Output**: Binary prediction (Normal / Pneumonia)
- **Usage in Task 2**:
  - Loaded pretrained weights
  - Used to identify:
    - Correctly classified images
    - Misclassified images

### 3.2 Image Selection Logic

From the test dataset:

- A subset of images is selected based on CNN outputs
- Images are grouped as:
  - True Positives / True Negatives
  - False Positives / False Negatives

This enables focused analysis of **model strengths and failure modes**.

### 3.3 Vision–Language Model (VLM)

- **Model**: Google MedGemma (medical instruction-tuned VLM)
- **Reason for Selection**:
  - Trained specifically on medical and radiology-style data
  - Generates clinically relevant language
  - Significantly outperforms general-purpose VLMs (e.g., BLIP-2, LLaVA) for medical imagery

The VLM receives:
- A chest X-ray image
- A structured medical prompt

And produces:
- A detailed, natural-language radiology-style report

---

## 4. Prompt Design

To ensure clinically meaningful outputs, prompts were carefully designed with:

- **System Role**: Senior Emergency Physician / Radiologist
- **User Instruction**: Describe findings, abnormalities, and possible interpretation

This prompt engineering step was critical in aligning generated text with expected medical reporting standards.

---

## 5. Results and Observations

### 5.1 Correctly Classified Images

For images correctly classified by the CNN:

- The VLM reports consistently:
  - Clear lung fields for normal cases
  - Opacities, infiltrates, or consolidation patterns for pneumonia cases
- Generated descriptions align well with CNN predictions

This demonstrates **strong agreement between visual classification and textual interpretation**.

### 5.2 Misclassified Images

Misclassified samples are particularly informative:

- The VLM often identifies **subtle abnormalities** even when the CNN prediction is incorrect
- In several false negatives, the generated report describes:
  - Mild or localized opacities
  - Low-contrast findings that are difficult for CNNs

This suggests that:
- The CNN may rely heavily on dominant global features
- The VLM provides complementary, descriptive reasoning

---

## 6. Error Analysis

Key insights from misclassification analysis:

- **Borderline cases** (early-stage pneumonia) are the most common failure mode
- Image quality and contrast significantly affect CNN performance
- The VLM’s textual output can help flag uncertain cases for **human review**

This highlights the importance of **human-in-the-loop AI systems** in medical imaging.

---

## 7. Why a Medical VLM Matters

Earlier attempts using general-purpose VLMs (e.g., BLIP-2, LLaVA) resulted in:

- Vague descriptions
- Non-medical language
- Poor alignment with radiological findings

By switching to **MedGemma**, the generated reports became:

- Domain-specific
- Clinically structured
- More interpretable and useful

This confirms that **domain-specific pretraining is critical** for medical AI applications.

---

## 8. Limitations

- The VLM does not replace expert diagnosis
- Reports may hallucinate subtle findings
- Performance depends on prompt quality and image resolution

These limitations reinforce the need for careful validation before clinical deployment.

---

## 9. Conclusion

Task 2 successfully demonstrates an end-to-end system that:

- Uses a pretrained CNN for medical image classification
- Identifies correct and incorrect predictions
- Generates clinically meaningful reports using a medical VLM

The combined approach improves **interpretability, transparency, and trust**, which are essential for real-world medical AI systems.

---

## 10. Repository Contents

- `Task2_report_generation.ipynb` – Full notebook implementation
- `resnet18_pneumonia.pth` – Pretrained CNN from Task 1
- `README.md` / this report – Detailed explanation and analysis

---

**Overall, this task demonstrates the practical value of combining discriminative CNN models with generative medical VLMs for explainable AI in healthcare.**

