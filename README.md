No-Broker Kathmandu

Modern, production-ready rental marketplace connecting tenants with property owners in Kathmandu — without brokers. This monorepo includes a Node.js/Express backend with PostgreSQL and a React + TypeScript frontend. Real-time messaging, visits scheduling, listings management, notifications, ads, recommendations, payments, and admin/staff tooling are included.

## Tech Stack
- Backend: Node.js, Express, Socket.IO, PostgreSQL (`pg`)
- Frontend: React, TypeScript, Redux Toolkit, Tailwind CSS, Vite/CRA build
- Security: Helmet, CORS, JWT
- Ops: Compression, Rate limiting, Custom monitoring middleware

## Key Modules & Features
- Authentication & Authorization (JWT-based, roles: tenant, owner, staff, admin)
- Listings & Media Uploads
- Visits Scheduling and Decisions
- Messaging (real-time via Socket.IO)
- Notifications (in-app, WebSocket broadcast)
- Favorites, Ratings, Recommendations
- Agreements & Payments
- Admin & Staff dashboards and APIs

## Quick Start
Prerequisites
- Node.js 18+
- PostgreSQL 13+

Environment
- Copy `.env.production` to `.env` for local use and adjust values

Install
```bash
cd backend && npm install
cd ../frontend && npm install
```

Database
- Create database and run SQL from `database/schema.sql` (plus incremental files as needed)

Run
```bash
# Backend
cd backend
npm run start

# Frontend
cd ../frontend
npm run dev
```

Health Check
- Backend: `GET /api/health`

## Architecture Preview
High-level architecture is documented in `diagrams/system_architecture.mmd` and referenced from `FULL_DOCUMENTATION.md`.

## Repository Structure
```
backend/        # Express server, routes, middleware
frontend/       # React + TS app
database/       # SQL schemas and migrations
diagrams/       # Mermaid diagrams (architecture, schema, module flows, use cases)
README.md
FULL_DOCUMENTATION.md
```

## License
Copyright © 2025. All rights reserved.

# No-Broker Kathmandu

Modern, full-stack property rental platform for Kathmandu, Nepal — connecting tenants and property owners directly, with streamlined discovery, messaging, visit scheduling, KYC, analytics, and monetization.

[Business Analyst Overview](docs/Business-Analyst-Overview.md) · [Deployment Guide](DEPLOYMENT_GUIDE.md) · [Optimization Plan](PRODUCTION_OPTIMIZATION_PLAN.md) · [Messaging System](MESSAGING_SYSTEM_IMPLEMENTATION.md) · [Database Fixes](DATABASE_FIXES.md)

---

## Table of Contents
- Features
- Technology Stack
- Prerequisites
- Installation
- Network Access
- Usage (Tenants, Owners)
- Security Features
- API Endpoints (summary)
- Troubleshooting
- Contributing
- License
- Roadmap


## 🚀 Features

### For Tenants
- Browse available properties with advanced search and filtering
- Schedule property visits
- Manage visit history and feedback
- User profile management with KYC verification
- Real-time notifications

### For Property Owners
- Create and manage property listings
- Upload property images
- Handle visit requests
- Track property performance
- Manage tenant agreements

### Core Features
- **Authentication & Authorization**: Secure login/registration with role-based access
- **Property Listings**: Comprehensive property management with search and filters
- **Visit Management**: Schedule, track, and manage property visits
- **KYC Verification**: Built-in identity verification system
- **Responsive Design**: Mobile-friendly interface
- **Network Access**: Accessible from any device on your network

## 🛠️ Technology Stack

### Backend
- **Node.js** with Express.js
- **PostgreSQL** database
- **JWT** authentication
- **Multer** for file uploads
- **CORS** enabled for network access

Key files and structure:
- `backend/server.js` — Express app, middleware, routing
- `backend/routes/*.js` — Feature routes (auth, listings, visits, messages, favorites, ratings, users, admin, owners, ads, notifications, payments, recommendations)
- `backend/middleware/*.js` — Auth and monitoring
- `backend/config/database.js` — DB connection and pooling

### Frontend
- **React** with TypeScript
- **Redux Toolkit** for state management
- **React Router** for navigation
- **Tailwind CSS** for styling
- **Axios** for API communication

Key files and structure:
- `frontend/src/pages/*` — Core pages (Home, Listings, Detail, Create, Dashboards, Auth, Terms/Privacy)
- `frontend/src/components/*` — Layout, messaging, notifications, ads, reports
- `frontend/src/store/*` — Redux store and slices (auth, listings, visits, favorites, notifications, payments, recommendations, ui)
- `frontend/src/services/*` — API clients (authAPI, listingsAPI, visitsAPI, messagingService)
- `frontend/tailwind.config.js` — Design system extensions

