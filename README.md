# FinPay Accelerated Backend L&D Workspace: Phase 1 & 2

Welcome to the FinPay 2-Week Accelerated Backend Engineering training repository. This workspace is explicitly configured for engineers transitioning from Python to the Java enterprise ecosystem. Over this 14-hour training track, you will transform dynamic data processing patterns into high-precision, statically typed microservices.

---

## 🎯 Core Training Objectives

By the completion of this curriculum, you will be able to:
* **Navigate Maven Lifecycles:** Master the structural transition from `pip` and `venv` environments to declarative XML dependency resolution engines (`pom.xml`).
* **Handle Statically-Typed Collections:** Map dynamic structures safely into thread-safe memory matrix structures like `ConcurrentHashMap` and data classes.
* **Implement Spring MVC Architecture:** Trace data pipelines through a structural request layout using the `DispatcherServlet`, explicit controller layers, and business logic services.
* **Abstract Database Persistence:** Model BSON transactional schemas using Spring Data MongoDB Object-Document Mapping interfaces.
* **Decouple and Orchestrate Distributed Services:** Split monolithic runtime blocks into two isolated microservices communicating synchronously via reactive `WebClient` nodes.

---

## 💻 Local Machine Pre-requisites

Ensure your system environment matches these target engineering tool dependencies before running compilation commands:

* **Java Development Kit (JDK):** Version 17 LTS (Eclipse Temurin preferred).
* **Build Automation Tool:** Apache Maven 3.8+.
* **Containerization Engine:** Docker Desktop or Docker Engine daemon.
* **Network Query Testing Client:** Native terminal `curl` or Postman.

# Environment Prerequisites & Component Installation Guide

Before compiling or running the microservices, your local workstation must have a compatible Java Runtime, the Apache Maven build engine, and a Docker container daemon installed.

---

## 🛠️ Required Component Stack

* **Java Development Kit (JDK):** Version 17 LTS (Eclipse Temurin build distribution).
* **Build Automation Tool:** Apache Maven (Version 3.x).
* **Containerization Engine:** Docker Desktop or Docker Engine daemon.
* **Network Command Utility:** Terminal-based `curl` or Postman for REST API verification.

---

## 📥 Explicit Installation Instructions

Select the execution path below that matches your local workstation operating system:

### 🍏 macOS Installation (Using Homebrew)

Open your terminal app and execute the following commands sequence:

1. **Install Eclipse Temurin OpenJDK 17:**
   ```bash
   brew install --cask temurin@17
   ```

2. **Install Apache Maven Build Tool:**
   ```bash
   brew install maven
   ```

