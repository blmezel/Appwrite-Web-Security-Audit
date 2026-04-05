# 🔍 Adım 5: Pasaport Kontrol Sistemi - Kaynak Kod ve Auth Analizi

## 🎯 Proje Senaryosu: Kimlik ve Pasaport Doğrulama
Bu proje, kullanıcıların pasaport verilerini güvenli bir şekilde doğruladığı bir sistem üzerine kurgulanmıştır. Altyapı olarak Appwrite'ın Auth ve Database servisleri kullanılmaktadır.

## 🔐 Kimlik Doğrulama (Authentication) Analizi
Sistemdeki pasaport verilerine erişim için Appwrite'ın **JWT (JSON Web Token)** mekanizması kullanılmaktadır. 
- **Entrypoint:** Kimlik doğrulama istekleri `/v1/account/sessions/email` endpoint'i üzerinden karşılanır.
- **Güvenlik Katmanı:** Pasaport verilerine erişen her istek, `X-Appwrite-Project` ve `X-Appwrite-JWT` başlıklarıyla doğrulanmak zorundadır.

## 🔴 KRİTİK SORU: Hacker Gözüyle Pasaport Verisi Tehdit Modellemesi
Hocanın "Bir hacker ne tür veriyi çalabileceğini nasıl bilir?" sorusuna pasaport senaryosuyla yanıt:

**Soru:** Hacker hangi veriye saldıracağını nasıl anlar?
**Yanıt:** Appwrite açık kaynak bir proje olduğu için, hacker `users` ve `documents` tablolarının yapısını bilir. Pasaport numarası gibi hassas verilerin (PII - Personally Identifiable Information) hangi koleksiyonlarda tutulduğunu kod analizi yaparak (Reverse Engineering) tespit edebilir.

**Soru:** Bu pasaport sistemine dışarıdan nasıl saldırılabilir?
1. **JWT Hijacking:** Eğer kullanıcı halka açık bir Wi-Fi üzerinden sisteme girerse ve TLS (HTTPS) katmanında bir zayıflık varsa, hacker pasaport erişim token'ını (JWT) çalarak kullanıcının kimliğine bürünebilir.
2. **Broken Object Level Authorization (BOLA):** Bir kullanıcı kendi pasaportunu görüntülerken, URL'deki ID'yi değiştirerek başkasının pasaport bilgilerine erişmeye çalışabilir. Appwrite bu noktada "Server-side Permissions" ile savunma yapar.

**Sonuç:** Pasaport gibi kritik veriler, "Least Privilege" (En az yetki) kuralıyla sadece yetkili memur veya kullanıcıya açılmalıdır.
