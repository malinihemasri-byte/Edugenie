# EduGenie 🧞‍♂️📚

EduGenie is an intelligent, AI-powered learning assistant built with **Python**, **FastAPI**, and the **Google Gemini API**. Designed to empower students, educators, and lifelong learners, EduGenie simplifies complex subjects, answers academic inquiries, generates interactive self-assessment quizzes, summarizes extensive study materials, and crafts personalized multi-stage learning roadmaps.

EduGenie combines a robust, modular RESTful API backend with a clean and responsive web interface for rapid, seamless interaction.

---

## 📑 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Architecture & Structure](#-project-architecture--structure)
- [Prerequisites](#-prerequisites)
- [Installation & Setup](#-installation--setup)
- [Environment Configuration](#-environment-configuration)
- [Running the Application](#-running-the-application)
- [API Documentation & Endpoints](#-api-documentation--endpoints)
  - [Interactive Swagger / OpenAPI](#interactive-swagger--openapi)
  - [Endpoints Overview](#endpoints-overview)
  - [Request & Response Examples](#request--response-examples)
- [Running Tests](#-running-tests)
- [Configuration Reference](#-configuration-reference)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

- 💬 **Academic Q&A (`/qa`)**: Get direct, accurate, and student-friendly explanations for academic and conceptual questions.
- 💡 **Concept Simplification (`/explain`)**: Break down intricate concepts into simple definitions, underlying mechanics, real-world analogies, and revision summaries.
- 📝 **Automated Quiz Generation (`/quiz`)**: Automatically extract exactly 3 multiple-choice questions (with 4 plausible options, answers, and explanations) from any provided reading passage or notes.
- 📋 **Smart Summarization (`/summarize`)**: Condense lengthy lecture notes, chapters, or articles into concise, structured bullet points while preserving essential definitions and conclusions.
- 🗺️ **Personalized Learning Paths (`/learn/recommendations`)**: Generate end-to-end, structured roadmaps (Beginner $\rightarrow$ Intermediate $\rightarrow$ Advanced) complete with timelines, core topics, practice activities, resource types, and study tips.
- 🌐 **Built-in Web Interface**: Fast, modern frontend rendered with Jinja2 templates and vanilla CSS/JS for distraction-free learning.
- 🛡️ **Robust Error Handling**: Structured error responses and fallback validations for Gemini API calls and JSON payloads.

---

## 🛠️ Tech Stack

- **Backend Framework**: [FastAPI](https://fastapi.tiangolo.com/) (v0.116+)
- **ASGI Server**: [Uvicorn](https://www.uvicorn.org/) (Standard)
- **AI / LLM Integration**: [Google GenAI SDK](https://github.com/googleapis/python-genai) (`google-genai` v1.30+) powered by `gemini-3.8-flash`
- **Data Validation & Settings**: [Pydantic v2](https://docs.pydantic.dev/) & [python-dotenv](https://github.com/theskumar/python-dotenv)
- **Frontend / Templating**: [Jinja2](https://palletsprojects.com/p/jinja/), HTML5, Vanilla CSS3 & Modern JavaScript
- **Testing**: [Pytest](https://docs.pytest.org/) & [HTTPX](https://www.python-httpx.org/) (FastAPI TestClient)
- **Language**: Python 3.11+

---

## 📂 Project Architecture & Structure

The repository is organized cleanly with separation of concerns between API routing, business logic modules, external AI services, and web presentation assets:

```text
Edugenie/
├── EduGenie/
│   ├── .env.example              # Template for environment variables
│   ├── .gitignore                # Git ignore rules for EduGenie directory
│   ├── config.py                 # Application configuration & settings loader
│   ├── main.py                   # FastAPI app entry point, routing & middleware
│   ├── requirements.txt          # Python dependencies
│   ├── schemas.py                # Pydantic request/response data models
│   ├── modules/                  # Specialized AI educational modules
│   │   ├── __init__.py
│   │   ├── explanation.py        # Concept simplification logic
│   │   ├── learning_path.py      # Multi-stage learning roadmap generation
│   │   ├── qna.py                # Academic Q&A processing
│   │   ├── quiz.py               # MCQ quiz generator with JSON validation
│   │   └── summary.py            # Educational text summarization
│   ├── services/                 # External service wrappers
│   │   ├── __init__.py
│   │   └── gemini_service.py     # Google Gemini API client & JSON parser
│   ├── static/                   # Static frontend assets
│   │   ├── app.js                # Frontend client-side logic & API calls
│   │   └── style.css             # UI styling & responsive layout
│   ├── templates/                # Jinja2 templates
│   │   └── index.html            # Main single-page web interface
│   └── tests/                    # Automated test suite
│       └── test_health.py        # Health check and homepage tests
├── README.md                     # Repository documentation
└── .gitignore                    # Root-level Git ignore rules
```

---

## 📋 Prerequisites

Before setting up EduGenie, ensure you have:

1. **Python 3.11 or higher** installed ([python.org](https://www.python.org/downloads/)).
2. A **Google Gemini API Key**. You can generate a free API key at [Google AI Studio](https://aistudio.google.com/).
3. **Git** installed on your system.

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/malinihemasri-byte/Edugenie.git
cd Edugenie
```

### 2. Navigate to the Application Directory

```bash
cd EduGenie
```

### 3. Install Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

---

### 4. Create and Activate a Virtual Environment

- **On Windows (PowerShell):**
  ```powershell
  python -m venv .venv
  .venv\Scripts\Activate.ps1
  ```

- **On Windows (Command Prompt):**
  ```cmd
  python -m venv .venv
  .venv\Scripts\activate.bat
  ```

- **On macOS / Linux:**
  ```bash
  python3 -m venv .venv
  source .venv/bin/activate
  ```



## ⚙️ Environment Configuration

1. In the `EduGenie/` folder, copy the example environment file:
   ```bash
   # On Windows (PowerShell)
   Copy-Item .env.example .env

   # On Linux / macOS
   cp .env.example .env
   ```

2. Open `.env` and fill in your Gemini API key:
   ```env
   GEMINI_API_KEY=your_actual_gemini_api_key_here
   GEMINI_MODEL=gemini-3.8-flash
   APP_NAME=EduGenie
   ```

---

## 💻 Running the Application

Ensure your virtual environment is active and you are inside the `EduGenie/` directory:

```bash
uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

Once started:
- 🌐 **Web Interface**: Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in your browser.
- 📖 **Interactive API Docs (Swagger UI)**: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)
- 📑 **Alternative API Docs (ReDoc)**: [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc)

---

## 📡 API Documentation & Endpoints

### Interactive Swagger / OpenAPI
FastAPI automatically generates interactive OpenAPI documentation. Visit `http://127.0.0.1:8000/docs` to test all endpoints directly from your browser.

### Endpoints Overview

| Method | Endpoint | Description | Request Body | Response Model |
| :--- | :--- | :--- | :--- | :--- |
| `GET` | `/` | Web UI single-page interface | None | `HTMLResponse` |
| `GET` | `/health` | Service health status check | None | `{"status": "ok", "service": "EduGenie"}` |
| `POST` | `/qa` | Answer academic questions | `{"text": "string"}` | `TaskResponse` |
| `POST` | `/explain` | Simplify and explain concepts | `{"text": "string"}` | `TaskResponse` |
| `POST` | `/quiz` | Generate 3-question MCQ quiz | `{"text": "string"}` | `TaskResponse` |
| `POST` | `/summarize` | Summarize educational text | `{"text": "string"}` | `TaskResponse` |
| `POST` | `/learn/recommendations` | Generate personalized learning roadmap | `{"text": "string"}` | `TaskResponse` |

---

### Request & Response Examples

#### 1. Q&A (`POST /qa`)
**Request:**
```bash
curl -X POST "http://127.0.0.1:8000/qa" \
     -H "Content-Type: application/json" \
     -d '{"text": "What is the difference between supervised and unsupervised learning?"}'
```

**Response:**
```json
{
  "task": "qa",
  "result": "Supervised learning uses labeled training data where the algorithm learns the relationship between input features and target labels..."
}
```

---

#### 2. Concept Explanation (`POST /explain`)
**Request:**
```bash
curl -X POST "http://127.0.0.1:8000/explain" \
     -H "Content-Type: application/json" \
     -d '{"text": "Recursion in computer science"}'
```

**Response:**
```json
{
  "task": "explain",
  "result": "1. Simple definition: Recursion is a programming technique where a function solves a problem by calling a smaller instance of itself.\n2. How it works: A recursive function has two parts: a base case that stops recursion and a recursive case that breaks down the task...\n3. Real-world example: Like Russian nesting dolls..."
}
```

---

#### 3. Quiz Generation (`POST /quiz`)
**Request:**
```bash
curl -X POST "http://127.0.0.1:8000/quiz" \
     -H "Content-Type: application/json" \
     -d '{"text": "Photosynthesis is the process used by plants to convert light energy into chemical energy. Chlorophyll absorbs sunlight, which drives the reaction between carbon dioxide and water to produce glucose and oxygen."}'
```

**Response:**
```json
{
  "task": "quiz",
  "result": {
    "questions": [
      {
        "question": "What pigment absorbs sunlight during photosynthesis?",
        "options": ["Carotenoid", "Chlorophyll", "Hemoglobin", "Melanin"],
        "correct_answer": "Chlorophyll",
        "explanation": "Chlorophyll is the primary pigment that captures light energy in plants."
      },
      {
        "question": "What are the primary products of photosynthesis?",
        "options": ["Glucose and oxygen", "Carbon dioxide and water", "Nitrogen and methane", "Lipids and ozone"],
        "correct_answer": "Glucose and oxygen",
        "explanation": "Light energy drives the conversion of CO2 and water into glucose and oxygen."
      },
      {
        "question": "What type of energy is light converted into during photosynthesis?",
        "options": ["Nuclear energy", "Kinetic energy", "Chemical energy", "Thermal energy"],
        "correct_answer": "Chemical energy",
        "explanation": "Light energy is converted into chemical energy stored in glucose molecules."
      }
    ]
  }
}
```

---

#### 4. Summarization (`POST /summarize`)
**Request:**
```bash
curl -X POST "http://127.0.0.1:8000/summarize" \
     -H "Content-Type: application/json" \
     -d '{"text": "Cloud computing is the on-demand delivery of IT resources over the Internet with pay-as-you-go pricing..."}'
```

**Response:**
```json
{
  "task": "summarize",
  "result": "- Cloud Computing: On-demand delivery of computing power, database storage, and applications over the Internet.\n- Pricing Model: Pay-as-you-go instead of buying physical data centers."
}
```

---

#### 5. Learning Path Recommendations (`POST /learn/recommendations`)
**Request:**
```bash
curl -X POST "http://127.0.0.1:8000/learn/recommendations" \
     -H "Content-Type: application/json" \
     -d '{"text": "FastAPI Web Development"}'
```

**Response:**
```json
{
  "task": "learn",
  "result": {
    "topic": "FastAPI Web Development",
    "goal": "Build robust, asynchronous REST APIs with Python and FastAPI",
    "stages": [
      {
        "level": "Beginner",
        "duration": "2 weeks",
        "topics": ["Python type hints", "FastAPI basics & routing", "Pydantic models"],
        "practice": ["Build a simple CRUD note-taking API", "Validate inputs with Pydantic"],
        "resources": ["Official FastAPI Tutorial", "Python Type Hints Guide"]
      },
      {
        "level": "Intermediate",
        "duration": "3 weeks",
        "topics": ["Dependency Injection", "Database ORM (SQLAlchemy)", "Authentication with JWT"],
        "practice": ["Implement user authentication and secure endpoints", "Connect to PostgreSQL"],
        "resources": ["FastAPI Advanced User Guide", "SQLAlchemy 2.0 Docs"]
      },
      {
        "level": "Advanced",
        "duration": "4 weeks",
        "topics": ["Background tasks", "WebSockets", "Docker containerization", "Testing with Pytest"],
        "practice": ["Deploy containerized FastAPI app with CI/CD", "Write full test suite"],
        "resources": ["Docker for Python Developers", "Pytest Testing Guide"]
      }
    ],
    "study_tips": [
      "Code along with official documentation examples",
      "Always inspect generated Swagger docs at /docs"
    ]
  }
}
```

---

## 🧪 Running Tests

EduGenie includes automated unit and integration tests using **Pytest** and FastAPI's `TestClient`.

To execute the test suite:

```bash
# Navigate to EduGenie directory if not already there
cd EduGenie

# Run tests
pytest

# Run tests with detailed verbose output
pytest -v
```

---

## ⚙️ Configuration Reference

All settings can be configured using environment variables or directly inside `EduGenie/.env`:

| Variable | Default Value | Description |
| :--- | :--- | :--- |
| `GEMINI_API_KEY` | *(None / Required)* | Google Gemini API key obtained from Google AI Studio |
| `GEMINI_MODEL` | `gemini-3.8-flash` | The Gemini model version used for generation |
| `APP_NAME` | `EduGenie` | Display name of the application |

---

## 🤝 Contributing

Contributions, issues, and feature requests are welcome!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
