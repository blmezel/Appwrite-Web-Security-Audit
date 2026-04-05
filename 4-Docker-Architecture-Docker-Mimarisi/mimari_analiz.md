# 🐋 Adım 4: Docker Mimarisi ve Konteyner Güvenlik Analizi

## 🎯 Docker İmajı ve Katman (Layer) Analizi
**Docker İmajı Nedir?** Uygulamanın çalışması için gereken kod, kütüphane ve ayarların paketlenmiş halidir. 
- **Katmanlı Yapı:** Her bir komut (RUN, COPY) yeni bir katman oluşturur. Appwrite imajları incelendiğinde "Alpine Linux" gibi hafif dağıtımların kullanıldığı görülür. Bu, saldırı yüzeyini (attack surface) küçülterek güvenliği artırır.

## 🔴 KRİTİK SORU: Ortamı Nasıl Daha Güvenli Hale Getiririz?
Hocanın "Ortamı en güvenli hale nasıl getirebiliriz?" sorusuna mimari çözümler:

1. **Ağ İzolasyonu (Network Segmentation):** Appwrite servisleri (MariaDB, Redis vb.) dış dünyaya kapalı bir iç ağda (bridge network) çalışır. Sadece ana API servisi dışarıya port açar. Bu, veritabanına doğrudan sızılmasını engeller.
2. **Resource Limits:** Konteynerların CPU ve RAM kullanımı sınırlandırılarak, bir servisin ele geçirilmesi durumunda tüm sistemi kilitlemesi (DoS) önlenir.
3. **ReadOnly Root FS:** Konteyner içindeki dosya sistemi "salt okunur" yapılarak, saldırganın konteyner içine zararlı yazılım indirmesi engellenebilir.

## ⚙️ Kubernetes ve VM Farkı
- **VM (Virtual Machine):** Donanımı sanallaştırır, her VM'in kendi işletim sistemi çekirdeği (kernel) vardır. İzolasyon yüksektir ama hantaldır.
- **Docker:** İşletim sistemini sanallaştırır, ana makinenin çekirdeğini paylaşır. Hafiftir ama kernel seviyesinde izolasyon daha zayıftır.
- **Kubernetes (K8s):** Bu konteynerların binlercesini yöneten "orkestra şefidir". Appwrite, ölçeklenebilirlik için K8s desteği sunar.

**Sonuç:** Docker mimarisi, "Microservices" yaklaşımıyla servisleri birbirinden izole ederek sistemin genel güvenliğini artırır.
