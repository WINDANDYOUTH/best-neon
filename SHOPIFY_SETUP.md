# Shopify Environment Setup Guide

## 🚀 Quick Start

You need to create a `.env.local` file in the root directory with your Shopify credentials to make this project work.

## 📝 Step-by-Step Instructions

### 1. Create `.env.local` file

Create a new file named `.env.local` in the root directory (`c:\best-neon\.env.local`)

### 2. Add the following content to `.env.local`:

```env
# Your company/brand name
COMPANY_NAME="Your Company Name"

# Your site name (will appear in page titles)
SITE_NAME="Next.js Commerce"

# Shopify Store Domain (e.g., your-store.myshopify.com)
SHOPIFY_STORE_DOMAIN="your-store.myshopify.com"

# Shopify Storefront API Access Token
SHOPIFY_STOREFRONT_ACCESS_TOKEN="your-storefront-access-token-here"

# Shopify Webhook Revalidation Secret (any random string)
SHOPIFY_REVALIDATION_SECRET="your-random-secret-string"
```

### 3. Get Your Shopify Credentials

#### Option A: If you have a Shopify store already

1. **Get SHOPIFY_STORE_DOMAIN:**
   - Look at your Shopify admin URL
   - It will be something like `your-store.myshopify.com`
   - Copy just the domain part

2. **Get SHOPIFY_STOREFRONT_ACCESS_TOKEN:**
   - Go to your Shopify Admin
   - Navigate to: **Settings** → **Apps and sales channels**
   - Click **"Develop apps"** (you may need to enable this first)
   - Click **"Create an app"**
   - Name it (e.g., "Next.js Storefront")
   - Click **"Configure Storefront API"**
   - Enable these access scopes:
     - `unauthenticated_read_product_listings`
     - `unauthenticated_read_product_inventory`
     - `unauthenticated_read_product_tags`
     - `unauthenticated_read_collection_listings`
   - Click **"Save"**
   - Go to **"API credentials"** tab
   - Click **"Install app"**
   - Copy the **Storefront API access token**

3. **Set SHOPIFY_REVALIDATION_SECRET:**
   - Use any random string (e.g., generate one at https://randomkeygen.com/)

#### Option B: Create a Shopify Partner Development Store (FREE)

1. **Sign up for Shopify Partners** (free):
   - Go to: https://www.shopify.com/partners
   - Click "Join now" and create an account

2. **Create a Development Store:**
   - Log in to your Partner Dashboard
   - Click **"Stores"** → **"Add store"**
   - Select **"Development store"**
   - Fill in the store details
   - Choose **"Start with test data"** (this will populate your store with sample products)
   - Click **"Create development store"**

3. **Get your credentials:**
   - Follow the same steps as "Option A" above to get your access token

### 4. Verify Your Setup

After creating the `.env.local` file with your credentials:

```bash
# Install dependencies (if not already done)
npm install

# Run the development server
npm run dev
```

The app should now start without errors!

### 5. Deploy to Production

When deploying to Vercel or other platforms, add these environment variables in your deployment platform's settings:

- `COMPANY_NAME`
- `SITE_NAME`
- `SHOPIFY_STORE_DOMAIN`
- `SHOPIFY_STOREFRONT_ACCESS_TOKEN`
- `SHOPIFY_REVALIDATION_SECRET`

## ⚠️ Important Notes

- **Never commit `.env.local` to git** - it's already in `.gitignore`
- The `.env.local` file takes precedence over `.env`
- Restart your dev server after changing environment variables
- For production deployments, set these variables in your hosting platform's dashboard

## 🔧 Troubleshooting

**Build Error: "Error occurred prerendering page"**
- This means your environment variables are missing or incorrect
- Double-check that `.env.local` exists and has valid credentials
- Make sure `SHOPIFY_STORE_DOMAIN` doesn't include `https://` or brackets

**"Invalid Storefront Access Token"**
- Make sure you're using the **Storefront API** token, not the Admin API token
- Verify the token has the required access scopes enabled

**No products showing**
- Make sure your Shopify store has products
- Check that products are published to the "Online Store" sales channel
- If using a development store, select "Start with test data" when creating it

## 📚 Additional Resources

- [Shopify Storefront API Documentation](https://shopify.dev/docs/api/storefront)
- [Next.js Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)
- [Shopify Partners Program](https://www.shopify.com/partners)
