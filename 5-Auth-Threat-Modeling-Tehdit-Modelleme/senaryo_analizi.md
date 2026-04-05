# 🔐 Tehdit Modelleme: Pasaport Kontrolü (Authentication)

- **Entrypoint:** /v1/account/sessions/email (Kullanıcı giriş kapısı)
- **JWT Yapısı:** Kullanıcı pasaport verilerine erişim, sunucu tarafından imzalanmış JSON Web Token'lar ile yetkilendirilir.
- **Olası Saldırı Vektörleri:** Brute-force saldırılarına karşı 'Rate Limiting' ve JWT çalınmasına karşı 'Secure Cookies' önlemleri mevcuttur.

## 📸 Terminal Kanıtı
![Auth Analizi](https://raw.githubusercontent.com/blmezel/Appwrite-Web-Security-Audit/main/images/ss4.png)
