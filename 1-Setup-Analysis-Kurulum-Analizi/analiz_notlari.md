# 🔍 Adım 1: Kurulum ve install.sh Analizi
Appwrite kurulum scripti (install.sh) incelenmiştir. Scriptin root yetkisi istemesi ve Docker socket erişimi siber güvenlik açısından 'Privilege Escalation' riskleri taşımaktadır. Ayrıca paketlerin hash kontrolü yapılmadan indirilmesi MITM saldırılarına kapı açmaktadır.

## 📸 Terminal Kanıtı
![Kurulum Analizi](../images/ss1.png)