### Database
- PostgreSQL with scripts in `database/`
- Start from `database/schema.sql` then apply feature scripts (favorites, photos, views, messaging, ads, visit decisions, notifications, optimization)

## 📋 Prerequisites

- Node.js (v14 or higher)
- PostgreSQL database
- npm or yarn package manager

## 🔧 Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd no-broker-kathmandu
```

### 2. Backend Setup
```bash
cd backend
npm install
```

### 3. Database Setup
- Create a PostgreSQL database
- Update the database configuration in `backend/.env`
- Run the base schema then feature scripts:
  - `database/schema.sql`
  - `database/add_favorites_table.sql`
  - `database/add_listing_photos_table.sql`
  - `database/add_listing_views_table.sql`
  - `database/add_messaging_tables.sql`
  - `database/add_notifications_updated_at.sql`
  - `database/add_visit_decisions_columns.sql`
  - `database/ads_schema.sql`
  - `database/production_optimization.sql`
  - See `DATABASE_FIXES.md` for context

### 4. Environment Variables
Create `backend/.env` file:
```env
PORT=5000
DB_HOST=localhost
DB_PORT=5432
DB_NAME=no_broker_kathmandu
DB_USER=your_username
DB_PASSWORD=your_password
JWT_SECRET=your_jwt_secret
BCRYPT_ROUNDS=10
FRONTEND_URL=http://localhost:3000
```

### 5. Frontend Setup
```bash
cd frontend
npm install
```

### 6. Start the Application

#### Development Mode
```bash
# Terminal 1 - Backend
cd backend
npm run dev

# Terminal 2 - Frontend
cd frontend
npm start
```

#### Production Mode
```bash
# Backend
cd backend
npm start

# Frontend
cd frontend
npm run build
npm start
```

## 🌐 Network Access

The application is configured to be accessible from other devices on your network:

### Backend API
- **Local**: http://localhost:5000
- **Network**: http://YOUR_IP:5000

### Frontend App
- **Local**: http://localhost:3000
- **Network**: http://YOUR_IP:3000

### Get Your Network IP
Run the provided script:
```bash
get-network-info.bat
```

## 📱 Usage

### For Tenants
1. **Register/Login**: Create an account or sign in
2. **Browse Properties**: Use search and filters to find properties
3. **Schedule Visits**: Book property visits with owners
4. **Manage Profile**: Update personal information and KYC status

### For Property Owners
1. **Register/Login**: Create an owner account
2. **Create Listings**: Add property details and upload images
3. **Manage Visits**: Handle tenant visit requests
4. **Track Performance**: Monitor listing views and inquiries

## 🔒 Security Features

- JWT-based authentication
- Password hashing with bcrypt
- CORS protection
- Rate limiting
- Input validation
- SQL injection prevention

## 📊 API Endpoints

For detailed API docs and workflows, see `NO_BROKER_KATHMANDU_DOCUMENTATION.txt` (Sections 3–4). Below is a high-level summary.

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `GET /api/auth/profile` - Get user profile
- `PUT /api/auth/profile` - Update profile
- `PUT /api/auth/change-password` - Change password

### Listings
- `GET /api/listings` - Get all listings
- `POST /api/listings` - Create new listing
- `GET /api/listings/:id` - Get listing by ID
- `PUT /api/listings/:id` - Update listing
- `DELETE /api/listings/:id` - Delete listing

### Visits
- `GET /api/visits` - Get user visits
- `POST /api/visits` - Schedule visit
- `PUT /api/visits/:id` - Update visit status
- `DELETE /api/visits/:id` - Cancel visit

## 🐛 Troubleshooting

### Common Issues

1. **Port Already in Use**
   ```bash
   # Kill process on port 5000
   netstat -ano | findstr :5000
   taskkill /PID <PID> /F
   ```

2. **Database Connection Error**
   - Check PostgreSQL service is running
   - Verify database credentials in `.env`
   - Ensure database exists

3. **CORS Errors**
   - Check CORS configuration in `server.js`
   - Verify frontend URL in environment variables

4. **Network Access Issues**
   - Check Windows Firewall settings
   - Ensure both backend and frontend are running
   - Verify IP address is correct

## 📝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 🤝 Support

For support and questions:
- Create an issue in the repository
- Contact the development team

## 🎯 Roadmap

- [ ] Mobile app development (React Native)
- [ ] Payment integration and document signing
- [ ] Advanced analytics and dashboards
- [ ] Multi-language support and SEO
- [ ] Push notifications and PWA
- [ ] Video tours and virtual walkthroughs
- [ ] AI-powered recommendations

---

This repository includes comprehensive implementation and documentation targeted at both business and engineering stakeholders. Start with the [Business Analyst Overview](docs/Business-Analyst-Overview.md) for strategy and KPIs, then dive into the technical docs linked above for deployment and scaling.

---

**No-Broker Kathmandu** - Making property rental simple and transparent in Kathmandu Valley.
