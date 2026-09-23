# 🎓 SnapClass — AI-Powered Attendance System

> **Smart attendance powered by Facial Recognition + Voice Recognition**

SnapClass is a full-stack AI-powered attendance management system designed to replace slow and error-prone manual roll calls.

Teachers can record attendance for an entire classroom using a **single photo or a short voice recording**, while students can register using **FaceID** and track their personal attendance history.

The application combines **AI/ML pipelines, relational database management, authentication, and a modern Streamlit interface** into one deployable system.

### 🚀 Live Project

* 🌐 **Live Application:** [Open SnapClass](https://snapclass-wjyzofaajafvxeegufx6ch.streamlit.app/)
* 🎨 **Landing Page:** [Visit SnapClass Landing Page](https://ai-attendance-project-landing-alpha.vercel.app/)
* 💻 **Source Code:** [GitHub Repository](https://github.com/Himanshu1425/snapclass)

---

## ✨ Key Features

### 👨‍🏫 Teacher Portal

* 🔐 Secure teacher registration and login
* 🔒 Password hashing using **bcrypt**
* 📚 Create and manage multiple subjects
* 🔗 Generate unique subject join codes and shareable links
* 📸 **Photo-based attendance** using facial recognition
* 🎙️ **Voice-based attendance** using speaker recognition
* 👥 Automatically identify enrolled students
* ✏️ Review and edit attendance results before confirmation
* 📊 View attendance history and subject-wise statistics

### 👨‍🎓 Student Portal

* 📷 FaceID-based registration using webcam capture
* ⚡ Automatic login using facial recognition
* 🎙️ Optional voice profile enrollment
* 🔗 Join subjects using codes or shared links
* 📚 View enrolled subjects
* 📈 Track personal attendance history

---

## 🤖 AI Attendance Pipeline

### 📸 Facial Recognition

SnapClass processes classroom images through a facial-recognition pipeline:

```text
Classroom Photo
      ↓
Face Detection
      ↓
128-D Face Embeddings
      ↓
SVM Classification
      ↓
Student Identification
      ↓
Attendance Result
```

The system uses facial embeddings together with an **SVM classifier** to identify enrolled students.

### 🎙️ Voice Recognition

Voice attendance follows a separate speaker-recognition pipeline:

```text
Voice Recording
      ↓
Audio Processing
      ↓
Speaker Embedding
      ↓
Voice Matching
      ↓
Student Identification
      ↓
Attendance Result
```

This allows teachers to record attendance through short voice clips in addition to classroom photographs.

---

## 🛠️ Technology Stack

| Layer                     | Technologies                    |
| ------------------------- | ------------------------------- |
| **Application Framework** | Streamlit                       |
| **Programming Language**  | Python                          |
| **Database**              | Supabase / PostgreSQL           |
| **Face Recognition**      | dlib, face_recognition_models   |
| **Face Classification**   | scikit-learn, SVM               |
| **Face Representation**   | 128-dimensional face embeddings |
| **Voice Processing**      | librosa                         |
| **Speaker Recognition**   | Resemblyzer                     |
| **Authentication**        | bcrypt                          |
| **Deployment**            | Streamlit Community Cloud       |
| **Version Control**       | Git, GitHub                     |

---

## 🏗️ System Architecture

```text
                        ┌─────────────────────┐
                        │      SnapClass      │
                        │    Streamlit App    │
                        └──────────┬──────────┘
                                   │
                ┌──────────────────┴──────────────────┐
                │                                     │
        ┌───────▼────────┐                   ┌────────▼────────┐
        │ Teacher Portal │                   │ Student Portal  │
        └───────┬────────┘                   └────────┬────────┘
                │                                     │
        ┌───────▼─────────────────────────────────────▼───────┐
        │                  Attendance Engine                   │
        └───────────────┬───────────────────┬─────────────────┘
                        │                   │
                ┌───────▼───────┐   ┌──────▼────────┐
                │ Face Pipeline │   │ Voice Pipeline│
                │  Face + SVM   │   │   Embeddings  │
                └───────┬───────┘   └──────┬────────┘
                        │                   │
                        └─────────┬─────────┘
                                  │
                         ┌────────▼────────┐
                         │ Supabase /      │
                         │ PostgreSQL      │
                         └─────────────────┘
```

---

## 📂 Project Structure

```text
snapclass/
│
├── app.py                         # Streamlit application entry point
├── requirements.txt               # Python dependencies
├── .gitignore
│
├── .streamlit/
│   └── secrets.toml               # Local secrets - not committed
│
└── src/
    │
    ├── ui/
    │   └── base_layout.py         # Global UI styling
    │
    ├── database/
    │   ├── config.py              # Supabase configuration
    │   └── db.py                  # Database operations
    │
    ├── pipelines/
    │   ├── face_pipeline.py       # Face detection + classification
    │   └── voice_pipeline.py      # Voice embedding + matching
    │
    ├── screens/
    │   ├── home_screen.py
    │   ├── teacher_screen.py
    │   └── student_screen.py
    │
    └── components/
        ├── header.py
        ├── footer.py
        ├── subject_card.py
        └── dialog_*.py            # Subject & attendance dialogs
```

---

## 🗄️ Database Design

SnapClass uses **Supabase PostgreSQL** for persistent application data.

### Core Tables

| Table              | Purpose                                   |
| ------------------ | ----------------------------------------- |
| `teachers`         | Teacher accounts and authentication data  |
| `students`         | Student profiles and biometric embeddings |
| `subjects`         | Subjects/classes created by teachers      |
| `subject_students` | Student-subject enrollment relationship   |
| `attendance_logs`  | Attendance records and timestamps         |

### Relationship Overview

```text
Teachers
   │
   └──< Subjects
          │
          └──< Subject_Students >── Students
                                      │
                                      └──< Attendance_Logs
```

---

## 🔐 Security & Secrets

Sensitive credentials are intentionally kept outside the repository.

Local development uses:

```text
.streamlit/secrets.toml
```

Example:

```toml
SUPABASE_URL = "your-supabase-project-url"
SUPABASE_KEY = "your-supabase-publishable-key"
```

> ⚠️ Never commit real credentials, API keys, passwords, or secrets to GitHub.

---

## 🚀 Deployment

The production application is deployed using **Streamlit Community Cloud**.

### Deployment Flow

```text
Local Development
       ↓
     Git
       ↓
    GitHub
       ↓
Streamlit Community Cloud
       ↓
   Live SnapClass
```

Changes pushed to the `main` branch can trigger an updated deployment.

---

## 💻 Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/Himanshu1425/snapclass.git
cd snapclass
```

### 2. Create a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Streamlit secrets

Create:

```text
.streamlit/secrets.toml
```

Add your own Supabase credentials:

```toml
SUPABASE_URL = "your-supabase-project-url"
SUPABASE_KEY = "your-supabase-publishable-key"
```

### 5. Start the application

```bash
streamlit run app.py
```

The application will be available at:

```text
http://localhost:8501
```

---

## 🎯 Project Goals

SnapClass was built to explore the practical integration of:

* Artificial Intelligence
* Machine Learning
* Computer Vision
* Speaker Recognition
* Full-Stack Application Development
* Authentication
* Relational Database Design
* Cloud Deployment

The project focuses on turning individual AI/ML pipelines into a **usable end-to-end application** rather than treating them as isolated models.

---

## 👤 Author

### Himanshu Raj

Final-year Computer Science Engineering student interested in **Software Engineering, AI/ML, and Generative AI**.

* GitHub: [Himanshu1425](https://github.com/Himanshu1425)
* LinkedIn: [Connect with Himanshu](https://www.linkedin.com/)

---

## ⭐ Support

If you find the project interesting, consider giving the repository a ⭐ on GitHub.

**Built with Python, AI/ML, Streamlit, and Supabase.**

