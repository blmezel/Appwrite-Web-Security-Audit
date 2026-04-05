# 🔐 Adım 5: Tehdit Modelleme ve Kimlik Doğrulama Analizi

Projenin kurgulanan **"E-Pasaport Doğrulama Sistemi"** senaryosu üzerinden, Appwrite'ın kimlik doğrulama (Authentication) modülleri için Tehdit Modelleme (Threat Modeling) gerçekleştirilmiştir:

- **JWT (JSON Web Token) Analizi:** Pasaport verilerine erişim, sunucu tarafından imzalanan JWT token'lar ile sağlanmaktadır. Yapılan analizde, token imzalarının güçlü kriptografik algoritmalarla (HS256/RS256) korunduğu ve "None Algorithm" zafiyetine kapalı olduğu teyit edilmiştir.
- **BOLA (Broken Object Level Authorization) Koruması:** Bir kullanıcının URL'deki parametreleri manipüle ederek başka birinin pasaport verisine erişme girişimi simüle edilmiştir. Appwrite'ın sunucu taraflı Rol Bazlı Erişim Kontrolü (RBAC) sayesinde bu saldırı vektörünün kapalı olduğu doğrulanmıştır.
- **Sonuç:** Uygulama giriş noktaları (Entrypoints), Brute-Force saldırılarına karşı "Rate Limiting" (İstek Sınırlandırma) ile korunmaktadır. Tüm denetim süreci başarıyla tamamlanmıştır.
