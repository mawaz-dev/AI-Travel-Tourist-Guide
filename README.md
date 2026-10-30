# 🌍 AI Travel Tourist Guide

A lightweight web app that suggests tourist attractions for any country, state, or city. Enter a location and an AI model (AI21 Jamba) returns a short, curated list of must-see destinations, each with a quick teaser.

## Features

- 🗺️ Search by **country**, with an optional **city or state** for local results
- ⚡ AI-generated highlights: six destinations with short, punchy teasers
- 🎨 Glassmorphism UI with a typing-animation header, built with Tailwind CSS
- 🔄 One-click "Search Again" flow
- 🧩 Minimal setup: one Flask file and one HTML file, with no build step

## Tech Stack

| Layer | Technology |
| --- | --- |
| Frontend | HTML, Tailwind CSS (CDN), vanilla JavaScript, Typed.js |
| Backend | Python, Flask, Flask-CORS |
| AI | [AI21 Studio](https://studio.ai21.com/) Jamba (`jamba-mini`) |
| Config | python-dotenv |

## How It Works

1. The user enters a country (required) and a city/state (optional) in the browser.
2. The frontend sends a `POST` request to the Flask API at `/get_travel_info`.
3. The backend builds a structured prompt and sends it to the AI21 chat completions API.
4. The model replies with a small HTML snippet: country, city/state, and a list of highlights.
5. The frontend renders that HTML inside a result card.

## Project Structure

```text
AI-Travel-Tourist-Guide/
├── app.py        # Flask API and AI21 prompt
├── index.html    # Single-page frontend
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.9+
- An [AI21 API key](https://studio.ai21.com/)

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/AI-Travel-Tourist-Guide.git
cd AI-Travel-Tourist-Guide
```

### 2. Install dependencies

```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

pip install flask flask-cors ai21 python-dotenv
```

### 3. Add your API key

Create a `.env` file in the project root:

```bash
AI21_API_KEY=your_api_key_here
```

> ⚠️ Never commit your `.env` file. Add it to `.gitignore`.

### 4. Start the backend

```bash
python app.py
```

The API runs at `http://127.0.0.1:5000`.

### 5. Open the frontend

Open `index.html` in your browser (double-click it, or serve it with `python -m http.server 8000` and visit `http://localhost:8000`).

## API Reference

### `POST /get_travel_info`

**Request body**

```json
{
  "country": "Japan",
  "city": "Kyoto"
}
```

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `country` | string | ✅ | Country to explore |
| `city` | string | ❌ | City or state to narrow the results |

**Success response** (`200`)

```json
{
  "travel_info": "<p>📍 <strong>Country:</strong> Japan</p> ... <ul><li>...</li></ul>"
}
```

`travel_info` is an HTML string ready to be inserted into the page.

**Error responses**

| Status | Meaning |
| --- | --- |
| `400` | `country` is missing |
| `500` | The AI21 request failed (check your API key and model access) |

## Configuration

| Setting | Where | Notes |
| --- | --- | --- |
| `AI21_API_KEY` | `.env` | Required |
| Model | `app.py` | Defaults to `jamba-mini`. Change it to `jamba-large` or another model you have access to |
| API URL | `index.html` | The frontend calls `http://127.0.0.1:5000`. Update it if you deploy the backend elsewhere |

## Roadmap

- Add images and map links for each destination
- Add best time to visit, local food, and budget tips
- Save favorite destinations
- Support more languages
- Deploy the app (Render, Railway, or Vercel + a hosted API)

## Acknowledgments

- [AI21 Labs](https://www.ai21.com/) for the Jamba models and API
- [Tailwind CSS](https://tailwindcss.com/) and [Typed.js](https://github.com/mattboldt/typed.js)

## License

No license has been specified yet. Add a `LICENSE` file (for example MIT) before others reuse the code.
