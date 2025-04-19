# Drink Store - MuleSoft Application

This is a MuleSoft application built in Anypoint Studio for a drink store that has adopted a **service-based architecture** approach.

## Project Overview

The application handles two main resources:

- **Buyers**
- **Orders**

The goal was to implement a robust system for handling CRUD operations on these entities, including specific business logic for large orders and external system integration.

## Technologies Used

- MuleSoft
- RAML
- JSON & XML
- Embedded File Storage
- Database - PostgreSQL

## Features & Endpoints

### **Buyers Resource**

- **GET /buyers**  
  Returns all buyers.  
  Optional Header: `active` (`true` or `false`) to filter by activity status.  
  If an invalid value is sent, a proper error message is returned.

- **POST /buyers**  
  Adds a new buyer.  
  Handles duplicate entries with custom exception handling.

- **GET /buyers/{id}**  
  Fetches a buyer by ID.  
  Also writes buyer details into a file stored locally.

- **PUT /buyers/{id}**  
  Updates a buyer if they exist, otherwise inserts as a new record.

- **DELETE /buyers/{id}**  
  Deletes a buyer by ID.  
  Returns `404 Not Found` if buyer does not exist.

### Status Code Handling
- All endpoints return appropriate status codes (`200`, `201`, `404`, `400`, etc.) depending on the operation result or error.


### 📍 **Orders Resource**

- **POST /orders**  
  Handles order submissions.

  ✅ For **all orders**:
  - Stored in an XML file with a unique name (prefix: `internalERP`)  
  - XML structure is wrapped in `<order>` root element  
  - Saved to: `src/main/resources/internalERP/`

  ✅ For **large orders** (outsourced to Chinese ERP):
  - Conditions:
    - `productType == "C"`  
    - `amount > 100` units
  - Order saved in JSON format  
  - Amount is multiplied by 2  
  - File saved with prefix `chineseERP` to: `src/main/resources/chineseERP/`
 
The RAML document included in this repository describes all the CRUD operations and request/response structures for both `buyers` and `orders` resources.
