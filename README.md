# 🛡️ Parallax: An AI-Powered Multi-Modal Misinformation Detection Platform

**Parallax is a state-of-the-art, end-to-end ecosystem designed to combat digital misinformation by providing forensic-grade analysis of content across all major media formats. Powered by a suite of custom deep learning models and seamlessly integrated with Google Cloud AI, this project delivers a robust, scalable, and transparent solution for verifying the authenticity of the digital world.**

This repository is the central hub for all components of the Parallax project, from the backend APIs and advanced AI models to the user-facing frontend and browser extension.

http://104.197.87.77:8080/
---

# 🏛️ Technical Architecture & Google Cloud Integration
Parallax is architected as a modern, cloud-native application, leveraging a microservice-inspired approach where each detection modality can be scaled and updated independently. The entire platform is built upon the powerful, scalable, and secure infrastructure of Google Cloud to ensure performance and reliability.

## How We Use Google Cloud to Deliver Value
Our use of Google Cloud is focused on two key areas: powering our intelligent analysis and ensuring a seamless user experience.

## 🧠 For Intelligent Text Analysis
We combine Google's powerful AI services to create an instant, authoritative verification engine for our users.

### Gemini, Fact Checker, & Search APIs: 
This trio forms our real-time verification engine.
Gemini API first pinpoints the central claim within a piece of text.
The Fact Checker and Search APIs then instantly validate that claim against trusted global sources and up-to-date search results.

### User Value: 
This delivers authoritative, real-time answers directly to the user, moving beyond a simple "fake" label to provide actual, verified information.

## ⚙️ For Robust Deployment & Performance
We use Google's infrastructure to ensure Parallax is always fast, secure, and reliable.

### Google Compute Engine (VM Instances & Load Balancer): 
This is our high-performance engine.
We use GCE to host our custom AI models (rPPG, image detectors, etc.) and our n8n agentic workflows.
The Load Balancer ensures we can handle user demand efficiently by managing our VM instances, scaling resources, and even shutting down instances when demand is low to maintain cost-effectiveness.

### User Value: 
This guarantees fast, real-time analysis and a smooth, uninterrupted service that is always responsive.

### Google Cloud Storage & Docker: 
This is the backbone of our application's stability and security.
We use Google Cloud Storage buckets for common, secure storage of our model artifacts and user-uploaded media across multiple instances.
The entire application is containerized with Docker, ensuring consistency from development to deployment on Google Cloud.

### User Value: 
This provides a secure and dependable experience. Users can trust that their data is handled safely and that the platform performs reliably every single time.

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
