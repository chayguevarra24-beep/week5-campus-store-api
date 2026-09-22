# Activity: Design a Campus Store API

**Name:** Joyce Anne J. Guevarra  
**Section:** ACT2  
**Activity:** Week 5 — Design a Campus Store API

## Scenario

A campus store has thousands of products. Students may retry order requests after connection failures, and two students may attempt to purchase the last item.

The API must handle idempotency, transactions and concurrency, pagination, response DTOs, and API versioning.

---

# 1. Endpoints & Pagination

## 1.1 Get One Product

This endpoint retrieves a specific product by its ID.

### Request

```http
GET /api/v1/products/101 HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json

{
  "id": 101,
  "name": "Campus Hoodie",
  "price": 89.00
}

GET /api/v1/products?category=clothing&sort=price&direction=asc&limit=3 HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json

GET /api/v1/products?limit=3 HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json

{
  "data": [
    {
      "id": 101,
      "name": "Campus Hoodie",
      "price": 89.00
    },
    {
      "id": 102,
      "name": "University Shirt",
      "price": 45.00
    },
    {
      "id": 103,
      "name": "Campus Tote Bag",
      "price": 25.00
    }
  ],
  "next_cursor": "eyJpZCI6MTAzfQ=="
}

GET /api/v1/products?limit=3&cursor=eyJpZCI6MTAzfQ== HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json

POST /api/v1/orders HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json
Content-Type: application/json
Idempotency-Key: checkout-abc123

{
  "product_id": 101,
  "quantity": 1
}

POST /api/v1/orders HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json
Content-Type: application/json
Idempotency-Key: checkout-abc123

{
  "product_id": 101,
  "quantity": 1
}

POST /api/v1/orders HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json
Content-Type: application/json
Idempotency-Key: checkout-abc123

{
  "product_id": 101,
  "quantity": 1
}
