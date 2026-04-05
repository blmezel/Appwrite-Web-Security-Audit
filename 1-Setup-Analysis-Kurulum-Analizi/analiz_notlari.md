# 🔍 Adım 1: Kurulum Süreci ve install.sh Analizi

Appwrite altyapısının kurulum sürecinde kullanılan 'install.sh' betiği, tersine mühendislik (Reverse Engineering) yaklaşımıyla incelenmiştir. Yapılan teknik analizde şu bulgulara rastlanmıştır:

- **Privilege Escalation (Yetki Yükseltme) Riski:** Betiğin çalıştırılabilmesi için doğrudan 'root' yetkisi talep edilmektedir. Bu durum, betik içerisine sızabilecek zararlı bir kodun tüm sistemi ele geçirmesi riskini barındırır.
- **Docker Socket Erişimi:** Kurulum süreci, Docker daemon socket'ine doğrudan erişim sağlamaktadır. Konteyner kaçış (Container Breakout) senaryolarında bu durum kritik bir zafiyet noktası oluşturabilir.
- **Güvenlik Sıkılaştırma Önerisi:** Üretim ortamlarında doğrudan shell betiği yerine, 'Least Privilege' (En Az Yetki) ilkesine uygun olarak Terraform veya Ansible gibi Infrastructure as Code (IaC) araçları ile kurulum yapılması önerilmektedir.
