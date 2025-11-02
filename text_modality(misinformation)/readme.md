
---

# Misinformation Detector — Powered by n8n, Gemini, and External APIs

This project is an automated misinformation detection pipeline built using **n8n**, **Google Fact Check API**, **NewsAPI**, **Tavily Web Search**, and **Gemini**.
It gathers real-time information from multiple trusted sources, merges the results, and uses large language model reasoning to verify whether a given statement, claim, or piece of news is likely to be true or false.

---

## Features

* **Multi-Source Fact Gathering:**
  Collects relevant news articles from **NewsAPI**, verified claims from the **Google Fact Check Tools API**, and general search insights from **Tavily Search API**.

* **Automated Reasoning via Gemini:**
  Combines all gathered information into a single structured JSON and sends it to **Gemini (Google’s LLM)** to analyze and produce a factual verdict.

* **Visual Workflow Automation:**
  Entirely managed through **n8n**, allowing modular, no-code configuration and easy expansion.

* **Real-Time or Trigger-Based Execution:**
  Can be run manually, on a schedule, or through a webhook for external integrations such as chatbots or web applications.

---

## Architecture Overview

```
        ┌────────────┐
        │ Webhook/API│
        └──────┬─────┘
               │
               ▼
        ┌────────────┐
        │ NewsAPI Node│──┐
        └────────────┘  │
                        ├──▶ Merge Node ──▶ Gemini (LLM)
        ┌────────────┐  │
        │ FactCheck API│─┘
        └────────────┘
               │
               ▼
        ┌────────────┐
        │ Tavily API │
        └────────────┘
```

**Workflow Steps:**

1. Input claim or message received via webhook or manual trigger.
2. **NewsAPI Node** fetches related news articles.
3. **Google Fact Check API Node** retrieves verified fact-checks.
4. **Tavily Search Node** performs a general web search for supporting data.
5. **Merge Node** combines all collected JSON data.
6. **Gemini Node** analyzes the merged data to produce a final factual verdict.
7. Output is returned as structured JSON with a verdict, confidence score, and reasoning.

---

## API Setup

### 1. NewsAPI

* Sign up at [https://newsapi.org](https://newsapi.org)
* Use the API key in your HTTP Request node.

### 2. Google Fact Check Tools API

* Enable **Fact Check Tools API** in Google Cloud Console.
* Use your API key in the endpoint:

  ```
  https://factchecktools.googleapis.com/v1alpha1/claims:search?query={{$json["query"]}}&key=YOUR_API_KEY
  ```

### 3. Tavily Search API

* Register at [https://tavily.com](https://tavily.com)
* Use the endpoint:

  ```
  POST https://api.tavily.com/search
  Headers: 
    Content-Type: application/json
    Authorization: Bearer YOUR_API_KEY
  Body:
    { "query": "{{$json['query']}}" }
  ```

### 4. Gemini API

* Connect Gemini using the official node or via HTTP Request.
* Example prompt:

  ```
  Analyze the following JSON data from NewsAPI, Fact Check API, and Tavily.
  Determine whether the claim is likely true or false and explain briefly.
  {{$json}}
  ```

---

## Environment Variables (Optional)

If running behind a reverse proxy (for example, using ngrok), set the webhook URL:

**Command Prompt:**

```bash
set WEBHOOK_URL=https://<your-ngrok-or-domain-url>/
```

**PowerShell:**

```powershell
$env:WEBHOOK_URL="https://<your-ngrok-or-domain-url>/"
```

---

## Example Output

```json
{
  "claim": "COVID-19 vaccines cause microchips in the body",
  "verdict": "Likely misinformation",
  "confidence": 95,
  "reasoning": "No credible sources support this claim. Verified fact-checks and news reports consistently classify it as misinformation.",
  "sources": [
    "https://www.reuters.com",
    "https://www.snopes.com"
  ]
}
```

