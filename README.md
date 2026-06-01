# Lipaharaka Bulk STK Push Bot

A web application for sending bulk M-Pesa STK Push payment requests via the **Lipaharaka API**. Built with Flask and designed for easy deployment on Render.

## Features

- **Single & Bulk STK Push** — Send payment requests to one or hundreds of numbers
- **Manual Entry** — Paste phone numbers directly (one per line)
- **CSV Upload** — Drag & drop CSV files with phone numbers
- **Live Results Dashboard** — Track success/failure in real-time
- **Export to CSV** — Download transaction history
- **Secure Credential Input** — Password fields with toggle visibility
- **Responsive Design** — Works on desktop and mobile

## API Provider

This bot uses [Lipaharaka](https://lipaharakaapis.co.ke) — M-Pesa STK Push API.

Required credentials:
- **API Key** — Your Lipaharaka API key
- **Channel ID** — Your assigned channel (e.g., `16`)

## Quick Start (Local)

```bash
# 1. Clone the repo
git clone https://github.com/YOUR_USERNAME/lipaharaka-bulk-stk.git
cd lipaharaka-bulk-stk

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run locally
python app.py
```

Open http://localhost:5000 in your browser.

## Deploy to Render (Free)

### Step 1: Push to GitHub

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/lipaharaka-bulk-stk.git
git push -u origin main
```

### Step 2: Create Render Account

1. Go to [render.com](https://render.com) and sign up (free, no credit card)
2. Connect your GitHub account when prompted

### Step 3: Create Web Service

1. Click **New +** → **Web Service**
2. Find and select your `lipaharaka-bulk-stk` repository
3. Configure:

| Setting | Value |
|---------|-------|
| **Name** | `lipaharaka-bulk-stk` |
| **Region** | `Oregon (US West)` or closest to you |
| **Branch** | `main` |
| **Runtime** | `Python 3` |
| **Build Command** | `pip install -r requirements.txt` |
| **Start Command** | `gunicorn app:app` |
| **Instance Type** | `Free` |

4. Click **Create Web Service**

Your app will be live in ~2 minutes at `https://lipaharaka-bulk-stk.onrender.com`.

### Step 4: Set Environment Variables (Optional)

In Render dashboard → your service → **Environment** tab:

| Key | Value |
|-----|-------|
| `SECRET_KEY` | Random string from [random.org](https://random.org) |
| `LIPAHARAKA_URL` | `https://lipaharakaapis.co.ke/api.php?action=api_stk` |

Click **Save Changes** — Render redeploys automatically.

> **Note:** Free instances spin down after 15 min inactivity and take ~60s to wake. Upgrade to Starter ($7/mo) for always-on.

## Usage

1. **Enter Credentials** — API Key and Channel ID from Lipaharaka
2. **Add Recipients** — Paste numbers manually or upload a CSV
3. **Set Amount** — Payment amount in KES
4. **Send** — Click "Send STK Push" and watch results in real-time

### Phone Number Format

Numbers must start with `254` (e.g., `254712345678`).

### CSV Format

Any CSV works — the app extracts all cells starting with `254`:

```csv
254712345678
254723456789
254734567890
```

Or with headers:
```csv
name,phone
John,254712345678
Jane,254723456789
```

## API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Web interface |
| `/api/push-single` | POST | Send to one number |
| `/api/push-bulk` | POST | Send to multiple numbers |
| `/api/upload-csv` | POST | Upload CSV file |
| `/api/transactions` | GET | Get all transactions |
| `/api/export` | GET | Export transactions as CSV |
| `/api/clear` | POST | Clear transaction history |

## Security Notes

- **Never commit credentials** — enter them via the web UI
- **Use HTTPS** — Render provides this automatically
- **Set a strong SECRET_KEY** environment variable
- Transactions are stored in memory only (resets on restart)

## Tech Stack

- **Backend:** Flask (Python)
- **Frontend:** Vanilla JS + CSS
- **Server:** Gunicorn
- **Hosting:** Render

## License

MIT
