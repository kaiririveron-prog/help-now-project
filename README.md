# HelpNow (website + Python backend)

The website is `index.html`. The Python server (`app.py`) shows the site and
lets the "What do you need help with?" box use real AI (Claude).

## Run it

1. Install Python 3.9 or newer from python.org.
2. Open this folder in VS Code, then open the Terminal (Terminal > New Terminal).
3. Create a private Python environment:

   - Windows: `python -m venv .venv` then `.venv\Scripts\activate`
   - Mac/Linux: `python3 -m venv .venv` then `source .venv/bin/activate`

4. Install the tools: `pip install -r requirements.txt`
5. Get an API key from the Claude Console (https://platform.claude.com/docs/get-started).
6. Make a copy of `.env.example` named `.env` and paste your key after `ANTHROPIC_API_KEY=`.
7. Start the server: `python app.py`
8. Open http://127.0.0.1:5000 in your browser.

Try typing "my car won't start" or "water is pouring from under my sink".

## No key yet?

The site still works. The box falls back to simple keyword matching, and the
result card says which method was used.

## How it fits together

- `index.html`: the whole website (map, helpers, ratings, request flow).
- `app.py`: Flask server. `POST /api/match` sends the customer's text to Claude
  and returns `{category, urgent, summary, tip}`. Your API key stays on the
  server, never in the page.
- Safety: words like fire, gas smell, or injury always show the 911 banner in
  the page, whatever the AI says. The server also limits each visitor to
  20 requests a minute.

## Keep your key secret

Never share `.env` or post it online. `.gitignore` already keeps it out of Git.

## Ideas for next steps

- Save helpers, requests, and ratings in a database (SQLite works well with Flask).
- Add helper sign-up and login.
- Replace the drawn map with a real one (Leaflet or Google Maps).
