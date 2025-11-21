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
📂 Project Structure
The codebase is organized to separate data processing steps from the inference logic.

Bash

├── 📁 jsons/               # Staging area for transcribed text data
├── 📄 embeddings.joblib    # The "Brain" - Serialized vector database
├── 📄 video_to_mp3.py      # STEP 1: Extract audio from video
├── 📄 mp3_to_json.py       # STEP 2: Transcribe audio using OpenAI Whisper/AssemblyAI
├── 📄 preprocess_json.py   # STEP 3: Clean text & generate embeddings
├── 📄 process_incoming.py  # STEP 4: Main Interface for asking questions
├── 📄 prompt               # System prompt engineering file
└── 📄 response             # Output log for the last generated answer
🚀 Getting Started
Prerequisites
Python 3.8+

FFmpeg (for video processing)

Installation
Clone the repository

Bash

git clone [https://github.com/devidattamishra45/RAG-based-AI-teaching-Assistant.git](https://github.com/devidattamishra45/RAG-based-AI-teaching-Assistant.git)
cd RAG-based-AI-teaching-Assistant
Install dependencies

Bash

pip install -r requirements.txt
(Note: Ensure libraries like joblib, openai, moviepy or torch are installed)

⚡ Usage Guide
This pipeline is designed to be run sequentially when adding new course material.

1. Ingest Data
Place your lecture video in the project root.

Bash

# Extract audio
python video_to_mp3.py

# Transcribe to text
python mp3_to_json.py

# Build the Knowledge Base (Embeddings)
python preprocess_json.py
2. Ask a Question
Once the embeddings.joblib file is ready, you can query the system:

Bash

python process_incoming.py
The script will prompt you for a question and return the answer based strictly on the course material.

🛠️ Tech Stack
Core: Python

Data Processing: Joblib, JSON

AI/ML: Retrieval Augmented Generation (RAG) technique

NLP: OpenAI / LangChain (Assumed)

## 🏗️ Architecture & Workflow

This project follows a linear ETL (Extract, Transform, Load) pipeline followed by a RAG query loop.

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
