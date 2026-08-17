# 🌿 AI-Based Employee Wellness Management Platform

An **AI-powered Employee Wellness Management Platform** designed to help employees track, understand, and improve their emotional and overall wellness while providing managers with meaningful, data-driven wellness insights.

The platform combines **Natural Language Processing (NLP), sentiment analysis, emotion detection, AI-powered wellness chat, facial emotion recognition, daily wellness tracking, and weekly analytics** into a single platform.

---

## 📌 Overview

Employee well-being has a direct impact on productivity, engagement, and workplace satisfaction. Traditional employee management systems mainly focus on attendance, tasks, and performance, but often overlook emotional and mental well-being.

This platform provides a dedicated wellness environment where employees can:

* Track their daily mood
* Write personal journal entries
* Analyze emotions using AI
* Record stress, sleep, and workload
* Interact with an AI wellness chatbot
* Analyze emotions from facial expressions
* View personal wellness trends
* Generate weekly wellness reports

Managers can access employee-level wellness insights and monitor recent mood information to better understand overall team wellness.

---

## ✨ Key Features

### 👤 Employee Features

#### 🔐 Secure Authentication

The platform provides secure user authentication with:

* Employee and Manager roles
* Password hashing using **bcrypt**
* JWT-based authentication
* Email verification using OTP
* Password reset using OTP
* Role-based access control

Passwords are never stored directly. They are converted into secure bcrypt hashes before being stored in the database. JWT tokens contain the user's ID, username, email, role, and expiration information.

---

### 😊 Daily Mood Tracking

Employees can select their current mood using a simple mood picker.

Available mood labels include:

* Amazing
* Happy
* Normal
* Sad
* Angry

Manual mood selections are stored separately from AI-generated NLP results.

---

### 📔 AI-Powered Journaling

Employees can write about their daily experiences, feelings, or workplace situations.

The journal text is processed through a multilingual NLP pipeline to identify:

* Sentiment
* Emotion
* Emotion confidence
* Compound sentiment score
* Positive score
* Negative score
* Neutral score
* Detected language

Past journal entries are also stored and displayed with their corresponding analysis results.

---


### NLP Technologies

* `ftfy` — text normalization
* `langdetect` — language detection
* `stopwordsiso` — multilingual stopword filtering
* `deep-translator` — translation
* `spaCy` — NLP processing and lemmatization
* `VADER` — sentiment analysis
* Hugging Face Transformers — emotion classification

The application includes language mappings for languages such as English, Telugu, Hindi, Tamil, Kannada, Malayalam, Marathi, Bengali, Gujarati, French, German, Spanish, Arabic, Chinese, Japanese, Korean, and Russian.

---

## 📊 Sentiment Analysis

VADER is used to calculate sentiment information from the processed text.

The system stores:

* Positive score
* Negative score
* Neutral score
* Compound score

The sentiment result is mapped to application-level moods:

```text
Positive  → Happy
Neutral   → Normal
Negative  → Sad
```

---

## 🤖 AI Emotion Detection

The platform uses a fine-tuned BERT emotion model:

```text
bhadresh-savani/bert-base-go-emotion
```

The model produces emotion scores, and the application maps the GoEmotions predictions into the application's emotion categories.

The highest-scoring application emotion becomes the detected emotion, while its normalized score is used as the confidence value.

---

## 💬 AI Wellness Chatbot

The platform includes an AI-powered wellness chatbot that provides a supportive conversational environment.

Employees can enter messages such as:

```text
"I am feeling stressed because of my workload."
```

The chatbot processes the message and generates a supportive response.

The chatbot uses:

```text
Qwen/Qwen2.5-0.5B-Instruct
```

The recent conversation history is passed to the backend so that the chatbot can maintain conversational context.

> **Note:** The wellness chatbot is designed as a supportive wellness feature and is not a replacement for professional medical or psychological care.

---

## 📷 Facial Emotion Recognition

The platform also provides an optional face-based emotion analysis feature.

The employee can:

1. Open the Face Recognition section
2. Capture an image using the camera
3. Select **Analyze Face**
4. The system analyzes the facial expression
5. The dominant emotion is displayed
6. The model's confidence percentage is shown

## The implementation uses **DeepFace** for facial emotion analysis.

