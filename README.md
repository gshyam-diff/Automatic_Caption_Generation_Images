# Neural Image Caption Generator with Visual Attention
### Research Internship Project | Indian Institute of Technology (IIT), Kanpur

![Python](https://img.shields.io/badge/Python-3.7-blue?logo=python&logoColor=white) ![TensorFlow](https://img.shields.io/badge/TensorFlow-2.0-orange?logo=tensorflow&logoColor=white) ![Status](https://img.shields.io/badge/Status-Completed-success) ![Dataset](https://img.shields.io/badge/Dataset-MS_COCO%2FFlickr8k-lightgrey)

## 📖 Project Overview
This repository contains the implementation of an **End-to-End Deep Learning Pipeline** for automatic image captioning. Developed during a research internship at **IIT Kanpur**, this project implements the *Show, Attend and Tell* paper, utilizing a visual attention mechanism to allow the model to focus on specific regions of an image while generating the corresponding words in the caption sequence.

**Authors:** Ghanashyam R K P, Sharan Nagarajan, Balamurugan

> **📄 Documentation:** For a comprehensive explanation of the math and experiments, please refer to the [Detailed Final Report](Savvy_captioners_Final_Report.pdf) included in this repo.

---

## 🧠 Model Architecture & Methodology
The architecture follows an **Encoder-Decoder** paradigm enhanced with **Bahdanau Attention**.

### 1. The Encoder (Feature Extraction)
* **Backbone:** We utilize **InceptionV3**, pre-trained on the ImageNet dataset.
* **Transfer Learning:** The final classification layer (SoftMax) is removed to extract the raw feature map ($8 \times 8 \times 2048$) from the penultimate convolutional layer.
* **Dimensionality:** These high-dimensional features are passed to the attention mechanism.

### 2. The Attention Mechanism
* **Type:** Visual Attention (Soft/Hard blend) based on Bahdanau et al.
* **Function:** Instead of averaging the entire image, the model calculates a **weighted average** of pixels based on the current context vector. This allows the decoder to "look" at specific objects (e.g., a bat, a ball) when predicting relevant words.

### 3. The Decoder (Sequence Generation)
* **Core Unit:** **Gated Recurrent Unit (GRU)**. We opted for GRUs over LSTMs to reduce computational expense while effectively capturing temporal dependencies.
* **Process:** At each time step, the GRU receives the context vector (from the attention layer) and the previously generated word to predict the next token in the sequence.

![Architecture Diagram](Images/ImageCap.PNG)
*Figure 1: The complete Encoder-Decoder architecture with Attention Flow.*

---

## 📊 Datasets & Evaluation
The model was trained and validated on two benchmark datasets:
* **Flickr-8k:** ~8,000 images (Used for rapid prototyping).
* **MS-COCO:** ~120,000 images (Used for final model training).

**Evaluation Metric:**
We utilized the **BLEU Score** (Bilingual Evaluation Understudy) to quantitatively measure the quality of the generated captions against reference human annotations.

---

## 📷 Qualitative Results
The model demonstrates the ability to correctly identify and describe complex scenes. Below are examples of the generated captions and the visual attention focus.

| **Sports Classification** | **Human Action Recognition** |
|:---:|:---:|
| ![Cricket](Images/Cricket.PNG) | ![Sharan](Images/Sharan.PNG) |
| *Accurate identification of "People playing cricket"* | *Semantic understanding of "Man doing jump on beach"* |

---

## 📺 Video Demonstration
We have produced a comprehensive video explaining the code structure, the intuition behind the Attention Mechanism, and a walkthrough of the Jupyter Notebook.

[![IMAGE ALT TEXT](http://img.youtube.com/vi/XAd_0c44ex4/0.jpg)](http://www.youtube.com/watch?v=XAd_0c44ex4 "Neural Image Caption Generator with Visual Attention")

---

## 📂 Repository Structure
* `Final-Notebook.ipynb`: The complete training and inference pipeline (Data Preprocessing -> Model Definition -> Training Loop -> Inference).
* `Savvy_captioners_Final_Report.pdf`: Detailed project report with mathematical formulations and loss plots.
* `Images/`: Visual assets and result screenshots.

---
*Created by Ghanashyam R K P & Team | IIT Kanpur Internship*
