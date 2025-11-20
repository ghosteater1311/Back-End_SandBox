# 🚀 QUICK START - Do This Now!

## Step 1: Your Neon Connection String

**Go to neon.tech:**
1. Login to your account
2. Find your project
3. Click "Connection string" (copy button)
4. You'll get something like:
```
postgresql://user:password@aws.neon.tech/database_name
```

**OR if using Local Extension:**
```
postgresql://user:password@localhost:5432/database_name
```

---

## Step 2: Update .env File

Open `.env` file in this folder, update this line:

```bash
DATABASE_URL=<YOUR_CONNECTION_STRING_HERE>
```

Example (with real values):
```bash
DATABASE_URL=postgresql://neon_user:neon_password@aws.neon.tech/my_ecommerce_db
```

Also change these (generate random values):
```bash
ADMIN_JWT_SECRET=abc123def456ghi789jkl012 (min 32 chars)
TRANSFER_TOKEN_SALT=xyz987uvw654rst321opq098 (min 32 chars)
```

---

## Step 3: Start Docker

Open PowerShell in this folder:

```bash
# Navigate to this folder
cd d:\HUST\GHWorkspace\Back-End_SandBox

# Start Strapi + Database
docker-compose up -d

# Wait 30 seconds for startup...

# Check if running
docker-compose ps
```

Expected output:
```
NAME          STATUS
strapi        Up (healthy)
postgres      Up (healthy)
```

---

## Step 4: Go to Admin Panel

Open in browser:
```
http://localhost:1337/admin
```

You should see Strapi login screen.

---

## Step 5: Create Admin Account

1. Enter your email
2. Enter strong password
3. Click "Ready to start"
4. Done! You're in the admin panel

---

## Step 6: Create First Collection

1. Click "Content Manager" (left sidebar)
2. Click "Create new Collection Type"
3. Name it: `Product`
4. Click "Continue"

### Add fields by clicking "Add another field":
1. `name` - Text type - Check "Required"
2. `price` - Number type
3. `description` - Rich Text
4. `image` - Media type

Click "Save"

---

## Step 7: Add a Product

1. Go to "Content Manager" → "Product"
2. Click "Create new entry"
3. Fill in the fields:
   - Name: "Laptop"
   - Price: 999.99
   - Description: "Gaming laptop"
   - Image: Upload a photo
4. Click "Save" then "Publish"

---

## Step 8: Test Your API

Open new browser tab:
```
http://localhost:1337/api/products
```

You should see your product as JSON:
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

---

## Done! 🎉

You now have:
- ✅ Strapi Admin (http://localhost:1337/admin)
- ✅ REST API (http://localhost:1337/api/products)
- ✅ Connected to Neon Database
- ✅ Running in Docker

---

## Common Issues

### Containers not starting?
```bash
docker-compose logs strapi
# Check what the error is
```

### Can't reach admin panel?
```bash
# Wait 60 seconds (startup takes time)
# Then try again
```

### Database connection error?
```bash
# Check .env file has correct DATABASE_URL
# Verify Neon connection string is correct
# If using local extension, verify it's running
```

### Forgot admin password?
```bash
# Stop and delete everything
docker-compose down -v

# Start fresh
docker-compose up -d

# Admin panel will ask for new account
```

---

## Next Steps

1. **Read**: STRAPI_DOCKER_SETUP.md (detailed guide)
2. **Explore**: Admin panel (create more collections)
3. **Test**: APIs (use browser or curl)
4. **Build**: Your frontend (React, Vue, etc.)
5. **Deploy**: When ready (we'll help)

---

## Files You Have

- `.env` - Configuration (YOUR PASSWORDS HERE)
- `docker-compose.yml` - Docker setup
- `STRAPI_DOCKER_SETUP.md` - Detailed guide
- `NEON_CONNECTION.md` - Database connection help
- `QUICK_START.md` - This file!

---

**Read**: NEON_CONNECTION.md if you need help getting your connection string.

**Ready?** Let me know once you've updated `.env` and I'll guide you through Docker startup! 🚀
