<b>AI Career Trend Predictor</b>

This project automatically collects daily technology trends and uses NLP + machine learning to predict emerging careers in the AI era.

It runs entirely on free, public data sources, stores everything locally, and incrementally improves predictions as more data is collected over time.

---
🚀 What This Project Does

- Collects daily trending tech posts from:
   - Hacker News
   - YouTube Trending (no API, HTML scraping)
- Stores data in a local SQLite database
- Uses sentence embeddings + clustering to detect emerging topics
- Maps trends to potential future AI job roles
- Designed to improve accuracy over months of data collection
- Runs automatically via cron on Ubuntu

---
🧠 How the Prediction Works (High Level)

- Collect daily post titles
- Convert titles to vector embeddings
- Cluster similar topics
- Extract keywords from each cluster
- Map keywords → AI-era job categories
- Rank jobs by topic strength and frequency

This is an unsupervised trend discovery system, not a hard-coded rules engine.

---
🗂 Project Structure  
ai_trends/  
    ├── fetch_data.py        # Daily data collection (HN + YouTube)  
    ├── predict_now.py       # Lightweight predictor (small datasets)  
    ├── predict_jobs.py      # Advanced predictor (large datasets)  
    ├── trends.db            # SQLite database (auto-created)  
    ├── log.txt              # Cron logs  
    └── README.md

---
🖥 System Requirements

- Ubuntu 20.04+
- Python 3.9+
- Internet connection
- ~1GB disk space (over months of data)

---
🐍 Python Setup (Recommended: Virtual Environment)  

    sudo apt update
    sudo apt install python3 python3-venv python3-pip build-essential python3-dev

Create and activate venv:

    python3 -m venv venv
    source venv/bin/activate

Install dependencies:

    pip install requests beautifulsoup4 sentence-transformers scikit-learn pandas hdbscan

---
📥 Data Collection

Run manually:

    python3 fetch_data.py


This will:

- Create trends.db automatically
- Insert new daily records
- Avoid duplicate failures

Verify data:

    sqlite3 trends.db "SELECT COUNT(*) FROM trends;"

---
⏰ Automatic Daily Collection (Cron)

Edit crontab:

    crontab -e

Add:

    0 6 * * * /usr/bin/python3 /home/simon/ai_trends/fetch_data.py >> /home/simon/ai_trends/log.txt 2>&1

Runs every day at 6:00 AM.

---
📊 Prediction (Current Data)

For small datasets (e.g. < 500 records):

    python3 predict_now.py

This:

- Clusters all existing posts
- Produces early AI career predictions
- Prints results directly to terminal

Example output:

Likely future AI careers:
- AI/ML Engineer
- Prompt Engineer
- Generative AI Specialist

---
🔮 Prediction (Long-Term Data)

After weeks or months of data:

    python3 predict_jobs.py

This version:

- Uses HDBSCAN (better for large datasets)
- Detects emerging topics over time
- Writes predictions to predicted_jobs table

View predictions:

    sqlite3 trends.db "SELECT * FROM predicted_jobs ORDER BY score DESC;"

---
📈 How Accuracy Improves Over Time
| Data Age	| Prediction Quality|
| ------ | ------ |
| 1–7 days	| Prototype / noisy |
| 2–4 weeks	| Early trend detection |
| 2–3 months	| Strong signals |
| 6+ months	| Meaningful career forecasting |

---
🧩 Why This Is Not a “Typical LLM”

- No paid APIs
- No retraining giant models
- Uses RAG-style intelligence:
    - embeddings
    - clustering
    - trend growth
- Can later be connected to:
    - LLaMA / Mistral
    - Hugging Face models
    - Chat interfaces

---
🛣 Future Roadmap

 - Trend growth scoring (momentum detection)
 - Weekly AI career reports
  - Web dashboard (Flask)
  - RAG-based LLM interface
  - Hugging Face model publishing

---
⚠️ Disclaimer

This project predicts trends, not guaranteed job outcomes.
It is intended for exploration, research, and education.

---
⭐ Why This Project Matters

As AI automates tasks faster than curricula can adapt, trend-based career intelligence becomes critical. This system continuously learns from the tech ecosystem itself — not static job listings.
