# 🧪 Testing Your Strapi APIs with Postman

A complete guide to testing your E-Commerce backend using Postman.

---

## 📮 What is Postman?

Postman is a tool to **test APIs without building frontend code**.

Think of it like this:
- **Browser**: Shows websites (HTML)
- **Postman**: Tests APIs (JSON responses)

You can:
- ✅ Test GET requests
- ✅ Test POST requests (create data)
- ✅ Test PUT requests (update data)
- ✅ Test DELETE requests (remove data)
- ✅ Pass authentication tokens
- ✅ Save requests for later
- ✅ Share with team

---

## 🚀 Setup Postman

### Step 1: Download

Go to: **https://www.postman.com/downloads/**

- Download for Windows
- Install it
- Create free account (or skip)

### Step 2: Open Postman

```
1. Click Postman icon
2. You're ready to test!
```

---

## 🧪 Basic API Testing

### Test 1: Get All Products (Easiest)

```
Method: GET
URL: http://localhost:1337/api/products
Headers: None needed
Body: Empty

Steps in Postman:
1. Select: GET (dropdown)
2. Paste URL: http://localhost:1337/api/products
3. Click "Send"
4. See response below!
```

**Expected Response:**
```json
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Laptop",
        "price": 999.99,
        "description": "Gaming laptop"
      }
    }
  ]
}
```

**If empty:** Go to Strapi admin and create a product first!

---

### Test 2: Get One Product

```
Method: GET
URL: http://localhost:1337/api/products/1

Response:
{
  "data": {
    "id": 1,
    "attributes": {
      "name": "Laptop",
      "price": 999.99,
      "description": "Gaming laptop"
    }
  }
}
```

---

### Test 3: Create Product (Needs Authentication)

#### Part 1: Get JWT Token (Login)

```
Method: POST
URL: http://localhost:1337/api/auth/local

Headers:
Content-Type: application/json

Body (raw JSON):
{
  "identifier": "admin@example.com",
  "password": "your-admin-password"
}
```

**Response:**
```json
{
  "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNzAwNDc4NDUxLCJleHAiOjE3MDMwNzA0NTF9.abc123...",
  "user": {
    "id": 1,
    "email": "admin@example.com",
    "username": "admin"
  }
}
```

**💾 COPY the JWT token (the long string)**

#### Part 2: Create Product with JWT

```
Method: POST
URL: http://localhost:1337/api/products

Headers:
Key: Authorization
Value: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...

(Paste your JWT token after "Bearer ")

Headers:
Key: Content-Type
Value: application/json

Body (raw JSON):
{
  "data": {
    "name": "iPhone 15",
    "price": 999.99,
    "description": "Latest iPhone"
  }
}
```

**Response:**
```json
{
  "data": {
    "id": 2,
    "attributes": {
      "name": "iPhone 15",
      "price": 999.99,
      "description": "Latest iPhone"
    }
  }
}
```

---

## 📋 All API Endpoints to Test

### Authentication Endpoints

#### 1. Register New User
```
POST http://localhost:1337/api/auth/local/register

Body:
{
  "username": "john_doe",
  "email": "john@example.com",
  "password": "SecurePassword123"
}

Response: JWT token + user info
```

#### 2. Login
```
POST http://localhost:1337/api/auth/local

Body:
{
  "identifier": "john@example.com",
  "password": "SecurePassword123"
}

Response: JWT token + user info
```

#### 3. Get Current User Profile
```
GET http://localhost:1337/api/me

Headers:
Authorization: Bearer [YOUR_JWT_TOKEN]

Response: Current user info
```

---

### Product Endpoints

#### 4. Get All Products
```
GET http://localhost:1337/api/products

Response: Array of all products
```

#### 5. Get One Product
```
GET http://localhost:1337/api/products/1

Response: Single product by ID
```

#### 6. Create Product
```
POST http://localhost:1337/api/products

Headers:
Authorization: Bearer [YOUR_JWT_TOKEN]
Content-Type: application/json

Body:
{
  "data": {
    "name": "Product Name",
    "price": 999.99,
    "description": "Product description"
  }
}

Response: Created product
```

#### 7. Update Product
```
PUT http://localhost:1337/api/products/1

Headers:
Authorization: Bearer [YOUR_JWT_TOKEN]
Content-Type: application/json

Body:
{
  "data": {
    "price": 799.99
  }
}

Response: Updated product
```

#### 8. Delete Product
```
DELETE http://localhost:1337/api/products/1

Headers:
Authorization: Bearer [YOUR_JWT_TOKEN]

Response: Empty or confirmation
```

---

