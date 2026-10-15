# Cyber Incident Report Analyzer

A Flask web app that analyzes cyber incident report PDFs using classical NLP (no LLM).
It extracts IOCs, threat actors, MITRE ATT&CK techniques, a timeline, impact, response actions and
reporting gaps, then produces a templated summary report.

## Features
- PDF text extraction (PyMuPDF) with OCR fallback (Tesseract)
- Sentence segmentation and entity extraction with spaCy
- MITRE ATT&CK technique mapping using sentence-transformers and TF-IDF similarity
- Timeline reconstruction with dateparser
- Reports stored in MongoDB (GridFS for files)

## Requirements
- Python 3.10+
- MongoDB running locally on `mongodb://localhost:27017`
- [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) installed (for scanned PDFs)

## Setup
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
python -m spacy download en_core_web_sm
```

## Run
```bash
python app.py
```
Open http://127.0.0.1:5000

On first run the app downloads the `all-MiniLM-L6-v2` model (~90 MB) and the MITRE ATT&CK
dataset (~36 MB, cached as `mitre_cache.json`). Later runs work offline.

## Project structure
```
app.py            Flask server and API routes
nlp_engine.py     NLP pipeline
templates/        HTML templates
static/           CSS
```
