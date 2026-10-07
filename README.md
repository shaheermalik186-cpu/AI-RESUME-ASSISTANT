# AI-RESUME-ASSISTANT
# ATS Resume Checker

A Streamlit app that scores a resume for ATS (Applicant Tracking System) compatibility and tells you how to improve it, using Google's Gemini Flash model.

## Features

- Upload a resume as **PDF, DOCX or TXT** (max 5 MB)
- Optional **job description** field for a targeted keyword and match score
- **ATS score out of 100** with a weighted category breakdown
- Strengths, **prioritised improvements** (High / Medium / Low) with rewrite examples, and **missing keywords**
- Instant rule-based checks: contact info, key sections, length, bullets, quantified results
- Download the full report as Markdown

## How the score works

The AI scores each category from 0 to 100, and the app calculates the final score in code as a weighted average, so it is consistent and transparent.

| Category | Weight |
|---|---|
| Keywords & Relevance | 25 |
| ATS Formatting | 20 |
| Experience & Impact | 20 |
| Section Completeness | 15 |
| Skills | 10 |
| Clarity & Grammar | 10 |
| Job Description Match (only if a job description is pasted) | 25 |

> The score is an AI-based estimate. Real ATS products differ, so use it as guidance, not a guarantee.

## Run locally

1. Install Python 3.10 or newer.
2. Get a free Gemini API key at <https://aistudio.google.com/apikey>.
3. In the project folder:

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

4. Provide the key, either way:
   - paste it into the app sidebar when it runs, or
   - set an environment variable:
     - macOS/Linux: `export GEMINI_API_KEY="your-key"`
     - Windows PowerShell: `$env:GEMINI_API_KEY="your-key"`
   - or create `.streamlit/secrets.toml` containing `GEMINI_API_KEY = "your-key"`

5. Start the app:

```bash
streamlit run app.py
```

## Configuration

| Setting | How | Default |
|---|---|---|
| API key | sidebar, `GEMINI_API_KEY` env var, or Streamlit secret | none |
| Model | sidebar dropdown, or `GEMINI_MODEL` env var | `gemini-3.5-flash` |

If Google renames or retires a model, change `MODEL_CHOICES` near the top of `app.py`.

## Deploy on Streamlit Community Cloud

1. Push this folder to a GitHub repository (`app.py`, `requirements.txt`, `README.md` in the repo root).
2. Go to <https://share.streamlit.io> and sign in with GitHub.
3. Click **Create app**, choose your repository, branch `main`, and main file path `app.py`.
4. Open **Advanced settings**, and in **Secrets** add:

```toml
GEMINI_API_KEY = "your-key"
```

5. Click **Deploy**.

Never commit your API key. Add `.streamlit/secrets.toml` to a `.gitignore` file.

## Privacy

The text of the uploaded resume is sent to the Gemini API for analysis. The app does not save uploads or reports.

## Project files

- `app.py` - the Streamlit app
- `requirements.txt` - Python dependencies
- `README.md` - this file
