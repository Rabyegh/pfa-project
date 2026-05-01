# PFA â€” Parapharmacy AI Search System

An AI-powered search platform for Tunisian parapharmacy products, featuring:
- **Image Search**: Upload a product photo â†’ YOLO detects â†’ PaddleOCR reads label â†’ Elasticsearch finds matches
- **Barcode Search**: Scan or enter an EAN barcode â†’ scrapes real-time prices from Tunisian parapharmacy websites

---

## Project Structure

`
pfa_github/
â”œâ”€â”€ Back_End/           # FastAPI backend
â”‚   â”œâ”€â”€ main.py         # All API endpoints
â”‚   â”œâ”€â”€ enhanced_search.py  # Barcode search scraper
â”‚   â”œâ”€â”€ barcode_search.py   # Barcode search (legacy fallback)
â”‚   â”œâ”€â”€ database.py     # SQLite/SQLAlchemy setup
â”‚   â”œâ”€â”€ models.py       # DB models (User, Report, Site)
â”‚   â”œâ”€â”€ config.py       # API keys
â”‚   â””â”€â”€ requirements.txt
â”œâ”€â”€ image_search/       # AI pipeline
â”‚   â”œâ”€â”€ detect_and_ocr.py     # YOLO + PaddleOCR + Groq
â”‚   â”œâ”€â”€ pipeline_api.py       # FastAPI integration entry point
â”‚   â”œâ”€â”€ elasticsearch_search.py  # Hybrid BM25 + cross-encoder search
â”‚   â”œâ”€â”€ rerank_cross_encoder.py  # Groq LLM reranker
â”‚   â”œâ”€â”€ best_yolov11.pt       # YOLO model weights
â”‚   â”œâ”€â”€ .env                  # GROQ_API_KEY
â”‚   â””â”€â”€ requirements.txt
â”œâ”€â”€ Front_End/          # Vue.js 3 + Vuetify frontend
â”‚   â”œâ”€â”€ src/
â”‚   â”‚   â”œâ”€â”€ components/
â”‚   â”‚   â”‚   â”œâ”€â”€ ImageSearch.vue   # Image search page
â”‚   â”‚   â”‚   â”œâ”€â”€ BarcodeSearch.vue # Barcode search page
â”‚   â”‚   â”‚   â””â”€â”€ ...
â”‚   â”‚   â”œâ”€â”€ router/index.js
â”‚   â”‚   â””â”€â”€ main.js
â”‚   â”œâ”€â”€ package.json
â”‚   â””â”€â”€ vite.config.js
â””â”€â”€ alembic/            # DB migrations
`

---

## Quick Start

### 1. Backend (FastAPI)
`ash
cd Back_End
pip install -r requirements.txt
# Also install image_search dependencies:
pip install -r ../image_search/requirements.txt
uvicorn main:app --reload --port 8000
`

### 2. Frontend (Vue.js)
`ash
cd Front_End
npm install
npm run dev
`

### 3. Prerequisites
- **Elasticsearch** running on http://localhost:9200 (for image search)
- **Tesseract OCR** installed at C:\Program Files\Tesseract-OCR\tesseract.exe
- **GROQ_API_KEY** set in image_search/.env

---

## Tech Stack
- **Frontend**: Vue.js 3, Vuetify, Vue Router, Axios, @zxing/library (barcode scanner)
- **Backend**: FastAPI, SQLAlchemy, SQLite, aiohttp
- **AI Pipeline**: YOLOv11 (Ultralytics), PaddleOCR, Groq/Llama-3, Elasticsearch
