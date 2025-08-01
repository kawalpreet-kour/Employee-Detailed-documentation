# Documentation on Employee-API

<img width="311" height="162" alt="Image" src="https://github.com/user-attachments/assets/4d1f784e-0f45-499b-86f5-47ca6e6c4940" />

---

## Author Information
| Last Updated On | Version | Author           | Level           | Reviewer               |
|-----------------|---------|------------------|-----------------|------------------------|
| 29-07-2025      | V1.0    | Kawalpreet Kour  | Internal Review | Pritam                 |
|   31-07-2025   |         | Kawalpreet Kour  | L0              | Shreya/Sharvari        |
|                 |         | Kawalpreet Kour  | L1              | Abhishek V             |
|                 |         | Kawalpreet Kour  | L2              | Abhishek Dubey/Rishabh sharma |

---

<details>
  <summary><strong> Table of Contents</strong></summary>

- [Introduction](#introduction)
- [Pre-requisites](#pre-requisites)  
- [Architecture](#architecture)  
- [Dataflow Diagram](#dataflow-diagram)  
- [Step-by-step installation](#step-by-step-installation-of-employee-api)  
- [Troubleshooting](#troubleshooting)  
- [Endpoint Information](#endpoint-information)
- [Contact Information](#contact-information)
- [References](#references)
</details>

---
## Pre-requisites

### System Requirements

| Hardware Specifications | Minimum Recommendation |
|------------------------|-----------------------|
| Processor              | Dual-core             |
| RAM                    | 4GB                   |
| Disk                   | 20GB SSD              |
| OS                     | Ubuntu 22.04 LTS      |
| Network                | Internet access       |

---

### Dependencies

#### Build time Dependency

| Name   | Version  | Description                        |
|--------|----------|------------------------------------|
| Golang | 1.21.6+  | For building and running the API   |
| jq     | Latest   | CLI JSON processor (optional)      |

#### Run time Dependency

| Name      | Version  | Description                              |
|-----------|----------|------------------------------------------|
| ScyllaDB  | 5.4+     | Main database for employee data          |
| Redis     | Latest   | Optional caching                         |
| Java      | 17       | For ScyllaDB driver/sample scripts       |
| migrate   | Latest   | DB migrations                            |

#### Other Dependency

| Name         | Version | Description                           |
|--------------|---------|---------------------------------------|
| python3-apt  | Latest  | For fixing Go install errors on Ubuntu|

---

### Important Ports

#### Inbound Traffic

| Port  | Description                        |
|-------|------------------------------------|
| 9042  | Used by ScyllaDB                   |
| 6379  | Redis default port                 |

#### Outbound Traffic

| Port  | Description                        |
|-------|------------------------------------|
| 8080  | Employee API default HTTP port     |
| 8081  | Alternative API port (if 8080 busy)|

---

### Others

| Others                | Description                            |
|-----------------------|----------------------------------------|
| Internet access       | Required for installing dependencies   |
| Private IP            | Used for DB host and API config        |

---
## Architecture

**Description:**  
The Employee API is a stateless, RESTful Golang microservice that interacts with ScyllaDB for persistent employee data storage and optionally with Redis for caching. It is deployed as a systemd service for reliability and scalability.

![WhatsApp Image 2025-08-02 at 1 02 19 AM](https://github.com/user-attachments/assets/b549a610-9d21-4278-b58b-438ebbec08c5)

---

## Dataflow Diagram

**Data Flow Steps:**

1. Client sends HTTP requests (CRUD) to API endpoints.  
2. API validates and processes logic.  
3. Interacts with ScyllaDB for data operations.  
4. Uses Redis (if enabled) for caching.  
5. Responds to client with result or error message.

---

## Step-by-step installation of Employee API

_Follow this link for full installation guide_  
(**[Click here to view installation guide](https://team-snaatak-p-15.atlassian.net/browse/SCRUM-72)**)


---

## Troubleshooting

Common issues and resolutions:

| **Issue**                             | **Possible Cause**                                      | **Suggested Solution**                                                                 |
|--------------------------------------|---------------------------------------------------------|-----------------------------------------------------------------------------------------|
| API not running                      | Port conflict                                            | Run `netstat -tuln | grep 8080` and change port in code if needed                      |
| ScyllaDB not starting                | Service error or crash                                  | Check logs using `sudo journalctl -u scylla-server` and DB status with `nodetool status` |
| Go not found / Python error          | Missing dependencies                                     | Run: `sudo apt update && sudo apt install python3-apt golang-go -y`                   |
| Redis not responding                 | Redis service not started                               | Start it: `sudo systemctl start redis-server`                                          |
| Wrong ScyllaDB host/IP               | Incorrect config in `config.yaml`                       | Edit the file and correct `scylladb.host` value                                        |
| Swagger UI not working               | Private IP not set correctly in Swagger URL             | In `main.go`, set: `url := ginSwagger.URL("http://<PRIVATE_IP>:8080/swagger/doc.json")`|

---

## Endpoint Information

| Endpoint                             | Method | Description                   |
|-------------------------------------|--------|-------------------------------|
| `/api/v1/employee/health`           | GET    | Health check endpoint         |
| `/api/v1/employee`                  | POST   | Create new employee record    |
| `/api/v1/employee/{id}`             | GET    | Fetch employee by ID          |
| `/api/v1/employee/{id}`             | PUT    | Update employee details       |
| `/api/v1/employee/{id}`             | DELETE | Delete employee record        |
| `/api/v1/employee`                  | GET    | Get all employee records      |

---

## Contact Information

| Name             | Email                                         |
|------------------|-----------------------------------------------|
| Kawalpreet Kour  | Kawalpreet.kour.snaatak@mygurukulam.co        |

---

## References

| Description                     | Link                                                                                          |
|---------------------------------|-----------------------------------------------------------------------------------------------|
| ScyllaDB Installation Guide     | [Click here](https://team-snaatak-p-15.atlassian.net/browse/SCRUM-82)                         |
| Redis Installation Guide        | [Click here](https://redis.io/docs/getting-started/installation/) 
