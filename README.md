 AI Career Trends - Project Documentation body { font-family: Arial, sans-serif; line-height: 1.6; margin: 2rem; background-color: #f7f7f7; } h1, h2, h3 { color: #2c3e50; } a { color: #2980b9; text-decoration: none; } a:hover { text-decoration: underline; } code { background: #ecf0f1; padding: 2px 4px; border-radius: 4px; } pre { background: #ecf0f1; padding: 10px; border-radius: 4px; overflow-x: auto; } footer { margin-top: 2rem; font-size: 0.9rem; color: #555; } .container { max-width: 900px; margin: auto; background: #fff; padding: 2rem; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }

AI Career Trends Dashboard - Project Documentation
==================================================

Project Overview
----------------

This project predicts emerging careers in the AI era by analyzing daily technology trends and discussion data. It combines data ingestion, natural language processing, and clustering techniques to surface actionable insights.

*   **Goal:** Identify emerging AI-era career paths.
*   **Approach:**
    1.  Collect daily trend data from sources like Hacker News.
    2.  Preprocess and embed text using Transformer models.
    3.  Cluster trends using HDBSCAN.
    4.  Map clusters to potential careers and aggregate.
*   **Outcome:** A dynamic dashboard showing ranked AI career predictions.

Project Structure
-----------------

ai\_career\_predictor/
├── fetch\_data.py
├── predict\_now.py
├── app.py
├── venv39/
├── ai\_trends/
│   ├── templates/
│   │   └── index.html
│   └── trends.db
├── readme.html
    

SQLite Tables
-------------

*   `trends`: Raw trend data collected daily
*   `predictions`: Aggregated AI career predictions

Python Libraries Used
---------------------

*   requests, beautifulsoup4 → Data collection
*   numpy, sentence-transformers, torch, hdbscan, scikit-learn → ML & embeddings
*   flask, werkzeug.middleware.proxy\_fix → Web app & API

AWS Deployment
--------------

*   **EC2:** Runs Python virtual environment, hosts Flask API.
*   **ALB:** Routes `/api/*` requests to EC2, security group allows CloudFront.
*   **S3:** Serves static `index.html`.
*   **CloudFront:**
    *   Default behavior → S3 static files
    *   /api/\* behavior → ALB
    *   HTTPS enforced for clients
*   **Route53:** Subdomain `ai.mydomain.com` points to CloudFront

Deployment Steps
----------------

1.  Set up Python 3.9 virtual environment and install dependencies.
2.  Run `fetch_data.py` to populate SQLite DB.
3.  Start Flask app on EC2.
4.  Configure CloudFront behaviors: `*` → S3, `/api/*` → ALB.
5.  Invalidate CloudFront cache after updates.
6.  Access dashboard via [https://ai.mydomain.com](https://ai.mydomain.com)

Importance & Perspective
------------------------

*   Helps individuals anticipate AI-driven job changes and upskill.
*   Provides organizations with trend intelligence for workforce planning.
*   Future extensions: automated forecasting, additional sources, visualization dashboards, alerts.
*   Demonstrates cost-effective AI pipelines on AWS.

© 2025 AI Career Trends. [Back to Dashboard](index.html)
