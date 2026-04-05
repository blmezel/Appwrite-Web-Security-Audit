# ⚙️ Adım 3: DevSecOps ve CI/CD Pipeline Güvenliği

Projenin GitHub üzerindeki entegrasyon iş akışları (Workflows), 'DevSecOps' prensipleri çerçevesinde denetlenmiştir:

- **CodeQL ve SAST Entegrasyonu:** Kaynak kodların her 'push' işleminde GitHub CodeQL tarafından otomatik Statik Analiz (SAST) testine tabi tutulduğu tespit edilmiştir. Bu mekanizma, XSS, SQLi ve Path Traversal gibi zafiyetleri geliştirme aşamasında yakalar.
- **Workflow İzinleri:** '.github/workflows' dizinindeki YAML dosyaları incelendiğinde, pipeline'lara sadece 'security-events: write' yetkisi verildiği, bu sayede "Least Privilege" kuralının başarıyla uygulandığı görülmüştür.
- **Tedarik Zinciri (Supply Chain) Güvenliği:** Dışarıdan çekilen Docker imajlarının ve paketlerin güvenliği için Webhook imzalarının (X-Signature) kullanıldığı onaylanmıştır.
