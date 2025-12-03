# 🧠 Simple Streamlit Chatbot App  
A lightweight chatbot built using Streamlit and the Free LLM API. Includes a clean UI and configurable settings.

## 📚 Table of Contents
1 [Features](#-features)
2 [Demo](#-demo)
3 [Installation](#-installation)
 - [Tools and Dependencies](#-tools and dependencies)
 - [Scripting and Running the app](#-scripting and running app)
4 [Configuration](#-configuration)
5 [Usage](#-usage)
6 [Project Structure](#-project-structure)
7 [How the Chatbot Works](#-how-the-chatbot-works)
8 [Example Interactions](#-example-interactions)
9 [License](#-license)

## ✨ Features
- **Streamlit UI** with live chat interface  
- **API-based LLM responses** using APIFreeLLM  
- **Simple `call_llm()` wrapper** for HTTP requests  
- **Lightweight** and runs locally with no GPU  

## 💻 Demo
![Bioinformatics Chatbot](https://drive.google.com/file/d/1dlbNz8J822lMk_KuF72fkyyL0A94R3AI/view?usp=sharing)
**_Bioinformatics_ chatbot*

##  Installation
*🧰 Tools and Dependencies*
[x] Ensure Python (>=3.8) is installed.
[x] Create a virtual environment (e.g., python -m venv chatbot_env, activate it).
[x] Install required packages:

- If working from a Linux Environment:
1. Install pip:
 `sudo apt-get install python3-pip.`
2. Install required packages:
 `pip install streamlit requests.`
4. Check if the  streamlit installation worked:
 `streamlit hello`

- *🏃 Scripting and Running the app*
1. Create a venv environment:
 `python -m venv chatbot_env`

2. Activate the venv environment
   `source chatbot_env/bin/activate`
   
3. Choose and Configure a [*_ApiFreeLLM_*](https://www.apifreellm.com/?utm_source=chatgpt.com) 
   ApiFreeLLM is a free, no-signup API that lets you send simple chat requests instantly using a single POST endpoint. With just a JSON message, you can start interacting with the model right away, making it perfect for quick prototypes, demos, and lightweight applications. It’s fast, easy to use, and accessible to anyone, with a modest rate limit of about one request every five seconds per IP.

   3.1 Configuration of our API request
   To avoid hard-coding values that require modification frequently, like an API URL, store them in a configuration file. The config file allows updating or swapping the API, changing environments, or adding keys later without editing the entire code base. Configuration would include TIMEOUT, API_URL and API_KEY. APIFreeLLM does not require an API key to use which makes it an open access program.
   
   - Create a config.py file `nano config.py`
   - Add script
   ```python
      API_URL = "https://apifreellm.com/api/chat"
      API_KEY = None
      TIMEOUT = 5
   ```
4. Building the Streamlit App
   4.1 Create an app.py file `nano app.py`
   ```python
   import requests
   import streamlit as st
   import json
   import time

   from config import API_URL, API_KEY, TIMEOUT

   headers = {
   "User-Agent": "Mozilla/5.0",
   "Accept": "application/json",
   }

   omics_terms = [
    "rna", "rna-seq", "sequencing", "chip-seq", "genome", "genomic",
    "variant", "annotation", "assembly", "alignment", "transcriptome",
    "proteomics", "metabolomics", "epigenomics", "differential expression","metagenomics",
    "gene ontology", "pathway analysis", "mutation", "snv", "cnv",
    "raw reads", "fastq", "bam", "vcf", "gtf", "gff","dna"
   ]

   def omics_terms(message):
    msg = message.lower()
    return any(term in msg for term in OMICS_KEY_TERMS)


   ## creating a function that pulls info from an LLM
   def call_llm(message):
   if not omics_terms(message):
      return "This query does not contain omics-related terms. Please refine your question using genomic or bioinformatics keywords."
   payload={'message':message}
   
   resp=requests.post(API_URL, headers=headers, json=payload, timeout=30)

   try:
      resp_json=resp.json()
   except ValueError:
      return("Error, Non-Json")   

   if resp_json.get("status") == "success":
        return resp_json["response"]
   else:
        return resp_json.get("error", "Unknown error")

   ```


   
