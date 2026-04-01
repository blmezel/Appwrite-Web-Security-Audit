# Adım 1: Kurulum ve install.sh Güvenlik Analizi (Static Analysis)

## 🎯 Analiz Amacı
Appwrite kurulum scriptinin sisteme giriş metodolojisini inceleyerek, olası bir manipülasyonda sistemde yaratabileceği "Yetki Yükseltme" ve "Bütünlük Bozulması" risklerini tespit etmek.

## 🛠️ Teknik Bulgular
1. **Bütünlük (Integrity) Kontrolü Eksikliği:** Kurulum "curl | bash" yöntemiyle yapılıyor. İndirilen bileşenler için yerel bir **SHA256 Checksum** doğrulaması script içinde yapılmıyor.
2. **Privilege Escalation Riski:** Script, Docker daemon socket erişimi talep ediyor. Bu, saldırganın konteyner üzerinden ana makinede (host) root yetkisi kazanmasına yol açabilecek bir zafiyet noktasıdır.
3. **Entropy ve Secrets:** Üretilen Master Key (`_APP_OPENSSL_KEY_V1`) yapısı incelendiğinde, rastgeleliğin işletim sistemi kaynaklı olduğu ancak statik dosyalara yazıldığı tespit edildi.

**Analiz Sonucu:** Kurulum mimarisi "Implicit Trust" (Örtülü Güven) üzerine kuruludur.
