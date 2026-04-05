# 👮 Middleware Hiyerarşisi: Zabıta ve Polis Analojisi

Pasaport doğrulama sistemi gibi yüksek kritiklikteki sistemlerde, sunucu kaynaklarını verimli kullanmak ve güvenliği kademelendirmek için "Zabıta ve Polis" stratejisi uygulanmıştır.

### 🛡️ 1. Katman: Zabıta (Rate Limiter / Edge Security)
Sistemin kapısında duran ilk koruma katmanıdır. 
- **Görevi:** Henüz ağır kimlik doğrulama kontrollerine girmeden, gelen isteğin hızını ve miktarını kontrol eder.
- **Teknik Uygulama:** Appwrite ve Nginx üzerindeki **Rate Limiting** mekanizmasıdır. Eğer bir IP adresinden saniyede 100 pasaport sorgusu geliyorsa, "Zabıta" bu trafiği sunucuyu yormadan kapıda reddeder.

### 🚔 2. Katman: Polis (Auth & Permission Middleware)
Zabıta süzgecinden geçen "meşru" trafiği karşılayan ağır güvenlik katmanıdır.
- **Görevi:** İsteğin içindeki **JWT (JSON Web Token)** verisini, imza doğruluğunu ve kullanıcının pasaport verisini görmeye yetkili olup olmadığını (ACL) kontrol eder.
- **Teknik Uygulama:** Appwrite Auth Service. Bu katman sunucu kaynağı harcar (CPU/Database), bu yüzden sadece Zabıta'dan geçen "temiz" istekler buraya ulaşır.

### 📝 3. Katman: Şahit (Logging Middleware)
- **Görevi:** Tüm süreci kayıt altına alır.
- **Teknik Uygulama:** Appwrite Audit Logs. Kim, ne zaman, hangi pasaport verisine erişmeye çalıştı? Başarılı mı yoksa başarısız mı? Her şey "Forensics" analizi için kaydedilir.

**Sonuç:** Bu hiyerarşi sayesinde, kaba kuvvet (Brute-force) saldırıları sunucunun "Polis" katmanını yormadan "Zabıta" tarafından bertaraf edilir.
