[Aliexpress Product Scraper](https://apify.com/sovereigntaylor/aliexpress-product-scraper?fpr=data)

# AliExpress Product Scraper

Scrape AliExpress products at scale. Extract titles, prices, discounts, order counts, ratings, reviews, store info, shipping details, images, and variants. Built for dropshipping research, supplier discovery, and competitive intelligence.

## Features

- **Search by keyword** — scrape products matching any search term
- **Direct product URLs** — scrape specific product pages for full details
- **Category browsing** — scrape all products in any AliExpress category
- **Store scraping** — extract all products from a specific AliExpress store
- **Price & rating filters** — narrow results to products that match your criteria
- **Free shipping filter** — find products with free shipping for dropshipping
- **Rich data extraction** — prices, discounts, order counts, ratings, reviews, images, variants, store info, and shipping details
- **Pay-per-result pricing** — only pay for products successfully scraped

## Input

| Field | Type | Default | Description |
| --- | --- | --- | --- |
| searchTerms | array | `[]` | Keywords to search (e.g., `["wireless earbuds", "phone case"]`) |
| productUrls | array | `[]` | Direct AliExpress product or store URLs to scrape |
| category | string | `""` | Category page URL to browse |
| minPrice | integer | `0` | Minimum price filter in USD |
| maxPrice | integer | `0` | Maximum price filter in USD |
| freeShipping | boolean | `false` | Only scrape products with free shipping |
| minRating | number | `0` | Minimum star rating (0-5) |
| maxResults | integer | `500` | Maximum products to scrape |
| proxy | object | Apify residential | Proxy configuration |

## Output

Each scraped product includes:

```
{
  "title": "TWS Wireless Bluetooth Earbuds Noise Cancelling",
  "price": 12.99,
  "originalPrice": 25.98,
  "discount": "50%",
  "orders": 15432,
  "rating": 4.8,
  "reviews": 3241,
  "store": "TechGadgets Official Store",
  "storeUrl": "https://www.aliexpress.com/store/12345678",
  "storeRating": 96.5,
  "shippingCost": "Free Shipping",
  "shippingTime": "15-30 days",
  "images": [
    "https://ae01.alicdn.com/kf/...",
    "https://ae01.alicdn.com/kf/..."
  ],
  "variants": [
    { "name": "Color", "options": ["Black", "White", "Blue"] },
    { "name": "Ships From", "options": ["China", "US"] }
  ],
  "url": "https://www.aliexpress.com/item/1005006123456789.html",
  "productId": "1005006123456789",
  "currency": "USD",
  "scrapedAt": "2026-03-01T12:00:00.000Z"
}
```

## Use Cases

### Dropshipping Research

Find winning products with high order counts and good ratings. Filter by free shipping and price range to identify profitable products for your store.

```
{
  "searchTerms": ["wireless earbuds", "phone accessories", "LED lights"],
  "freeShipping": true,
  "minRating": 4.0,
  "maxResults": 200
}
```

### Supplier Discovery

Scrape entire stores to evaluate suppliers. Compare product ranges, pricing, and store ratings.

```
{
  "productUrls": [
    "https://www.aliexpress.com/store/12345678"
  ],
  "maxResults": 1000
}
```

### Price Monitoring

Track specific products by URL. Run daily to monitor price changes and discount events.

```
{
  "productUrls": [
    "https://www.aliexpress.com/item/1005006123456789.html",
    "https://www.aliexpress.com/item/1005006987654321.html"
  ]
}
```

### Competitor Analysis

Search for products in your niche, filter by rating, and analyze pricing strategies.

```
{
  "searchTerms": ["yoga mat premium"],
  "minPrice": 10,
  "maxPrice": 50,
  "minRating": 4.5,
  "maxResults": 100
}
```

### Category Analysis

Browse an entire AliExpress category to understand market trends and pricing.

```
{
  "category": "https://www.aliexpress.com/category/44/consumer-electronics.html",
  "maxResults": 500
}
```

## Pricing

Pay-per-result pricing at $0.004 per product scraped. You only pay for products successfully extracted. No charge for failed or duplicate requests.

## Tips for Best Results

1. **Use residential proxies** — AliExpress may block datacenter IPs at scale
2. **Start with smaller batches** — test with 50-100 products first
3. **Use specific search terms** — more specific queries yield more relevant results
4. **Combine filters** — use minRating + freeShipping to find dropshipping winners
5. **Schedule regular runs** — prices and availability change frequently on AliExpress

## Legal Disclaimer

This actor is provided for legitimate research purposes including market analysis, price monitoring, and competitive intelligence. Users are responsible for ensuring their use complies with applicable laws and AliExpress terms of service.

## Integration — Python

```
from apify_client import ApifyClient

client = ApifyClient("YOUR_API_TOKEN")
run = client.actor("sovereigntaylor/aliexpress-scraper").call(run_input={
    "searchTerm": "aliexpress",
    "maxResults": 50
})

for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(f"{item.get('title', item.get('name', 'N/A'))}")
```

## Integration — JavaScript

```
import { ApifyClient } from 'apify-client';
const client = new ApifyClient({ token: 'YOUR_API_TOKEN' });

const run = await client.actor('sovereigntaylor/aliexpress-scraper').call({
    searchTerm: 'aliexpress',
    maxResults: 50
});

const { items } = await client.dataset(run.defaultDatasetId).listItems();
items.forEach(item => console.log(item.title || item.name || 'N/A'));
```