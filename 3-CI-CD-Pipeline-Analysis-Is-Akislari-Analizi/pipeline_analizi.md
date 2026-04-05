# ⚙️ Adım 3: CI/CD Pipeline ve Otomatik Güvenlik Analizi (SAST)

## 🎯 Seçilen İş Akışı: CodeQL (Static Analysis Results)
Appwrite projesinin kaynak kod güvenliğini sağlamak için kullandığı **CodeQL** mekanizması incelenmiştir. Bu dosya, bir "Güvenlik Mimarı" için projenin en kritik savunma hattıdır.

### 🛠️ Teknik Analiz (CodeQL Workflow):
- **Kaynak Dosya:** [github.com/appwrite/appwrite/blob/master/.github/workflows/codeql.yml](https://github.com/appwrite/appwrite/blob/master/.github/workflows/codeql.yml)
- **Yetki İlkesi:** `permissions: contents: read` ve `security-events: write` tanımlanmıştır. Pipeline sadece gerekli kodları okur ve sadece güvenlik raporlarını yazar.
- **SAST Taraması:** `Initialize CodeQL` ve `Perform CodeQL Analysis` adımları, her "Push" anında gizli zafiyetleri otomatik olarak tarar.

## 🔴 KRİTİK SORU: Webhook ve CI/CD İlişkisi
**Soru:** Webhook nedir ve bu proje özelinde ne işe yarar?

**Yanıt:** Webhook, GitHub ile CodeQL tarayıcısı arasındaki "anlık haberci"dir. Geliştirici kodu gönderdiği (push) anda GitHub bir Webhook tetikler ve bu analizi başlatır. Bu otomasyon sayesinde insan hatası devre dışı bırakılır.

**Sonuç:** Appwrite, "DevSecOps" prensiplerini uygulayarak güvenlik testlerini iş akışının bir parçası yapmıştır.
