# 🧟 İstemci Zombi Olursa: CSRF (Cross-Site Request Forgery) Analizi

Bu analiz, pasaport doğrulama sistemindeki yetkili bir memurun tarayıcısının, saldırgan tarafından bir "silah" olarak kullanılma riskini denetler.

### 🎯 Saldırı Senaryosu (Zombi İstemci)
Saldırgan, pasaport sisteminde oturumu açık olan bir memura (admin) masum görünen bir link veya resim gönderir. Memur bu linke tıkladığında, arka planda memurun haberi olmadan pasaport kayıtlarını silen bir istek (`POST /v1/database/collections/...`) tetiklenir. Tarayıcı memurun çerezlerini (Cookie) otomatik olarak gönderdiği için sistem bu isteği meşru sanır.

### 🛡️ Kısa Yol Haritası ve Savunma Stratejisi
Hocanın görselindeki "Kısa Yol Haritası"na uygun olarak sistemde şu önlemler analiz edilmiştir:

1. **Anti-CSRF Tokens:** Her kritik işlemde (pasaport güncelleme/silme) istemciden sunucuya gönderilen, tahmin edilemez ve eşsiz bir token kullanılır. Saldırgan bu token'ı bilmediği için dışarıdan tetik çekemez.
2. **Modern Cookie Politikası (SameSite=Strict):** Appwrite oturum çerezleri `SameSite=Strict` veya `Lax` modunda yapılandırılmıştır. Bu sayede, tarayıcı başka bir siteden gelen isteklerde pasaport sisteminin çerezlerini asla göndermez. Memurun eli "zombi" olsa bile, saldırgan tetiği çekemez.

**Sonuç:** Pasaport gibi kritik verilerin manipüle edilmesini sağlayan CSRF saldırı vektörü, modern oturum politikalarıyla %100 kapatılmıştır.