## 🌱 Daily Wellness Tracking

Employees can separately record:

* Stress level: `0–10`
* Sleep hours
* Workload:

  * Low
  * Medium
  * High
  * Not recorded

These values are stored separately from journal entries, so saving daily wellness information does not automatically create a journal entry.

---

## 📈 Personal Wellness Dashboard

The personal dashboard provides visual insights into an employee's wellness history.

It can display:

* Mood trends
* Emotion trends
* Sentiment analysis
* Wellness score trends
* Average stress
* Average sleep
* Sleep consistency
* High workload days
* Emotion distribution
* Sentiment distribution

The application generates a **Wellness Score Trend** over time and displays detailed wellness metrics.

---

## 📅 Weekly Wellness Report

The platform generates a holistic **7-day wellness assessment** based on available:

* Mood data
* Journal/NLP results
* Stress
* Sleep
* Workload
* Journal consistency

Missing values are not automatically treated as zero. The scoring system uses only the components for which actual data is available.

### Weekly Report Includes

* Weekly wellness score
* Most common mood
* Most common detected emotion
* Average stress
* Average sleep
* Average compound sentiment
* Wellness trend
* Personalized recommendations
* Achievements
* Graphs and visual analytics

The system can also generate a PDF wellness report using **ReportLab**.

---

## 🏆 Wellness Achievements

The platform provides achievement-style feedback based on wellness activity.

Examples include:

* 🏆 7-Day Wellness Tracker
* 😊 Positive Week
* 💪 Consistent Journal Writer
* 🌟 Healthy Work-Life Balance
* 🌱 Keep Building Your Wellness Record

These achievements are generated from actual wellness statistics.

---

# 👨‍💼 Manager Dashboard

Managers have access to employee-level wellness information.

The manager functionality includes:

* Viewing employee wellness information
* Viewing recent employee mood entries
* Monitoring employee sentiment
* Viewing detected emotions
* Viewing emotion confidence
* Viewing recent wellness trends

The database specifically provides manager queries for retrieving employee mood logs and the latest mood of each employee.

This helps managers identify general wellness patterns and support healthier workplace practices.

---

# 🏗️ System Architecture

The platform follows a layered architecture:

```text
                    ┌─────────────────────┐
                    │      Employee       │
                    │       Manager       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     Streamlit UI    │
                    │  Frontend / Pages   │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │      FastAPI        │
                    │      Backend        │
                    └──────────┬──────────┘
                               │
             ┌─────────────────┼──────────────────┐
             │                 │                  │
             ▼                 ▼                  ▼
       Authentication       NLP Engine        AI Chatbot
       bcrypt + JWT       VADER + BERT          Qwen
             │                 │                  │
             └─────────────────┼──────────────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     PostgreSQL      │
                    │      Database       │
                    └─────────────────────┘
```

The application runs Streamlit on port `8501`, while the FastAPI backend runs on port `8000`.

---

# 🛠️ Technology Stack

## Frontend

* Python
* Streamlit
* HTML/CSS customization
* Matplotlib

## Backend

* FastAPI
* Uvicorn
* Python
* Requests

## Database

* PostgreSQL
* Psycopg2

## Authentication & Security

* bcrypt
* PyJWT
* OTP verification
* Gmail SMTP
* Environment variables

## Artificial Intelligence & NLP

* Hugging Face Transformers
* BERT GoEmotions
* Qwen 2.5
* VADER Sentiment
* spaCy
* langdetect
* deep-translator
* stopwordsiso
* ftfy
* emoji

## Computer Vision

* DeepFace
* OpenCV

## Reporting & Visualization

* Matplotlib
* ReportLab
* Pandas

## Deployment / Tunneling

* Google Colab
* ngrok

The project dependencies include Streamlit, FastAPI, PostgreSQL drivers, PyJWT, bcrypt, NLP libraries, Transformers, Torch, DeepFace, OpenCV, Pandas, Matplotlib, and ReportLab.

---



# 🔄 Application Flow

