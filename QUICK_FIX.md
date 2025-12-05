# 🚀 Quick Fix for Deployment Error

## The Problem
Your build is failing because Shopify environment variables are missing.

## The Solution (3 Steps)

### Step 1: Create `.env.local` file
Create a new file in the root directory: `c:\best-neon\.env.local`

### Step 2: Copy this content into `.env.local`
```
COMPANY_NAME="Your Company Name"
SITE_NAME="Next.js Commerce"
SHOPIFY_STORE_DOMAIN="your-store.myshopify.com"
SHOPIFY_STOREFRONT_ACCESS_TOKEN="your-token-here"
SHOPIFY_REVALIDATION_SECRET="any-random-string"
```

### Step 3: Fill in your actual Shopify values
Replace the placeholder values with your real Shopify credentials.

---

## Where to get your Shopify credentials?

**If you already have a Shopify store:**
1. Go to Shopify Admin → Settings → Apps and sales channels
2. Click "Develop apps" → "Create an app"
3. Configure Storefront API and get your access token

**If you DON'T have a Shopify store:**
1. Sign up for free at: https://www.shopify.com/partners
2. Create a development store with test data
3. Follow the steps above to get your credentials

---

## After setting up `.env.local`:

```bash
# Install dependencies
npm install

# Run dev server
npm run dev

# Build for production
npm run build
```

✅ Your deployment should now work!

---

📖 For detailed instructions, see: **SHOPIFY_SETUP.md**
