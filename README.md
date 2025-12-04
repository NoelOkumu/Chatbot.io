# 🧠 Simple Streamlit Chatbot App  

A lightweight chatbot built using Streamlit and the Free LLM API. Includes a clean UI and configurable settings.


## 📚 Table of Contents

1 [Features](#-features)

2 [Demo](#-demo)

3 [Installation](#-installation)
 
 - [Tools and Dependencies](#-tools-and-dependencies)
 
 - [Configuration](#-configuration)
 
4 [Scripting and Running the app](#-scripting-and-running-app) 

6 [Project Structure](#-project-structure)

 - [Fetching Results from APIFree](#-Fetching-Results-from-APIFree-(aLarge-Language-Model))

 - [Creating a Graphic User using Streamlit](#-Creating-a-Graphic-User-using-Streamlit-for-End-User)
   
7 [Acknowledgement](#-acknowledgement)


## ✨ Features

- **Streamlit UI** with live chat interface  

- **API-based LLM responses** using APIFreeLLM  

- **Simple `call_llm()` wrapper** for HTTP requests  

- **Lightweight** and runs locally with no GPU  

---
## 🧑‍💻 Demo

![Bioinformatics Chatbot](https://raw.githubusercontent.com/NoelOkumu/Chatbot.io/b37ce2c907929ad41719432c0ccd078b8cfb315b/annah_env/Images/Screenshot%20From%202025-12-03%2015-37-14.png))

---
## 🧰 Installation

### * 🛠️ Tools and Dependencies*

- [x] Ensure Python (>=3.8) is installed.

- [x] Create a virtual environment (e.g., python -m venv chatbot_env, activate it).

- [x] Ensure you are working on a Linux Environment

- [x] Install required packages:

- If working from a Linux Environment:

1. Install pip:
 
 `sudo apt-get install python3-pip.`

2. Install required packages:
 
 `pip install streamlit requests.`

3. Check if the  streamlit installation worked:

  `streamlit hello`

## 🏃 Scripting and Running the app*

1. Create a venv environment:
 
   `python -m venv chatbot_env`

2. Activate the venv environment
 
   `source chatbot_env/bin/activate`
   
3. Choose and Configure an LLM API:[*_ApiFreeLLM_*](https://www.apifreellm.com/?utm_source=chatgpt.com) 

ApiFreeLLM is a free, no-signup API that lets you send simple chat requests instantly using a single POST endpoint. With just a JSON message, you can start interacting with the model right away, making it perfect for quick prototypes, demos, and lightweight applications. It’s fast, easy to use, and accessible to anyone, with a modest rate limit of about one request every five seconds per IP.

---
   *🧩_Configuration of our API request_*

To avoid repeatedly changing hard-coded values like API URLs, it’s best practice to store them in a configuration file. This makes it easy to update or switch APIs, change environments, or add keys later without modifying your entire codebase. Typical configuration values include TIMEOUT, API_URL, and API_KEY. Since ApiFreeLLM doesn’t require an API key, it remains fully open-access and simple to integrate.
   
   - Create a config.py file `nano config.py` and add configuration settings based on APIFreeLLM requirements:
   
   ```python
      API_URL = "https://apifreellm.com/api/chat"
      API_KEY = None
      TIMEOUT = 5
   ```
---

5. Building the Streamlit App

   Create an app.py file `nano app.py`
   
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
6. Running the app

   `streamlit run app.py`

   _View Chatbot_app on web-browser_


---
## Project Structure

   ![Chatbot_build_Structure](https://github.com/NoelOkumu/Chatbot.io/blob/main/annah_env/Images/Screenshot%20From%202025-12-04%2008-55-28.png?raw=true)

### a) Fetching data from a Large Language Model

  Large Language Models(LLMs) are being used across diverse fields for tasks involving human language. Application Programming Interfaces (APIs), on the other hand, aid in connecting multiple platforms while allowing machines to talk to machines without manual input. This project makes use of a large language model's API to automate processes, enhance productivity, and enable more natural computer interaction by bioinformaticians as they try to access solutions to problems they face in their omics analysis workflows.

  ApiFreeLLM, which was used in this workflow, is a free, no-signup API that lets you send simple chat requests instantly using a single POST endpoint. With just a JSON message, a user can start interacting with the model right away, making it perfect for quick prototypes, demos, and lightweight applications. It’s fast, easy to use, and accessible to anyone, with a modest rate limit of about one request every five seconds per IP. To possibly detect some keywords that make the responses more bioinformatics-aware, some key terminologies frequently used in omics research were added (e.g., “bioinformatics”, “data analysis”) that would accommodate, send, and fetch different prompts or route to special responses.

### b) Creating a Graphic User Interface for End User

  Streamlit is a free, open-source Python library that creates tools that can display data and collect parameters for modelling. With a few lines of code, Streamlit can deploy models easily and quickly while being compatible with the majority of existing Python libraries: Pandas, Matplotlib, Seaborn, Plotly, Keras, Pytorch, and SymPy. Streamlit was used to customise the User Interface for Bioinformaticians and Life Scientists involved in Life Science Research. The documentation found in this repository provides scripts that were used for both data fetching and creating a virtual user interface.

---
### 🛠️ Built With

- [Streamlit](https://docs.streamlit.io/get-started)
- [APIFree LLM](https://www.apifreellm.com/?utm_source=chatgpt.com)
  
## 🙏 Acknowledgements

This project uses **Streamlit** for rapid interactive app development and **APIFree LLM** for free large-language-model API access.  
Much appreciation to both communities for supporting open and accessible research tools.





 

   
