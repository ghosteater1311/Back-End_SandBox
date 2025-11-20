# 🛍️ E-Commerce Backend with Strapi + Docker + Neon

A **production-ready** E-Commerce backend using **Strapi CMS**, **Docker**, and **Neon PostgreSQL**. 

**No backend coding required!** ✨

---

## 🎯 What You Get

✅ **Admin Panel** - Manage products, users, orders (built-in)  
✅ **REST API** - Auto-generated endpoints (no coding)  
✅ **GraphQL API** - Modern queries and mutations (no coding)  
✅ **PostgreSQL** - Connected to Neon Cloud database  
✅ **Docker** - Production-ready containerization  
✅ **Authentication** - User login, JWT tokens (built-in)  
✅ **Media Upload** - Images and files (drag & drop)  
✅ **Permissions** - Role-based access control (UI configuration)  

---

## 🚀 Quick Start (15 minutes)

### 1. Get Neon Connection String
```bash
# Go to: https://console.neon.tech
# Find your project
# Click "Connection string"
# Copy the PostgreSQL URL
```

### 2. Update .env
```bash
# Edit .env file in this folder
DATABASE_URL=postgresql://user:password@aws.neon.tech/database_name
```

### 3. Start Docker
```bash
docker-compose up -d
```

### 4. Open Admin Panel
```
http://localhost:1337/admin
```

Create admin account and you're done! 🎉

---

## 📁 Project Structure

```
.env                        ← Your configuration (secrets)
docker-compose.yml          ← Docker setup
LICENSE                     ← MIT License

📖 Documentation:
QUICK_START.md             ← Launch guide
NEON_CONNECTION.md         ← Database setup help
STRAPI_DOCKER_SETUP.md     ← Detailed walkthrough
ARCHITECTURE_OVERVIEW.md   ← System architecture
---

## 📚 How Strapi Works

### No Coding Required! 🎉

**Traditional Backend (Express):**
```typescript
// You write TypeScript code (hours of work)
@Controller('products')
export class ProductController {
  @Get()
  findAll() { ... }
  @Post()
  create() { ... }
  // ... 100+ lines
}
```

**Strapi (What You Actually Do):**
```
1. Click "Create Collection Type"
2. Name it "Product"
3. Add fields (name, price, image)
4. Click "Save"

DONE! APIs auto-generated! ✅
```

### Create Collections (No Coding!)

```
Admin Panel → Content Manager → Create Collection Type
│
├─ Collection: "Product"
│  ├─ Field: name (Text)
│  ├─ Field: price (Number)
│  ├─ Field: description (Rich Text)
│  └─ Field: image (Media)
│
└─ APIs Auto-Generated:
   GET    /api/products
   POST   /api/products
   PUT    /api/products/:id
   DELETE /api/products/:id
```

---

## 🔌 API Examples

### Get All Products
```bash
curl http://localhost:1337/api/products

# Response:
{
  "data": [
    {
      "id": 1,
      "attributes": {
        "name": "Laptop",
        "price": 999.99,
        "image": { "url": "/uploads/..." }
      }
    }
  ]
}
```

### Create Product (From Your Frontend)
```javascript
const response = await fetch('http://localhost:1337/api/products', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    data: {
      name: 'Phone',
      price: 599.99
    }
  })
});
const product = await response.json();
```

### GraphQL Query
```graphql
query {
  products {
    data {
      id
      attributes {
        name
        price
        image {
          url
        }
      }
    }
  }
}
```

---

## 🗄️ Collections You'll Create

### Products
- name (Text)
- price (Number)
- description (Rich Text)
- image (Media)
- category (Relation to Categories)

### Users
- email (Email)
- username (Text)
- password (Password)
- role (Single Select: admin, user)

### Orders
- order_number (Text)
- user (Relation to Users)
- products (Relation to Products)
- total_amount (Number)
- status (Single Select: pending, shipped, delivered)

### Categories
- name (Text)
- description (Rich Text)

---

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|---|---|---|
| CMS | Strapi | Content management & API generation |
| Container | Docker | Deployment & environment |
| Database | PostgreSQL (Neon) | Cloud database |
| API | REST + GraphQL | Frontend communication |
| Auth | JWT | User authentication |
| Admin | Built-in React | Content management UI |

---

## 📋 Common Commands

```bash
# Navigate to project
cd d:\HUST\GHWorkspace\Back-End_SandBox

