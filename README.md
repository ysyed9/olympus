# Olympus - AI-Powered Infrastructure Management Platform

**Olympus** is a full-stack infrastructure orchestration and monitoring platform that combines AI-driven insights, automated infrastructure provisioning, and intelligent ticketing systems. Built with modern web technologies, it provides a comprehensive solution for managing AWS cloud resources, monitoring system health, and automating incident response.

## 🎯 Project Overview

Olympus integrates a multi-layer orchestration path for cloud infrastructure operations (Terraform) mediated by an NVIDIA-routed Model Context Protocol (MCP) client. The platform enables teams to:

- **Provision AWS Infrastructure** (S3, EC2, Lambda) via Terraform with natural language commands
- **Monitor Resources** in real-time with CloudWatch metrics integration and AI-powered analysis
- **Automate Incident Response** with intelligent ticket creation and employee assignment
- **Chat with AI** using real-time WebSocket communication for infrastructure queries
- **Manage Resources** through a modern React-based dashboard with Firebase authentication

### Who Is This For?

This project demonstrates skills in:
- **Full-Stack Development**: React, Flask, Node.js
- **Cloud Infrastructure**: AWS (EC2, S3, Lambda, CloudWatch, DynamoDB)
- **Infrastructure as Code**: Terraform
- **AI/ML Integration**: NVIDIA LLM APIs, natural language processing
- **DevOps Practices**: Docker, CI/CD patterns, environment management
- **Real-time Communication**: WebSockets
- **Database Design**: DynamoDB, JSON-based data management

---

## ✨ Key Features

### 1. Infrastructure Orchestration
- **Terraform Integration**: Create and destroy AWS resources (S3 buckets, EC2 instances, Lambda functions) via REST API
- **Natural Language Interface**: Use conversational AI to issue infrastructure commands
- **MCP (Model Context Protocol)**: Advanced protocol for AI-tool interactions
- **Persistent Mode**: Long-lived Docker containers for faster operations

### 2. Monitoring & Observability
- **CloudWatch Integration**: Real-time metrics fetching (CPU, memory, disk, network)
- **Log Analysis**: AI-powered log parsing and pattern detection
- **Resource Health Scoring**: Automated health metrics with color-coded status
- **Customer Health Dashboards**: Aggregate health metrics across customer accounts

### 3. AI-Powered Ticketing System
- **Automatic Ticket Creation**: Generate tickets from metrics anomalies and log errors
- **Intelligent Assignment**: Multi-factor scoring algorithm (skills match, experience, workload, specialization)
- **Admin Approval Workflow**: Critical tickets require admin approval before assignment
- **AI Analysis**: LLM-powered issue detection and recommendation generation

### 4. Real-time AI Chat
- **WebSocket Communication**: Real-time bidirectional messaging
- **Natural Language Queries**: Ask questions about infrastructure, metrics, or system status
- **Context-Aware Responses**: AI understands infrastructure context and provides relevant answers

### 5. Resource Management
- **DynamoDB Integration**: Scalable resource storage and retrieval
- **Filtering & Search**: Query resources by customer, type, batch group, or status
- **Metrics Snapshot**: Capture resource state at ticket creation time
- **Cost Estimation**: Track estimated monthly costs per resource

---

## 🛠 Technology Stack

### Frontend
- **React 19** with functional components and hooks
- **Vite** for fast development and optimized builds
- **Tailwind CSS 4** for modern styling
- **Framer Motion** for smooth animations
- **PrimeReact** for UI components
- **React Router** for client-side routing
- **Firebase Authentication** for secure user management
- **Chart.js** for data visualization
- **WebSocket API** for real-time communication

### Backend
- **Flask 3.0** (Python) - REST API for monitoring, metrics, and tickets
- **Node.js** - MCP client server with WebSocket support
- **Express.js** - HTTP server for Node MCP client
- **AWS SDK (boto3/botocore)** - CloudWatch, EC2, S3, Lambda, DynamoDB integration
- **OpenAI SDK** - NVIDIA API integration for LLM operations

