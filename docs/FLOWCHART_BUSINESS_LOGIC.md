### A. Architecture Diagram
```mermaid
graph TD
    Start([User Klik Ajukan Pinjaman]) --> Input[Backend Terima Payload: user_id, nominal, tenor]
    Input --> CekNominal{Apakah Nominal <br> <= Rp 12.000.000?}
    
    CekNominal -- Tidak --> ErrNominal[Return Error 400: <br> Nominal melebihi batas maksimal]
    CekNominal -- Ya --> CekTenor{Apakah Tenor <br> <= 12 Bulan?}
    
    CekTenor -- Tidak --> ErrTenor[Return Error 400: <br> Tenor maksimal 1 tahun]
    CekTenor -- Ya --> CekHutang{Cek DB: Apakah ada pinjaman <br> berstatus 'PENDING' atau 'APPROVED'?}
    
    CekHutang -- Ya --> ErrHutang[Return Error 400: <br> Masih ada pinjaman aktif/proses]
    CekHutang -- Tidak --> SimpanDB[Simpan data ke DB <br> Status: 'PENDING']
    
    SimpanDB --> EngineProses{Engine Keputusan: <br> Scoring Otomatis}
    EngineProses -->|Ditolak| UpdateTolak[Update Status: 'REJECTED']
    EngineProses -->|Diterima| UpdateTerima[Update Status: 'APPROVED']
    
    UpdateTolak --> KirimNotifTolak[Kirim Event ke RabbitMQ: <br> Kirim Email/SMS Ditolak]
    UpdateTerima --> GenerateCicilan[Generate Otomatis 12 baris record <br> di tabel INSTALLMENTS]
    GenerateCicilan --> KirimNotifTerima[Kirim Event ke RabbitMQ: <br> Kirim Email/SMS Diterima]
    
    KirimNotifTolak --> EndTolak([Return Response 201: <br> Loan Processed - Rejected])
    KirimNotifTerima --> EndTerima([Return Response 201: <br> Loan Processed - Approved])

    %% Styling Penolak/Error
    classDef error fill:#fab1a0,stroke:#e17055,stroke-width:1px,color:#000;
    class ErrNominal,ErrTenor,ErrHutang error;