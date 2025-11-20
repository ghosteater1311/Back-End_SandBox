# 🚀 Strapi + Docker + Neon Setup Guide

## Overview
You have:
- ✅ Strapi (CMS) in Docker
- ✅ PostgreSQL connected to Neon Cloud
- ✅ Neon Local Extension for local development

---

## Step 1: Get Your Neon Connection String

### Option A: Using Neon Local Extension (Recommended for Local Dev)
```bash
# If you installed Neon local extension, it auto-creates a proxy
# Your connection string looks like:
postgresql://user:password@localhost:5432/database_name

# This connects to Neon Cloud through the local extension
```

### Option B: Direct Neon Cloud Connection
```bash
# From Neon console:
# 1. Go to neon.tech
# 2. Login to your account
# 3. Select your project
# 4. Click "Connection string"
# 5. Copy the full string: postgresql://...@aws.neon.tech/...
```

---

## Step 2: Update .env File

Edit `.env` file in this folder:

```bash
# Replace these values:
DATABASE_URL=postgresql://user:password@aws.neon.tech/database_name

# Or if using Neon Local Extension:
DATABASE_URL=postgresql://user:password@localhost:5432/database_name

# Generate random JWT secrets:
ADMIN_JWT_SECRET=your-super-secret-key-min-32-chars
TRANSFER_TOKEN_SALT=your-transfer-salt-min-32-chars
```

### How to Generate JWT Secret:
```bash
# Run this in terminal:
node -e "console.log(require('crypto').randomBytes(16).toString('hex'))"
```

---

## Step 3: Verify Docker is Running

```bash
# Check Docker version
docker --version

# Should output: Docker version 20.x.x or higher
```

---

## Step 4: Start Strapi with Docker

```bash
# Navigate to this folder
cd d:\HUST\GHWorkspace\Back-End_SandBox

# Start services
docker-compose up -d

# Check if services are running
docker-compose ps

# Should show:
# NAME          STATUS
# strapi        Up (healthy)
# postgres      Up (healthy)
```

---

## Step 5: Access Strapi Admin

Once containers are running:

1. **Open Admin Panel**: http://localhost:1337/admin
2. **Create Admin Account**: 
   - Email: your-email@example.com
   - Password: your-strong-password
   - Click "Ready to start"

3. **You should see**: Strapi Admin Dashboard

---

## Step 6: Create Your First Collection (Products)

### In Admin Panel:
1. Click **"Content Manager"** (left sidebar)
2. Click **"Create new Collection Type"**
3. Name it: **"Product"**
4. Click **"Continue"**

### Add Fields:
1. Click **"Add another field"**
   - Field name: `name`
   - Type: `Text`
   - Check: "Required"
   - Click **"Add"**

2. Click **"Add another field"**
   - Field name: `price`
   - Type: `Number`
   - Click **"Add"**

3. Click **"Add another field"**
   - Field name: `description`
   - Type: `Rich Text`
   - Click **"Add"**

4. Click **"Add another field"**
   - Field name: `image`
   - Type: `Media`
   - Click **"Add"**

5. Click **"Save"**

---

## Step 7: Add Sample Products

### Via Admin Panel:
1. Go to **"Content Manager"** → **"Product"**
2. Click **"Create new entry"**
3. Fill in:
   - Name: "Laptop"
   - Price: 999.99
   - Description: "High-performance laptop"
   - Image: Click and upload a photo
4. Click **"Save"**
5. Click **"Publish"**

---

## Step 8: Test Your APIs

### REST API - Get All Products:
```bash
curl http://localhost:1337/api/products
```

### REST API - Get One Product:
```bash
curl http://localhost:1337/api/products/1
```

### GraphQL API:
```bash
curl -X POST http://localhost:1337/graphql \
  -H "Content-Type: application/json" \
  -d '{
    "query": "{ products { data { id attributes { name price } } } }"
  }'
```

---

## Step 9: Connect Frontend (Later)

Once you build your React/Vue frontend:

```javascript
// In your frontend code:
const response = await fetch('http://localhost:1337/api/products');
const data = await response.json();
console.log(data); // Your products!
```

---

## Troubleshooting

### Docker container not starting?
```bash
# Check logs
docker-compose logs strapi

# Restart containers
docker-compose restart
```

### Can't connect to database?
```bash
# Verify .env file has correct DATABASE_URL
cat .env

# Check if Neon Local Extension is running
# Or verify Neon Cloud connection string is correct
```

### Admin panel not loading?
```bash
# Clear browser cache
# Try incognito window
# Check: http://localhost:1337/admin (not just localhost:1337)
```

### Neon connection fails?
```bash
# If using Neon Local Extension:
# Make sure extension is running
# Verify: psql --version (should work)

# If using Neon Cloud directly:
# Verify connection string from neon.tech
# Check firewall allows outbound connections
```

---

## Common Commands

```bash
# Start services
docker-compose up -d

# Stop services
docker-compose down

# View logs
docker-compose logs strapi

# Restart specific service
docker-compose restart strapi

# Remove all data (WARNING: deletes database)
docker-compose down -v

# Rebuild containers
docker-compose build --no-cache
```

---

## Architecture

```
Your Frontend (React/Vue)
       ↓
REST API / GraphQL
       ↓
Strapi CMS (Container)
       ↓
PostgreSQL DB
       ↓
Neon Cloud
```

---

## Next Steps

1. ✅ Update .env with your Neon connection string
2. ✅ Run `docker-compose up -d`
3. ✅ Go to http://localhost:1337/admin
4. ✅ Create admin account
5. ✅ Create "Product" collection
6. ✅ Add sample products
7. ✅ Test API endpoints
8. 🎉 Ready to build your frontend!

---

## Need Help?

- Strapi Docs: https://docs.strapi.io
- Neon Docs: https://neon.tech/docs
- Docker Docs: https://docs.docker.com

Good luck! 🚀
