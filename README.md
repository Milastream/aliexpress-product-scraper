[Aliexpress Product Scraper](https://apify.com/thirdwatch/aliexpress-product-scraper?fpr=data)

# AliExpress Scraper

> Scrape AliExpress product search results — titles, sale and original prices, discount percentages, ratings, orders count, and selling points.

## What you get

Search AliExpress by keyword and extract structured product data. Useful for dropshipping research, cross-border price comparison, and trend spotting. Supports sorting by relevance, best-selling, or price, plus min/max price filtering.

## Output fields

| Field | Description |
| --- | --- |
| `product_id` | AliExpress product ID |
| `title` | Product title |
| `url` | Product page URL |
| `sale_price` | Current sale price (numeric) |
| `original_price` | Original price before discount (numeric) |
| `discount_percentage` | Discount percentage (numeric) |
| `rating` | Product star rating |
| `orders_count` | Number of orders placed |
| `image_url` | Product image URL |
| `selling_points` | Highlighted selling points (e.g., "Free Shipping", "Noise Cancelling") |
| `is_sponsored` | Whether the result is a sponsored listing |

## Example output

```
{
    "product_id": "1005006789123456",
    "title": "Wireless Bluetooth Earbuds TWS Headphones with Noise Cancelling",
    "url": "https://www.aliexpress.com/item/1005006789123456.html",
    "sale_price": 12.99,
    "original_price": 25.99,
    "discount_percentage": 50.0,
    "rating": 4.7,
    "orders_count": 10234,
    "image_url": "https://ae01.alicdn.com/kf/...",
    "selling_points": ["Free Shipping", "Noise Cancelling", "30h Battery"],
    "is_sponsored": false
}
```

## Input parameters

| Parameter | Required | Description |
| --- | --- | --- |
| `queries` | Yes | Product search terms (e.g., `["bluetooth earbuds", "phone case"]`). |
| `maxResults` | No | Max products per query. Default `15`, max `500`. |
| `sortBy` | No | One of `default` (relevance), `orders` (best selling), `price_asc`, `price_desc`. Default `default`. |
| `minPrice` | No | Minimum price filter in USD. |
| `maxPrice` | No | Maximum price filter in USD. |
| `proxyConfiguration` | No | Pre-configured for best results. Leave as-is. |

## Use cases

- **Dropshippers**: Identify high-order, high-rating products with large margins before listing on Shopify or Amazon.
- **Price analysts**: Track original vs. sale prices and discount depth across product categories.
- **Market researchers**: Spot trending cross-border products and emerging brands.
- **Sourcing teams**: Filter by price range and order count to find reliable suppliers.

## Pricing

Pay-per-result pricing. Tiered discounts apply automatically based on usage volume.

| Tier | Price per result |
| --- | --- |
| FREE | $0.003 |
| BRONZE | $0.0025 |
| SILVER | $0.002 |
| GOLD | $0.0016 |

## Limitations

- Returns search-results data; product-detail pages (variant SKUs, shipping matrix, full review text) are not fetched.
- Prices shown in USD may differ from what a buyer in another region sees — AliExpress localizes pricing by geo.
- Sponsored listings may be missing `rating` or `orders_count`.
- Filters `minPrice`/`maxPrice` are applied at AliExpress's end in USD; precision can vary slightly for non-USD catalogs.

## Compared to alternatives

- **vs. scrapefish/aliexpress-scraper** (~$0.01/result): This actor runs at $0.003/result on FREE and drops to $0.0016 on GOLD — roughly 3-6x cheaper.
- **vs. AliExpress Open Platform API**: Requires an approved affiliate account and strict traffic auditing. This actor has no login, no partnership, and works for any category.

Pairs well with [Amazon Scraper](https://apify.com/thirdwatch/amazon-product-scraper) and [Noon.com Scraper](https://apify.com/thirdwatch/noon-scraper) for global marketplace coverage.

## FAQ

**Can I filter by price?**
Yes. Use `minPrice` and `maxPrice` (USD) to narrow results.

**Can I sort by best-selling?**
Yes. Set `sortBy: "orders"`.

**Do I need an AliExpress account?**
No. Only publicly visible search results are scraped.

**Are shipping costs included?**
No. Shipping is calculated per buyer location on AliExpress and is not present in search listings.

Last verified: 2026-04

More scrapers at [thirdwatch.dev](https://thirdwatch.dev).