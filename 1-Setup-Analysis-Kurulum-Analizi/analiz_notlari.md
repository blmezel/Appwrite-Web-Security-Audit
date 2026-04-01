# Step 1: Setup Script Security Audit

## 🔍 Analiz Bulguları
- **Bütünlük Kontrolü:** "curl | php" metodu kullanılıyor. İndirilen bileşenler için yerel bir SHA256 checksum doğrulaması yok (Risk: MITM).
- **Yetki Analizi:** Kurulum /var/run/docker.sock erişimi istiyor. Bu, konteynerden ana makineye sızma (escape) riski taşır.
- **Secrets:** Master Key üretimi için sistem rastgeleliği kullanılıyor ancak statik dosyalarda saklanıyor.