## 🎯 Complete Testing Workflow

### Scenario: User buys a product

**Step 1: Register New User**
```
POST http://localhost:1337/api/auth/local/register

Body:
{
  "username": "customer1",
  "email": "customer@example.com",
  "password": "Password123"
}

✅ Response: JWT token
💾 Copy JWT token
```

**Step 2: Get All Products**
```
GET http://localhost:1337/api/products

✅ See available products
💾 Note a product ID (e.g., 1)
```

**Step 3: Create Order**
```
POST http://localhost:1337/api/orders

Headers:
Authorization: Bearer [JWT_FROM_STEP_1]

Body:
{
  "data": {
    "user": 1,
    "products": [1],
    "status": "pending",
    "total_amount": 999.99
  }
}

✅ Order created!
```

**Step 4: Get Order Details**
```
GET http://localhost:1337/api/orders/1

Headers:
Authorization: Bearer [JWT_FROM_STEP_1]

✅ See complete order info
```

---

## 💾 Saving Requests in Postman

### Create Collection

```
1. Click "Collections" (left sidebar)
2. Click "+" icon
3. Name: "Strapi E-Commerce Tests"
4. Create
```

### Create Folders

```
In your collection, right-click and add folders:

├─ Authentication
│  ├─ Register
│  ├─ Login
│  └─ Get Profile
│
├─ Products
│  ├─ Get All
│  ├─ Get One
│  ├─ Create
│  ├─ Update
│  └─ Delete
│
└─ Orders
   ├─ Get All
   ├─ Create
   └─ Delete
```

### Save Requests

```
1. Make a request
2. Click "Save" button (top right)
3. Select collection and folder
4. Name: "Get All Products"
5. Save!

Now next time: Just click the saved request!
```

---

## 🔐 Using Environment Variables

### Why Use Variables?

Instead of copying/pasting JWT token every time, save it to a variable!

### Setup

**1. Create Environment**
```
Click: Environments (top right)
Click: Create New

Name: Strapi Development

Variables:
- Name: base_url
  Initial: http://localhost:1337
  Current: http://localhost:1337

- Name: jwt_token
  Initial: (empty)
  Current: (empty)
```

**2. Use Variables in Requests**

Instead of:
```
http://localhost:1337/api/products
```

Use:
```
{{base_url}}/api/products
```

Instead of:
```
Authorization: Bearer eyJhbGciOi...
```

Use:
```
Authorization: Bearer {{jwt_token}}
```

**3. Update Variable After Login**

After logging in:
1. Copy JWT from response
2. Click "Environments"
3. Find "Strapi Development"
4. Paste JWT in `jwt_token`
5. Now all requests use it!

---

## 🧪 Test All Your Endpoints

### Quick Testing Checklist

```
Authentication:
□ POST /api/auth/local/register - Register new user
□ POST /api/auth/local - Login user
□ GET /api/me - Get user profile (with JWT)

Products:
□ GET /api/products - Get all
□ GET /api/products/1 - Get one
□ POST /api/products - Create (with JWT)
□ PUT /api/products/1 - Update (with JWT)
□ DELETE /api/products/1 - Delete (with JWT)

Orders (if created):
□ GET /api/orders - Get all (with JWT)
□ POST /api/orders - Create (with JWT)
□ GET /api/orders/1 - Get one (with JWT)
```

---

## 🐛 Common Issues & Solutions

### Issue 1: "Cannot GET /api/products"

**Problem:** Strapi is not running

**Solution:**
```bash
# Check if running
docker-compose ps

# Should show: strapi Up

# If not, start it
docker-compose up -d

# Wait 60 seconds and retry
```

---

### Issue 2: "401 Unauthorized"

**Problem:** Missing or invalid JWT token

**Solution:**
```
1. Check headers have: Authorization: Bearer [token]
2. Check JWT token is not expired
3. Login again to get new token
4. Paste new token in Authorization header
5. Try again
```

---

### Issue 3: "400 Bad Request"

**Problem:** Body format is wrong

**Solution:**
```
1. Check method is POST (not GET)
2. Check Body is set to "raw"
3. Check Content-Type is "application/json"
4. Check JSON syntax (no trailing commas)
5. Validate JSON at: https://jsonlint.com
```

---

### Issue 4: Empty Products List

**Problem:** No products created yet

**Solution:**
```
1. Go to Strapi admin: http://localhost:1337/admin
2. Content Manager → Product
3. Click "Create new entry"
4. Fill in fields
5. Click "Save" then "Publish"
6. Go back to Postman
7. Click "Send" again
```

---

### Issue 5: CORS Error

**Problem:** Frontend can't reach API

