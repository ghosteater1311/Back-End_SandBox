# 🛠️ Development & Debugging Guide

Complete guide for developing, debugging, and testing your Strapi E-Commerce backend.

---

## 📍 Where to Develop?

### Option 1: Docker-Only Development (Recommended) ✅

**Best for:** Non-developers, quick setup, production-ready

**Setup:**
- No cloning needed
- Use existing folder: `d:\HUST\GHWorkspace\Back-End_SandBox`
- Manage via Docker commands

**Workflow:**
```bash
# 1. Start backend
docker-compose up -d

# 2. Access admin panel
# Open browser → http://localhost:1337/admin

# 3. Create collections (no coding)
# Click buttons in Strapi UI

# 4. Test APIs
# Use Postman or REST Client

# 5. Stop when done
docker-compose down
```

**No TypeScript coding needed!**

---

### Option 2: Local Development (Advanced) 🔧

**Best for:** Full customization, plugin development, Strapi tweaking

**Setup:**
```bash
# Clone repo
git clone <repo-url>
cd Back-End_SandBox

# Install dependencies
npm install

# Create .env file
copy .env.example .env

# Run Strapi locally (not Docker)
npm run develop
```

**Workflow:**
- Edit TypeScript files in VS Code
- Hot reload on save
- Access admin panel: http://localhost:1337/admin

**When to use:**
- Need custom Strapi plugins
- Building middleware
- Advanced authentication flows
- Performance optimization

---

## 🎯 Your Recommended Approach

**Use Option 1 (Docker-Only)** because:

✅ You said "I don't focus on software engineering"
✅ Zero backend coding required
✅ Everything done via Strapi UI (click buttons)
✅ Production-ready automatically
✅ No need to install Node.js or dependencies
✅ Portable and easy to deploy

---

## 📁 Project Structure

### Docker-Only (Option 1)
```
Back-End_SandBox/
├── .env                    ← Database credentials
├── docker-compose.yml      ← Container config
├── .gitignore              ← Git ignore rules
├── README.md               ← Project overview
├── QUICK_START.md          ← Quick start guide
├── STRAPI_NO_CODING.md     ← Why no coding needed
├── NEON_CONNECTION.md      ← Database setup
├── STRAPI_DOCKER_SETUP.md  ← Docker setup details
├── TESTING.md              ← API testing guide
├── ARCHITECTURE_OVERVIEW.md ← System architecture
└── DEVELOPMENT_GUIDE.md    ← This file
```

### Local Development (Option 2)
```
Back-End_SandBox/
├── src/                    ← Strapi source code
├── .strapi-updater.json    ← Strapi updater
├── package.json            ← Dependencies
├── tsconfig.json           ← TypeScript config
├── .env                    ← Environment variables
└── ... (same docs as above)
```

---

## 🚀 Starting Development

### Option 1: Docker-Only

```bash
# Navigate to project folder
cd d:\HUST\GHWorkspace\Back-End_SandBox

# Verify Docker is running
docker --version
docker ps

# Start containers
docker-compose up -d

# Wait ~60 seconds for startup...

# Verify all healthy
docker-compose ps
```

Expected output:
```
NAME          STATUS
strapi        Up (healthy)
postgres      Up (healthy)
```

### Option 2: Local Development

```bash
# Navigate to project folder
cd d:\HUST\GHWorkspace\Back-End_SandBox

# Install dependencies
npm install

# Start Strapi development server
npm run develop
```

Server runs on: http://localhost:1337

---

## 🐛 Debugging & Troubleshooting

### Option 1: Docker Debugging

#### View Logs
```bash
# All services
docker-compose logs

# Just Strapi
docker-compose logs strapi

# Just Database
docker-compose logs postgres

# Follow logs in real-time
docker-compose logs -f strapi
```

#### Check Container Status
```bash
# See all containers
docker-compose ps

# Inspect specific container
docker inspect strapi
```

