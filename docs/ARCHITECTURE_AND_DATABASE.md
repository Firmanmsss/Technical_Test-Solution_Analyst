### A. Diagram Arsitektur
```mermaid
graph TD
    subgraph Client_Layer [Client Layer - Mobile App]
        MobileApp["📱 Mobile App <br> (Flutter / React Native)"]
    end

    subgraph Gateway_Layer [Gateway & Security Layer]
        APIGateway["🔒 API Gateway <br> (Reverse Proxy / Rate Limiting)"]
    end

    subgraph Service_Layer [Backend Core Services]
        AuthService["🔑 Authentication Service <br> (Password & Biometric Auth)"]
        UserService["👤 User Profile Service <br> (Registration & Data Diri)"]
        LoanService["💰 Loan & Billing Service <br> (Core Loan Logic)"]
        NotificationService["🔔 Notification Dispatcher <br> (Queue-based)"]
    end

    subgraph Data_Layer [Data & Storage Layer]
        MainDB[("🗄️ Relational Database <br> PostgreSQL / SQL Server")]
        BlobStorage["☁️ Cloud Blob Storage <br> (AWS S3 / Azure Blob for KTP)"]
        MessageQueue["📥 Message Queue <br> (RabbitMQ / Redis PubSub)"]
    end

    subgraph Third_Party [Third-Party Services]
        SMTPServer["📧 Email SMTP Provider"]
        SMSGateway["💬 SMS/WhatsApp Gateway"]
    end

    MobileApp --> APIGateway
    
    APIGateway --> AuthService
    APIGateway --> UserService
    APIGateway --> LoanService
    
    UserService --> BlobStorage
    AuthService --> MainDB
    UserService --> MainDB
    LoanService --> MainDB
    
    LoanService --> MessageQueue
    MessageQueue --> NotificationService
    
    NotificationService --> SMTPServer
    NotificationService --> SMSGateway
    
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