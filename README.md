<div align="center">
  <img width="320" height="320" alt="istinye-universitesi-logo-png_seeklogo-610039" src="https://github.com/user-attachments/assets/da681d83-2f61-4daf-be78-c01abe656e88" />

  # 🛡️ Güvenli Web Yazılımı Geliştirme: Vize Projesi

  ![Security Audit](https://img.shields.io/badge/Security-Audit-red)
  ![Docker Security](https://img.shields.io/badge/Docker-Container_Security-blue)
  ![CI/CD Pipeline](https://img.shields.io/badge/CI%2FCD-Pipeline_Analysis-green)
  ![Instructor](https://img.shields.io/badge/E%C4%9Fitmen-Keyvan_Arasteh-purple)
  ![Target Repo](https://img.shields.io/badge/Target-Appwrite-ff69b4)

  <br>

  🚀 **[CANLI SİBER GÜVENLİK PANELİNİ GÖRÜNTÜLEMEK İÇİN TIKLAYIN](https://blmezel.github.io/Appwrite-Web-Security-Audit/)**
</div>

---

## 📑 İçindekiler (TOC)
1. [Proje ve Öğrenci Bilgileri](#-proje-ve-öğrenci-bilgileri)
2. [Projenin Amacı](#-projenin-amacı)
3. [Planlanan Analiz Aşamaları](#-planlanan-analiz-aşamaları)
4. [🐞 Tespit Edilen Buglar (Ek Puan)](#-tespit-edilen-buglar-ve-zafiyetler-ek-puan)
5. [Kullanılacak Teknolojiler](#️-kullanılacak-teknolojiler)
6. [Çıktılar ve Sonuç](#-beklenen-çıktılar)

---

## 📋 Proje ve Öğrenci Bilgileri

| Kriter                   | Detay                                                      |
| :----------------------- | :--------------------------------------------------------- |
| **Öğrenci Adı Soyadı** | Ezel Balım Atik                                            |
| **Üniversite & Bölüm** | İstinye Üniversitesi - Bilişim Güvenliği Teknolojisi       |
| **Ders** | Güvenli Web Yazılımı Geliştirme                            |
| **Eğitmen** | Keyvan Arasteh                                             |
| **Analiz Edilecek Repo** | [Appwrite (v1.x)](https://github.com/appwrite/appwrite)    |
| **Seçilen Senaryo** | **Standart Senaryo 1: Authentication (Pasaport Kontrolü)** |

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

**Planlanan saldırı analizleri:**
* Brute Force → Rate limiting kontrolü
* Session Hijacking → cihaz/IP doğrulama
* JWT Forging → imza doğrulama mekanizması

🔴 **Araştırma Sorusu:**
Kimlik doğrulama sistemi hangi katmanlarda korunmaktadır?

---

## 🐞 Tespit Edilen Buglar ve Zafiyetler (EK PUAN)

Analiz süreçlerinde, sistemin açık kaynak altyapısında aşağıdaki güvenlik zafiyetleri tespit edilmiş ve mimari çözümler sunulmuştur:

1. **Supply Chain (Tedarik Zinciri) Zafiyeti (install.sh):**
   * **Bulgu:** Kurulum betiklerinde `curl | bash` mantığı kullanıldığı, ancak paketlerin **SHA-256 Checksum** doğrulamasının yapılmadığı tespit edilmiştir (Ortadaki Adam / MitM riski).
2. **Rate Limit Bypass (Zabıta Katmanı):**
   * **Bulgu:** Rate Limit uygulanırken sadece `X-Forwarded-For` başlığına güvenildiği saptanmıştır (IP Spoofing ile Brute-Force riski).
3. **Güvensiz Direct Object Reference (IDOR):**
   * **Bulgu:** Pasaport dosyalarında "Directory Listing" (Dizin Listeleme) zafiyeti riski saptanmıştır. Çözüm olarak **Presigned-URL** mimarisi zorunlu kılınmıştır.

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

## 🔐 Sonuç

Bu çalışma, sadece teorik değil; kurulum, analiz ve test süreçlerini içeren **uygulamalı bir güvenlik incelemesi** olarak başarıyla gerçekleştirilmiştir. Repo profesyonelliği kapsamında hassas sırlar (`.env`) gizlenmiş ve kod mimarisi modüler hale getirilmiştir.

---
---

## 👨‍🏫 Eğitmen Bilgisi
**Instructor:** Keyvan Arasteh

---

## 📽️ Proje Demo ve AI Güvenlik Raporu

Bu proje, **Google Antigravity AI** kullanılarak kapsamlı bir siber güvenlik denetiminden (Security Audit) geçirilmiştir.

* [▶️ Teknik Analiz Videosunu İzle (Demo)](Video%20Projesi.mp4)
* [📄 Teknik Siber Dayanıklılık Raporu (AI Generated)](cyber_resilience_report.md)

---
