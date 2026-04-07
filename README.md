<div align="center">
  <img width="320" height="320" alt="istinye-universitesi-logo-png_seeklogo-610039" src="https://github.com/user-attachments/assets/da681d83-2f61-4daf-be78-c01abe656e88" />


  # 🛡️ Güvenli Web Yazılımı Geliştirme: Vize Projesi

  <div align="center">
  <img width="320" height="320" alt="istinye-universitesi-logo-png_seeklogo-610039" src="https://github.com/user-attachments/assets/da681d83-2f61-4daf-be78-c01abe656e88" />

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
6. [Gelişmiş Sistem Mimarisi ve DevSecOps](#️-gelişmiş-sistem-mimarisi-ve-devsecops)
7. [Çıktılar ve Sonuç](#-sonuç)

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
 
## 👨‍🏫 Eğitmen Bilgisi
**Instructor:** Keyvan Arasteh

---

## 📽️ Proje Demo ve AI Güvenlik Raporu

Bu proje, **Google Antigravity AI** kullanılarak kapsamlı bir siber güvenlik denetiminden geçirilmiştir.

* [▶️ Teknik Analiz Videosunu İzle (Demo)](demo/Video%20Projesi.mp4)
* [📄 Teknik Siber Dayanıklılık Raporu (AI Generated)](cyber_resilience_report.md)

---