#### Common Docker Issues

**Problem: Container won't start**
```bash
# View error logs
docker-compose logs strapi

# Rebuild container
docker-compose build --no-cache

# Restart
docker-compose restart strapi
```

**Problem: Database connection error**
```bash
# Check database logs
docker-compose logs postgres

# Verify DATABASE_URL in .env is correct

# Restart database
docker-compose restart postgres
```

**Problem: Port 1337 already in use**
```bash
# Find what's using port 1337
netstat -ano | findstr :1337

# Kill process (replace PID with actual number)
taskkill /PID <PID> /F

# Or change port in docker-compose.yml
# Change: ports: - "1337:1337" to "1338:1337"
```

---

### Option 2: Local Development Debugging

#### Debug in VS Code

**Setup debugger:**

1. Create `.vscode/launch.json`:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "attach",
      "name": "Attach",
      "port": 9229,
      "skipFiles": ["<node_internals>/**"]
    }
  ]
}
```

2. Start with debugging:
```bash
node --inspect-brk=9229 node_modules/.bin/strapi develop
```

3. In VS Code: Press `F5` to attach debugger

#### Breakpoints
- Click line number to set breakpoint
- Code pauses when breakpoint hit
- Inspect variables in Debug panel

#### Console Logs
```typescript
// In your custom code
console.log('Variable:', variableName);
```

View in terminal where Strapi is running.

---

## 🧪 Testing APIs

### Using Postman

**Step 1: Get JWT Token**
```
Method: POST
URL: http://localhost:1337/api/auth/local
Body (JSON):
{
  "identifier": "admin@example.com",
  "password": "your_admin_password"
}
```

**Response:**
```json
{
  "jwt": "eyJhbGc...",
  "user": { ... }
}
```

**Step 2: Copy JWT Token**

**Step 3: Test Protected Endpoint**
```
Method: GET
URL: http://localhost:1337/api/products
Headers:
  Authorization: Bearer <your_jwt_token>
```

See **TESTING.md** for complete guide.

---

## 📝 Common Development Tasks

### Create a New Collection

**Via Admin Panel (No Coding!):**

1. Open: http://localhost:1337/admin
2. Click "Content-Type Builder" (builder icon)
3. Click "Create new collection type"
4. Name: `products` (or your collection)
5. Add fields (name, price, description, etc.)
6. Click "Save"
7. Done! API auto-generated ✨

**API automatically created:**
```
GET    /api/products
POST   /api/products
GET    /api/products/:id
PUT    /api/products/:id
DELETE /api/products/:id
```

### Add Sample Data

**Via Admin Panel:**

1. Open: http://localhost:1337/admin
2. Click "Content Manager"
3. Select your collection (e.g., "products")
4. Click "Create new entry"
5. Fill in the fields
6. Click "Save"
7. Click "Publish"

Data now in database! 🎉

---

## 🔐 Environment Variables

Edit `.env` file to configure:

```env
# Database
DATABASE_URL=postgresql://user:pass@aws.neon.tech/db

# Admin panel
ADMIN_JWT_SECRET=your-secret-key-32-chars-min
TRANSFER_TOKEN_SALT=your-salt-32-chars-min

# Server
NODE_ENV=development
HOST=0.0.0.0
PORT=1337

# JWT
JWT_SECRET=another-secret-key

# Optional: API Token
API_TOKEN_SALT=optional-salt
```

**After editing:**
```bash
# Docker: Rebuild and restart
docker-compose restart strapi

