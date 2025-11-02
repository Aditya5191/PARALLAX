## A Note on Our Two-Pronged Strategy

It's important to understand the distinct and specialized roles of our two image analysis models. The Zero-Shot detector is intentionally a generalist. Since it is not trained on a specific dataset, its primary purpose is to detect a broad range of AI-generated content like artwork, cartoons, and landscapes where a specialized detector would fail. Consequently, it may not work perfectly for the nuanced task of detecting human face deepfakes.

Conversely, our Custom CNN is a specialist, meticulously trained on a massive dataset of human faces to achieve the highest possible accuracy in that critical domain. Its job is to see the human faces and it is not intended for other fields like AI art. We designed these two models to be complementary, not interchangeable; each is optimized for a different purpose to provide comprehensive protection.

# 🖼️ Image Modality: A Two-Pronged Approach to Deepfake Detection
This directory contains the complete solution for our image authenticity analysis. We recognize that "deepfake" content is not limited to human faces; it can include AI-generated art, animals, landscapes, and more. To address this, we've developed a powerful, two-pronged strategy:

## A Specialized Custom CNN:
A highly accurate, fine-tuned model built exclusively for the most common and critical use case: detecting deepfake human faces.

## A Generalized Zero-Shot Detector: 
A flexible and future-proof pipeline that can identify any type of AI-generated image (art, animals, objects) without ever needing to be retrained.

Together, these two components provide a robust and comprehensive defense against all forms of image-based misinformation.
---

#  Zero-Shot Deepfake Detection using CLIP + Digital Forensics

##  Project Overview

This project presents a **revolutionary Deepfake Detection Pipeline** that combines the power of **Zero-Shot Learning (ZSL)** using **OpenAI's CLIP** model with classic **Digital Image Forensics**. Unlike conventional models that are fine-tuned on specific deepfake datasets (usually human face datasets), this pipeline makes **generalized predictions** — capable of detecting **deepfakes of faces, landscapes, animals, objects, artworks**, and more — **without any retraining**.

>  The model also provides **human-interpretable reasoning** for its verdict based on measurable features like **sharpness, noise residuals**, and **ELA artifacts**.


---

##  Key Features

- **Zero-Shot Classification**: Uses CLIP to classify images into `real` or `deepfake` without any additional training.
- **Digital Forensics Analysis**:
  - **ELA (Error Level Analysis)**: Identifies abnormal compression artifacts common in manipulated images.
  - **Blur Score (Sharpness)**: Measures image sharpness — deepfakes often appear unnaturally smooth or blurry.
  - **Noise Residual Mean**: Detects inconsistent noise patterns caused by editing or synthesis.
- **Explainability**: For each prediction, the model provides reasoning such as:
  - `"Low blur score → possibly fake"`
  - `"High noise mean → tampered content likely"`
- **Multi-Domain Generalization**: Unlike traditional models, it’s **not limited to facial deepfakes**. Can detect deepfakes across:
  - Human faces
  - Landscapes and scenes
  - Digital and traditional art
  - Animals, objects, synthetic images, etc.
- **Image Display**: Visualizes the original input image alongside results for transparency and review.

---

##  How It Works

###  Full Pipeline

1. **Input Image**
2. **CLIP Zero-Shot Prediction**
   - CLIP computes similarity between the image and the textual labels `"a real image"` and `"a deepfake image"`.
3. **Error Level Analysis (ELA)**
   - Detects inconsistencies in JPEG compression that can expose tampering.
4. **Blur Detection**
   - Calculates Laplacian variance as a sharpness metric.
5. **Noise Residual Estimation**
   - Measures residual image noise that may indicate manipulation.
6. **Final Verdict**
   - Combines forensic metrics and CLIP scores to output:
     - `Real` or `Deepfake`
     - Category of image (e.g., face, landscape, etc.)
     - Explanation: why this decision was made.

---

##  Example Output

- Image Category : Artwork
- CLIP Prediction : Deepfake (Real=0.28, Deepfake=0.72)
- Blur Score (sharpness): 288.06 (Low → more fake-like)
- Noise Residual Mean : 4.18 (High → more manipulation)
- Final Verdict : Deepfake
- Explanation : Low sharpness and high residual noise with CLIP favoring 'deepfake'

---

##  Why This Approach is Novel

-  **No Training Required**: Works out-of-the-box via Zero-Shot Inference.
-  **Multimodal Fusion**: Combines **language + image** similarity with **classic image forensics** — a hybrid method not commonly seen in existing literature.
-  **Explainability Matters**: Provides interpretable outputs for humans — not just black-box probabilities.
-  **Not Face-Only**: Most deepfake detectors rely on facial datasets — this pipeline generalizes to all image domains.
-  **Lightweight & Portable**: Can be deployed via Flask or Streamlit without GPU-heavy training.

