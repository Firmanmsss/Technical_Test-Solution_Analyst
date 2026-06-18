# Technical_Test-Solution_Analyst
Interview Technical Test for Livin` Mandiri as Solution Analyst

## 1. docs/ARCHITECTURE_AND_DATABASE
Mobile App ini saya buat dengan menerapkan arsitektur Client-Server berbasis API-First Approach dengan pemisahan fungsionalitas yang jelas antara lapisan 
Frontend Mobile, API Gateway, Backend Services, dan Third-Party Integrations. 
Keamanan data transaksi dilindungi menggunakan protokol HTTPS, enkripsi end-to-end, dan tokenisasi JWT.

### Entity Relationship Diagram (ERD)

```mermaid
erDiagram
    USERS {
        int id PK
        string nama
        string email
        string nomor_telepon
        string password_hash
        string foto_ktp_url
    }
    LOANS {
        int id PK
        int user_id FK
        decimal nominal
        int tenor_bulan
        string status
    }
    USERS ||--o{ LOANS : "mengajukan"