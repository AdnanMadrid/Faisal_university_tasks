# Task 2: Using the Pretrained Model for Medical Image Report Generation

## 1. Overview

This guide explains how to access and use the **pretrained ResNet18 model** for **Task 2: Medical Image Report Generation**. The pretrained model is essential for running the Task 2 notebook (`Task2_reports_generation.ipynb`) without needing to retrain the CNN.  

Because the model is large (~48 MB), it is **not stored directly in the main branch**. Instead:

* The **main branch** contains all notebooks and reports for Task 2:
  - `Task2_reports_generation.ipynb` – Notebook for generating medical reports using a Vision–Language Model (VLM)
  - `task1_pneumonia_classification.ipynb` – Notebook for Task 1 classification
  - `task_1_classification_report.md` – Task 1 report
  - `task_2_medical_image_report_generation_vlm.md` – Task 2 report

* The **pretrained model** is in the **master branch** and is also associated with a **GitHub Release** tag for easy access.

---

## 2. Motivation

The pretrained model allows:

* Quick setup for Task 2 without retraining
* Reproducible results for medical report generation
* Focused evaluation of the Vision–Language Model using correctly and incorrectly classified images

Providing the pretrained model in a **Release** ensures users can safely download and use it without worrying about GitHub’s file size limits or branch conflicts.

---

## 3. Pretrained Model Details

* **Model Name:** ResNet18
* **Purpose:** Classifies chest X-ray images as Normal / Pneumonia
* **Location:** `Documents/Task2_GitHubRepo/pretrained_model.zip` in the **master branch**
* **Release Tag:** `trained_model`
* **GitHub Releases Page:** [trained_model Release](https://github.com/AdnanMadrid/Faisal_university_tasks/releases)

> Users should download the model from the Release to ensure proper file integrity and avoid exceeding GitHub’s 25 MB web upload limit.

---

## 4. Using the Pretrained Model

### 4.1 Clone the Repository

Open Google Colab and run:

```bash
!git clone https://github.com/AdnanMadrid/Faisal_university_tasks.git
%cd Faisal_university_tasks

This downloads all notebooks, reports, and other repository files.
4.2 Download the Model
1.	Visit the GitHub Releases page.
2.	Locate the release tag trained_model.
3.	Download pretrained_model.zip — this is the pretrained ResNet18 model used for Task 2.
Note: The file resides in the master branch in the repository, but using the Release ensures all users get the correct version without switching branches manually.
4.3 Unzip the Model
After downloading, unzip the model into a folder named pretrained_model:
import zipfile
import os

os.makedirs("pretrained_model", exist_ok=True)

with zipfile.ZipFile("pretrained_model.zip", "r") as zip_ref:
    zip_ref.extractall("pretrained_model")

print("Pretrained model is ready to use!")
he folder pretrained_model now contains all model weights.
4.4 Run Task 2 Notebook
Open and run:
Task2_reports_generation.ipynb
The notebook automatically loads the model from the pretrained_model/ folder. No retraining is required.
