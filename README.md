
# 🏥 Hospital Microservices System

A full-stack hospital management platform built using **Go**, **gRPC**, **Kafka**, **React**, and **Kubernetes**, implementing **Clean Architecture** and the **Repository Pattern**. The system supports **Role-Based Access Control (RBAC)** for various hospital departments including doctors, pharmacy, finance, ward, and admin.

---

## 📦 Project Structure

```
hospital-system/
├── api/                  # Protobuf/gRPC definitions
├── cmd/                  # Entry points for each service
├── internal/             # Business logic, handlers, repositories
├── pkg/                  # Shared libraries (middleware, logging)
├── deployments/          # Kubernetes manifests
├── scripts/              # SQL migrations and dev scripts
├── test/                 # Unit/integration tests
├── go.mod
└── README.md             # This file
```

---

## 🧩 Microservices Overview

### 1. **Auth Service**
- Handles registration, login, and JWT-based authentication.
- Supports Role-Based Access (Doctor, Admin, Ward, Finance, Pharmacy).

### 2. **User Service**
- Manages user profiles and role assignments.

### 3. **Patient Service**
- CRUD operations for patient records.

### 4. **Appointment Service**
- Handles appointment scheduling and management.
- Produces appointment events to Kafka.

### 5. **Notification Service**
- Kafka consumer to send notifications (email/SMS placeholders).

### 6. **Finance Service**
- Manages billing, invoices, payments.

### 7. **Pharmacy Service**
- Handles drug inventory and prescriptions.

### 8. **Ward Service**
- Manages inpatient records, bed allocations.

### 9. **API Gateway**
- Acts as a unified HTTP entrypoint.
- Forwards requests to gRPC services via gRPC-Gateway or direct HTTP clients.
- Handles auth middleware and logging.

---

## 🛠 Tech Stack

| Layer           | Technology                    |
|----------------|-------------------------------|
| Language        | Go                            |
| Communication   | gRPC, Protocol Buffers        |
| Messaging       | Kafka                         |
| DB              | PostgreSQL                    |
| Auth            | JWT                           |
| Gateway         | API Gateway with gRPC Proxy   |
| Frontend        | React.js                      |
| Deployment      | Kubernetes                    |
| CI/CD           | GitHub Actions (planned)      |

---

## 🗃️ Clean Architecture

```go
/internal/
  ├── handler/      // gRPC & HTTP delivery
  ├── service/      // Use cases and business logic
  ├── repository/   // Data layer abstraction
  ├── config/       // App configuration
/pkg/
  ├── middleware/   // Auth, Logging
  └── logger/       // Shared logger
```

---

## 🔐 Role-Based Access

RBAC is implemented using:
- JWT tokens with embedded roles.
- Middleware that checks allowed roles per endpoint.

### Supported Roles
- `admin`
- `doctor`
- `pharmacist`
- `finance`
- `ward_staff`

---

## 🚀 Deployment (Kubernetes)

### Requirements
- Docker
- Kubernetes (Minikube or cloud)
- Skaffold (optional)

### Steps

1. **Build Docker images** for each service:

```bash
docker build -t hospital/patient ./cmd/patient
```

2. **Apply Kubernetes manifests**:

```bash
kubectl apply -f deployments/k8s/
```

3. **Expose API Gateway** (Minikube example):

```bash
minikube service api-gateway
```

---

## 🔄 Kafka Topics

| Event Producer      | Topic         | Consumer          |
|---------------------|---------------|-------------------|
| appointment service | appointments  | notification svc  |

---

## 📂 Proto Definitions

All `.proto` files live under `/api/proto`. Example:

```proto
syntax = "proto3";

service PatientService {
  rpc GetPatient(GetPatientRequest) returns (Patient);
}
```

Use `protoc` with Go plugin to generate service code.

---

## 🧪 Testing

- Unit tests live under `/test/`
- Run tests with:

```bash
go test ./...
```

---

## 🖥️ Frontend

- Built with React and Tailwind CSS.
- Auth integrated with API Gateway.
- Role-specific dashboards for each department.

---

## 📈 Future Improvements

- CI/CD via GitHub Actions
- Monitoring (Prometheus + Grafana)
- Tracing (Jaeger)
- Redis caching layer
- Email/SMS integrations

---

## 👥 Contributors

- **Willicent Mbugua** – Lead Developer  

---

## 📃 License

[MIT License](LICENSE)
