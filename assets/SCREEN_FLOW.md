### A. Architecture Diagram
```mermaid
graph TD
    %% Definisi Nodes/Halaman
    Splash["🎬 Splash Screen"]
    Login["🔑 Login Screen <br>(Password / Biometric Auth)"]
    Register["📝 Register Screen <br>(Data Diri, Email, No Telp)"]
    KTPUpload["📸 Upload KTP & Foto Screen"]
    Dashboard["🏠 Dashboard Utama <br>(Sisa Hutang & Tagihan Bulanan)"]
    LoanForm["💰 Form Pengajuan Pinjaman <br>(Max 12jt, Max Tenor 1 Thn)"]
    LoanStatus["⏳ Status Proses Peminjaman <br>(Menunggu Persetujuan)"]
    
    %% Alur Navigasi
    Splash --> Login
    Login -->|Belum Punya Akun| Register
    Register --> KTPUpload
    KTPUpload -->|Registrasi Selesai| Login
    
    Login -->|Otentikasi Sukses| Dashboard
    
    Dashboard -->|Klik Ajukan Pinjaman| LoanForm
    LoanForm -->|Submit Data Pinjaman| LoanStatus
    LoanStatus -->|Kembali ke Dashboard / Polling State| Dashboard

    %% Aturan Logika Percabangan (State Check)
    classDef rule fill:#f1c40f,stroke:#f39c12,stroke-width:1px,color:#000;
    style Splash fill:#34495e,stroke:#2c3e50,color:#fff
    style Dashboard fill:#2ecc71,stroke:#27ae60,color:#fff