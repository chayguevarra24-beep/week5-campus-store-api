# Campus Store API Design Document

* **Student Name:** Joyce Anne J. Guevarra
* **Course:** ACT2
* **Activity:** Week 5 — Design a Campus Store API

---

## 1. Endpoints & Pagination

This section covers retrieving individual products, listing filtered/sorted product catalogs, and creating customer orders.

### API Endpoints
* **Get Single Product:** `GET /api/v1/products/{id}`
  * *Path Parameter:* `id` (integer) — Unique identifier of the product.
* **List Products:** `GET /api/v1/products`
  * *Query Parameters:* `limit` (integer), `cursor` (string), `category` (string), `sort` (string: `price_asc`, `price_desc`, `name_asc`).
* **Create Order:** `POST /api/v1/orders`
  * *Body Parameters:* `student_id` (string), `product_id` (integer), `quantity` (integer).

### Pagination Choice: Cursor-Based Pagination
With thousands of products in the campus store, **cursor-based pagination** (using `cursor` and `limit`) is selected over offset-based pagination (`page` and `offset`). Offset-based queries degrade performance on large database tables (`OFFSET 10000` requires scanning previous rows) and lead to duplicate or missed items if new products are added while browsing. Cursors use stable pointers (such as record IDs).

### Example Requests & Responses

**First Request (Initial Batch):**
```http
GET /api/v1/products?limit=2&category=stationery&sort=price_asc
```
