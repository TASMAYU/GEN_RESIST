GEN_RESIST – AMR Prediction with GAT
GEN_RESIST is a web application for predicting antimicrobial resistance (AMR) from bacterial whole-genome FASTA files using a Graph Attention Network (GAT). The frontend is hosted on GitHub Pages and communicates with a FastAPI backend deployed on Render, which loads the trained GAT model and returns resistance predictions for multiple antibiotics.

Features
Upload bacterial genome FASTA files and get AMR predictions.

GAT-based model over k-mer co‑occurrence graphs.

Reports:

Resistant / Susceptible calls per antibiotic.

Probabilities for each antibiotic.

Detected resistance genes (from a CARD‑like list).

Basic genome statistics (GC content, normalized length).

REST API with endpoints for prediction and model metadata.

Tech Stack
Frontend: HTML, CSS, JavaScript (GitHub Pages).

Backend: FastAPI, Uvicorn.

ML / Data: PyTorch, PyTorch Geometric, NumPy, Biopython.

Deployment: Docker, Render Web Service.

Project Structure
index.html, dashboard.html, style.css, grid.png, etc. – frontend UI.

backend.py – FastAPI app exposing the AMR prediction API.

inference.py – local interactive CLI/Tkinter inference script (for development).

model/

best_model.pt – trained GAT weights.

kmer_vocab.json – k‑mer vocabulary and mapping.

antibiotics.json – list of antibiotics the model predicts.

card_genes.json – resistance gene list.

requirements.txt – Python dependencies.

Dockerfile – container definition for the backend + model.

render.yaml – Render service configuration.

How It Works (System Design)
Frontend

Hosted on GitHub Pages.

When a user uploads a FASTA file, the browser JS sends a POST /predict request with the file as multipart/form-data to the backend URL (Render).

Backend + Model (Render)

Render builds and runs the Docker image defined in Dockerfile.

On container start:

FastAPI app (backend.py) is launched with Uvicorn (port 8000 inside the container).

Configuration JSONs and best_model.pt are loaded from model/.

A MemoryEfficientGAT model is instantiated and its weights are loaded.

For POST /predict:

The FASTA file is saved to a temp path.

The genome is parsed with Biopython, k‑mers are extracted, and a co‑occurrence graph is built.

Genome features and a simple CARD‑gene vector are computed.

The PyTorch Geometric Data object is passed to the GAT model.

Sigmoid outputs are converted into probabilities and Resistant/Susceptible labels.

JSON with predictions, probabilities, detected genes, and genome stats is returned.

Frontend Rendering

The frontend receives the JSON response and displays:

Per‑antibiotic predictions.

Confidence scores.

Detected resistance genes and summary stats.

API Endpoints
Base URL (example):
https://<your-render-service>.onrender.com

GET /
Health/info (service status, model name, counts).

POST /predict
Input: FASTA file (file field in multipart/form-data).
Output:

json
{
  "file_name": "...",
  "predictions": { "Ampicillin": "Resistant", ... },
  "probabilities": { "Ampicillin": 0.93, ... },
  "detected_genes": ["blaCTX-M-15", ...],
  "genome_stats": { "gc_content": 0.51, "length_normalized": 0.87 }
}
GET /antibiotics
Returns the list and count of antibiotics used by the model.

GET /genes
Returns the list and count of CARD genes.

GET /config
Returns model configuration (k-mer size, number of kmers, etc.).

Running Locally
Clone the repository and move into it.

Create and activate a virtual environment (optional but recommended).

Install dependencies:

bash
pip install -r requirements.txt
Ensure the model/ directory contains best_model.pt, kmer_vocab.json, antibiotics.json, and card_genes.json.

Start the backend:

bash
uvicorn backend:app --host 0.0.0.0 --port 8000 --reload
Open the frontend locally (e.g., using a simple static file server) and set the API base URL to http://localhost:8000.

Docker / Render Deployment
Build and run locally:

bash
docker build -t amr-prediction-api .
docker run -p 8000:8000 amr-prediction-api
Render:

render.yaml defines a web service using the Dockerfile.

On push to the main branch, Render rebuilds the image and deploys.

The health check uses GET /.
