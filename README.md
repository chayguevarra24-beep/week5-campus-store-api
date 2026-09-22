# Activity: Design a Campus Store API

**Name:** Joyce Anne J. Guevarra  
**Section:** ACT2  
**Activity:** Week 5 — Design a Campus Store API

## Scenario

A campus store has thousands of products. Students may retry order requests after connection failures, and two students may attempt to purchase the last item.

This API design addresses duplicate orders, concurrent purchases, large product catalogs, controlled API responses, and future API changes.

---

# 1. Endpoints & Pagination

## 1.1 Get One Product

This endpoint retrieves a specific product by its ID.

### Request

```http
GET /api/v1/products/101 HTTP/1.1
Host: api.campusstore.example.com
Accept: application/json
