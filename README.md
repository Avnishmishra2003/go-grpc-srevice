# go-grpc-srevice
# Go gRPC Report Generation Service

This project is a Go-based microservice that uses **gRPC** to expose a `GenerateReport` endpoint and runs a **cron job** every 10 seconds to auto-generate reports for predefined users. All reports are stored in memory and logged with timestamps. A `HealthCheck` endpoint is also included to ensure service health.

---

## Features

- gRPC API with two endpoints:
  - GenerateReport(UserID)
  - HealthCheck()
- ⏱️ Periodic cron job to generate reports every 10 seconds.
- 🧠 In-memory report storage using a Go map.
- 📅 Logging of all operations with timestamps.
- 🔧 Built with Go Modules.
- 📦 Used libraries:
  - [`google.golang.org/grpc`](https://pkg.go.dev/google.golang.org/grpc)
  - [`github.com/robfig/cron/v3`](https://pkg.go.dev/github.com/robfig/cron/v3)

---

## How to Run

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/go-grpc-report-service.git
cd go-grpc-report-service

## Install Dependencies:
go mod tidy

## Generate Go Code from .proto .
Make sure protoc is installed. Then run:

protoc --go_out=. --go-grpc_out=. proto/report.proto
/// Note: The .proto file has a go_package option set correctly.

*** Run the Server ***

go run main.go
You should see logs showing that the server is running and cron jobs are generating reports every 10 seconds.

*** Testing the gRPC Service ***
We tested all endpoints using CMD and the command-line tool grpcurl.

*** Health Check ***

grpcurl -plaintext localhost:50051 report.ReportService/HealthCheck
 Expected Output:
{
  "status": "SERVING"
}
