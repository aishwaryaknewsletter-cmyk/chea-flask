# Chéa Studios — Flask Website

Full-stack Python Flask website for Chéa Studios ethnic wear brand.

## Stack
- **Backend**: Python + Flask
- **Frontend**: HTML + CSS + Vanilla JavaScript
- **Templates**: Jinja2
- **Payments**: Razorpay

## Local Setup

### Step 1 — Install Python 3.11+
Download from https://python.org

### Step 2 — Create virtual environment
```
python -m venv venv
```

### Step 3 — Activate it
- Windows: `venv\Scripts\activate`
- Mac/Linux: `source venv/bin/activate`

### Step 4 — Install dependencies
```
pip install -r requirements.txt
```

If you see a `No module named 'pkg_resources'` error, run:
```
python -m pip install -U pip setuptools
```

### Step 5 — Set up environment variables
Copy `.env.example` to `.env` inside the `chea-flask/` folder and fill in your values:
```
Copy-Item .env.example .env
```

If you run the app from the workspace root, keep the `.env` file in `chea-flask/.env` so Flask can load it correctly.

### Step 6 — Run the server
```
python chea-flask/app.py
```

Open `http://localhost:5000` in your browser.

## Adding Razorpay Payments

1. Create a free Razorpay account at https://razorpay.com
2. Go to Settings → API Keys → Generate Test Key
3. Copy the Key ID and Key Secret into `chea-flask/.env`:
   ```
   RAZORPAY_KEY_ID=rzp_test_xxxxxxxxxxxx
   RAZORPAY_KEY_SECRET=xxxxxxxxxxxxxxxxxxxx
   ```
4. Restart the Flask server after saving the file.
5. Open the site, add a product to cart, and use the checkout button to test payment.
6. When ready for live payments, generate Live Keys and update `chea-flask/.env`

### Payment flow used by the site

- The browser sends the cart total to `/api/create-order`.
- Flask creates a Razorpay order using your secret key.
- The Razorpay checkout popup uses the Key ID returned by the backend.
- After payment, the browser sends the payment IDs to `/api/verify-payment`.
- Flask verifies the signature with your secret key before showing success.

### Common setup mistakes

- Putting the `.env` file in the wrong folder.
- Restarting the server after editing the keys.
- Leaving the cart empty, which makes the payment amount zero.
- Using Live keys on a Test dashboard account, or Test keys on a Live dashboard account.

## Deploy to Render (free hosting with custom domain)

1. Push code to GitHub
2. Go to https://render.com → New → Web Service
3. Connect your GitHub repo
4. Build command: `pip install -r requirements.txt`
5. Start command: `gunicorn app:app`
6. Add your environment variables in the Render dashboard
7. Add your custom domain in Render → Settings → Custom Domains

## Pages
- `/` — Homepage
- `/shop` — All co-ord sets with filters
- `/product/<id>` — Product detail with payment
- `/about` — About Chéa Studios & founder
- `/contact` — Contact form
- `/policies` — Shipping, returns, size guide
