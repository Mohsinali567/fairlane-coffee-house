# ☕ Fairlane Coffee House

An all-in-one Streamlit app for an independent café: customer storefront, menu & deals,
online ordering, table reservations with an **interactive 3D café floor plan**, a customer
portal, and a back-office suite (marketing, inventory, HR & attendance, analytics, AI manager,
and the *Fairlane OS* autopilot).

## Features

| Area | What it does |
|---|---|
| **Home / Our Story** | Seasonal storefront (auto-switches for Ramadan, winter, spring, summer, autumn), live store status, social links. |
| **Menu & Deals** | Category menu, deals, cart, favourites and ordering. |
| **Reservations** | Pick party size, then choose a table in a rotatable **3D café** (or the classic 2D floor plan). Tables are colour-coded: recommended, fits, too small. Bookings are saved to MongoDB with clash checking. |
| **Customer Portal** | Sign up / sign in (salted password hashes), order history, reusable orders. |
| **Business Operations** | Live metrics, operations copilot. |
| **Advanced Features** | Marketing, inventory, HR & attendance, innovation feedback, AI manager, analytics dashboard, and **Fairlane OS** (zero-wait forecasting, tomorrow's plan, autopilot actions). |
| **Voice** | Optional spoken summaries via ElevenLabs. |

All images are embedded in `app.py`, so no separate `assets/` folder is needed.

## Quick start

```bash
git clone https://github.com/<your-username>/fairlane-coffee-house.git
cd fairlane-coffee-house
python -m venv .venv
# Windows: .venv\Scripts\activate     macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt

cp .streamlit/secrets.toml.example .streamlit/secrets.toml   # then edit it
streamlit run app.py
```

## Configuration

| Setting | Required | Purpose |
|---|---|---|
| `MONGODB_URI` | Yes | MongoDB Atlas connection string (customers, orders, reservations, staff). |
| `ELEVENLABS_API_KEY` | Optional | Enables the voice briefings. Without it, voice buttons show a friendly message. |
| `MONGODB_DB` | Optional | Database name (default `fairlane_coffee_house`). |
| `FAIRLANE_MAP_ADDRESS` | Optional | Address used for Google Maps links. |

Set them in `.streamlit/secrets.toml` (local) or as environment variables.
In MongoDB Atlas, allow your app's IP under **Network Access**
(for Streamlit Cloud use `0.0.0.0/0`).

## Deploy on Streamlit Community Cloud

1. Push this repository to GitHub.
2. Go to <https://share.streamlit.io> → **New app** → pick the repo, branch `main`, file `app.py`.
3. Under **Advanced settings → Secrets**, paste the contents of your `secrets.toml`.
4. Deploy.

## Notes

- The 3D floor plan uses three.js loaded from a CDN, so the visitor's browser needs internet
  access and WebGL. If 3D can't start, guests can switch to the 2D floor plan.
- `app.py` is large (~12 MB) because every image is embedded as base64. That is within
  GitHub's 100 MB per-file limit.

## Tech stack

Python · Streamlit · pandas · Altair · MongoDB Atlas (PyMongo) · three.js · ElevenLabs
