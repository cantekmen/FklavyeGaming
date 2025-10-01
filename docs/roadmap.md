# Fklavye Gaming Yol Haritası

Aşağıdaki adımlar, projeyi sıfırdan üretim ortamına hazırlamak için izlenmesi gereken sırayı açıklar. Her bölüm, ilgili ekip veya geliştirici tarafından tamamlanacak görevleri listeler.

## 1. Proje Temelleri
1. Gereksinimleri ayrıntılı şekilde yazın ve kullanıcı hikayeleri oluşturun.
2. Tasarım dili, renk paleti ve tipografi için bir stil rehberi hazırlayın.
3. Teknik kararlar: Frontend (React + Vite), backend (Node.js + NestJS veya Express), gerçek zamanlı iletişim (Socket.io), veritabanı (PostgreSQL) ve kimlik doğrulama stratejisini netleştirin.
4. Monorepo veya çoklu repo stratejisine karar verin. Başlangıç için tek repo içinde `/frontend`, `/backend` ve `/infrastructure` klasörleri önerilir.

## 2. Tasarım & UX
1. Lichess benzeri ana sayfa ve oyun odası taslaklarını Figma vb. araçlarda oluşturun.
2. Mobil ve masaüstü için responsive layout tasarlayın.
3. Lobi akışları, arkadaş ekleme, sohbet ve bildirim panellerini prototipleyin.
4. Kullanıcı testleri için düşük seviye prototipler hazırlayın ve geri bildirim toplayın.

## 3. Frontend Kurulumu
1. `frontend/` klasöründe React + Vite projesi başlatın.
2. Tailwind CSS veya tercih edilen stil kütüphanesini entegre edin.
3. Router yapılandırması: Ana sayfa, lobi listesi, oyun odası, profil, arkadaşlık/sohbet sayfaları.
4. Global state yönetimi (örn. Zustand, Redux Toolkit) planlayın.
5. Phaser entegrasyonu için `frontend/src/game/` altında temel bir Pong sahnesi oluşturun.

## 4. Oyun Geliştirme (Phaser Pong)
1. `frontend/src/game/scenes/` içinde `LobbyScene`, `MatchScene`, `ResultsScene` gibi sahneler tanımlayın.
2. Pong mekaniği: Paddle, top, skor, çarpışmalar ve hız artışı.
3. Maç başlatma: Soket bağlantısı üzerinden rakip eşleştirme ve maç başlangıç sinyali.
4. Oyun sonu: Kazananın puanını +5, kaybedenin puanını -5 olacak şekilde backend'e sonuç gönderme.
5. Gecikme telafisi için temel ağ senkronizasyon teknikleri (ör. state reconciliation).

## 5. Backend & Gerçek Zamanlı Servisler
1. `backend/` klasöründe Node.js projesi oluşturun (NestJS veya Express + Socket.io).
2. PostgreSQL şemasını tasarlayın: `users`, `friendships`, `matches`, `lobbies`, `ratings` tabloları.
3. Kimlik doğrulama: JWT tabanlı oturum veya OAuth sağlayıcıları (Google, Discord) entegrasyonu.
4. Lobi yönetimi: Puan aralıklarına göre oyuncu eşleştirme ve lobiler arası geçiş kuralları.
5. Gerçek zamanlı oyun kanalı: Socket.io namespace/room yapısı, oyun güncellemeleri ve sohbet mesajları.
6. Matchmaking servisi ile Pong oyun motoru arasında veri alışverişi sözleşmesi (API) belirleyin.

## 6. Arkadaşlık ve Sohbet
1. Arkadaşlık isteği, kabul/ret, bloklama gibi uç noktaları tanımlayın.
2. Lobi bazlı sohbet kanalları oluşturun; kullanıcılar yalnızca aynı lobidekilerle iletişim kurabilir.
3. Mesaj geçmişi saklama ve moderasyon araçları (kelime filtreleme, raporlama) geliştirin.

## 7. Operasyonel Hazırlık
1. Docker tabanlı geliştirme ortamı kurun (`docker-compose` ile frontend, backend, database servisleri).
2. CI/CD pipeline planlayın (GitHub Actions veya GitLab CI).
3. Otomatik testler: Unit, integration, end-to-end (Playwright/Cypress) testleri için temel yapı hazırlayın.
4. Performans ve yük testleri planlayın.
5. Loglama, hata izleme (Sentry) ve izleme (Prometheus + Grafana) çözümleri entegre edin.

## 8. Yayına Hazırlık
1. Üretim ortamı için altyapı seçimi (AWS, GCP, DigitalOcean) ve IaC (Terraform) planı hazırlayın.
2. Domain, SSL sertifikası ve CDN yapılandırmalarını planlayın.
3. Kullanıcı destek, FAQ ve topluluk yönergeleri dokümanlarını hazırlayın.
4. Beta test süreci ve geri bildirim toplama mekanizmasını belirleyin.

> Yol haritası, proje ilerledikçe güncellenmelidir. Yeni gereksinimler ortaya çıktıkça ilgili bölüme yeni maddeler ekleyin.
