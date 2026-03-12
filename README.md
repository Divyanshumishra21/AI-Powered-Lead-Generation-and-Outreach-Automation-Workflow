🚀 AI-Powered Lead Generation & Outreach Automation Workflow

An AI-powered lead generation and outreach automation system built using n8n, Apify, Google Sheets, and LLM APIs.

This workflow automatically collects company leads, enriches them with website data, generates business summaries using AI, and creates personalized HTML outreach emails.

📌 Project Overview

Lead generation and outreach are critical for businesses, but manually researching companies and writing personalized emails is time-consuming.

This project automates the entire process using workflow automation and AI.

The system performs:

1️⃣ Automated lead scraping
2️⃣ Lead enrichment
3️⃣ Website content analysis
4️⃣ AI business summarization
5️⃣ Personalized outreach email generation

All results are stored automatically inside Google Sheets.

🧠 Problem Statement

The goal of this project is to design an AI-powered workflow that automates lead generation and outreach.

The workflow should:

Fetch company leads automatically

Enrich the leads with available web data

Summarize the company website

Generate personalized outreach emails

This entire process should run without manual intervention.

🛠️ Technologies Used
Technology	Purpose
n8n	Workflow automation platform
Apify API	Google Maps lead scraping
Google Sheets API	Lead storage and updates
OpenRouter API	LLM access
Mistral-7B Model	AI summarization and email generation
JavaScript (n8n Code Node)	Data processing and cleaning
HTTP Requests	API integrations
⚙️ Workflow Architecture

🔄 Complete Workflow Explanation

The workflow follows a multi-stage automation pipeline.

1️⃣ Lead Data Ingestion
Trigger

The workflow starts when a new lead is added to Google Sheets.

Node:

New Lead Trigger (Google Sheet)

This allows the system to automatically process new leads in real time.

2️⃣ Lead Fetching from Apify

Node:

Fetching the Data (Apify - Google Maps Scraper)

This step uses the Apify API to fetch company leads including:

Company name

Website

Address

Phone number

Location

Business details

The data is returned in JSON format.

3️⃣ Lead Field Mapping

Node:

Extract Sheet Fields (Mapping)

This node structures the lead data into a standard format:

Fields created:

Company Name

Email

Website

Domain

City

State

Phone

Address

Summary

This ensures the rest of the workflow processes consistent data.

4️⃣ Domain Extraction Logic

Node:

Function Node (Domain Extraction)

If the domain is missing, the workflow attempts to extract it using:

Priority order:

1️⃣ Domain field
2️⃣ Email address
3️⃣ Website URL

Example:

contact@company.com → company.com

If no domain or website is found:

The lead is skipped and logged.

5️⃣ Lead Validation

Node:

Check for Missing Domain / Email / Website

This step checks whether the lead has enough information to continue.

If missing:

The lead is recorded in an Error Logs sheet.

6️⃣ Loop Through Leads

Node:

Loop Over Items

This allows the workflow to process multiple leads in batches.

Batch size:

5 leads per batch

This prevents API rate limits and improves performance.

7️⃣ Website Scraping

Node:

Doing Scraping

This step sends an HTTP request to the company website and retrieves the full HTML content of the homepage.

8️⃣ HTML Cleaning & Text Extraction

Node:

Clean HTML & Extract Text

This node performs advanced HTML processing:

Removes:

Scripts

Styles

Images

Metadata

SVG graphics

Then extracts:

Main content

Headers

Navigation text

Business descriptions

Finally, it produces clean textual content about the company.

9️⃣ AI Business Summary Generation

Node:

Summarize Business Info (OpenRouter)

The cleaned website text is sent to an AI model:

Model used:

Mistral-7B Instruct

The model generates a 2–3 sentence summary describing the company’s business.

Example output:

“XYZ Technologies is a digital solutions company specializing in AI-driven software development and enterprise automation solutions.”

🔟 Summary Processing

Node:

Extract Summary Text

This node cleans the AI output and extracts the final business summary.

The summary is then stored back into the Google Sheets lead record.

1️⃣1️⃣ AI Email Prompt Creation

Node:

Build HTML Email Prompt

A prompt is created that includes:

Company name

City and state

Website

Business summary

Example prompt:

Generate a personalized HTML outreach email for this company...
1️⃣2️⃣ AI Email Generation

Node:

Generate HTML Email (OpenRouter)

The AI model generates a personalized outreach email in HTML format.

Features:

Professional tone

Personalized business reference

Call-to-action button

Clean HTML formatting

1️⃣3️⃣ Store Generated Email

Node:

Save HTML Email to Sheet

The generated HTML email is saved in the Google Sheets “HTML Email” tab.

This allows the email to be directly copied or used in outreach campaigns.

📊 Final Output

Each lead record now contains:

Field	Description
Company Name	Business name
Website	Company website
City / State	Location
Business Summary	AI generated company summary
HTML Email	Personalized outreach email
🔐 Error Handling

The workflow includes basic error handling:

Missing domains

Missing websites

Failed scraping

Empty AI responses

Invalid leads are stored in an Error Logs sheet for review.

💰 API Usage
API	Purpose
Apify	Lead scraping
OpenRouter	LLM access
Google Sheets	Data storage

All APIs used have free tier support.

📂 Project Files
workflow/
   lead_generation_outreach_workflow.json

images/
   workflow_screenshot.png

docs/
   problem_statement.pdf
🚀 How to Run the Workflow

1️⃣ Install n8n

npm install n8n -g

2️⃣ Import workflow JSON

Import → lead_generation_outreach_workflow.json

3️⃣ Add API credentials:

Apify

Google Sheets

OpenRouter

4️⃣ Start the workflow.
