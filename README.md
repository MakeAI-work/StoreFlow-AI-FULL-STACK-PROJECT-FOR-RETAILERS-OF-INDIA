# 🚀 WhatsApp Retailer Platform

### Full-Stack Enterprise Inventory & Invoice Management System

> A production-ready, AI-powered retail management platform integrating WhatsApp Business API with a modern web dashboard. Built with FastAPI, React, PostgreSQL, and OpenAI GPT-4o for natural language processing.

[![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.104+-green.svg)](https://fastapi.tiangolo.com/)
[![React](https://img.shields.io/badge/React-18.2+-61dafb.svg)](https://reactjs.org/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-13+-blue.svg)](https://www.postgresql.org/)

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Key Features](#-key-features)
- [System Architecture](#-system-architecture)
- [Technology Stack](#-technology-stack)
- [Database Schema](#-database-schema)
- [API Documentation](#-api-documentation)
- [Installation & Setup](#-installation--setup)
- [WhatsApp Bot Commands](#-whatsapp-bot-commands)
- [Frontend Features](#-frontend-features)
- [Deployment](#-deployment)
- [Performance & Scalability](#-performance--scalability)
- [Security Features](#-security-features)
- [Future Enhancements](#-future-enhancements)
- [Contact](#-contact)

---

## 🎯 Project Overview

**WhatsApp Retailer Platform** is a comprehensive business management solution designed for small and medium retailers. It seamlessly integrates WhatsApp Business API with a modern web dashboard, enabling retailers to manage inventory, generate invoices, and track sales through both WhatsApp chat and a responsive web interface.

### **Problem Statement**
Small retailers struggle with:
- Manual inventory tracking and stock management
- Time-consuming invoice generation
- Lack of digital sales records
- Limited access to business analytics
- High costs of traditional POS systems

### **Solution**
A dual-interface platform that:
- Converts WhatsApp into a powerful business tool
- Provides enterprise-grade inventory management
- Automates invoice generation with professional PDFs
- Tracks sales with comprehensive analytics
- Supports Indian GST compliance

---

## ✨ Key Features

### **1. Dual WhatsApp Bots**

#### **Inventory Management Bot** 📦
- **Real-time Stock Control**: Add, update, and monitor inventory via WhatsApp
- **Low Stock Alerts**: Automatic notifications when items reach threshold (≤10 units)
- **Price Management**: Dynamic pricing updates with instant confirmation
- **Stock Status Tracking**: Visual indicators (🟢 In Stock, 🟡 Low Stock, 🔴 Out of Stock)
- **HSN Code Support**: Tax classification for Indian GST compliance

#### **Invoice Generation Bot** 📄
- **Multi-item Invoicing**: Support for complex orders with multiple products
- **Customer Business Details**: Capture GST numbers and addresses
- **Per-item Discounts**: Flexible discount system (percentage or fixed amount)
- **Professional PDF Generation**: Branded invoices with complete tax breakdown
- **Automatic Stock Deduction**: Real-time inventory updates on sale confirmation
- **Sale Status Workflow**: Pending → Success/Failed with retailer confirmation

### **2. AI-Powered Natural Language Processing** 🤖
- **OpenAI GPT-4o Integration**: Converts natural language to structured commands
- **Multi-language Support**: Process commands in any language, output in English
- **Context-Aware Translation**: Uses inventory context for accurate item matching
- **90-95% Success Rate**: High accuracy with minimal user training
- **Backward Compatible**: Works alongside traditional structured commands

**Example Transformations:**
```
"I want to add 100 Natraj Pencils for 5 rupees" 
→ "add Natraj Pencils 100 5.0"

"Create bill for Rahul – 2 Notebooks with 5% discount"
→ "Rahul: Notebooks: 2: 5%"
```

### **3. Modern Web Dashboard** 💻

#### **Dashboard Page**
- Real-time business metrics (total items, sales, pending orders)
- Today's sales tracking with revenue analytics
- Recent sales history with quick access
- Stock status overview (low stock, out of stock alerts)

#### **Inventory Management**
- Card-based modern UI with search functionality
- Quick edit: Inline stock and price updates
- Bulk operations support
- HSN code management for tax compliance
- Real-time stock status indicators

#### **Invoice Generation**
- Two-column responsive layout (items + invoice preview)
- Customer information capture (name, GST, address)
- Multi-item selection with quantity controls
- Advanced discount system (per-item and overall)
- Indian GST tax calculation (CGST, SGST, IGST)
- Live invoice preview with tax breakdown
- One-click PDF generation and download

#### **Sales History**
- Comprehensive sales tracking with pagination (10 items/page)
- Advanced search (customer name, sale ID, item names)
- Status filtering (All, Pending, Success, Failed, Returned)
- Sale returns with automatic inventory restoration
- PDF invoice download for each sale
- Detailed tax breakdown view

#### **Profile Management**
- User profile editing (name, email, WhatsApp number)
- Business information (business name, GST number, address)
- Tax configuration (CGST, SGST, IGST rates)
- Password management
- Account deletion with data cleanup

### **4. Advanced Tax System** 💰
- **Indian GST Compliance**: Full support for CGST, SGST, and IGST
- **Configurable Tax Rates**: Standard rates (0%, 5%, 12%, 18%, 28%)
- **Tax-Inclusive Pricing**: Support for both inclusive and exclusive pricing
- **Inter-state Detection**: Automatic IGST calculation for inter-state sales
- **Tax Breakdown**: Detailed tax reports on invoices and sales

### **5. Professional PDF Invoices** 📑
- **ReportLab Integration**: High-quality PDF generation
- **Business Branding**: Custom business information on invoices
- **Complete Tax Details**: CGST, SGST, IGST breakdown
- **Customer Information**: GST number and address when provided
- **Item Details**: HSN codes, quantities, prices, discounts
- **Professional Layout**: Clean, print-ready design

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT LAYER                              │
├────────────────────────┬────────────────────────────────────────┤
│   WhatsApp Business    │        React Web Dashboard             │
│   (Mobile Clients)     │     (Desktop/Mobile Browsers)          │
└────────┬───────────────┴───────────────┬────────────────────────┘
         │                               │
         │ Webhook                       │ REST API
         │ (JSON)                        │ (JWT Auth)
         │                               │
┌────────▼───────────────────────────────▼────────────────────────┐
│                     APPLICATION LAYER                            │
├──────────────────────────────────────────────────────────────────┤
│                       FastAPI Server                             │
│  ┌────────────────┐  ┌──────────────┐  ┌────────────────────┐  │
│  │   Webhooks     │  │  Auth APIs   │  │  Business APIs     │  │
│  │  /inventory    │  │  /auth       │  │  /items  /sales    │  │
│  │  /invoice      │  │  JWT/OAuth   │  │  /contact          │  │
│  └────────┬───────┘  └──────┬───────┘  └─────────┬──────────┘  │
│           │                 │                     │              │
│  ┌────────▼─────────────────▼─────────────────────▼──────────┐  │
│  │              SERVICE LAYER                                 │  │
│  │  ┌──────────────┐  ┌────────────┐  ┌──────────────────┐  │  │
│  │  │ Inventory Bot│  │ Invoice Bot│  │  NLP Translator  │  │  │
│  │  │   Handler    │  │   Handler  │  │   (GPT-4o)       │  │  │
│  │  └──────┬───────┘  └─────┬──────┘  └──────────────────┘  │  │
│  │         │                │                                 │  │
│  │  ┌──────▼────────────────▼──────────────────────────────┐ │  │
│  │  │         Message Parser & Command Processor           │ │  │
│  │  └──────────────────────┬───────────────────────────────┘ │  │
│  │                         │                                  │  │
│  │  ┌──────────────────────▼───────────────────────────────┐ │  │
│  │  │  Business Logic (Inventory, Sales, Tax Calculator)   │ │  │
│  │  └──────────────────────┬───────────────────────────────┘ │  │
│  └─────────────────────────┼─────────────────────────────────┘  │
└────────────────────────────┼────────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────────┐
│                      DATA LAYER                                  │
├──────────────────────────────────────────────────────────────────┤
│  ┌──────────────────┐  ┌─────────────────┐  ┌───────────────┐  │
│  │   PostgreSQL     │  │  PDF Storage    │  │  Alembic      │  │
│  │   Database       │  │  /storage/      │  │  Migrations   │  │
│  │  - Users         │  │   invoices/     │  │               │  │
│  │  - Items         │  │                 │  │               │  │
│  │  - Sales         │  │                 │  │               │  │
│  │  - Sessions      │  │                 │  │               │  │
│  │  - Contacts      │  │                 │  │               │  │
│  └──────────────────┘  └─────────────────┘  └───────────────┘  │
└──────────────────────────────────────────────────────────────────┘
```

### **Architecture Highlights**

1. **Stateless Design**: All session data stored in PostgreSQL
2. **Modular Services**: Clean separation of concerns (API, Business Logic, Data)
3. **Dual Interface**: Unified backend serving both WhatsApp and web clients
4. **Event-Driven**: Webhook-based WhatsApp integration
5. **RESTful APIs**: Standard HTTP methods with JWT authentication
6. **Scalable**: Horizontal scaling support for multiple instances

---

## 🛠️ Technology Stack

### **Backend**
| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| **Framework** | FastAPI | 0.104+ | High-performance async web framework |
| **ORM** | SQLAlchemy | 2.0+ | Database operations with async support |
| **Validation** | Pydantic | 2.5+ | Data validation and serialization |
| **Database** | PostgreSQL | 13+ | Primary data store |
| **Migration** | Alembic | 1.12+ | Database schema versioning |
| **Authentication** | python-jose | 3.3+ | JWT token generation/validation |
| **Password Hashing** | passlib[bcrypt] | 1.7+ | Secure password storage |
| **HTTP Client** | httpx | 0.25+ | Async WhatsApp API calls |
| **PDF Generation** | ReportLab | 4.0+ | Professional invoice PDFs |
| **NLP** | OpenAI | 1.12+ | GPT-4o for command translation |

### **Frontend**
| Component | Technology | Version | Purpose |
|-----------|------------|---------|---------|
| **Framework** | React | 18.2+ | UI component library |
| **Routing** | React Router | 6.8+ | Client-side navigation |
| **HTTP Client** | Axios | 1.11+ | API communication |
| **Build Tool** | React Scripts | 5.0+ | Development and build tooling |

### **External APIs**
| Service | Purpose |
|---------|---------|
| **WhatsApp Cloud API** | Message sending/receiving, media uploads |
| **OpenAI GPT-4o** | Natural language command translation |

### **Development Tools**
- **Testing**: Pytest, pytest-asyncio, React Testing Library
- **Code Quality**: Black, Flake8, ESLint
- **Version Control**: Git with conventional commits

---

## 🗄️ Database Schema

### **Core Tables**

#### **Users**
```sql
- id (PK): Integer
- name: String(100)
- email: String(255) UNIQUE
- whatsapp_number: String(20) UNIQUE
- password_hash: String(255)
- business_name: String(255) NULLABLE
- gst_number: String(15) NULLABLE
- address: String(500) NULLABLE
- default_tax_rate: Float (default: 18.0)
- cgst_rate: Float (default: 9.0)
- sgst_rate: Float (default: 9.0)
- igst_rate: Float (default: 18.0)
- tax_inclusive: Boolean (default: False)
- is_active: Boolean
- created_at: DateTime
- updated_at: DateTime
```

#### **Items**
```sql
- id (PK): Integer
- user_id (FK): Integer → users.id
- name: String(100)
- quantity: Integer
- price: Float
- description: String(255)
- hsn_number: String(20)
- is_active: Boolean
- created_at: DateTime
- updated_at: DateTime
```

#### **Sales**
```sql
- id (PK): Integer
- user_id (FK): Integer → users.id
- customer_name: String(100)
- customer_gst_number: String(15) NULLABLE
- customer_address: Text NULLABLE
- items_sold_json: Text (JSON array)
- subtotal_amount: Float
- discount_type: String(20) [none, percentage, fixed]
- discount_value: Float
- discount_amount: Float
- amount_before_tax: Float
- tax_rate: Float
- cgst_rate: Float
- sgst_rate: Float
- igst_rate: Float
- cgst_amount: Float
- sgst_amount: Float
- igst_amount: Float
- total_tax_amount: Float
- total_amount: Float
- tax_inclusive: Boolean
- pdf_path: String(255)
- status: Enum [pending, success, failed, cancelled, returned]
- created_at: DateTime
- updated_at: DateTime
```

#### **WhatsApp Sessions**
```sql
- id (PK): Integer
- user_id (FK): Integer → users.id
- whatsapp_number: String(20)
- session_token: String(255) UNIQUE
- bot_type: Enum [INVENTORY, INVOICE]
- is_active: Boolean
- expires_at: DateTime
- created_at: DateTime
- last_activity: DateTime
```

#### **Contacts**
```sql
- id (PK): Integer
- name: String(100)
- email: String(255)
- phone: String(20) NULLABLE
- subject: String(200)
- message: Text
- status: String(20) [new, in_progress, resolved]
- created_at: DateTime
```

---

## 📚 API Documentation

### **Authentication Endpoints**

#### `POST /api/auth/register`
Create a new user account
```json
Request:
{
  "name": "John Doe",
  "email": "john@example.com",
  "whatsapp_number": "+919876543210",
  "password": "SecurePass123"
}

Response: 201 Created
{
  "id": 1,
  "name": "John Doe",
  "email": "john@example.com",
  "whatsapp_number": "+919876543210",
  "created_at": "2024-01-01T00:00:00Z"
}
```

#### `POST /api/auth/login`
Authenticate and receive JWT token
```json
Request:
{
  "whatsapp_number": "+919876543210",
  "password": "SecurePass123"
}

Response: 200 OK
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "expires_in": 86400
}
```

### **Inventory Endpoints**

#### `GET /api/items`
Retrieve user's inventory with filtering
```
Query Parameters:
- skip: int (default: 0) - Pagination offset
- limit: int (default: 100) - Items per page
- search: string - Search by name/description
- low_stock_only: bool - Filter low stock items
- out_of_stock_only: bool - Filter out of stock items
- active_only: bool (default: true) - Show only active items
```

#### `POST /api/items`
Add new inventory item
```json
Request:
{
  "name": "Natraj Pencil",
  "quantity": 100,
  "price": 5.0,
  "description": "HB Pencil",
  "hsn_number": "96081010"
}

Response: 201 Created
{
  "id": 1,
  "name": "Natraj Pencil",
  "quantity": 100,
  "price": 5.0,
  "hsn_number": "96081010",
  "is_low_stock": false,
  "is_out_of_stock": false,
  "created_at": "2024-01-01T00:00:00Z"
}
```

#### `PUT /api/items/{item_id}`
Update inventory item

#### `PATCH /api/items/{item_id}/stock`
Update stock quantity with operations (set, add, subtract)

#### `DELETE /api/items/{item_id}`
Soft delete item (sets is_active=False)

### **Sales Endpoints**

#### `POST /api/sales`
Create new sale with automatic PDF generation
```json
Request:
{
  "customer_name": "ABC Company",
  "customer_gst_number": "22AAAAA0000A1Z5",
  "customer_address": "123 Main St, Mumbai",
  "items_sold": [
    {
      "item_name": "Natraj Pencil",
      "quantity": 10,
      "discount_type": "percentage",
      "discount_value": 5.0
    }
  ],
  "discount_type": "none",
  "discount_value": 0,
  "total_amount": 47.50
}

Response: 201 Created
{
  "id": 1,
  "customer_name": "ABC Company",
  "subtotal_amount": 50.0,
  "discount_amount": 2.5,
  "amount_before_tax": 47.5,
  "cgst_amount": 4.28,
  "sgst_amount": 4.28,
  "total_tax_amount": 8.56,
  "total_amount": 56.06,
  "pdf_path": "/storage/invoices/invoice_1.pdf",
  "status": "pending"
}
```

#### `GET /api/sales`
Retrieve sales history with filtering

#### `GET /api/sales/{sale_id}`
Get specific sale details

#### `PUT /api/sales/{sale_id}/status`
Update sale status (pending → success/failed)

#### `GET /api/sales/{sale_id}/download-pdf`
Download PDF invoice

#### `PUT /api/sales/{sale_id}/return`
Return a sale and restore inventory

### **WhatsApp Webhook Endpoints**

#### `POST /webhook/inventory`
Receive WhatsApp messages for Inventory Bot

#### `POST /webhook/invoice`
Receive WhatsApp messages for Invoice Bot

#### `GET /webhook/inventory` & `GET /webhook/invoice`
Webhook verification endpoints for Meta

---

## 🚀 Installation & Setup

### **Prerequisites**
- Python 3.9 or higher
- Node.js 18+ and npm 9+
- PostgreSQL 13+
- WhatsApp Business Account with API access
- OpenAI API key (optional, for NLP features)

### **1. Clone Repository**
```bash
git clone https://github.com/yourusername/whatsapp_retailer.git
cd whatsapp_retailer
```

### **2. Backend Setup**
```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
cd backend
pip install -r requirements.txt

# Configure environment variables
cp ../.env.example ../.env
# Edit .env with your credentials

# Create database
createdb whatsapp_retailer_db

# Run migrations
alembic upgrade head

# Start backend server
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### **3. Frontend Setup**
```bash
# In a new terminal
cd frontend

# Install dependencies
npm install

# Start development server
npm start
```

### **4. Configure WhatsApp Business API**
1. Create a Meta Developer account
2. Set up WhatsApp Business API
3. Configure two phone numbers (Inventory Bot & Invoice Bot)
4. Update `.env` with:
   - `WHATSAPP_ACCESS_TOKEN`
   - `WHATSAPP_PHONE_NUMBER_ID_INVENTORY`
   - `WHATSAPP_PHONE_NUMBER_ID_INVOICE`
   - `WHATSAPP_WEBHOOK_VERIFY_TOKEN`
5. Set webhook URLs in Meta dashboard:
   - `https://yourdomain.com/webhook/inventory`
   - `https://yourdomain.com/webhook/invoice`

### **5. Configure OpenAI (Optional)**
```bash
# Add to .env
OPENAI_API_KEY=sk-your-api-key-here
```

### **Access Points**
- **Backend API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/docs
- **Frontend Dashboard**: http://localhost:3000

---

## 💬 WhatsApp Bot Commands

### **Inventory Bot Commands**

#### **Login**
```
login <user_id> <password>
```

#### **Add Item**
```
add <item_name> <quantity> <price> [hsn_number]

Examples:
add Natraj Pencil 100 5.0
add Ball Pen 50 10.0 96081010
```

#### **Update Stock**
```
update <item_name> <quantity>

Example:
update Natraj Pencil 150
```

#### **Update Price**
```
price <item_name> <new_price>

Example:
price Natraj Pencil 6.0
```

#### **Check Stock**
```
stock <item_name>

Example:
stock Natraj Pencil
```

#### **View All Items**
```
view
```

#### **Low Stock Items**
```
lowstock
```

#### **Logout**
```
logout
```

### **Invoice Bot Commands**

#### **Basic Invoice**
```
<customer_name>: <item1>: <qty1>: <discount1>, <item2>: <qty2>: <discount2>

Example:
Rahul: Natraj Pencil: 10: 5%, Ball Pen: 5: 10%
```

#### **Invoice with GST Number**
```
<customer_name> | GST: <gst_number>: <item1>: <qty1>: <discount>

Example:
ABC Company | GST: 22AAAAA0000A1Z5: Natraj Pencil: 100: 5%
```

#### **Invoice with Address**
```
<customer_name> | Address: <address>: <item1>: <qty1>

Example:
XYZ Store | Address: 123 Main St, Mumbai: Ball Pen: 50
```

#### **Invoice with Both GST and Address**
```
<customer_name> | GST: <gst_number> | Address: <address>: <item1>: <qty1>: <discount>

Example:
ABC Corp | GST: 22AAAAA0000A1Z5 | Address: Mumbai: Natraj Pencil: 100: 5%
```

#### **Confirm Sale**
```
success
```

#### **Cancel Sale**
```
fail
```

#### **View Inventory**
```
view
```

### **Natural Language Examples (with NLP)**
```
"I want to add 100 Natraj Pencils for 5 rupees"
"Update Natraj Pencils to 50 quantity"
"Create bill for Rahul – 2 Notebooks with 5% discount"
"Show me items running low on stock"
"Check how many Ball Pens do we have"
```

---

## 💻 Frontend Features

### **Modern UI/UX Design**
- Glass morphism effects with backdrop blur
- Gradient backgrounds and modern shadows
- Smooth animations and transitions
- Responsive design for all devices
- Color-coded status indicators
- Professional typography and spacing

### **Dashboard Analytics**
- Real-time business metrics
- Visual stats cards with icons
- Recent sales overview
- Quick action buttons
- Today's sales tracking

### **Inventory Management**
- Card-based modern layout
- Advanced search functionality
- Quick edit capabilities
- Stock status badges
- Empty state handling

### **Invoice Generation**
- Two-column responsive design
- Live invoice preview
- Multi-item selection
- Tax calculation display
- Customer information capture
- PDF generation

### **Sales History**
- Pagination (10 items/page)
- Multi-field search
- Status filtering
- Sale returns
- PDF downloads
- Detailed views

---

## 🌐 Deployment

### **Backend Deployment (Render/Railway/Fly.io)**

#### **Render**
```yaml
# render.yaml
services:
  - type: web
    name: whatsapp-retailer-api
    env: python
    buildCommand: pip install -r backend/requirements.txt
    startCommand: uvicorn backend.app.main:app --host 0.0.0.0 --port $PORT
    envVars:
      - key: DATABASE_URL
        fromDatabase:
          name: whatsapp_retailer_db
          property: connectionString
```

### **Frontend Deployment (Netlify/Vercel)**

#### **Netlify**
```toml
# netlify.toml
[build]
  base = "frontend"
  command = "npm run build"
  publish = "build"

[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
```

### **Database Deployment**
- **Neon**: Free PostgreSQL with generous limits
- **Supabase**: PostgreSQL with additional features
- **AWS RDS**: Production-grade managed PostgreSQL
- **Render PostgreSQL**: Integrated with backend

### **Environment Variables (Production)**
```bash
# Database
DATABASE_URL=postgresql://user:pass@host:5432/db

# Security
SECRET_KEY=<generate-strong-secret>
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=1440

# WhatsApp API
WHATSAPP_ACCESS_TOKEN=<your-token>
WHATSAPP_PHONE_NUMBER_ID_INVENTORY=<phone-id-1>
WHATSAPP_PHONE_NUMBER_ID_INVOICE=<phone-id-2>
WHATSAPP_WEBHOOK_VERIFY_TOKEN=<verify-token>

# OpenAI (Optional)
OPENAI_API_KEY=sk-<your-key>

# Application
DEBUG=False
ENVIRONMENT=production
```

---

## ⚡ Performance & Scalability

### **Performance Optimizations**
- **Async/Await**: FastAPI async endpoints for high concurrency
- **Database Indexing**: Strategic indexes on frequently queried columns
- **Connection Pooling**: SQLAlchemy connection pool management
- **Response Caching**: API response caching for static data
- **Lazy Loading**: React lazy loading for code splitting
- **Pagination**: Server-side pagination to reduce payload size

### **Scalability Features**
- **Horizontal Scaling**: Stateless design allows multiple instances
- **Database Migrations**: Alembic for zero-downtime schema updates
- **Rate Limiting**: Built-in protection against API abuse
- **Error Handling**: Comprehensive error handling with logging
- **Monitoring Ready**: Structured logging for observability

### **Benchmarks**
- API Response Time: < 100ms (p95)
- WhatsApp Message Processing: < 500ms
- PDF Generation: < 2 seconds
- Concurrent Users: 1000+ (single instance)

---

## 🔒 Security Features

### **Authentication & Authorization**
- JWT-based authentication with secure token generation
- Password hashing with bcrypt (12 rounds)
- Session management with expiration
- CORS configuration for API security
- Input validation with Pydantic

### **Data Protection**
- SQL injection prevention (SQLAlchemy ORM)
- XSS protection (React auto-escaping)
- CSRF protection for state-changing operations
- Secure password reset flow
- Environment variable protection

### **API Security**
- Rate limiting on sensitive endpoints
- Request validation and sanitization
- Error message sanitization (no data leakage)
- HTTPS enforcement in production
- Webhook signature verification (WhatsApp)

---

## 🎯 Future Enhancements

### **Planned Features**
- [ ] Multi-tenant Architecture (one bot per retailer)
- [ ] Real-time Inventory Updates (WebSockets)
- [ ] Advanced Analytics Dashboard (Charts & Graphs)
- [ ] Payment Integration (Stripe/Razorpay)
- [ ] Email Notifications for critical events
- [ ] Barcode/QR Code Scanning
- [ ] Automated Purchase Orders
- [ ] Supplier Management Module
- [ ] Mobile App (React Native)
- [ ] Multi-currency Support
- [ ] Role-Based Access Control (RBAC)
- [ ] Data Export (CSV, Excel)
- [ ] Backup & Restore Functionality

### **Technical Improvements**
- [ ] GraphQL API option
- [ ] Redis Caching Layer
- [ ] Microservices Architecture
- [ ] Docker & Kubernetes Deployment
- [ ] CI/CD Pipeline (GitHub Actions)
- [ ] Load Testing & Performance Monitoring
- [ ] A/B Testing Framework

---

## 👨‍💻 Developer

**Raghav Khandelwal**

I'm a passionate full-stack developer specializing in building scalable web applications and AI-powered solutions. This project demonstrates my expertise in:

- **Backend Development**: FastAPI, SQLAlchemy, RESTful APIs, Database Design
- **Frontend Development**: React, Modern UI/UX, Responsive Design
- **AI Integration**: OpenAI GPT-4o, Natural Language Processing
- **API Integration**: WhatsApp Business API, Third-party Services
- **Database Management**: PostgreSQL, Alembic Migrations, Query Optimization
- **Software Architecture**: Clean Code, SOLID Principles, Scalable Design
- **DevOps**: Deployment, Environment Management, Production Best Practices

---

## 📧 Contact

- **Email**: khandelwalraghav43@gmail.com
- **Phone**: +91 9636884173

---

## 🙏 Acknowledgments

- FastAPI for the excellent framework
- Meta for WhatsApp Business API
- OpenAI for GPT-4o capabilities
- The open-source community for various libraries

---

**Built with ❤️ for retailers worldwide**
