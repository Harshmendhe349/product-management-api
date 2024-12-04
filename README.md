# Product Management API

This repository contains the source code for the **Product Management API**, a backend system to manage products, including creating, updating, retrieving, and managing stock quantities. The system is built using **Node.js**, **Express.js**, and an **SQLite database**.

## Live Demo
The API is hosted at: **[https://your-public-url.vercel.app](https://your-public-url.vercel.app)**

## Features
- **Create a Product:** Add a new product with its name, category, price, and stock quantity.
- **Update a Product:** Update existing product details, including stock quantities.
- **Get All Products:** Retrieve a list of all products.
- **Get a Product by ID:** Retrieve details of a specific product using its ID.
- **Get Total Stock Quantity:** Calculate the total stock available for all products.

## Technologies Used
- **Node.js**: Server-side JavaScript runtime.
- **Express.js**: Web framework for building APIs.
- **SQLite**: Lightweight relational database for storage.
- **Vercel**: Platform for hosting and deployment.

---

## Deployment
The application is deployed on **Vercel** for public access. Use the public URL to test endpoints with tools like **Postman** or **curl**.

---

## Concurrency Control Techniques

### 1. **Optimistic Concurrency Control**
This method assumes that stock conflicts are rare. When an order is placed:
- The system reads the current stock level.
- Calculates the new stock after the order.
- Attempts to update the stock in the database.
- Before finalizing, the system verifies that the stock quantity has not changed since it was initially fetched.

If the stock has changed (e.g., another order was placed in parallel), the update fails, and the process may be retried or a conflict message is displayed.

#### Advantages:
- Simple and easy to implement.
- Suitable for systems with low traffic.

#### Disadvantages:
- Can lead to race conditions if many orders are placed simultaneously.

---

### 2. **Pessimistic Locking**
This approach involves locking the database record to prevent other transactions from modifying the stock until the current process completes. For example:
- When an order is placed, the product’s row is locked during the stock update.
- No other transaction can interfere until the process is finished.

#### Advantages:
- Avoids race conditions and ensures consistency.
- Ideal for high-concurrency systems with frequent stock updates.

#### Disadvantages:
- Can introduce performance bottlenecks due to row locking.
- May cause delays if long-running transactions lock rows for extended periods.

---

## How to Run Locally
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/product-management-api.git
   cd product-management-api
2. Install Dependencies:
    ```bash
    npm install
3. Start the Server:
    ```bash
    npm start
4. Access the API Locally: 
   The API will be accessible at: http://localhost:3000

## API Endpoints
### Create a Product
POST /products
-Request Body: { name, category, price, stock_quantity }
Update a Product
PUT /products/:id

Request Body: { name, category, price, stock_quantity }
Get All Products
GET /products

Get a Product by ID
GET /products/:id

Get Total Stock Quantity
GET /products/getQuantity
write 