---

##  Key Concepts Explained

###  Zero-Shot Learning (ZSL)
Zero-shot learning allows models to **classify samples from unseen classes** using semantic understanding — in this case, CLIP uses text descriptions to determine similarity with images.

###  Error Level Analysis (ELA)
ELA helps identify parts of an image that have been edited. Areas with different compression levels stand out, making deepfake regions visible under analysis.

###  Blur Detection
Measures the **sharpness** of an image. Deepfakes, especially GAN-based ones, often appear overly smooth or blurry due to generation artifacts.

###  Noise Residuals
Natural images contain consistent sensor noise. Synthetic or edited images disrupt this pattern, resulting in abnormal noise residuals.

---

##  Tech Stack

- **Python**
- **CLIP (OpenAI)**
- **Pillow (for ELA)**
- **NumPy / OpenCV (for sharpness & noise)**
- **Matplotlib / Streamlit / Flask** (for visualization or deployment)

---

##  Example Visualization

<img width="1307" height="548" alt="image" src="https://github.com/user-attachments/assets/a09adab2-1f72-4683-9319-0b774792db11" />

*A deepfake detected through noise inconsistency and low blur score*

---

## 2. Custom CNN: Specialized Human Face Deepfake Detector

### Project Overview

While our Zero-Shot model provides broad coverage, this Custom Convolutional Neural Network (CNN) is a specialist, engineered for one purpose: **to achieve the highest possible accuracy in detecting deepfake human faces**. It has been trained on a massive dataset of over 140,000 real and synthetic face images, allowing it to learn the subtle, intricate artifacts that distinguish even the most convincing fakes.

The cornerstone of this model is its commitment to **transparency through Explainable AI (XAI)**.

### Model Architecture

The model is built with a standard, robust CNN architecture designed for stability and performance.

* **Input**: `Image (224x224)`
* **Core**: A stack of `Conv2D` layers for feature extraction, stabilized with `Batch Normalization` and made robust against overfitting with `Dropout`.
* **Output**: A `GlobalAveragePooling` layer followed by a `Dense` layer to produce the final classification.
<img width="577" height="647" alt="image" src="https://github.com/user-attachments/assets/84b0691b-3a1e-4d01-bdb1-fefdbe181ef0" />


### 📊 Performance Metrics

The model demonstrates excellent performance on a held-out test set:

| Metric | Score |
| :--- | :---: |
| **ROC AUC** | 0.96 |
| **Accuracy** | 0.86 |
| **F1-Score** | 0.86 |
| **Precision** | 0.87 |
| **Recall** | 0.85 |

<img width="450" height="406" alt="image" src="https://github.com/user-attachments/assets/1f86ba9c-007b-4c87-8703-0599eec5962c" />

![Uploading image.png…]()



### 💡 Explainable AI (XAI): Building Trust via Transparency

A simple "real" or "fake" verdict is not enough. To build trust, our Custom CNN provides clear, visual explanations for its decisions. This answers the crucial "why" and allows users to see the evidence for themselves.

We integrate several state-of-the-art XAI techniques:

* **Saliency Maps / Integrated Gradients**: These methods produce a heatmap that highlights the most important pixels in the input image. **Bright areas** in the map are the pixels the model "looked at" the most to make its decision.
  <img width="690" height="729" alt="image" src="https://github.com/user-attachments/assets/5c76d5fd-2355-4b69-9179-d865063b6968" />
  <img width="1224" height="635" alt="image" src="https://github.com/user-attachments/assets/7dcddd5c-9c19-441f-b2b2-6b8b0da2b276" />


* **SHAP (SHapley Additive exPlanations)**: SHAP goes deeper by showing which parts of the face push the prediction towards "fake" (**red pixels**) and which parts push it towards "real" (**blue pixels**). This provides a nuanced, pixel-by-pixel contribution map.
<img width="1115" height="852" alt="image" src="https://github.com/user-attachments/assets/ebdc2a9b-5631-4013-9849-552774c37bc2" />

* **LIME (Local Interpretable Model-agnostic Explanations)**: LIME identifies which "superpixels" or regions of the image were most influential. This is useful for seeing if the model is focusing on logical areas, like inconsistent eyes or a blurry jawline.
 <img width="633" height="667" alt="image" src="https://github.com/user-attachments/assets/80d8c000-9598-4b03-b2c7-949221eee472" />


By providing these transparent insights, our Custom CNN moves beyond being a black box and becomes a trustworthy forensic tool.