# Start services
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs strapi

# Stop services
docker-compose down

# Rebuild containers
docker-compose build --no-cache
```

---

## 🔐 Security

✅ **Built-in:**
- JWT authentication
- Password hashing
- Permissions system
- Role-based access control
- SSL/TLS (Neon)

⚠️ **Production Checklist:**
- [ ] Change `ADMIN_JWT_SECRET` to random 32+ chars
- [ ] Change `TRANSFER_TOKEN_SALT` to random 32+ chars
- [ ] Use strong admin password
- [ ] Enable rate limiting (if needed)
- [ ] Configure CORS for your frontend domain
- [ ] Use HTTPS in production

---

## 🚀 Deployment

Your backend is ready for production:

1. **Docker Image**: `docker-compose build`
2. **Deploy to**: Vercel, Railway, Heroku, AWS, etc.
3. **Database**: Neon cloud (always backed up)
4. **Scaling**: Increase container replicas as needed

---

## 📖 Documentation

- **QUICK_START.md** - 3-step launch guide
- **NEON_CONNECTION.md** - Database connection help
- **STRAPI_DOCKER_SETUP.md** - Detailed setup walkthrough
- **ARCHITECTURE_OVERVIEW.md** - System architecture diagrams

---

## ❓ FAQ

**Q: Do I need to write TypeScript code?**
A: No! Strapi generates everything. 0 lines of code needed.

**Q: How do I add products?**
A: Click admin panel → Content Manager → Add entry → Fill forms → Publish

**Q: How do I use the API?**
A: Just fetch from `/api/products`, `/api/users`, etc. (auto-generated)

**Q: Can I customize Strapi?**
A: Yes, but you won't need to for basic E-Commerce.

**Q: How do I deploy?**
A: Push Docker image to your hosting provider. Database stays in Neon cloud.

---

## 🎓 Learning Resources

- [Strapi Documentation](https://docs.strapi.io)
- [Neon Database Docs](https://neon.tech/docs)
- [Docker Documentation](https://docs.docker.com)
- [REST API Best Practices](https://restfulapi.net)
- [GraphQL Guide](https://graphql.org/learn)

---

## 💡 Next Steps

1. ✅ Update `.env` with Neon connection string
2. ✅ Run `docker-compose up -d`
3. ✅ Open http://localhost:1337/admin
4. ✅ Create admin account
5. ✅ Create first collection
6. ✅ Add sample data
7. ✅ Build your frontend
8. ✅ Launch! 🚀

---

## 📞 Troubleshooting

### Docker won't start?
```bash
docker-compose logs strapi
# Check the error message
```

### Can't connect to database?
- Verify `.env` has correct `DATABASE_URL`
- Check Neon connection string from console.neon.tech
- Verify internet connection (if using cloud)

### Admin panel not loading?
- Wait 60 seconds for startup
- Clear browser cache
- Try incognito window
- Check: http://localhost:1337/admin (not just localhost:1337)

---

## 📄 License

MIT License - feel free to use for any project

---

**Your backend is ready to launch! 🚀**

Start with: **QUICK_START.md**

Happy building! ✨
- ✅ SQL injection prevention (parameterized queries)
- ✅ Error handling without exposing sensitive info

## Next Steps

1. Implement Order Management endpoints
2. Add Payment Integration (Stripe)
3. Add Review and Rating system
4. Implement Cart functionality
5. Add Email notifications
6. Set up pagination for all list endpoints
7. Add file upload for product images
8. Implement admin dashboard endpoints
9. Add API documentation with Swagger
10. Set up comprehensive testing (Jest)

## Testing with Postman

1. Import the API endpoints into Postman
2. Create environment variables:
   - `base_url`: http://localhost:5000
   - `token`: <JWT token from login>
3. Test each endpoint using the examples above

## Troubleshooting

### Database Connection Issues
- Verify `DATABASE_URL` in `.env`
- Check Neon DB credentials
- Ensure database migrations have been run

### JWT Token Issues
- Verify token is included in Authorization header
- Check token hasn't expired
- Ensure JWT_SECRET matches on server

### CORS Errors
- Update `CORS_ORIGIN` in `.env` to match frontend URL
- Verify credentials are included in requests

## License

MIT
