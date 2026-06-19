# Technical_Test-Solution_Analyst
Interview Technical Test for Livin` Mandiri as Solution Analyst

## 1. assets/ARCHITECTURE_AND_DATABASE
Mobile App ini saya buat dengan menerapkan arsitektur Client-Server berbasis API-First Approach dengan pemisahan fungsionalitas yang jelas antara lapisan 
Frontend Mobile, API Gateway, Backend Services, dan Third-Party Integrations. 
Keamanan data transaksi dilindungi menggunakan protokol HTTPS, enkripsi end-to-end, dan tokenisasi JWT.

## 2. assets/SCREEN_FLOW
Screen flow ini akan menggambarkan bagaimana memakai aplikasi, 
mulai dari membuka aplikasi (Splash Screen), proses pendaftaran, otentikasi login, hingga alur pengajuan serta pemantauan pinjaman uang.

## 3. assets/ENTITY_RELATIONSHIP_DIAGRAM
Desain database relasional ini disesuaikan dengan ekosistem untuk mencatat manajemen pengguna, 
pengajuan pinjaman, jadwal tagihan bulanan (installments), serta log notifikasi.

## 4. docs/FLOWCHART_BUSINESS_LOGIC
Sebelum backend menyimpan data pengajuan pinjaman ke database, sistem wajib melakukan  
validasi ketat untuk memastikan kepatuhan terhadap aturan bisnis (business rules).

## 5. docs/RESTful_API_SPESIFICATION
Bagian ini mendokumentasikan spesifikasi teknis API dan flowchart logika bisnis backend 
untuk menangani proses otentikasi, pengecekan dashboard, dan pengajuan pinjaman uang.

## 6. docs/SCREEN_BEHAVIOR
Dokumen ini mendefinisikan kriteria perilaku fungsional (behavior) dan aturan validasi pada  
aplikasi mobile (Frontend) untuk setiap halaman utama.