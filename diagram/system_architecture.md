# 📊 E-Pasaport Güvenlik Sistemi Mimari Akış Şeması

Bu şema, pasaport verilerine erişim sırasında uygulanan **"Zabıta ve Polis"** (Rate Limiting & Auth) hiyerarşisini ve veri izolasyonunu teknik olarak özetler.

```mermaid
graph TD
    %% Aktörler
    User[🌐 İstemci / Memur] -- "POST /v1/account" --> Zabita{🛡️ Zabıta Katmanı}
    
    %% Zabıta (Rate Limit) Denetimi
    Zabita -- "Spam / DDoS Tespit" --> Deny1[❌ 429 Too Many Requests]
    Zabita -- "Temiz Trafik" --> Polis{👮 Polis Katmanı}
    
    %% Polis (Authentication) Denetimi
    Polis -- "Hatalı JWT / Yetkisiz" --> Deny2[❌ 401/403 Unauthorized]
    Polis -- "Doğrulanmış Kimlik" --> Backend[⚙️ Appwrite Backend]
    
    %% Backend İşlemleri
    Backend -- "Geçici İmzalı Bağlantı" --> Storage[📁 Storage / Presigned-URL]
    Backend -- "İzole Sorgu" --> DB[(🐋 Internal DB - MariaDB)]
    
    %% Veri Teslimi
    Storage -- "Yetki Kontrolü" --> Result[✅ Güvenli Pasaport Belgesi]
    
    %% Stil Tanımları
    style User fill:#1f2833,stroke:#ff3366,stroke-width:2px,color:#fff
    style Zabita fill:#1f2833,stroke:#f59e0b,stroke-width:2px,color:#fff
    style Polis fill:#1f2833,stroke:#ef4444,stroke-width:2px,color:#fff
    style DB fill:#151b22,stroke:#10b981,stroke-width:2px,color:#fff
    style Result fill:#10b981,stroke:#fff,stroke-width:2px,color:#000
```

### 🔍 Şema Açıklaması:
1.  **Zabıta (Edge Security):** Henüz sunucu yorulmadan, saniyedeki istek sayısını denetleyerek Brute-force saldırılarını engeller.
2.  **Polis (Identity Management):** Sadece meşru kullanıcının JWT imzasını ve pasaportu görme yetkisini (ACL) kontrol eder.
3.  **İzolasyon:** Veritabanı dış dünyaya kapalıdır, sadece Backend üzerinden erişilebilir.
