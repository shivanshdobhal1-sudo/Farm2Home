# Farm2Home — Technical Design Document

## 1. Architecture

```text
                    ┌─────────────────────┐
                    │      Consumer       │
                    └──────────┬──────────┘
                               │ Search / Browse
                               ▼
┌─────────────────┐     ┌─────────────────────┐
│     Farmer      │────▶│  Farm2Home Web App  │
└─────────────────┘     │     (MVP Frontend)  │
  Product Listing       └───────┬───────┬─────┘
                                │       │
                         Product Data   │ Map/Farm Data
                                │       │
                                ▼       ▼
                         Marketplace  GIS Layer
                                │       │
                                └───┬───┘
                                    ▼
                              Order Journey
```

## 2. Current MVP Components

### Frontend
- `index.html` contains the UI, CSS and JavaScript.
- Product data is stored in an in-memory JavaScript array.
- Cart and demo orders are handled in browser memory.
- The map is a schematic SVG to demonstrate the intended GIS experience.

### Data model

A product record contains:

```text
id
name
category
price
quantity
farmer
village
district
emoji
```

## 3. User flows

### Consumer
1. Open Farm2Home.
2. Browse/search products.
3. Filter by category.
4. View farmer and village details.
5. Add products to cart.
6. Place a demo order.
7. View order history.

### Farmer
1. Open Farmer Corner.
2. Enter farmer name and location.
3. Add product, category, price and quantity.
4. Publish product.
5. Product appears in the marketplace and village map view.

## 4. GIS evolution path

The current SVG map is intentionally a lightweight prototype. A production version can replace it with a real GIS layer using a mapping provider such as OpenStreetMap/Leaflet or another approved map service.

Planned location attributes:

```text
farmer_id
latitude
longitude
village
block
district
farm_area
crop/product
availability
```

## 5. Production architecture (future)

```text
Mobile/Web Client
       │
       ▼
API Gateway / Backend
   ┌───┼───────────┐
   ▼   ▼           ▼
Users Products   Orders
   │   │           │
   └───┼───────────┘
       ▼
 PostgreSQL/PostGIS
       │
       ├── GIS / farm locations
       ├── marketplace data
       └── analytics

External services:
- Maps/GIS
- Payment/UPI
- Notifications
- Logistics
```

## 6. Security and privacy considerations

- Authenticate farmers and consumers in the production version.
- Validate and sanitize all user input.
- Protect phone numbers and personal data.
- Use HTTPS and secure API authentication.
- Do not expose precise farm coordinates publicly without farmer consent.

## 7. Scalability

The concept can start with one district, expand to multiple districts in Uttarakhand, and then scale to other remote agricultural regions in India.