3. **Install Docker Desktop:**
   Download the visual desktop setup app matching your hardware processor type (Apple Silicon or Intel) directly from the [Official Docker Desktop for Mac Portal](https://www.docker.com/products/docker-desktop/).

---

### 🪟 Windows Installation (Using Winget Windows Package Manager)

Open your Command Prompt (`cmd`) or PowerShell terminal running with Administrator privileges:

1. **Install Eclipse Temurin OpenJDK 17:**
   ```cmd
   winget install Eclipse.Temurin.17.JDK
   ```

2. **Install Apache Maven Build Tool:**
   ```cmd
   winget install Apache.Maven
   ```

3. **Install Docker Desktop:**
   ```cmd
   winget install Docker.DockerDesktop
   ```
   *Note:* Ensure you restart your machine after installing Docker Desktop to let the WSL2 (Windows Subsystem for Linux) backend integrations bind correctly.

---

### 🐧 Linux Installation (Using Debian/Ubuntu APT Package Manager)

Open your shell window and execute the following administration commands:

1. **Install OpenJDK 17 Kit:**
   ```bash
   sudo apt-get update && sudo apt-get install -y openjdk-17-jdk
   ```

2. **Install Apache Maven Build Tool:**
   ```bash
   sudo apt-get install -y maven
   ```

3. **Install Docker Engine and Compose Plugin:**
   ```bash
   sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-compose-plugin
   ```

---

## 🔍 Local Tooling Verification Loop

To guarantee that paths, environmental runtime properties, and binaries are registered on your shell session context profile, open a brand-new terminal window and type the verification checks below:

1. **Verify Java Runtime Environment Engine (JRE):**
   ```bash
   java -version
   ```
   *Expected Console Confirmation:* `openjdk version "17.x.x"`

2. **Verify Maven Build Environment Tooling:**
   ```bash
   mvn -version
   ```
   *Expected Console Confirmation:* `Apache Maven 3.x.x`

3. **Verify Local Docker Operational Daemon Health:**
   ```bash
   docker --version && docker compose version
   ```
   *Expected Console Confirmation:* Prints active system application container version tags.

---

## 🚀 Environment Local Setup

### 1. Initialize Infrastructure Container
Spin up your local detached MongoDB instance from the repository root:
```bash
docker compose up -d
```
*Verification:* Run `docker ps` to verify that container `local-mongo` is healthy and listening on port `27017`.

### 2. Compile and Package Workspace Modules
Execute a full lifecycle compilation scan across the entire multi-module codebase layout from the root workspace directory:
```bash
mvn clean package
```

### 3. Run Microservices Concurrently
Open two separate terminal windows to boot both isolated nodes simultaneously:

* **Terminal 1 (Wallet Microservice Node):**
  ```bash
  cd wallet-service
  mvn spring-boot:run
  ```
  *Listens on HTTP Interface:* `http://localhost:8081`

* **Terminal 2 (Ledger Microservice Node):**
  ```bash
  cd ledger-service
  mvn spring-boot:run
  ```
  *Listens on HTTP Interface:* `http://localhost:8082`

---

## 🧪 Functional Verification Verification Loop

Once both service nodes are up, run this terminal test pipeline using `curl` commands to confirm distributed system health:

### 1. Seed Sandbox Account Entities
```bash
curl -X POST "http://localhost:8081/api/v1/wallets/create?walletId=ACC-101&initialDeposit=1500.00"
curl -X POST "http://localhost:8081/api/v1/wallets/create?walletId=ACC-202&initialDeposit=500.00"
```

### 2. Fire Inter-Service Transfer Request
Instruct the Wallet Service on Port 8081 to process an asset deduction, which triggers an out-of-band WebClient REST logging operation to the Ledger Service on Port 8082:
```bash
curl -X POST "http://localhost:8081/api/v1/wallets/transfer" \
     -H "Content-Type: application/json" \
     -d '{"sourceWalletId":"ACC-101","destinationWalletId":"ACC-202","transferAmount":250.00}'
```

### 3. Audit Local MongoDB Record Isolation
Query your isolated database container records directly to verify that the Ledger Service persisted the immutable transactional trail document successfully:
```bash
docker exec -it local-mongo mongosh --eval "db.getSiblingDB('finpay_ledger').audit_ledger.find().pretty()"
```
```
```

---

## 4. Git Repository Scaffolding Automation

finpay-backend-workspace/
├── .gitignore
├── docker-compose.yml
├── pom.xml (Root Parent POM)
├── README.md
├── wallet-service/
│   ├── pom.xml (Module POM)
│   └── src/
│       └── main/
│           ├── java/com/finpay/wallet/
│           │   ├── WalletApplicationLauncher.java
│           │   ├── config/
│           │   ├── controller/
│           │   ├── dto/
│           │   └── service/
│           └── resources/
│               └── application.properties
└── ledger-service/
    ├── pom.xml (Module POM)
    └── src/
        └── main/
            ├── java/com/finpay/ledger/
            │   ├── LedgerApplicationLauncher.java
            │   ├── controller/
            │   ├── domain/
            │   └── repository/
            └── resources/
                └── application.properties

To transform these structures into a tracking history without capturing build artifacts or transient local storage caches, copy and paste this complete script sequence into your terminal inside the root `finpay-backend-workspace/` folder:


```bash
# Initializing Git Tracking Mechanics
git init

# Writing Core Exclusion Matrices (.gitignore)
cat << 'EOF' > .gitignore
# Compilation Target Spaces
target/
*.jar
*.war
*.class

# JetBrains and Eclipse IDE Core Metadata Caches
.idea/
*.iml
.classpath
.project
.settings/
.DS_Store

# Local Volatile Log Vectors
*.log
EOF

# Capturing Initial Blueprint Baseline Commit
git add .
git commit -m "chore: scaffold multi-module maven structure, docker engine configs, and setup documentation"
```

The Git repository setup is complete. Your engineering team can now pull this down, boot the core MongoDB container structure, and begin day-to-day module implementation tasks. Let me know if you would like me to generate the parent or child `pom.xml` configuration structures next!