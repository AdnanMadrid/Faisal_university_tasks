
# Task 3: Semantic Image Retrieval System

## 1. Overview

This task implements a **content-based image retrieval (CBIR) system** for chest X-ray images using the PneumoniaMNIST dataset. The objective is to retrieve visually similar medical images based on learned image embeddings and vector similarity search.

The system is fully implemented in the provided Google Colab notebook and is **strictly aligned with the practical implementation and results**. The retrieval pipeline focuses exclusively on **image-to-image retrieval** and does not rely on text-based queries.

---

## 2. Embedding Model Selection

### Selected Model: CLIP (ViT-B/32)

The system uses the **CLIP ViT-B/32** model provided by OpenAI to extract fixed-length image embeddings.

**Rationale:**
- CLIP provides robust, general-purpose visual representations.
- The model is publicly available and compatible with Google Colab.
- It enables embedding-based similarity search without additional training.
- The image encoder is used directly without fine-tuning.

> The model used is **not a medical-domain–specific model**. It is applied as-is to medical images to demonstrate semantic retrieval.

---

## 3. Dataset and Preprocessing

- **Dataset:** PneumoniaMNIST (MedMNIST v2)
- **Data split:** Test set
- **Classes:** Normal, Pneumonia
- **Image resolution:** 28 × 28 (grayscale)

### Preprocessing Steps:
- Grayscale images are converted to 3-channel RGB format.
- Images are resized and normalized using the CLIP processor.
- Preprocessed images are passed to the CLIP image encoder.

Each image is associated with:
- An image embedding
- A ground-truth class label

---

## 4. Embedding Extraction

For each image in the test set:
1. The image is preprocessed using the CLIP processor.
2. The CLIP image encoder generates a dense embedding vector.
3. All embeddings are collected into a single matrix for indexing.

These embeddings form the basis of similarity comparison.

---

## 5. Vector Database Implementation

### Similarity Engine: FAISS

The system employs **FAISS (Facebook AI Similarity Search)** to perform efficient nearest-neighbor retrieval.

- **Index type:** IndexFlatL2
- **Distance metric:** Euclidean (L2)
- **Stored vectors:** Image embeddings

### Index Construction:
1. Extract embeddings for all test images.
2. Add embeddings to the FAISS index.
3. Store corresponding labels and indices for evaluation and visualization.

The index is constructed once and reused for all retrieval experiments.

---

## 6. Image-to-Image Retrieval Pipeline

### Input:
- A query chest X-ray image from the test set

### Retrieval Procedure:
1. Encode the query image using the CLIP image encoder.
2. Search the FAISS index for the nearest neighbors.
3. Retrieve the top-k most similar images based on embedding distance.

### Output:
- Top-k visually similar images
- Corresponding class labels

---

## 7. Quantitative Evaluation

### Evaluation Metric: Precision@k

Precision@k is defined as:

\[
\text{Precision@k} = \frac{\text{Number of retrieved images with the same label}}{k}
\]

### Experimental Setup:
- k values: **1, 3, and 5**
- Multiple query images sampled from the test set
- Ground-truth labels used for correctness evaluation

### Results Summary:
- Precision@k values are consistently higher than random chance.
- Pneumonia images generally retrieve other pneumonia cases more reliably.
- Normal images exhibit slightly lower precision due to visual similarity across samples.

These results confirm that the embedding space captures meaningful visual patterns.

---

## 8. Visualization of Retrieval Results

The notebook includes visualizations displaying:
- The query image
- The top-k retrieved images

### Observations:
- Retrieved images often share similar lung structure and intensity patterns.
- Pneumonia queries tend to retrieve images with visible opacities.
- Some overlap occurs in visually ambiguous cases.

Qualitative inspection supports the quantitative evaluation.

---

## 9. Failure Case Analysis

### Common Failure Modes:
- **Low resolution:** The 28×28 image size limits fine-grained detail.
- **Subtle pathology:** Mild pneumonia cases may resemble normal lungs.
- **General-purpose embeddings:** CLIP is not trained specifically on medical images.

These limitations are inherent to the dataset and model choice.

---

## 10. Discussion and Future Improvements

### Strengths:
- Fully reproducible implementation
- Efficient similarity search using FAISS
- Clear evaluation and visualization

### Limitations:
- No text-to-image retrieval implemented
- No model fine-tuning on medical data
- Limited image resolution

### Potential Improvements:
- Use medical-domain embedding models
- Introduce cross-modal retrieval
- Apply the system to higher-resolution datasets
- Experiment with advanced FAISS indexes

---

## 11. Conclusion

This task demonstrates a complete and reproducible **image-to-image retrieval system** for chest X-ray images using CLIP embeddings and FAISS similarity search. Despite inherent limitations, the system successfully retrieves visually similar cases and provides a strong baseline for future extensions.

