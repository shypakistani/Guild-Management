# Guild Management Platform

[![Deployment Status](https://shields.io)](https://vercel.app)
[![Python Version](https://shields.io)](https://python.org)
[![Serialization](https://shields.io)](https://protobuf.dev)

An enterprise-grade, high-performance microservice architecture engineered for online gaming guild and clan operations. The platform leverages Google Protocol Buffers (Protobuf) for ultra-low latency, strongly-typed data serialization, structured over a serverless framework optimized for immediate global scalability via Vercel.

---

## 🎯 Core Capabilities

*   **Low-Latency Serialization:** Utilizes pre-compiled Protocol Buffers (`_pb2.py`) to bypass traditional JSON serialization overhead, minimizing payload sizes and CPU cycles.
*   **Stateful Clan Operations:** Native handling of high-throughput transactional states including join requests, membership lifecycle queries, and secure exit operations.
*   **Serverless Native Architecture:** Designed strictly around stateless functional constraints, allowing zero-cold-start scaling.

## 🏗️ Technical Architecture & Schema

The microservice processes binary-serialized network payloads mapping directly to strongly-typed internal data schemas.

### Directory Structure

```🗂️
├── app.py                 # Core application router and API gateway handler
├── vercel.json            # Infrastructure-as-Code (IaC) configuration for Vercel
├── requirements.txt       # Production package dependencies
├── ReqCLan_pb2.py         # Compiled Protobuf mapping for Clan Metadata requests
├── QuitClanReq_pb2.py     # Compiled Protobuf mapping for Member Disassociation requests
├── my_pb2.py              # Shared core infrastructure schema compilation
└── output_pb2.py          # Unified egress payload envelope definitions
```

---

## 🚀 Getting Started

### Prerequisites

*   **Runtime:** [Python 3.9+](https://python.orgdownloads/)
*   **Package Manager:** `pip` / `virtualenv`
*   **Optional Compiler:** [Protobuf Compiler (protoc)](https://grpc.io) for schema modifications.

### Local Development Environment

1. **Clone and Navigate**
   ```bash
   git clone https://github.com
   cd Guild-Management
   ```

2. **Initialize Isolated Virtual Environment**
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   # On Windows: .venv\Scripts\activate
   ```

3. **Install Dependencies**
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

4. **Boot Runtime Application**
   ```bash
   python app.py
   ```

---

## ⚙️ Protocol Buffer Compilation Workflow

Do not modify the `_pb2.py` source files manually. If modifications are required on the base `.proto` schemas, re-compile using the Protocol Compiler pipeline:

```bash
protoc --proto_path=. --python_out=. ./schemas/*.proto
```

---

## ☁️ Continuous Deployment

The repository features an automated Git-to-Deployment mapping via Vercel. Any pushes directly to the production branch are automatically built, validated, and provisioned serverless-side.

### Manual Infrastructure Provisioning
To deploy updates or spin up staging environments manually:
```bash
# Install Global CLI
npm install -g vercel

# Authenticate & Deploy
vercel --prod
```

---

## 🔒 Security & Compliance

*   **Payload Validation:** Strongly-typed schemas prevent standard injection vectors by strictly validating type and byte sizes at the network boundary.
*   **Stateless Execution:** No server-side session stickiness, guaranteeing isolation across parallel network transactions.
