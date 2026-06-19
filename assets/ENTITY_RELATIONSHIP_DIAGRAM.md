### A. Architecture Diagram
```mermaid
erDiagram
    USERS {
        int id PK
        string nama
        string email UK
        string nomor_telepon UK
        string password_hash
        string foto_profil_url
        string foto_ktp_url
        boolean is_biometric_enabled
        datetime created_at
    }

    LOANS {
        int id PK
        int user_id FK
        decimal nominal_pengajuan
        int tenor_bulan
        string status "PENDING / APPROVED / REJECTED / PAID"
        datetime tanggal_pengajuan
        datetime updated_at
    }

    INSTALLMENTS {
        int id PK
        int loan_id FK
        int cicilan_ke
        decimal nominal_tagihan
        datetime tanggal_jatuh_tempo
        string status_pembayaran "UNPAID / PAID"
        datetime tanggal_bayar
    }

    NOTIFICATION_LOGS {
        int id PK
        int user_id FK
        string tipe_notifikasi "EMAIL / SMS"
        string tujuan "Alamat Email / No Telp"
        string konten_pesan
        datetime sent_at
    }

    %% Relasi antar Tabel
    USERS ||--o{ LOANS : "mengajukan"
    USERS ||--o{ NOTIFICATION_LOGS : "menerima"
    LOANS ||--|{ INSTALLMENTS : "menghasilkan"