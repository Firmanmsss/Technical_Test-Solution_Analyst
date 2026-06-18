### A. Diagram Arsitektur
```mermaid
---
config:
  layout: fixed
---
flowchart TB
 subgraph Client_Layer["Client Layer - Mobile App"]
        MobileApp["📱 Mobile App <br> (Flutter / React Native)"]
  end
 subgraph Gateway_Layer["Gateway & Security Layer"]
        APIGateway["🔒 API Gateway <br> (Reverse Proxy / Rate Limiting)"]
  end
 subgraph Service_Layer["Backend Core Services"]
        AuthService["🔑 Authentication Service <br> (Password &amp; Biometric Auth)"]
        UserService["👤 User Profile Service <br> (Registration &amp; Data Diri)"]
        LoanService["💰 Loan &amp; Billing Service <br> (Core Loan Logic)"]
        NotificationService["🔔 Notification Dispatcher <br> (Queue-based)"]
  end
 subgraph Data_Layer["Data &amp; Storage Layer"]
        MainDB[("🗄️ Relational Database <br> PostgreSQL / SQL Server")]
        BlobStorage["☁️ Cloud Blob Storage <br> (AWS S3 / Azure Blob for KTP)"]
        MessageQueue["📥 Message Queue <br> (RabbitMQ / Redis PubSub)"]
  end
 subgraph Third_Party["Third-Party Services"]
        SMTPServer["📧 Email SMTP Provider"]
        SMSGateway["💬 SMS/WhatsApp Gateway"]
  end
    MobileApp --> APIGateway
    APIGateway --> AuthService & UserService & LoanService
    UserService --> MainDB & BlobStorage
    AuthService --> MainDB
    LoanService --> MainDB & MessageQueue
    MessageQueue --> NotificationService
    NotificationService --> SMTPServer & SMSGateway
    SMTPServer -.-> MobileApp
    SMSGateway -.-> MobileApp

    style MobileApp fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style APIGateway fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff
    style AuthService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style UserService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style LoanService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style NotificationService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style MainDB fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff
    style BlobStorage fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff
    style MessageQueue fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff