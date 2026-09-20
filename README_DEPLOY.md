# Personal CA — GitHub / Render / Netlify deployment

## Render backend
- Runtime: Python 3
- Root Directory: `.`
- Build Command: `pip install -r requirements.txt`
- Start Command: `uvicorn server:app --host 0.0.0.0 --port $PORT`

Required Render environment variables:
- `OPENROUTER_API_KEY`
- `OPENROUTER_MODEL=openrouter/free`
- `SESSION_SECRET`
- `DATA_ENCRYPTION_KEY`
- `FRONTEND_ORIGIN=https://personal-ca-555.netlify.app`
- `GOOGLE_CLIENT_ID` (if Google Sign-In is used)

Optional Gemini fallback variables:
- `GEMINI_API_KEY`
- `GEMINI_MODEL`

## Health check
Open:
`https://personal-ca-1.onrender.com/api/health`

Expected: JSON containing `"ok": true`.

The API root `/api` and `/api/` also return a JSON status instead of 404.

## Netlify frontend
Publish the repository root. `_redirects` must remain named exactly `_redirects` (not `_redirects.txt`).

The frontend calls the Render backend directly, so `FRONTEND_ORIGIN` must exactly match the deployed frontend origin.
