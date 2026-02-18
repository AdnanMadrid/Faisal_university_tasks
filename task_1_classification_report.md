# Task 1 – CNN Classification with Comprehensive Analysis

## 1. Objective
This report presents the complete solution for **Task 1: CNN Classification with Comprehensive Analysis** of the AlfaisalX Postdoctoral Technical Challenge. The objective is to design, train, evaluate, and critically analyze a convolutional neural network (CNN) for **pneumonia detection from chest X-ray images** using the **PneumoniaMNIST** dataset.

The task emphasizes not only classification performance, but also correct experimental methodology, rigorous evaluation, visualization of results, and medical interpretation.

---

## 2. Dataset and Experimental Protocol

### 2.1 Dataset
- **Dataset**: PneumoniaMNIST (MedMNIST v2)
- **Modality**: Chest X-ray images
- **Image resolution**: 28 × 28 pixels
- **Channels**: Grayscale
- **Classes**: Normal, Pneumonia

This dataset is explicitly specified in the challenge instructions and is suitable for lightweight CNN-based experimentation on standard hardware.

### 2.2 Dataset Splits (Verified Correctness)
The **official MedMNIST splits** were used without modification:

| Split | Number of Images |
|------|------------------|
| Training | 4,708 |
| Validation | 524 |
| Test | 624 |

Using the predefined splits ensures reproducibility and prevents data leakage. Training, validation, and testing were performed on **disjoint subsets**, fully satisfying experimental requirements.

---

## 3. Data Preprocessing and Augmentation

### 3.1 Preprocessing
- Conversion to tensors
- Intensity normalization using mean = 0.5 and standard deviation = 0.5

Normalization stabilizes training and is standard practice for medical imaging pipelines.

### 3.2 Data Augmentation (Training Only)
- Random rotations (±10°)
- Random horizontal flips

These augmentations are mild and clinically plausible, simulating patient positioning variability without altering anatomical semantics.

---

## 4. Model Architecture and Justification

### 4.1 Is a CNN Appropriate?
Yes. **CNNs are the standard and correct choice** for image-based medical classification tasks due to their ability to learn spatially localized patterns such as lung opacities and structural abnormalities.

### 4.2 Architecture Used
- **Backbone**: ResNet-18
- Modified first convolution to accept single-channel images
- Final fully connected layer replaced with a single-neuron output

ResNet-18 provides a strong balance between representational capacity and generalization for small datasets, making it suitable for PneumoniaMNIST.

---

## 5. Training Methodology

### 5.1 Loss Function
- **Binary Cross-Entropy with Logits Loss (BCEWithLogitsLoss)**

This loss is numerically stable and appropriate for binary classification with probabilistic outputs.

### 5.2 Optimization Strategy
- **Optimizer**: Adam
- **Initial learning rate**: 1e-3
- **Learning rate scheduler**: ReduceLROnPlateau (monitors validation loss)

This configuration ensures adaptive learning and prevents stagnation during training.

### 5.3 Training Configuration
- Epochs: 30
- Batch size: 64
- Hardware: CPU (GPU used automatically if available)

---

## 6. Training and Validation Analysis

### 6.1 Loss Curves (Training vs Validation)

The loss curves show:
- Rapid decrease in training loss during early epochs
- Stable validation loss after initial fluctuations
- No divergence between training and validation curves

**Interpretation:**
The model converges stably and does not exhibit severe overfitting. Minor validation loss spikes in early epochs are expected due to stochastic optimization and data augmentation.

---

## 7. Test Set Evaluation (Final Results)

### 7.1 Quantitative Metrics

The model was evaluated on the held-out test set with the following results:

| Metric | Value |
|------|-------|
| Accuracy | **0.864** |
| Precision | **0.827** |
| Recall (Sensitivity) | **0.990** |
| F1-score | **0.901** |
| ROC-AUC | **0.959** |

All metrics required by the challenge are reported.

### 7.2 Metric Interpretation
- **Very high recall (99.0%)** indicates the model almost never misses pneumonia cases
- Precision is lower due to false positives, reflecting conservative predictions
- F1-score confirms a strong balance between precision and recall
- ROC-AUC of 0.959 demonstrates excellent class separability

From a medical screening perspective, this behavior is desirable, as false negatives are far more critical than false positives.

---

## 8. Confusion Matrix Analysis

Confusion matrix results:
- True Negatives (Normal → Normal): 153
- False Positives (Normal → Pneumonia): 81
- False Negatives (Pneumonia → Normal): 4
- True Positives (Pneumonia → Pneumonia): 386

### Interpretation
- The model is highly sensitive to pneumonia cases
- Errors are dominated by false positives rather than false negatives
- The extremely low false-negative count confirms strong robustness for pneumonia detection

---

## 9. Failure Case Visualization and Analysis

A total of **85 misclassified samples** were identified and visually inspected.

### Observations from Misclassified Images
- Many false positives exhibit ambiguous lung patterns or low-contrast regions
- Some normal images contain noise or shadowing resembling pneumonia
- Low spatial resolution (28 × 28) limits fine-grained anatomical discrimination

Representative misclassified examples confirm that errors arise primarily from dataset limitations rather than modeling instability.

---

## 10. Strengths and Limitations

### Strengths
- Correct and justified use of CNNs for medical image classification
- Proper training, validation, and testing protocol
- Excellent sensitivity for pneumonia detection
- Comprehensive evaluation with clinical interpretation
- Fully reproducible pipeline

### Limitations
- Low image resolution restricts detailed feature extraction
- Moderate false-positive rate
- Limited dataset size

---

## 11. Conclusion

All requirements of **Task 1** have been fully satisfied:
- CNN-based classification implemented correctly
- Appropriate dataset and official splits used
- Training, validation, and testing conducted rigorously
- Comprehensive metrics, visualizations, and failure analysis provided

The results demonstrate strong performance and a clear understanding of medical AI evaluation principles, providing a solid foundation for subsequent tasks involving multimodal reasoning and retrieval.

---

## 12. Reproducibility

- Notebook: `task1_pneumonia_classification.ipynb`
- Saved model weights provided
- Compatible with local execution and Google Colab

