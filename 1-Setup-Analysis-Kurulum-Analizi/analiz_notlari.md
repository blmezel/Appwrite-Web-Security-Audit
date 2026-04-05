# 🔍 Adım 1: Kurulum ve install.sh Analizi (Reverse Engineering)

## 🎯 GÖREV: Dosya Sistemi ve Yetki Denetimi
- **Oluşturulan Dizinler:** Script ana dizinde /appwrite klasörü açarak yapılandırma (.env) ve orkestrasyon (docker-compose.yml) dosyalarını buraya konumlandırır.
- **İstenen Yetkiler:** Kurulum süreci Docker Daemon socket'ine (/var/run/docker.sock) doğrudan erişim ister. Bir Sistem Mimarı gözüyle bu durum; script manipüle edilirse saldırganın host sistemde root yetkisi kazanması (Privilege Escalation) riskini taşır.

## 🔴 KRİTİK SORU YANITI
**Soru:** Yazılımın indirdiği kaynaklar ne kadar güvenli? Hash (imza) kontrolü yapıyor mu, yoksa körü körüne 'curl | bash' mantığıyla mı çalışıyor?

**Analiz:** Appwrite kurulum scripti incelendiğinde, dışarıdan çekilen paketler veya imajlar için yerel bir **SHA256 Checksum** doğrulaması yapılmadığı tespit edilmiştir. Sistem sadece TLS (HTTPS) güvenliğine güvenmektedir. Eğer DNS zehirlenmesi veya MITM saldırısı gerçekleşirse, kullanıcı farkında olmadan zafiyetli bir mimariyi kurabilir. "Körü körüne güven" modeli mevcuttur.