### Infrastructure & DevOps
- **Terraform** - Infrastructure as Code for AWS resources
- **Docker** - Containerized Terraform MCP server
- **AWS Services**:
  - EC2 (compute instances)
  - S3 (object storage)
  - Lambda (serverless functions)
  - CloudWatch (monitoring & metrics)
  - DynamoDB (NoSQL database)

### AI/ML
- **NVIDIA Nemotron LLM** - Natural language processing and analysis
- **Model Context Protocol (MCP)** - Standardized AI-tool interaction protocol

### Development Tools
- **Concurrently** - Run multiple services in parallel
- **ESLint** - Code quality and linting
- **Python-dotenv** - Environment variable management
- **CORS** - Cross-origin resource sharing

---

## 🏗 Architecture Overview

### System Flow

```
┌─────────────────┐
│   React Frontend │ (Port 5173)
│   (Vite Dev)     │
└────────┬────────┘
         │ HTTP/WebSocket
         ▼
┌─────────────────────┐
│  Node MCP Server    │ (Port 8080) - Primary Backend
│  - WebSocket Chat   │
│  - Terraform Proxy  │
│  - NLP Router       │
│  - Monitoring Proxy │
└─────┬───────────┬───┘
      │           │
      │           ├─────────────┐
      │           │             │
      ▼           ▼             ▼
┌──────────┐ ┌─────────┐ ┌─────────────┐
│ Terraform│ │  Flask  │ │   NVIDIA    │
│ MCP      │ │ Backend │ │     LLM     │
│ (Docker) │ │ (5000)  │ │    API      │
└──────────┘ └────┬────┘ └─────────────┘
                  │
                  ▼
          ┌───────────────┐
          │  AWS Services │
          │  - CloudWatch │
          │  - DynamoDB   │
          │  - EC2/S3/λ   │
          └───────────────┘
```

### Component Responsibilities

| Component | Port | Responsibility |
|-----------|------|----------------|
| **React Frontend** | 5173 | User interface, authentication, real-time chat |
| **Node MCP Server** | 8080 | Primary backend, WebSocket server, Terraform/Flask proxy, NLP routing |
| **Flask Backend** | 5000 | Monitoring endpoints, metrics analysis, ticket system, AI integration |
| **Terraform MCP** | (Docker) | Infrastructure provisioning via Terraform tools |
| **DynamoDB** | (AWS) | Resource and metrics storage |

---

## 📋 Prerequisites

Before setting up the project, ensure you have the following installed:

- **Node.js** (v18 or higher) and npm
- **Python 3.8+** and pip3
- **Docker** (for Terraform MCP server)
- **AWS Account** with credentials configured (optional, for live AWS operations)
- **NVIDIA API Key** (for LLM features)
- **Firebase Project** (optional, for authentication)

---

## 🚀 Installation & Setup

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd haze
```

### Step 2: Install Dependencies

Install all project dependencies (Python, Node.js, and frontend):

```bash
npm run install:all
```

This command installs:
- Root Node.js dependencies
- MCP client dependencies (`mcp-client/`)
- Frontend dependencies (`Frontend/`)
- Python dependencies (`requirements.txt`)

**Manual installation (alternative):**

```bash
# Install Python dependencies
pip3 install -r requirements.txt

# Install root Node dependencies
npm install

# Install MCP client dependencies
cd mcp-client && npm install && cd ..

# Install frontend dependencies
cd Frontend && npm install && cd ..
```

### Step 3: Configure Environment Variables

Create a `.env` file in the project root:

```bash
cp .env.example .env  # If .env.example exists
# Or create .env manually
```

**Minimum required variables:**

```env
# NVIDIA API Key (required for AI features)
MODEL_API_KEY=your-nvidia-api-key-here

# Service URLs
FLASK_URL=http://localhost:5000
FRONTEND_ORIGIN=http://localhost:5173
VITE_FLASK_URL=http://localhost:5000
VITE_NODE_WS_URL=ws://localhost:8080

