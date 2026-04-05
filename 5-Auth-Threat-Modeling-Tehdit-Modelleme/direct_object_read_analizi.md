# 📁 Güvensiz Direct Object Read (IDOR & Directory Listing) Analizi

Bu analiz, pasaport görsellerinin ve PDF belgelerinin saklandığı "Storage" (Depolama) katmanındaki gizlilik ihlali risklerini denetler.

### 🎯 Saldırı Senaryosu (Açık Dizin)
Saldırgan, sistemdeki bir dosyaya eriştiğinde (örneğin: `/storage/passports/user123.jpg`), üst dizine çıkmaya veya dizini listelemeye çalışır (`/storage/passports/`). Eğer sistem "Directory Listing" özelliğini kapatmamışsa, saldırgan tüm kullanıcıların pasaport dosyalarını limitsizce listeleyebilir ve indirebilir.

### 🛡️ Kısa Yol Haritası ve Mimari Savunma
Görseldeki "Kısa Yol Haritası" prensiplerine uygun olarak şu önlemler analiz edilmiştir:

1. **Presigned-URL Mekanizması:** Pasaport dosyaları internete doğrudan (Public) açık değildir. Bir dosya indirilmek istendiğinde, Appwrite tarafında sadece o kullanıcıya özel, **zaman ayarlı ve imzalı bir URL** oluşturulur. Bu URL 5 dakika sonra geçerliliğini yitirir.
2. **Directory Listing Engelleme:** Web sunucusu ve depolama katmanı (S3 veya Lokal), dizin içeriğini listeleme isteklerine "403 Forbidden" dönecek şekilde sertleştirilmiştir.
3. **Kova (Bucket) İzinleri:** Her pasaport belgesi, Appwrite üzerindeki **"Permission-based"** (Yetki tabanlı) kovalarda saklanır. Dosyayı sadece "Owner" (Sahibi) ve "Admin" (Memur) görebilir.

> **💡 Altın Kural:** "Kullanıcı faturasını (pasaportunu) indirsin derken bütün dizini web'e açma!" Bu sistemde her indirme işlemi şifreli ve zaman ayarlı geçici bağlantılar üzerinden yürütülür.

**Sonuç:** Pasaport belgelerinin toplu olarak sızdırılmasına yol açabilecek "Direct Object Read" zafiyeti mimari olarak engellenmiştir.
