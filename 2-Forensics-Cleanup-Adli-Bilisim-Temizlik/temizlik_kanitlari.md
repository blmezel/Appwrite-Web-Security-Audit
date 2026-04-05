# 🧹 Adım 2: Forensics, Adli Bilişim ve Temizlik Analizi

Sistemin kurulumu tamamlandıktan sonra uygulamanın kaldırılma süreci ve arkasında bıraktığı izler Adli Bilişim (Forensics) metodolojileri ile incelenmiştir:

- **Network Forensics:** Uygulama durdurulduktan sonra 'ss -tulpn' ve 'netstat -anp' komutları ile dinlenen portlar taranmıştır. 80 (HTTP) ve 443 (HTTPS) portlarında herhangi bir hayalet (zombie) sürecin kalmadığı doğrulanmıştır.
- **Data Remanence (Veri Kalıntısı) Kontrolü:** Docker volume'leri silindikten sonra disk üzerinde 'find' komutu ile artık konfigürasyon dosyaları veya veritabanı logları aranmıştır. Sistemin "Zero Data Remanence" durumunda olduğu teknik olarak kanıtlanmıştır.
- **Sonuç:** Uygulama, sunucu üzerinde adli bir iz veya arka kapı (backdoor) bırakmadan tamamen izole edilebilmektedir.