# Terraform settings
PERSIST_TERRAFORM=1
FLASK_PORT=5000
```

**AWS Configuration (optional, for live AWS operations):**

```env
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
AWS_DEFAULT_REGION=us-east-1
```

**Firebase Configuration (optional, for authentication):**

```env
VITE_FIREBASE_API_KEY=your-api-key
VITE_FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your-project-id
VITE_FIREBASE_STORAGE_BUCKET=your-bucket.appspot.com
VITE_FIREBASE_MESSAGING_SENDER_ID=your-sender-id
VITE_FIREBASE_APP_ID=your-app-id
```

**Sync environment variables:**

After creating `.env`, sync variables to subdirectories:

```bash
npm run sync-env
```

This script:
- Copies `.env` to `mcp-client/.env`
- Extracts `VITE_*` variables to `Frontend/.env.local`

### Step 4: Build Terraform MCP Docker Image

Build the Docker image for the Terraform MCP server:

```bash
docker build -t mcps-terraform ./mcps
```

### Step 5: Verify Setup

Run the setup verification script:

```bash
npm run setup
```

This command:
1. Installs all dependencies
2. Syncs environment variables
3. Runs test suite (Python imports, Flask routes, frontend lint, Node CORS)

---

## 🏃 Running the Project

### Quick Start (All Services)

Start all services with a single command:

```bash
npm run dev
```

This uses `concurrently` to start:
- **Flask backend** (port 5000) - Blue output
- **Node MCP server** (port 8080) - Green output
- **Frontend** (port 5173) - Magenta output

The frontend will automatically open in your browser at `http://localhost:5173`.

**Alternative (using Makefile):**

```bash
make dev
```

### Manual Startup (Individual Services)

If you prefer to run services individually:

**1. Start Node MCP Server (Primary Backend):**

```bash
cd mcp-client
node server.js
```

**2. Start Flask Backend:**

```bash
python3 app.py
```

**3. Start Frontend:**

```bash
cd Frontend
npm run dev
```

### Using Development Scripts

**Start development environment:**
```bash
bash scripts/dev.sh
```

**Stop all services:**
```bash
npm run kill-ports
# or
bash scripts/stop.sh
```

**Check service status:**
```bash
make status
```

---

## 📁 Project Structure

```
haze/
├── Frontend/                    # React frontend application
│   ├── src/
│   │   ├── components/         # Reusable React components
│   │   │   ├── ChatBot.jsx    # AI chat interface
│   │   │   ├── MenuBar.jsx    # Navigation menu
│   │   │   └── ...
│   │   ├── pages/              # Page components
│   │   │   ├── Home.jsx
│   │   │   ├── Resources/     # Resource management
│   │   │   ├── Tickets/       # Ticketing system
│   │   │   └── LogsView/      # Log viewer
│   │   ├── hooks/              # Custom React hooks
│   │   ├── contexts/           # React contexts (auth)
│   │   └── lib/                # Utility libraries
│   └── package.json
│
├── mcp-client/                  # Node.js MCP client server
│   ├── server.js               # Main server (WebSocket, HTTP)
│   ├── model/
│   │   └── router.js           # NLP routing logic
│   ├── tools/                  # MCP tool implementations
│   └── package.json
│
├── mcp/                         # Python MCP modules
│   ├── monitor/                # Monitoring & ticketing
│   │   ├── routes.py           # Flask routes
│   │   ├── cloudwatch_client.py
│   │   ├── dynamodb_client.py
│   │   ├── ticket_system.py
│   │   └── metrics_updater.py
│   ├── infra/                  # Infrastructure routes
│   │   └── routes.py
│   └── Nvidia_llm/             # AI client
│       └── AI_client.py
│
├── mcps/                        # Terraform MCP server (Docker)
│   ├── mcp_server.py           # MCP server implementation
│   ├── Dockerfile
│   └── terraform/              # Terraform configurations
│       ├── s3/
│       ├── ec2/
│       └── lambda/
│
├── app.py                       # Flask application entry point
├── requirements.txt             # Python dependencies
├── package.json                 # Root package.json (scripts)
├── .env                         # Environment variables (create this)
└── README.md                    # This file
```

---

## 🔌 API Documentation

### Flask Backend (`/monitor` endpoints)

#### Metrics Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/monitor/metrics?instance_id=<id>` | Get CloudWatch metrics for EC2 instance |
| GET | `/monitor/metrics/enriched?instance_id=<id>` | Get enriched metrics with auto-update |
| POST | `/monitor/metrics/update?instance_id=<id>` | Update resource metrics in DynamoDB |
| GET | `/monitor/mock/metrics` | Get all mock resources |
| GET | `/monitor/mock/metrics/<resource_id>` | Get specific resource with AI analysis |

