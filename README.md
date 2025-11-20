# 🛍️ E-Commerce Backend (Strapi + Docker + Neon)
A clean, production-ready backend template for e-commerce projects using **Strapi CMS**, **Docker**, and **Neon PostgreSQL**.

This setup requires **zero backend coding** — everything is configured through Strapi’s powerful admin dashboard.

---

## 🚀 Features
- **Admin Panel** – Manage products, categories, users, orders
- **Auto‑Generated REST API** – No manual controllers or routes
- **GraphQL API** – Optional modern querying
- **Dockerized Deployment** – Easy to run locally or on cloud
- **PostgreSQL on Neon** – Cloud-hosted, secure, and scalable
- **Authentication Included** – JWT, roles & permissions
- **Media Upload Support** – Images & files via Strapi
- **Production‑ready Architecture** – Environment variables, secrets, scalability

---

## ⚙️ Prerequisites
Make sure you have these installed before starting:

### 1. Docker & Docker Compose
Check your installation:
```bash
docker --version
docker-compose --version
```
If missing → install Docker Desktop.

### 2. Neon PostgreSQL Account
1. Visit https://console.neon.tech
2. Create a project + database
3. Copy your PostgreSQL connection string:
```
postgresql://user:password@host/db?sslmode=require
```

### 3. Text Editor (to edit `.env`)
Recommended: VS Code

### 4. (Optional) Postman
For API testing.

---

## 🚀 Quick Start (15 Minutes)
### 1. Update the `.env` file
Inside the project folder:
```
DATABASE_URL=postgresql://user:password@host/database?sslmode=require
```
Use the connection string from Neon.

### 2. Start Docker
```bash
docker-compose up -d
```
Wait ~60 seconds for Strapi to boot.

### 3. Open Admin Panel
Navigate to:
```
http://localhost:1337/admin
```
Create your admin account → done!

---

## 📁 Project Structure
```
.env                       # Secrets & environment config
LICENSE                   # MIT License
docker-compose.yml        # Strapi + PostgreSQL containers
QUICK_START.md            # Fast 3-step guide
STRAPI_DOCKER_SETUP.md    # Full Docker walkthrough
NEON_CONNECTION.md        # Database connection help
ARCHITECTURE_OVERVIEW.md  # System architecture
TESTING.md                # Postman API testing guide
```

---

## 📚 How Strapi Works (No Coding Required)
Strapi generates everything automatically:
- Database tables
- REST endpoints
- GraphQL resolvers
- Authentication
- Admin UI
- Input validation

### What you actually do:
1. Create collection types (e.g., Product, Category)
2. Add fields through UI (Text, Number, Media, Relation)
3. Click **Save** → APIs instantly generated

### What you *don’t* do:
- ❌ Write backend TypeScript
- ❌ Build controllers
- ❌ Design routes
- ❌ Write SQL
- ❌ Code authentication

---

## 🗄️ Example Collections
### **Products**
- name (Text)
- price (Number)
- description (Rich Text)
- image (Media)
- category (Relation → Categories)

### **Users** (Built-in)
- username
- email
- password (hashed)
- role

### **Orders**
- order_number
- user (Relation → Users)
- products (Relation → Products)
- total_amount
- status (pending/shipped/delivered)

---

## 🔌 API Examples
### Get all products
```bash
GET http://localhost:1337/api/products
```

### Create a product (JWT required)
```bash
POST /api/products
Authorization: Bearer <token>
Content-Type: application/json
```

### Sample request body
```json
{
  "data": {
    "name": "Laptop",
    "price": 999.99
  }
}
```

---

## 🔐 Authentication
Strapi includes everything:
- Password hashing (bcrypt)
- JWT login / register
- Protected routes
- Roles & Permissions

Example:
```bash
POST /api/auth/local
POST /api/auth/local/register
```

---

## 🧪 Testing with Postman
1. Test: `GET /api/products`
2. Login → copy JWT token
3. Make authorized requests using:
```
Authorization: Bearer <your_jwt>
```
See **TESTING.md** for detailed steps.

---

## ⚠️ Security Checklist (Before Deployment)
- [ ] Change `ADMIN_JWT_SECRET`
- [ ] Change `TRANSFER_TOKEN_SALT`
- [ ] Use HTTPS
- [ ] Restrict CORS to your frontend
- [ ] Use strong admin password
- [ ] Never commit `.env`

---

## 🧩 Local Database Development (Neon Local Connect)
If you want to develop Strapi locally without affecting production data, the **recommended database workflow** is:

### ✅ Use Neon Development Branch
- Create a **dev branch** in Neon
- This isolates experimental data and schema changes
- Safe for testing, breaking things, deleting tables, etc.

### ✅ Use VS Code *Neon Local Connect* Extension
This extension creates a secure local proxy so Strapi connects like this:
```
Strapi (Docker) → localhost:5432 → Neon Cloud (dev branch)
```
You get the speed of local DB + the safety of cloud isolation.

### ✔️ Example `.env` for Local Development
```
DATABASE_URL=postgresql://user:password@localhost:5432/your_dev_branch
```

### 🔥 Benefits
- No need to install PostgreSQL locally
- Does *not* touch production or main DB branch
- Low latency & stable connection
- Safe environment for testing new collections

---

## 🚀 Deployment
Your backend can be deployed to:
- Railway
- Render
- AWS ECS / EC2
- Azure
- Google Cloud
- Any Docker-compatible provider

Build image:
```bash
docker-compose build
```
Push & deploy.
Database remains on Neon.

---

## 🆘 Troubleshooting
### Docker not starting?
```
docker-compose logs strapi
```

### Can't connect to database?
- Wrong `DATABASE_URL`
- Neon project not running
- SSL mode missing

### Admin panel not loading?
- Wait 60 seconds
- Try incognito mode
- Check port 1337

---

## 📄 License
MIT License — free to use anywhere.

---

**Your backend is ready to launch! 🚀**

