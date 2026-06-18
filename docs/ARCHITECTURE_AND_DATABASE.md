graph TD
    %% Lapisan Client
    subgraph Client_Layer [Client Layer - Mobile App]
        MobileApp["📱 Mobile App <br> (Flutter / React Native)"]
    end

    %% Lapisan Keamanan & Router
    subgraph Gateway_Layer [Gateway & Security Layer]
        APIGateway["🔒 API Gateway <br> (Reverse Proxy / Rate Limiting)"]
    end

    %% Lapisan Backend Services
    subgraph Service_Layer [Backend Core Services]
        AuthService["🔑 Authentication Service <br> (Password & Biometric Auth)"]
        UserService["👤 User Profile Service <br> (Registration & Data Diri)"]
        LoanService["💰 Loan & Billing Service <br> (Core Loan Logic)"]
        NotificationService["🔔 Notification Dispatcher <br> (Queue-based)"]
    end

    %% Lapisan Data Store
    subgraph Data_Layer [Data & Storage Layer]
        MainDB[("🗄️ Relational Database <br> PostgreSQL / SQL Server")]
        BlobStorage["☁️ Cloud Blob Storage <br> (AWS S3 / Azure Blob for KTP)"]
        MessageQueue["📥 Message Queue <br> (RabbitMQ / Redis PubSub)"]
    end

    %% Lapisan Pihak Ketiga
    subgraph Third_Party [Third-Party Services]
        SMTPServer["📧 Email SMTP Provider"]
        SMSGateway["💬 SMS/WhatsApp Gateway"]
    end

    %% Hubungan Aliran Data (Panah)
    MobileApp -->|HTTPS / REST API| APIGateway
    
    APIGateway --> AuthService
    APIGateway --> UserService
    APIGateway --> LoanService
    
    UserService -->|Upload Image| BlobStorage
    AuthService & UserService & LoanService --> MainDB
    
    LoanService -->|Trigger Notif Event| MessageQueue
    MessageQueue --> NotificationService
    
    NotificationService --> SMTPServer
    NotificationService --> SMSGateway
    
    SMTPServer -.->|Kirim Email| MobileApp
    SMSGateway -.->|Kirim SMS| MobileApp

    %% Styling Warna agar Presentatif
    style MobileApp fill:#3498db,stroke:#2980b9,stroke-width:2px,color:#fff
    style APIGateway fill:#e67e22,stroke:#d35400,stroke-width:2px,color:#fff
    style AuthService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style UserService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style LoanService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style NotificationService fill:#2ecc71,stroke:#27ae60,stroke-width:1px,color:#fff
    style MainDB fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff
    style BlobStorage fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff
    style MessageQueue fill:#9b59b6,stroke:#8e44ad,stroke-width:2px,color:#fff