# Local: Auto-reloads
# No restart needed
```

---

## 📊 Monitoring

### Real-time Logs

**Docker:**
```bash
docker-compose logs -f strapi
```

**Local:**
```
Terminal shows logs automatically when running
```

### Performance

**Check container resource usage:**
```bash
docker stats
```

Shows CPU, memory, network usage.

---

## 🔄 Workflow Comparison

| Task | Docker-Only | Local Dev |
|------|-------------|-----------|
| **Start** | `docker-compose up -d` | `npm run develop` |
| **Edit code** | Files in folder | VS Code editor |
| **Hot reload** | Manual restart | Automatic |
| **Debug** | Container logs | VS Code debugger |
| **Stop** | `docker-compose down` | Ctrl+C |
| **Database** | In container | Local or connection string |
| **Deployment** | Push image | Build and deploy |

---

## 🎓 Development Workflow (Docker-Only)

### Day 1: Setup
```bash
# 1. Start backend
docker-compose up -d

# 2. Create admin account
# Open http://localhost:1337/admin
# Fill form, create account

# 3. Create collections
# Content-Type Builder → Create collection
```

### Daily: Development
```bash
# Morning: Start services
docker-compose up -d

# During day: Make changes via admin panel
# Collections, fields, permissions, roles

# Evening: Test APIs with Postman
# GET, POST, PUT, DELETE requests

# End of day: Stop services
docker-compose down
```

### Debugging Workflow
```bash
# 1. See error in Postman or admin panel
# 2. Check logs
docker-compose logs strapi

# 3. Find the issue
# 4. Fix in admin panel or .env
# 5. Restart if needed
docker-compose restart strapi

# 6. Test again
```

---

## 🆘 Common Issues & Solutions

### "Port 1337 already in use"
```bash
# Option 1: Kill process using port
netstat -ano | findstr :1337
taskkill /PID <PID> /F

# Option 2: Change port in docker-compose.yml
# Modify: ports: - "1338:1337"
```

### "Cannot connect to database"
```bash
# 1. Check .env has correct DATABASE_URL
# 2. Verify Neon connection string
# 3. Test connection from terminal
# 4. Check internet connection

# Restart database
docker-compose restart postgres
```

### "Admin panel not loading"
```bash
# 1. Wait 60 seconds for startup
# 2. Clear browser cache (Ctrl+Shift+Delete)
# 3. Try incognito/private window
# 4. Check: http://localhost:1337 works first
# 5. Check logs: docker-compose logs strapi
```

### "Changes not appearing"
```bash
# Option 1: Docker - restart container
docker-compose restart strapi

# Option 2: Local - reload page (Ctrl+R)
# Hot reload should handle it automatically
```

### "Out of memory"
```bash
# Check resource usage
docker stats

# Increase Docker memory limit
# Docker Desktop → Settings → Resources
```

---

## 📚 Development Tips

### ✅ Do's
- ✅ Use admin panel for data management
- ✅ Test APIs with Postman before frontend
- ✅ Keep `.env` secrets safe (don't commit)
- ✅ Use version control (Git)
- ✅ Check logs when something breaks
- ✅ Create collections via UI (no code)
- ✅ Document collection structure

### ❌ Don'ts
- ❌ Don't commit `.env` file
- ❌ Don't share API tokens publicly
- ❌ Don't modify database directly (use admin panel)
- ❌ Don't hardcode credentials
- ❌ Don't use same admin password everywhere
- ❌ Don't skip reading error logs

---

## 🚀 Next Steps

1. **Choose your approach** (Docker-Only recommended)
2. **Start services** (docker-compose up -d)
3. **Create admin account** (http://localhost:1337/admin)
4. **Create first collection** (Products, Users, Orders)
5. **Add sample data** (via admin panel)
6. **Test with Postman** (see TESTING.md)
7. **Build your frontend** (React, Vue, Next.js)
8. **Connect frontend to API** (fetch from /api/...)

---

## 📖 Related Documentation

- **QUICK_START.md** - 3-step launch guide
- **STRAPI_DOCKER_SETUP.md** - Detailed Docker setup
- **TESTING.md** - API testing with Postman
- **NEON_CONNECTION.md** - Database connection
- **README.md** - Project overview

---

**Happy developing!** 🚀
