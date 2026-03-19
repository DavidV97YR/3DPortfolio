# hololive-Merch-Archive

Automated archive of all products from [shop.hololivepro.com](https://shop.hololivepro.com).

## What this is

A GitHub Actions scraper runs every 30 minutes and:
- Fetches the full product catalog from the hololive shop (JP + EN)
- Archives product images permanently to this repo
- Records `published_at` (launch date) from the Shopify JSON
- Marks products as `delisted` if they disappear from the shop

## Structure

```
merch.json          ← full product archive (metadata + archived image URLs)
Products/
  {product-handle}/
    original-filename.jpg
    original-filename.png
    ...
```

## merch.json fields

| Field | Description |
|---|---|
| `product_id` | Shopify product ID |
| `handle` | URL-safe product handle |
| `title_jp` | Japanese title |
| `title_en` | English title |
| `tags_jp` | Shopify tags from JP store |
| `tags_en` | Shopify tags from EN store |
| `images` | Archived image URLs (this repo, permanent) |
| `min_price` | Minimum variant price in JPY |
| `max_price` | Maximum variant price in JPY |
| `published_at` | When the product first launched on the shop |
| `is_available` | Whether any variant is currently purchasable |
| `delisted_at` | When the product was removed from the shop (null if still listed) |

## Using the data

```javascript
const res = await fetch(
  'https://raw.githubusercontent.com/YOUR_USERNAME/hololive-Merch-Archive/main/merch.json'
);
const merch = await res.json();
```

## Setup

1. Push this repo to GitHub
2. Go to **Settings → Actions → General → Workflow permissions** → set to **Read and write**
3. The scraper runs automatically every 30 minutes
4. Trigger it manually any time from **Actions → Scrape Hololive Merch → Run workflow**

No secrets or API keys needed — `GITHUB_TOKEN` is provided automatically by GitHub Actions.
