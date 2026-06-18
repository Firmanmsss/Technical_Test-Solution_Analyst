# Technical_Test-Solution_Analyst
Interview Technical Test for Livin` Mandiri as Solution Analyst

### 2. Entity Relationship Diagram (ERD)

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