**Solution:**
```
For local testing: Usually not an issue

For production: Configure CORS in Strapi
1. Go to admin panel
2. Settings → Users & Permissions Plugin
3. Roles → Public
4. Enable correct endpoints
5. Or add frontend domain to allowed origins
```

---

## 📊 Postman Features You Can Use

### Pre-request Scripts

Run code before request (e.g., generate token):
```javascript
// Example: Add timestamp
pm.environment.set("timestamp", new Date().getTime());
```

### Tests

Validate response automatically:
```javascript
// Check response status is 200
pm.test("Status is 200", function () {
    pm.response.to.have.status(200);
});

// Check response has data
pm.test("Response has data", function () {
    pm.expect(pm.response.json()).to.have.property("data");
});
```

### Workflows

Run multiple requests in sequence:
```
1. Login (get JWT)
2. Create product (use JWT)
3. Get product (use JWT)
4. Delete product (use JWT)

All automated!
```

---

## 🎓 Alternative Testing Tools

### Insomnia (Similar to Postman)
```
Free alternative
https://insomnia.rest
Same functionality as Postman
```

### Thunder Client (VS Code Extension)
```
VS Code → Extensions → Thunder Client
No separate download
Lightweight and fast
```

### cURL (Command Line)

```bash
# Get all products
curl http://localhost:1337/api/products

# Create product with JWT
curl -X POST http://localhost:1337/api/products \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"data": {"name": "Phone", "price": 599.99}}'

# Update product
curl -X PUT http://localhost:1337/api/products/1 \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"data": {"price": 499.99}}'

# Delete product
curl -X DELETE http://localhost:1337/api/products/1 \
  -H "Authorization: Bearer YOUR_JWT_TOKEN"
```

---

## ✅ Step-by-Step First Test

### Let's test your API RIGHT NOW!

**Step 1: Start Strapi** (if not running)
```bash
cd d:\HUST\GHWorkspace\Back-End_SandBox
docker-compose up -d
```

**Step 2: Wait 60 seconds**

**Step 3: Open Postman**

**Step 4: Test GET Products**
```
Method: GET
URL: http://localhost:1337/api/products
Click: Send
```

**Step 5: See Response**
```
✅ If you see products → Backend works!
❌ If empty → Go to admin and create product
❌ If error → Make sure Strapi is running
```

**Step 6: Go to Admin**
```
Open: http://localhost:1337/admin
Create a product:
- Name: "Test Product"
- Price: 99.99
- Click Save & Publish
```

**Step 7: Test Again**
```
Go back to Postman
Click Send (same request)
Now you should see your product!
```

---

## 💡 Pro Tips

```
1. Save your requests
   → Click "Save" button
   → Reuse them later

2. Use environment variables
   → Set {{base_url}} = http://localhost:1337
   → Set {{jwt_token}} after login

3. Test error cases
   → Wrong password
   → Missing JWT
   → Invalid data
   → Wrong method (POST vs GET)

4. Check response status
   → 200 = OK ✅
   → 201 = Created ✅
   → 400 = Bad request ❌
   → 401 = Unauthorized ❌
   → 404 = Not found ❌
   → 500 = Server error ❌

5. Format JSON responses
   → Pretty print makes it readable
   → Postman does this automatically

6. Share collection with team
   → Postman → Share → Export collection
   → Team can import and use
```

---

## 🎯 Testing Checklist

### Before Launching Frontend

```
□ All GET endpoints return data
□ POST creates data correctly
□ PUT updates data correctly
□ DELETE removes data correctly
□ JWT authentication works
□ Unauthorized requests return 401
□ Invalid data returns 400
□ All responses have correct structure
□ Images upload correctly (if applicable)
□ Pagination works (if large datasets)
□ Filters work (if applicable)
□ Sorting works (if applicable)
```

---

## 🚀 Next Steps

1. **Download Postman** - https://www.postman.com/downloads/
2. **Start Strapi** - `docker-compose up -d`
3. **Test GET products** - See if data appears
4. **Create sample data** - In Strapi admin
5. **Test POST** - Create via Postman
6. **Test PUT** - Update via Postman
7. **Test DELETE** - Remove via Postman
8. **Save requests** - In collection
9. **Use variables** - For JWT token
10. **Test complete flow** - Register → Login → Create → Get → Delete

---

## ✨ You're Ready!

Postman is your best friend for testing APIs! 🚀

Use it to:
- ✅ Verify backend works
- ✅ Find bugs before frontend
- ✅ Document APIs
- ✅ Share with team
- ✅ Automate testing

**Happy testing!** 🧪
