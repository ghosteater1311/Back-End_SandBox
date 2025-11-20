# 🔧 Neon Connection Setup

## Understanding the Flow

```
┌─────────────────────────────────────────────────────┐
│ Your Computer (Local)                               │
├─────────────────────────────────────────────────────┤
│ Neon Local Extension (if installed)                 │
│ localhost:5432                                      │
│       ↓                                             │
│   Tunnel/Proxy                                      │
│       ↓                                             │
└─────────────────────────────────────────────────────┘
            ↓
┌─────────────────────────────────────────────────────┐
│ Neon Cloud                                          │
│ aws.neon.tech                                       │
│ (Your PostgreSQL database)                          │
└─────────────────────────────────────────────────────┘
```

---

## Two Connection Methods

### Method 1: Using Neon Local Extension (Best for Local Development)

**Pros:**
- ✅ Faster local development
- ✅ Works offline (proxy caches)
- ✅ Same database as production
- ✅ No internet needed for queries

**Setup:**
1. You already have Neon CLI installed
2. Connect to Neon Cloud once
3. Local extension auto-proxies to cloud

**Connection String:**
```
postgresql://user:password@localhost:5432/database_name
```

**How to verify:**
```bash
# Check if extension is running
neon --version

# Connect to local proxy
psql postgresql://user:password@localhost:5432/database_name

# Should show: psql (15.x)
```

---

### Method 2: Direct Neon Cloud Connection (Simple but Slower)

**Pros:**
- ✅ No local setup needed
- ✅ Single connection string
- ✅ Works from anywhere

**Cons:**
- ❌ Requires internet always
- ❌ Slightly slower
- ❌ Connection limits on free tier

**Connection String:**
```
postgresql://user:password@aws.neon.tech/database_name
```

**Where to get it:**
1. Go to https://console.neon.tech
2. Login
3. Select your project
4. Click "Connection pooling"
5. Copy the full URL
6. Replace `{password}` and `{database}` with your values

---

## Update .env File

### Step 1: Open `.env` file

```bash
# This file is in: d:\HUST\GHWorkspace\Back-End_SandBox\.env
```

### Step 2: Find the DATABASE_URL line

```
DATABASE_URL=postgresql://user:password@aws.neon.tech/database_name
```

### Step 3: Replace with YOUR connection string

**If using Neon Local Extension:**
```
DATABASE_URL=postgresql://user:password@localhost:5432/strapi
```

**If using Neon Cloud Direct:**
```
DATABASE_URL=postgresql://user:password@aws.neon.tech/strapi
```

---

## Get Your Neon Connection String

### From Neon Console:

1. **Go to**: https://console.neon.tech
2. **Login** with your Neon account
3. **Select** your project (if multiple)
4. **Click** "Connection string" button
5. **Copy** the full URL

It looks like:
```
postgresql://neon_user:neon_password@aws.neon.tech/neon_database?sslmode=require
```

### Breakdown:
```
postgresql://  ← Protocol
neon_user      ← Username
:              ← Separator
neon_password  ← Password
@              ← At
aws.neon.tech  ← Neon cloud server
/neon_database ← Your database name
?sslmode=require ← SSL requirement
```

---

## Testing Connection

### Option 1: Test with psql

```bash
# If you have PostgreSQL client installed:
psql "postgresql://user:password@localhost:5432/strapi"

# Should show: psql (15.x)
# Type: \q to exit
```

### Option 2: Docker will test it

Docker automatically tests the connection when you run:
```bash
docker-compose up -d
```

---

## Neon Local Extension Commands

### Start/Stop Extension:
```bash
# Start the local proxy
neon up

# Stop the local proxy
neon down

# Check status
neon status
```

### View Connection Details:
```bash
# Show connection info
neon connection-string

# Copy to clipboard
neon connection-string | clip
```

---

## For Strapi in Docker

Your setup connects like this:

```
Docker Strapi Container
  ↓
  Uses DATABASE_URL from .env
  ↓
  If localhost:5432 → Uses Neon Local Extension
  ↓
  If aws.neon.tech → Uses Neon Cloud Direct
  ↓
Neon PostgreSQL Database
```

---

## Security Note

⚠️ **Never commit `.env` to git with real passwords!**

Your `.env` file should NEVER be pushed to GitHub.

Already protected by `.gitignore` ✅

---

## Quick Checklist

- [ ] Got Neon account at neon.tech
- [ ] Created PostgreSQL database in Neon
- [ ] Got connection string from Neon console
- [ ] Updated `.env` file with connection string
- [ ] Verified connection string format is correct
- [ ] (If local extension) Verified extension is running
- [ ] Ready to start Docker!

---

## Example Complete .env

```bash
# Database - Using Neon Cloud Direct
DATABASE_URL=postgresql://neon_user:neon_password@aws.neon.tech/neon_db?sslmode=require

# Database - Using Neon Local Extension (alternative)
# DATABASE_URL=postgresql://neon_user:neon_password@localhost:5432/neon_db

# Strapi Config
NODE_ENV=production
ADMIN_JWT_SECRET=your-random-secret-here-32-chars-min
TRANSFER_TOKEN_SALT=your-random-salt-here-32-chars-min
```

---

## Still Confused?

**Simple explanation:**
1. You have a database in the cloud (Neon)
2. You can connect to it in two ways:
   - **Direct**: Slow, internet required
   - **Local Extension**: Fast, cached locally
3. Pick one, get the connection string, put it in `.env`
4. Done! ✓

Now go to STRAPI_DOCKER_SETUP.md for next steps!