```text
                  START
                    │
                    ▼
              Signup / Login
                    │
          ┌─────────┴─────────┐
          │                   │
       Employee             Manager
          │                   │
          ▼                   ▼
   Employee Dashboard   Manager Dashboard
          │
    ┌─────┼────────┬─────────────┐
    │     │        │             │
    ▼     ▼        ▼             ▼
  Mood  Journal  Wellness      Face
 Tracker Analysis  Tracking   Analysis
    │     │        │             │
    └─────┴────────┴─────────────┘
                    │
                    ▼
              AI/NLP Analysis
                    │
        ┌───────────┼────────────┐
        ▼           ▼            ▼
    Sentiment     Emotion      Confidence
        │           │            │
        └───────────┼────────────┘
                    ▼
             Wellness Database
                    │
                    ▼
             Personal Dashboard
                    │
                    ▼
             Weekly Wellness
                  Report
                    │
                    ▼
            AI Recommendations
```

---

# ⚙️ Installation

## 1. Clone the Repository

```bash
git clone <YOUR_REPOSITORY_URL>
cd <YOUR_PROJECT_FOLDER>
```

## 2. Install Dependencies

```bash
pip install streamlit psycopg2-binary PyJWT bcrypt python-dotenv email-validator pyngrok fastapi uvicorn python-multipart requests langdetect ftfy emoji deep-translator vaderSentiment spacy pandas matplotlib reportlab transformers accelerate torch stopwordsiso deepface opencv-python-headless
```

Install the spaCy model:

```bash
python -m spacy download xx_sent_ud_sm
```

---

# 🔑 Environment Variables

Create a `.env` file:

```env
DB_HOST=your_database_host
DB_PORT=5432
DB_NAME=your_database_name
DB_USER=your_database_user
DB_PASSWORD=your_database_password

JWT_SECRET=your_random_secret
JWT_ALGORITHM=HS256
JWT_EXPIRY_MINUTES=60

SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_EMAIL=your_email@gmail.com
SMTP_APP_PASSWORD=your_gmail_app_password

OTP_EXPIRY_MINUTES=10
```

The project uses PostgreSQL with SSL enabled for the database connection.

---



# 📊 Example AI Analysis

### Input

```text
I have been feeling very stressed because of my workload.
```

### Processing

```text
Input Text
   ↓
Language Detection
   ↓
Text Cleaning
   ↓
Tokenization
   ↓
Lemmatization
   ↓
VADER Sentiment
   ↓
BERT Emotion Detection
```

### Output

```text
Sentiment: Negative
Emotion: Stress
Confidence: Model-dependent
Compound Score: Calculated by VADER
```

The resulting analysis is stored in the employee's wellness history.

---


```

> Never commit `.env`, database passwords, SMTP credentials, JWT secrets, or API tokens to GitHub.

---

# 🎯 Project Objectives

The main objectives of this project are:

1. Provide employees with an easy-to-use wellness tracking platform.
2. Use AI to analyze employee-written feedback and journal entries.
3. Detect sentiment and emotions from multilingual text.
4. Allow employees to monitor stress, sleep, workload, and mood.
5. Provide supportive AI-based wellness conversations.
6. Generate meaningful wellness analytics.
7. Provide managers with aggregated employee wellness insights.
8. Generate personalized weekly wellness reports.
9. Encourage consistent wellness tracking through achievements and recommendations.

---



# ⚠️ Privacy & Responsible AI

Employee wellness information is sensitive and should be handled responsibly.

The platform should be used to:

* Support employee well-being
* Identify general wellness trends
* Encourage healthy workplace practices
* Provide supportive insights

AI-generated emotion and sentiment results should **not be treated as medical diagnoses or definitive assessments of an employee's mental health**.

The weekly AI summary is explicitly instructed to use actual stored values and avoid inventing missing values or diagnosing employees.


# 👩‍💻 Project

**AI-Based Employee Wellness Management Platform**

### Core Technologies

`Python` • `Streamlit` • `FastAPI` • `PostgreSQL` • `Bcrypt` • `JWT` • `NLP` • `VADER` • `BERT` • `Qwen` • `DeepFace` • `Transformers`

---

## 🌿 Conclusion

The AI-Based Employee Wellness Management Platform combines **secure authentication, multilingual NLP, sentiment analysis, emotion detection, facial emotion recognition, AI wellness conversation, daily wellness tracking, analytics, and weekly reporting** into one integrated system.

The goal is to transform employee wellness from a simple periodic survey into a **continuous, AI-assisted, data-driven wellness experience**.