#### Logs Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/monitor/mock/logs?resource_id=<id>&status=<status>` | Get filtered logs |
| GET | `/monitor/mock/logs/analysis?resource_id=<id>` | Get AI analysis of logs |
| GET | `/monitor/mock/resource/<id>/combined` | Combined metrics + logs analysis |

#### Ticket Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/monitor/tickets` | Get all tickets (with filters) |
| GET | `/monitor/tickets/pending` | Get pending CRITICAL tickets |
| GET | `/monitor/tickets/<id>` | Get specific ticket |
| POST | `/monitor/tickets` | Create new ticket |
| POST | `/monitor/tickets/<id>/approve` | Approve CRITICAL ticket |
| POST | `/monitor/tickets/<id>/reject` | Reject CRITICAL ticket |
| POST | `/monitor/tickets/<id>/resolve` | Resolve ticket |
| POST | `/monitor/logs/create-tickets` | Create tickets from error logs |
| POST | `/monitor/metrics/create-tickets` | Create tickets from metrics anomalies |
| POST | `/monitor/metrics/analyze-and-create-tickets` | AI analysis + auto-create tickets |

#### Resource Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/monitor/resources?customer_name=<name>&type=<type>` | List resources with filters |
| POST | `/monitor/resources` | Create new resource |
| GET | `/monitor/resources/<id>` | Get specific resource |
| PUT | `/monitor/resources/<id>` | Update resource |
| DELETE | `/monitor/resources/<id>` | Delete resource |

### Infrastructure Endpoints (`/infra`)

| Method | Endpoint | Description | Body |
|--------|----------|-------------|------|
| GET | `/infra/ping` | Ping Terraform MCP server | - |
| POST | `/infra/s3` | Create S3 bucket | `{"bucket_name": "...", "aws_region": "..."}` |
| DELETE | `/infra/s3/<bucket>` | Destroy S3 bucket | - |
| POST | `/infra/ec2` | Create EC2 instance | `{...}` |
| DELETE | `/infra/ec2` | Destroy EC2 instance | - |
| POST | `/infra/lambda` | Create Lambda function | `{"function_name": "...", "source_code": "..."}` |
| DELETE | `/infra/lambda` | Destroy Lambda function | - |

### Node MCP Server (`/terraform/*`, `/nlp`, WebSocket)

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/terraform/ping` | GET | Ping Terraform MCP |
| `/terraform/tools` | GET | List available MCP tools |
| `/terraform/s3` | POST/DELETE | S3 bucket operations |
| `/terraform/ec2` | POST/DELETE | EC2 instance operations |
| `/terraform/lambda` | POST/DELETE | Lambda function operations |
| `/nlp` | POST | Natural language → tool execution |
| `ws://localhost:8080` | WebSocket | Real-time AI chat |

---

## ⚙️ Environment Variables Reference

| Variable | Purpose | Default | Required |
|----------|---------|---------|----------|
| `MODEL_API_KEY` | NVIDIA API key for LLM | - | Yes |
| `FLASK_PORT` | Flask server port | 5000 | No |
| `FLASK_URL` | Flask server URL | http://localhost:5000 | No |
| `FRONTEND_ORIGIN` | Frontend CORS origin | http://localhost:5173 | No |
| `NODE_MCP_URL` | Node MCP server URL | http://localhost:8080 | No |
| `VITE_NODE_WS_URL` | WebSocket URL for frontend | ws://localhost:8080 | No |
| `VITE_FLASK_URL` | Flask URL for frontend | http://localhost:5000 | No |
| `PERSIST_TERRAFORM` | Keep Docker container alive | 0 | No |
| `INFRA_CLIENT_TIMEOUT` | Terraform operation timeout (seconds) | 300 | No |
| `AWS_ACCESS_KEY_ID` | AWS access key | - | No* |
| `AWS_SECRET_ACCESS_KEY` | AWS secret key | - | No* |
| `AWS_DEFAULT_REGION` | AWS region | us-east-1 | No* |

