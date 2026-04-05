# 👮 Middleware Hiyerarşisi: Zabıta ve Polis Stratejisi

Pasaport doğrulama sistemi gibi yüksek kritiklikteki sistemlerde, sunucu kaynaklarını verimli kullanmak ve "DoS" (Denial of Service) saldırılarını engellemek için **"Zabıta ve Polis"** mimari hiyerarşisi uygulanmıştır.

### 🛡️ 1. Katman: Zabıta (Rate Limiter - Edge Security)
- **Görevi:** Henüz ağır kimlik doğrulama kontrollerine girmeden, gelen isteğin miktarını kontrol eder.
- **Kısa Yol Haritası Uygulaması:** "Basit rate limitleri en başa koy." 
- **Teknik Detay:** Appwrite önündeki bu katman, bir hacker saniyede binlerce istek attığında pasaport veritabanını yormadan isteği doğrudan reddeder.

### 🚔 2. Katman: Polis (Authentication & Authorization)
- **Görevi:** Zabıta süzgecinden geçen temiz isteğin içindeki **JWT (Token)** verisini ve yetkisini kontrol eder.
- **Kısa Yol Haritası Uygulaması:** "Ağır güvenlik kontrollerini sona koy."
- **Teknik Detay:** Şifre çözme ve veritabanı sorgulama gibi "ağır" işlemler sadece meşru (spam olmayan) kullanıcılar için çalıştırılır.

**Sonuç:** Bu hiyerarşi, sunucunun kaynak yönetimini optimize ederken, aynı zamanda sistemi kaba kuvvet saldırılarına karşı %100 dayanıklı hale getirir.
