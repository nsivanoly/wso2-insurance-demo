<div align="center">

# 🏢 Insurance Demo Platform

**A comprehensive, production-ready insurance management system built on WSO2 middleware stack**

[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=flat&logo=docker)](https://www.docker.com/)
[![WSO2](https://img.shields.io/badge/WSO2-API%20Manager%204.6.0-orange)](https://wso2.com/api-manager/)
[![WSO2](https://img.shields.io/badge/WSO2-Identity%20and%20Access%20Management%207.2.0-orange)](https://wso2.com/identity-and-access-management/)
[![WSO2](https://img.shields.io/badge/WSO2-Integration%204.5.0-orange)](https://wso2.com/integration/)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react)](https://reactjs.org/)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

*One-command deployment of a fully integrated insurance domain platform with automated API management, identity governance, data services, and modern React frontend.*

[Features](#-features) • [Quick Start](#-quick-start) • [Architecture](#-architecture) • [Documentation](#-documentation) • [Contributing](#-contributing)

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Architecture](#-architecture)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Service Endpoints](#-service-endpoints)
- [Project Structure](#-project-structure)
- [Configuration](#-configuration)
- [APIs & Data Services](#-apis--data-services)
- [Frontend Application](#-frontend-application)
- [Deployment Scripts](#-deployment-scripts)
- [Database Schema](#-database-schema)
- [Authentication & Authorization](#-authentication--authorization)
- [Upgrading Components](#-upgrading-components)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🔍 Overview

The Insurance Demo Platform is a fully containerized, enterprise-grade reference implementation showcasing an end-to-end insurance management system. Built on the WSO2 middleware stack, it demonstrates best practices for API management, identity & access management, data integration, and modern frontend development.

### What's Included

- **WSO2 API Manager 4.6.0** - API lifecycle management, gateway, publisher & developer portal
- **WSO2 Identity Server 7.2.0** - OAuth2/OIDC provider, user management, RBAC
- **WSO2 Micro Integrator 4.5.0** - Data services layer with JDBC connectivity
- **WSO2 Integration Control Plane 1.2.0** - Service catalog and governance
- **MySQL 8.0** - Pre-seeded relational database with insurance domain schema
- **React 19 + Vite** - Modern SPA with role-based portal routing (admin/customer/employee)
- **Automated Bootstrap** - Zero-config startup with API imports, key manager registration, and app provisioning

### Use Cases

✅ **Learning & Training** - Understand WSO2 product integration patterns  
✅ **POC Development** - Rapidly prototype insurance/financial domain solutions  
✅ **Integration Testing** - Test API management workflows with realistic data  
✅ **Architecture Reference** - Study microservices and API-first architecture

---

## ✨ Features

### 🔐 **Enterprise Security**
- OAuth 2.0 / OpenID Connect authentication via WSO2 IS
- Role-based access control (Admin, Employee, Customer)
- JWT token-based API authorization
- Secure key manager integration between APIM and IS

### 🚀 **API Management**
- 7 pre-configured REST APIs (Claims, Customers, Employees, Policies, Products, Email, Address Verification)
- Automatic API import, publication, and subscription during first boot
- Rate limiting and throttling policies
- CORS-enabled endpoints for frontend integration

### 💾 **Data Services**
- 7 Carbon applications (.car) for data service integrations
- MySQL connector pre-installed in Micro Integrator
- Transactional data operations for insurance entities
- Service catalog integration with APIM

### 🎨 **Modern Frontend**
- React 19 with TypeScript and Vite bundler
- Three portal experiences: Admin Dashboard, Employee Portal, Customer Portal
- Charts and visualizations (Chart.js, Recharts)
- Responsive design with styled-components
- Automatic portal routing based on user groups

### 🔄 **DevOps Ready**
- Docker Compose orchestration
- Health checks and service dependencies
- Persistent volumes for data and configurations
- Interactive CLI scripts with colored output
- Idempotent initialization (safe to restart)

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   React Frontend (Port 5173)                             │   │
│  │   - Admin Portal  - Employee Portal  - Customer Portal   │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓ HTTPS/OAuth2
┌─────────────────────────────────────────────────────────────────┐
│                      API GATEWAY LAYER                          │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   WSO2 API Manager (Port 9446)                           │   │
│  │   - Publisher  - DevPortal  - Gateway (8280/8246)        │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                    IDENTITY & ACCESS LAYER                      │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   WSO2 Identity Server (Port 9443)                       │   │
│  │   - OAuth2/OIDC Provider  - User Store  - Key Manager    │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────────┐
│                    INTEGRATION LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   WSO2 Micro Integrator (Port 8290)                      │   │
│  │   - Data Services  - Message Routing  - Transformations  │   │
│  └──────────────────────────────────────────────────────────┘   │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   Integration Control Plane (Port 9743)                  │   │
│  │   - Service Catalog  - Governance                        │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
                              ↓ JDBC
┌─────────────────────────────────────────────────────────────────┐
│                        DATA LAYER                               │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │   MySQL 8.0 (Port 3306)                                  │   │
│  │   - Insurance Domain Schema  - Sample Data               │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📦 Prerequisites

### System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| **RAM** | 8 GB | 16 GB |
| **CPU** | 4 cores | 8 cores |
| **Disk Space** | 20 GB free | 50 GB free |
| **OS** | macOS, Linux, Windows (WSL2) | - |

### Software Dependencies

- **Docker Engine** 20.10+ or **Docker Desktop** 4.0+
- **Docker Compose** v2.0+
- **Git** (for cloning the repository)

### Required Ports

Ensure these ports are available on your host machine:

| Port(s) | Service |
|---------|---------|
| 3306 | MySQL |
| 5173 | Frontend (Vite) |
| 8090, 8246, 8253, 8280, 8290 | WSO2 HTTP/HTTPS |
| 9090-9096, 9099 | WSO2 Management |
| 9164 | Micro Integrator Admin |
| 9443 | Identity Server Console |
| 9446 | API Manager Console |
| 9743 | Integration Control Plane |

---

## 🚀 Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/nsivanoly/wso2-insurance-demo.git
cd wso2-insurance-demo
```

### 2️⃣ Start the Platform

```bash
./start.sh
```

**What happens during startup:**
- Environment files auto-created from samples (`.env`, `apictl.env`, `iamctl.env`)
- Docker validates prerequisites and builds images (if needed)
- MySQL starts and schema is seeded
- WSO2 services start: IS → APIM → MI → ICP
- **First run only:**
  - APIs imported and published to APIM
  - IS registered as Key Manager in APIM
  - DevPortal application created and subscribed to all APIs
- Frontend dev server starts

⏱️ **Initial startup:** ~5-10 minutes (image pulls + service initialization)  
⏱️ **Subsequent starts:** ~2-3 minutes

### 3️⃣ Access Services

Once startup completes, access the platform:

| Service | URL | Credentials |
|---------|-----|-------------|
| **Frontend** | http://localhost:5173 | Click "Login" (redirects to IS) |
| **API Manager** | https://localhost:9446/publisher | `admin` / `admin` |
| **Identity Server** | https://localhost:9443/console | `admin` / `admin` |
| **Integration Control Plane** | https://localhost:9743/login | `admin` / `admin` |

### 4️⃣ Stop the Platform

```bash
# Graceful shutdown (preserves data)
./stop.sh

# Remove volumes (data wipe)
./stop.sh --remove-volumes

# Full cleanup (volumes + images)
./stop.sh --remove-all
```

### 5️⃣ Rebuild from Scratch

```bash
./rebuild-run.sh
```
This stops services, rebuilds images, and restarts everything fresh.

---

## 🌐 Service Endpoints

### 🎯 Main Access Points

| Service | URL | Default Port | Purpose |
|---------|-----|--------------|---------|
| **Frontend Application** | http://localhost:5173 | 5173 | User-facing SPA (Admin/Employee/Customer portals) |
| **API Manager Publisher** | https://localhost:9446/publisher | 9446 | API lifecycle management & publishing |
| **API Manager DevPortal** | https://localhost:9446/devportal | 9446 | Developer portal for API discovery & subscriptions |
| **Identity Server Console** | https://localhost:9443/console | 9443 | User/role management & OAuth app configuration |
| **Micro Integrator** | http://localhost:8290 | 8290 | Data services & integration endpoints |
| **Integration Control Plane** | http://localhost:9743 | 9743 | Service catalog & monitoring dashboard |
| **MySQL Database** | localhost:3306 | 3306 | Direct database access (host) |

### 🔑 Default Credentials

- **WSO2 Services (APIM/IS/ICP):** `admin` / `admin`
- **MySQL:** `root` / `12345` (configurable in `.env`)

---

## 📁 Project Structure

```
wso2-insurance-demo/
├── 📄 README.md                           # This file
├── 📄 docker-compose.yml                   # Container orchestration
├── 📄 Dockerfile                           # Multi-stage image build
├── 📄 .env                                 # Environment configuration
├── 🔧 start.sh                            # Interactive startup script
├── 🔧 stop.sh                             # Graceful shutdown script
├── 🔧 rebuild-run.sh                      # Full rebuild automation
│
├── 📂 deployment/                          # Container initialization
│   ├── container-entrypoint.sh            # Main orchestration script
│   ├── 📂 container-init/                 # Bootstrap scripts
│   │   ├── wait-for-services.sh           # Health check waiter
│   │   ├── setup-database.sh              # DB schema initialization
│   │   ├── start-services.sh              # WSO2 services starter
│   │   ├── setup-apis.sh                  # API import via apictl
│   │   ├── setup-keymanager.sh            # IS-APIM key manager registration
│   │   ├── setup-app.sh                   # DevPortal app creation & subscription
│   │   └── start-frontend.sh              # Vite dev server launcher
│   ├── 📂 config/                         # CLI tool configurations
│   │   ├── apictl.env.sample              # API Manager CLI config template
│   │   └── iamctl.env.sample              # Identity Server CLI config template
│   └── 📂 tools/                          # Bundled CLI binaries
│       ├── apictl                          # WSO2 API Manager CLI
│       └── iamctl                          # WSO2 Identity Server CLI
│
├── 📂 src/
│   ├── 📂 backend/
│   │   ├── 📂 apis/                       # OpenAPI definitions (7 APIs)
│   │   │   ├── claim-api-1.0/
│   │   │   ├── customer-api-1.0/
│   │   │   ├── employee-api-1.0/
│   │   │   ├── policies-api-1.0/
│   │   │   ├── products-api-1.0/
│   │   │   ├── email-api-1.0/
│   │   │   └── addressverification-api-1.0/
│   │   ├── 📂 config/                     # WSO2 configuration overlays
│   │   │   ├── certs/                      # JKS keystores
│   │   │   ├── wso2-am/repository/        # APIM configs (deployment.toml, etc.)
│   │   │   ├── wso2-is/repository/        # IS configs
│   │   │   └── wso2-mi/conf/              # MI configs
│   │   └── 📂 micro-integrator/
│   │       └── carbonapps/                 # Data service artifacts (7 .car files)
│   │
│   ├── 📂 database/
│   │   └── mysql-scripts/
│   │       └── insurance_domain.sql        # Schema + seed data
│   │
│   └── 📂 frontend/                       # React + Vite SPA
│       ├── package.json                    # Dependencies
│       ├── vite.config.ts                  # Vite configuration
│       ├── tsconfig.json                   # TypeScript config
│       └── src/
│           ├── App.tsx                     # Main app with auth & routing
│           ├── main.tsx                    # Entry point (Asgardeo provider)
│           ├── 📂 portals/                # Role-specific dashboards
│           │   ├── admin/
│           │   ├── customer/
│           │   └── employee/
│           ├── 📂 components/             # Reusable UI components
│           ├── 📂 routes/                 # React Router configuration
│           ├── 📂 lib/                    # Utilities & API clients
│           │   ├── auth/                   # Auth utilities (authUtils.ts)
│           │   └── api/                    # API service clients
│           ├── 📂 types/                  # TypeScript type definitions
│           └── 📂 styles/                 # Global styles & themes
```

---

## ⚙️ Configuration

### Environment Variables

All configuration is centralized in `.env` (auto-created from `.env.sample`):

#### Database Configuration
```env
MYSQL_ROOT_PASSWORD=12345
MYSQL_DATABASE=insurance
MYSQL_HOST_PORT=3306
```

#### WSO2 Version Control
```env
APIM_VERSION=4.6.0          # API Manager version
MI_VERSION=4.5.0            # Micro Integrator version
IS_VERSION=7.2.0            # Identity Server version
ICP_VERSION=1.2.0           # Integration Control Plane version
```

#### Port Mappings
```env
APIM_CONSOLE_PORT=9446      # API Manager console (offset +3 applied)
IS_CONSOLE_PORT=9443        # Identity Server console
MI_HTTP_PORT=8290           # Micro Integrator data services
FRONTEND_PORT=5173          # Vite dev server
ICP_PORT=9743               # Integration Control Plane
```

#### Key Manager Configuration
```env
KEY_MANAGER_NAME=WSO2IS72
KEY_MANAGER_TYPE=WSO2-IS
ENABLE_KEY_MANAGER_SETUP=true
```

### Frontend OIDC Configuration
```env
VITE_AUTH_SIGN_IN_REDIRECT_URL=http://localhost:5173
VITE_AUTH_SIGN_OUT_REDIRECT_URL=http://localhost:5173
VITE_AUTH_CLIENT_ID=<your-client-id>
VITE_AUTH_BASE_URL=https://localhost:9443
VITE_AUTH_SCOPE=openid profile groups email db_id
```

### CLI Tool Configuration

- **apictl:** `deployment/config/apictl.env` (API Manager operations)
- **iamctl:** `deployment/config/iamctl.env` (Identity Server operations)

Both auto-generated from `.sample` files if missing.

---

## 🔌 APIs & Data Services

### Available REST APIs

| API Name | Context Path | Version | Purpose |
|----------|--------------|---------|---------|
| **Claim API** | `/claim-api` | 1.0 | Claims submission, retrieval, status updates |
| **Customer API** | `/customer-api` | 1.0 | Customer CRUD operations |
| **Employee API** | `/employee-api` | 1.0 | Employee management |
| **Policies API** | `/policies-api` | 1.0 | Insurance policy lifecycle |
| **Products API** | `/products-api` | 1.0 | Insurance product catalog |
| **Email API** | `/email-api` | 1.0 | Email notification service |
| **Address Verification API** | `/addressverification-api` | 1.0 | Address validation service |

### Security Scheme
All APIs use OAuth 2.0 with JWT tokens. Security schemes:
- `oauth2`

### Data Service Artifacts (.car files)

Located in `src/backend/micro-integrator/carbonapps/`:

1. `ClaimsDataService_1.0.0.car` - Claims data operations
2. `CustomerDataService_1.0.0.car` - Customer data operations
3. `EmployeeDataService_1.0.0.car` - Employee data operations
4. `PoliciesDataService_1.0.0.car` - Policy data operations
5. `ProductsDataService_1.0.0.car` - Product catalog operations
6. `addressveriication_1.0.0.car` - Address verification logic
7. `sendemail_1.0.0.car` - Email sending service

These .car files are automatically deployed to the Micro Integrator on startup.

---

## 🎨 Frontend Application

### Technology Stack

- **React 19** - UI library
- **TypeScript** - Type safety
- **Vite 6** - Build tool & dev server
- **@asgardeo/auth-react** - OAuth2/OIDC authentication
- **React Router 7** - Client-side routing
- **styled-components** - CSS-in-JS styling
- **Chart.js / Recharts** - Data visualization
- **Axios** - HTTP client

### Portal Routing

The frontend automatically routes users to the appropriate portal based on their Identity Server group membership:

| Group | Portal Route | Features |
|-------|--------------|----------|
| **admin** | `/admin/*` | Dashboard, user management, system config |
| **Employees** | `/employee/*` | Claims processing, policy management |
| **Customers** | `/customer/*` | Policy view, claims submission, profile |

Routing logic in `src/frontend/src/lib/auth/authUtils.ts`:
```typescript
export const getUserPortalType = (groups: string[]): PortalType => {
  if (groups.includes('admin')) return 'admin';
  if (groups.includes('Employees')) return 'employee';
  if (groups.includes('Customers')) return 'customer';
  return 'customer'; // default
};
```

## 🛠️ Deployment Scripts

### `start.sh` - Interactive Startup

**Usage:**
```bash
./start.sh [OPTIONS]
```

**Options:**
- `--rebuild` - Rebuild Docker images before starting
- `--no-cache` - Build without Docker layer cache
- `--follow-logs` - Stream container logs after startup
- `--foreground` - Run containers in foreground (attached mode)
- `--help` - Show usage information

**Interactive Menu:**
```
1) Standard start (use existing containers)
2) Rebuild and start (rebuild images before starting)
3) Start and follow logs
4) Start in foreground mode
5) Full rebuild with cache purge (no cache)
6) Exit
```

### `stop.sh` - Graceful Shutdown

**Usage:**
```bash
./stop.sh [OPTIONS]
```

**Options:**
- `--remove-volumes` - Remove data volumes (⚠️ data loss)
- `--remove-all` - Remove containers, networks, and volumes
- `--non-interactive` - Skip confirmation prompts
- `--help` - Show usage information

**Interactive Menu:**
```
1) Graceful stop only (preserve everything)
2) Stop and remove volumes
3) Full cleanup (remove all images and networks)
4) Exit
```

### `rebuild-run.sh` - Full Clean Rebuild

Automates the complete rebuild process:
1. Stop and remove all containers/volumes
2. Rebuild Docker images from scratch
3. Start services with fresh state

---

## 🗄️ Database Schema

The MySQL database is automatically initialized with the insurance domain schema located in `src/database/mysql-scripts/insurance_domain.sql`.

### Core Tables

| Table | Primary Key | Auto-Increment Pattern | Description |
|-------|-------------|------------------------|-------------|
| `products` | `product_id` | `P_001`, `P_002`, ... | Insurance products catalog |
| `customers` | `customer_id` | `C_001`, `C_002`, ... | Customer records |
| `employees` | `employee_id` | `E_001`, `E_002`, ... | Employee records |
| `policies` | `policy_id` | `POL_001`, `POL_002`, ... | Insurance policies |
| `claims` | `claim_id` | `CLM_001`, `CLM_002`, ... | Claims submissions |

### Sample Data Included

- **5 Employees** - Claims officers, underwriters, agents
- **5 Customers** - Pre-registered users with contact info
- **5 Products** - Health, auto, home, life, travel insurance
- **5 Policies** - Active sample policies
- **5 Claims** - Sample claims with various statuses

### Relationships

```sql
policies.customer_id → customers.customer_id
policies.product_id → products.product_id
policies.employee_id → employees.employee_id
claims.policy_id → policies.policy_id
```

---

## 🔐 Authentication & Authorization

### OAuth 2.0 / OIDC Flow

1. User clicks "Login" in frontend
2. Redirected to WSO2 IS login page (`https://localhost:9443`)
3. User authenticates (credentials managed in IS)
4. IS returns authorization code
5. Frontend exchanges code for tokens (ID token, access token)
6. Access token used for API calls to APIM gateway
7. APIM validates token with IS (Key Manager)

### User Groups & Roles

Configured in WSO2 Identity Server:

- **admin** - Full system access
- **Employees** - Claims processing, policy management
- **Customers** - View policies, submit claims

### Test User Details

| Group     | Username | Password  |
|-----------|----------|-----------|
| Employee  | kim      | aBcd!23#  |
| Employee  | alice    | Xyz@456!  |
| Customer  | john     | Pass@789# |

### Token Structure

ID Token contains:
```json
{
  "sub": "user@example.com",
  "groups": ["Customers"],
  "db_id": "C_001",
  "email": "user@example.com"
}
```

The `db_id` claim links the authenticated user to database records.

---

## 🔄 Upgrading Components

### Changing WSO2 Versions

1. **Edit `.env` file:**
   ```env
   APIM_VERSION=4.7.0
   MI_VERSION=4.6.0
   IS_VERSION=7.3.0
   ICP_VERSION=1.3.0
   ```

2. **Rebuild images:**
   ```bash
   ./start.sh --rebuild
   # OR
   docker-compose build --no-cache
   ```

3. **Reconcile configurations:**
   - Compare new distribution configs with `src/backend/config/*`
   - Update `deployment.toml` files if needed
   - Verify port offsets remain correct

4. **Update MI artifacts:**
   - If JDBC driver changes, update MySQL connector version in Dockerfile
   - Rebuild .car files if data service schemas change

5. **Test thoroughly:**
   ```bash
   docker-compose logs -f wso2-insurance
   ```

### Version Compatibility Notes

- APIM 4.6.0 requires Java 21 (pre-configured in Dockerfile)
- IS 7.2.0 uses new console UI (different from 6.x)
- MI 4.5.0 service catalog integrates with APIM 4.6.0
- ICP version must be passed via docker-compose build arg (already configured)

---

## 🐛 Troubleshooting

### Common Issues

#### 1. Port Already in Use
**Symptom:** `Error starting userland proxy: listen tcp 0.0.0.0:9446: bind: address already in use`

**Solution:**
```bash
# Check what's using the port
lsof -i :9446

# Change ports in .env
APIM_CONSOLE_PORT=9450

# Restart
./start.sh
```

#### 2. Slow First Startup
**Symptom:** Services take 10+ minutes to start

**Cause:** Large WSO2 base images being pulled (~4GB total)

**Solution:** Be patient on first run. Subsequent starts reuse cached layers.

#### 3. API Import Failures
**Symptom:** APIs not appearing in Publisher portal

**Check logs:**
```bash
docker-compose logs -f wso2-insurance | grep "SETUP-APIS"
```

**Solution:**
- Verify `src/backend/apis/*` directories contain `api.yaml` files
- Ensure APIM is fully started before API import (wait 2-3 minutes)
- Rerun setup: `docker exec -it insurance-platform /app/container-scripts/setup-apis.sh`

#### 4. Key Manager Registration Failed
**Symptom:** "Key Manager WSO2IS72 not found" in logs

**Solution:**
```bash
# Manually run key manager setup
docker exec -it insurance-platform /app/container-scripts/setup-keymanager.sh

# Verify in APIM
# Admin Portal → Key Managers
```

#### 5. Frontend Won't Load
**Symptom:** `http://localhost:5173` shows connection refused

**Check:**
```bash
docker-compose logs -f wso2-insurance | grep "FRONTEND"
```

**Common causes:**
- Port 5173 in use → Change `FRONTEND_PORT` in `.env`
- npm install failed → Check Node.js version in container
- Vite config issue → Verify `vite.config.ts`

#### 6. Database Connection Errors
**Symptom:** MI logs show "Cannot create PoolableConnectionFactory"

**Solution:**
```bash
# Verify MySQL is healthy
docker-compose ps mysql

# Check connectivity from container
docker exec -it insurance-platform mysql -h mysql -u root -p12345 -e "SHOW DATABASES;"
```

#### 7. OAuth Login Fails
**Symptom:** Redirect loop or "Invalid client" error

**Check:**
- IS application callback URL matches `VITE_AUTH_SIGN_IN_REDIRECT_URL`
- Client ID in frontend .env matches IS application
- IS key manager registered in APIM

**Debug:**
```bash
# Check IS logs
docker-compose logs -f wso2-insurance | grep "wso2is"
```

### Getting Help

1. **Check logs:**
   ```bash
   docker-compose logs -f wso2-insurance
   ```

2. **Inspect service status:**
   ```bash
   docker-compose ps
   ```

3. **Verify initialization marker:**
   ```bash
   docker exec -it insurance-platform ls -la /home/wso2carbon/.initialization_complete
   ```

4. **Clean slate restart:**
   ```bash
   ./stop.sh --remove-volumes
   ./rebuild-run.sh
   ```

---

## 🤝 Contributing

We welcome contributions! Please follow these guidelines:

### Reporting Issues

When filing an issue, include:
- Output of `docker-compose ps`
- Relevant logs: `docker-compose logs wso2-insurance`
- Steps to reproduce
- Expected vs actual behavior

### Pull Requests

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Make changes with clear commit messages
4. Test thoroughly (provide test results)
5. Submit PR with description of changes

### Code Style

- **Shell scripts:** Use `shellcheck` for linting
- **TypeScript/React:** Follow existing ESLint configuration
- **Documentation:** Update README for new features

---

## 📄 License

This project is licensed under the Apache License 2.0 - see the [LICENSE](LICENSE) file for details.

### Third-Party Components

- **WSO2 Products:** [Apache License 2.0](https://wso2.com/licenses/apache-2.0/)
- **React:** [MIT License](https://github.com/facebook/react/blob/main/LICENSE)
- **MySQL:** [GPL 2.0](https://www.mysql.com/about/legal/)

---

## 📞 Support

- **Documentation:** This README + inline code comments
- **Script Help:** `./start.sh --help` | `./stop.sh --help`
- **WSO2 Docs:** [WSO2 API Manager](https://apim.docs.wso2.com/) | [WSO2 IS](https://is.docs.wso2.com/) | [WSO2 MI](https://mi.docs.wso2.com/)
- **Issues:** [GitHub Issues](https://github.com/nsivanoly/wso2-insurance-demo/issues)

---

<div align="center">

**Built with ❤️ for the WSO2 Community**

[⭐ Star this repo](https://github.com/nsivanoly/wso2-insurance-demo) • [🐛 Report Bug](https://github.com/nsivanoly/wso2-insurance-demo/issues) • [💡 Request Feature](https://github.com/nsivanoly/wso2-insurance-demo/issues)

</div>