*Required for live AWS operations

---

## 🔧 Troubleshooting

### Common Issues

| Issue | Cause | Solution |
|-------|-------|----------|
| **Frontend can't connect** | CORS or wrong origin | Set `FRONTEND_ORIGIN` in `.env` to match dev URL |
| **WebSocket fails** | Wrong `VITE_NODE_WS_URL` | Update `.env`, run `npm run sync-env`, restart frontend |
| **NVIDIA API errors** | Missing/invalid `MODEL_API_KEY` | Add valid key to `.env` |
| **Terraform timeouts** | Docker container not running | Build image: `docker build -t mcps-terraform ./mcps` |
| **Port already in use** | Previous process still running | Run `npm run kill-ports` or `bash scripts/stop.sh` |
| **Import errors** | Missing dependencies | Run `npm run install:all` and `pip3 install -r requirements.txt` |
| **DynamoDB errors** | Table not created | Run migration script or use JSON files for mock data |

### Debugging Steps

1. **Check service status:**
   ```bash
   make status
   # or
   lsof -nPiTCP -sTCP:LISTEN | grep -E "(5000|8080|5173)"
   ```

2. **Verify environment variables:**
   ```bash
   # Check if .env exists
   ls -la .env
   
   # Verify sync
   npm run sync-env
   ```

3. **Test individual services:**
   ```bash
   # Test Flask
   curl http://localhost:5000/monitor/mock/logs
   
   # Test Node MCP
   curl http://localhost:8080/health
   
   # Test frontend
   curl http://localhost:5173
   ```

4. **View logs:**
   - Flask: Check terminal output (blue)
   - Node MCP: Check terminal output (green)
   - Frontend: Check browser console and terminal (magenta)

---

## 🚀 Future Enhancements

### Planned Features

- [ ] **Structured JSON outputs** from Terraform (instead of raw text)
- [ ] **Authentication/Authorization** around `/infra` endpoints
- [ ] **Queued async job execution** for long-running Terraform operations
- [ ] **Observability**: Log each infra action to datastore with request + duration + result
- [ ] **Remote Terraform Backend**: S3 + DynamoDB for state management
- [ ] **Enhanced AI Analysis**: Multi-model support for better accuracy
- [ ] **Real-time Notifications**: WebSocket-based alerts for critical issues
- [ ] **Resource Tagging**: Advanced tagging and filtering capabilities
- [ ] **Cost Optimization**: AI-powered cost recommendations
- [ ] **Integration Tests**: Automated testing for full stack

### Architecture Improvements

- [ ] **Docker Compose**: Orchestrate all services in containers
- [ ] **Kubernetes Deployment**: Production-ready container orchestration
- [ ] **CI/CD Pipeline**: Automated testing and deployment
- [ ] **Monitoring Dashboard**: Prometheus + Grafana integration
- [ ] **API Rate Limiting**: Protect against abuse
- [ ] **Caching Layer**: Redis for frequently accessed data

---

## 📚 Additional Documentation

- [DEPLOYMENT.md](./DEPLOYMENT.md) - Detailed deployment and environment guide
- [TICKETING_INTEGRATION_SUMMARY.md](./TICKETING_INTEGRATION_SUMMARY.md) - Ticketing system integration details
- [Frontend/WEBSOCKET_INTEGRATION.md](./Frontend/WEBSOCKET_INTEGRATION.md) - WebSocket implementation guide

---

## 🧪 Testing

### Run All Tests

```bash
npm run test:stack
```

This runs:
- Python import validation
- Flask route tests
- Frontend linting
- Node CORS tests

### Individual Test Commands

```bash
# Python tests
npm run test:python:imports
npm run test:python:flask

# Frontend tests
npm run test:frontend

# Node tests
npm run test:node-cors
```

---

## 📝 License

ISC License (see [LICENSE](./LICENSE) file)

---

## 👤 Author

Built as a demonstration of full-stack development, cloud infrastructure management, and AI integration capabilities.

---

## 🤝 Contributing

This is a portfolio project. For questions or feedback, please open an issue or contact the repository maintainer.

---

**Built with ❤️ using React, Flask, Node.js, Terraform, and AWS**
