GEN_RESIST

Transforming Genomes into Actionable Resistance Insights

last-commit repo-top-language repo-language-count
Built with the tools and technologies:

JSON Markdown FastAPI NumPy Docker Python Pydantic YAML

Table of Contents

Overview
Getting Started
Prerequisites
Installation
Usage
Testing
Overview

GEN_RESIST is an advanced bioinformatics platform designed to predict antimicrobial resistance (AMR) from genome sequences using cutting-edge graph neural networks. It provides a scalable, API-driven backend and an intuitive dashboard for data visualization, making complex genomic analysis accessible and efficient.

Why GEN_RESIST?

This project aims to streamline antimicrobial resistance prediction and genomic analysis. The core features include:

🧬 🚀 FastAPI Backend: Enables fast, reliable API access for integrating AMR prediction into larger workflows.
🧠 🤖 Graph Attention Network: Utilizes sophisticated machine learning models for high-accuracy resistance profiling.
🐳 🛠 Containerized Deployment: Ensures consistent, scalable deployment via Docker and automated configs.
📊 🌐 Interactive Dashboard: Visualizes complex data and network relationships for easy interpretation.
🔍 🧬 Genomic Data Processing: Supports comprehensive analysis from raw genome sequences to detailed reports.
Getting Started

Prerequisites

This project requires the following dependencies:

Programming Language: Python
Package Manager: Pip
Container Runtime: Docker
Installation

Build GEN_RESIST from the source and install dependencies:

Clone the repository:

❯ git clone https://github.com/TASMAYU/GEN_RESIST
Navigate to the project directory:

❯ cd GEN_RESIST
Install the dependencies:

Using docker:

❯ docker build -t TASMAYU/GEN_RESIST .
Using pip:

❯ pip install -r requirements.txt
Usage

Run the project with:

Using docker:

docker run -it {image_name}
Using pip:

python {entrypoint}
Testing

Gen_resist uses the {test_framework} test framework. Run the test suite with:

Using docker:

echo 'INSERT-TEST-COMMAND-HERE'
Using pip:

pytest
