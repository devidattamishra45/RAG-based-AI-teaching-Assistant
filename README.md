<div align="center">

# 🤖 AI Teaching Assistant (RAG Pipeline)

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![AI](https://img.shields.io/badge/GenAI-RAG-FF4B4B?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Prototype-success?style=for-the-badge)

<h3>A Full-Stack Data Pipeline transforming video lectures into an interactive Knowledge Base.</h3>

[View Demo](#) · [Report Bug](../../issues) · [Request Feature](../../issues)

</div>

---

## 📖 About The Project

> **Problem:** Students spend hours scrubbing through long video lectures to find specific concepts.  
> **Solution:** This project automates the extraction of knowledge from video content, allowing students to "chat" with their course material.

This is a **Retrieval-Augmented Generation (RAG)** system built for the University AI Course. Unlike standard chatbots, this assistant is grounded in ground-truth data from course videos. It ingests video files, transcribes audio, generates vector embeddings, and retrieves precise context to answer student queries accurately.

### 🌟 Key Features
* **📹 Automated Video Processing:** Extracts audio tracks from lecture recordings (`video_to_mp3.py`).
* **🗣️ Speech-to-Text Pipeline:** Converts audio data into structured JSON transcripts (`mp3_to_json.py`).
* **🧠 Vector Embeddings:** Uses `joblib` to store semantic embeddings of the course content for O(1) retrieval.
* **🔍 Context-Aware Answers:** Fetches the exact timestamp/context relevant to the user's question before generating a response.

---

```mermaid
graph TD;
    A[Raw Course Video] -->|video_to_mp3.py| B(Audio File .mp3);
    B -->|mp3_to_json.py| C(Transcripts .json);
    C -->|preprocess_json.py| D{Vector Store};
    D -->|Saved as| E[embeddings.joblib];
    
    User[Student Query] -->|process_incoming.py| F[Retrieve Context];
    E --> F;
    F -->|Context + Query| G[LLM / AI Model];
    G --> H[Final Answer];
