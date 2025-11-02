# 🛡️ Parallax: An AI-Powered Multi-Modal Misinformation Detection Platform

**Parallax is a state-of-the-art, end-to-end ecosystem designed to combat digital misinformation by providing forensic-grade analysis of content across all major media formats. Powered by a suite of custom deep learning models and seamlessly integrated with Google Cloud AI, this project delivers a robust, scalable, and transparent solution for verifying the authenticity of the digital world.**

This repository is the central hub for all components of the Parallax project, from the backend APIs and advanced AI models to the user-facing frontend and browser extension.

http://104.197.87.77:8080/
---

## 🏛️ Technical Architecture & Google Cloud AI Integration

Parallax is architected as a modern, cloud-native application, leveraging a microservice-inspired approach where each detection modality can be scaled and updated independently. Our commitment to high-quality, modular code is evident in our clean project structure and well-documented components.

The entire platform is built upon the powerful, scalable, and secure infrastructure of **Google Cloud**.

### Our Use of Google Cloud AI:

* **☁️ Vertex AI (The Heart of our ML Operations):** Vertex AI is central to our entire machine learning lifecycle.
    * **Vertex AI Training:** All our custom deep learning models—including the **Image CNN**, **PhysNet3D (rPPG)**, and **LipFD**—were trained using custom training jobs on Vertex AI. This allowed us to leverage powerful GPU acceleration (NVIDIA A100s) and a managed environment for reproducible, high-performance model training.
    * **Vertex AI Prediction & Endpoints:** Trained models are deployed to **Vertex AI Endpoints**. Our backend API calls these secure, auto-scaling endpoints for real-time inference, ensuring low latency and high availability for our users. This abstracts away the complexity of model serving.

* **☁️ Cloud Run (Scalable Serverless Backend):**
    * Our entire backend, built with Python (Flask/FastAPI), is deployed on Cloud Run. This provides a fully managed, serverless platform that automatically scales from zero to handle any workload, ensuring cost-efficiency and operational excellence. The backend serves as the central API gateway for our frontend and web extension.

* **☁️ Cloud Storage:**
    * We use Cloud Storage as our primary data lake. It stores our massive training datasets (e.g., the 140k real/fake face images), raw media for analysis, and, most importantly, our versioned model artifacts, ensuring a single source of truth for our ML models.

---

## 📂 Project Component Breakdown

This repository is organized into the primary components of the Parallax ecosystem. Each directory contains a dedicated `README.md` with in-depth technical details, setup instructions, and performance metrics for that specific module.

| Component | Directory Path | Description & Key Technologies |
| :--- | :--- | :--- |
| **Video Modality** | [`./video_modality_raw_files/`](./video_modality_raw_files/) | Our most advanced module, targeting deepfakes with a two-pronged approach: analyzing both **behavioral** and **biological** signals in video streams. |
| **Image Modality** | [`./Image_modality_raw_files/Zero Shot Detection/`](./Image_modality_raw_files/Zero%20Shot%20Detection/) | A comprehensive solution for image authenticity, combining a specialized model for human faces with a generalized model for all other AI-generated content. |
| **Audio Modality** | [`./audio_modality_raw_files/Deepfake Audio Det.../`](./audio_modality_raw_files/Deepfake%20Audio%20Detection/) | A lightweight and highly accurate model that detects synthetic voices and audio clones by analyzing their unique "voiceprint" using MFCCs. |
| **Text Misinformation** | (https://github.com/Aditya5191/DEEPFAKE_DETECTION/tree/main/text_modality(misinformation)) | A hybrid model using stylistic and semantic analysis to determine if text was written by an LLM. Its logic is served via our main backend API. |
| **Backend** | [`./Backend/`](./Backend/) | The central nervous system of the platform. A Python-based API that handles requests, interfaces with Google Cloud services, and serves results. |
| **Frontend** | [`./Frontend/`](./Frontend/) | The user-facing web application (e.g., built in React/Vue) that provides a rich, interactive interface for uploading and analyzing content. |
| **Web Extension** | [`./Web-Extension/`](./Web-Extension/) | A powerful browser extension that brings Parallax's capabilities directly into the user's browsing experience for seamless, real-time protection. |

---

## 🏆 Coding Quality & Best Practices

We adhere to a high standard of software engineering to ensure our solution is robust, maintainable, and scalable.
* **Modular Design**: Each component is self-contained, allowing for independent testing and deployment without affecting the rest of the system.
* **Clean Code & Documentation**: Code is well-commented, and every module has its own detailed `README.md`, ensuring clarity and ease of understanding.
* **Version Control**: We follow standard Git practices, using meaningful commit messages and branching strategies to maintain a clean and comprehensible project history.
* **Dependency Management**: Each component has its own `requirements.txt` or `package.json` to ensure reproducible environments.

---

## 🚀 Getting Started

To explore or run the full Parallax platform, please follow the setup instructions within each component's dedicated `README.md`, starting with the Backend.

1.  Clone the repository:
    ```bash
    git clone [https://github.com/your-username/Parallax.git](https://github.com/your-username/Parallax.git)
    cd Parallax
    ```
2.  Navigate to the `Backend/` directory and follow its setup guide to deploy the core API.
3.  Proceed to the `Frontend/` and `Web-Extension/` directories to set up the user-facing components.

---

## 📜 License

This project is licensed under the **MIT License**.
