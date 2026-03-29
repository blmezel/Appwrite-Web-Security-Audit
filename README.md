# appwrite-security-audit-guvenli-web# 🛡️ Güvenli Web Yazılımı Geliştirme: Vize Proje Önerisi

![Security Audit](https://img.shields.io/badge/Security-Audit-red)
![Docker Security](https://img.shields.io/badge/Docker-Container_Security-blue)
![CI/CD Pipeline](https://img.shields.io/badge/CI%2FCD-Pipeline_Analysis-green)
![Target Repo](https://img.shields.io/badge/Target-Appwrite-ff69b4)
![Status](https://img.shields.io/badge/Status-Proposal-yellow)

---

## 📋 Proje ve Öğrenci Bilgileri

| Kriter                   | Detay                                                      |
| :----------------------- | :--------------------------------------------------------- |
| **Öğrenci Adı Soyadı**   | Ezel Balım Atik                                            |
| **Üniversite & Bölüm**   | İstinye Üniversitesi - Bilişim Güvenliği Teknolojisi         |
| **Ders**                 | Güvenli Web Yazılımı Geliştirme                            |
| **Analiz Edilecek Repo** | [Appwrite (v1.x)](https://github.com/appwrite/appwrite)    |
| **Seçilen Senaryo**      | **Standart Senaryo 1: Authentication (Pasaport Kontrolü)** |

---

## 🎯 Projenin Amacı

Bu projenin amacı, modern bir açık kaynak backend platformu olan Appwrite’ın:

* Kurulum sürecinin güvenliği
* Sistemle entegrasyonu
* Docker tabanlı mimarisi
* CI/CD süreçleri
* Kimlik doğrulama (Authentication) mekanizmaları

üzerinden kapsamlı bir **güvenlik analizi** gerçekleştirmektir.

Proje kapsamında özellikle aşağıdaki saldırı türlerine karşı sistemin dayanıklılığı incelenecektir:

* Brute Force saldırıları
* Session Hijacking
* JWT Forging

---

## 🔍 Planlanan Analiz Aşamaları

### 1️⃣ Kurulum ve Script Analizi (Reverse Engineering)

* `install.sh` scripti incelenecek
* Körlemesine çalıştırma (curl | bash) riskleri değerlendirilecek
* Scriptin:

  * Dosya sistemi değişiklikleri
  * Yetki kullanımı
  * Dış bağımlılıkları
    analiz edilecektir

🔴 **Araştırma Sorusu:**
İndirilen bileşenlerin bütünlüğü nasıl doğrulanmaktadır?

---

### 2️⃣ Sistem Temizliği ve Adli Analiz (Forensics)

* Kurulum sonrası sistemde bırakılan izler incelenecek
* Docker container, volume ve network kalıntıları analiz edilecek

Planlanan komutlar:

```bash
docker compose down --volumes --rmi all --remove-orphans
docker network prune -f
```

🔴 **Araştırma Sorusu:**
Bir uygulamanın sistemden tamamen kaldırıldığı nasıl kanıtlanır?

---

### 3️⃣ CI/CD Pipeline Analizi

* `.github/workflows` dosyaları incelenecek
* Otomatik güvenlik testleri analiz edilecek
* Dependabot ve güvenlik taramaları değerlendirilecek

🔴 **Araştırma Sorusu:**
Tedarik zinciri saldırıları bu pipeline üzerinden nasıl gerçekleşebilir?

---

### 4️⃣ Docker Mimarisi ve Güvenlik

* Servisler ve container yapısı analiz edilecek
* Network izolasyonu incelenecek
* Mikroservisler arası iletişim değerlendirilecek

🔴 **Araştırma Sorusu:**
Bir container ele geçirilirse diğerlerine sıçrama nasıl engellenir?

---

### 5️⃣ Authentication ve Threat Modeling

* Şifreleme ve oturum mekanizmaları incelenecek
* JWT yapısı analiz edilecek

Planlanan saldırı analizleri:

* Brute Force → Rate limiting kontrolü
* Session Hijacking → cihaz/IP doğrulama
* JWT Forging → imza doğrulama mekanizması

🔴 **Araştırma Sorusu:**
Kimlik doğrulama sistemi hangi katmanlarda korunmaktadır?

---

## 🛠️ Kullanılacak Teknolojiler

* Docker & Docker Compose
* Linux (Kali / Ubuntu)
* GitHub Actions
* Wireshark (trafik analizi için opsiyonel)

---

## 📅 Planlanan Çalışma Takvimi

| Gün | Aşama     | Yapılacak İş         |
| --- | --------- | -------------------- |
| 1   | Kurulum   | Script analizi       |
| 2   | Forensics | Sistem temizliği     |
| 3   | CI/CD     | Pipeline inceleme    |
| 4   | Docker    | Mimari analiz        |
| 5   | Auth      | Threat modeling      |
| 6   | Test      | API davranış analizi |
| 7   | Final     | Rapor yazımı         |

---

## 📌 Beklenen Çıktılar

* Güvenlik risk analizi raporu
* Docker mimari şeması
* CI/CD güvenlik değerlendirmesi
* Authentication saldırı modeli
* Teknik README ve dokümantasyon

---

## 🧠 Projenin Katkısı

Bu proje sayesinde:

* Gerçek dünya bir sistem üzerinde güvenlik analizi yapılacak
* Modern web uygulamalarının güvenlik mimarisi anlaşılacak
* Teorik bilgilerin pratik karşılığı gösterilecektir

---

## 🔐 Sonuç (Planlanan)

Bu çalışma, sadece teorik değil; kurulum, analiz ve test süreçlerini içeren **uygulamalı bir güvenlik incelemesi** olarak gerçekleştirilecektir.

---
