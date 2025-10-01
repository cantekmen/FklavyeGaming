# Fklavye Gaming Projesi Yol Haritası

Bu doküman, Fklavye Gaming adıyla geliştirilecek çevrim içi arkadaşlık ve pong tabanlı oyun platformunun baştan sona nasıl inşa edileceğini adım adım açıklar. Proje boyunca aşağıdaki bölümleri referans alarak ilerleyebilirsin.

## 1. Proje Genel Bakışı

- **Amaç:** Lichess benzeri bir kullanıcı deneyimi sunan, ancak klasik Pong oyununun oynandığı çok oyunculu bir platform kurmak.
- **Ana Özellikler:**
  - Kullanıcı kayıt/giriş sistemi.
  - Lobiler arası dereceli eşleştirme (herkes 50 puanla başlar, maçta kazanan kaybedenden 5 puan alır).
  - Phaser tabanlı gerçek zamanlı Pong motoru.
  - Arkadaşlık ve sohbet sistemi (sadece aynı lobideki oyuncular birbirine arkadaşlık isteği gönderebilir).
  - Profil, skor tabloları ve meydan okuma akışı.

## 2. Teknoloji Seçimleri

| Katman | Önerilen Teknolojiler | Açıklama |
| --- | --- | --- |
| **İstemci (Web)** | React + Vite, Tailwind CSS, Phaser 3 | Modern, hızlı arayüz + Phaser ile gömülü oyun sahnesi |
| **Sunucu** | Node.js (NestJS veya Express), WebSocket (Socket.IO) | Gerçek zamanlı iletişim ve REST API'leri |
| **Veri Tabanı** | PostgreSQL (Prisma ORM) | Kullanıcılar, maç geçmişi, puanlar ve arkadaşlık ilişkileri |
| **Kimlik Doğrulama** | JWT + Refresh Token veya Auth0/Clerk | Güvenli oturum yönetimi |
| **Barındırma** | Frontend: Vercel/Netlify, Backend: Railway/Render/Fly.io | CI/CD ile otomatik dağıtım |
| **Diğer** | Redis (geçici veri ve lobiler), Docker | Ölçeklenebilirlik ve geliştirme kolaylığı |

> Alternatif teknolojileri tercih edebilirsin; ancak Phaser oyun motoru şart ve gerçek zamanlı iletişim için WebSocket benzeri çift yönlü bir kanal gerekiyor.

## 3. Çalışma Ortamı Hazırlığı

1. **Depo Yapısı Oluştur:**
   ```
   fklavyegaming/
   ├─ apps/
   │  ├─ web/            # React + Phaser istemci uygulaması
   │  └─ api/            # Node.js sunucusu
   ├─ packages/
   │  ├─ ui/             # Ortak arayüz bileşenleri (opsiyonel)
   │  └─ config/         # ESLint, Tailwind vb. paylaşılan konfigürasyonlar
   ├─ docs/              # Tasarım dokümanları, wireframe'ler
   ├─ assets/            # Logo ve ikon dosyalarının saklanacağı klasör
   └─ README.md
   ```
2. **Geliştirme Araçları:**
   - Node.js LTS, pnpm veya yarn (monorepo çalışmaları için önerilir).
   - Docker ve Docker Compose (veri tabanı/redis için).
   - Git + GitHub/GitLab.

## 4. Logo ve İkon Yönetimi

- **assets/logo/**: PNG, SVG formatlarında ana logo varyasyonları (koyu/açık versiyonlar).
- **assets/icons/**: Uygulamada kullanılacak küçük ikonlar (ör. lobiler, arkadaşlık, skor tablosu).
- **assets/branding-guide.md**: Renk paleti, tipografi ve logonun kullanım kuralları.

> Tasarım dosyalarını Figma gibi araçlarda üretip `docs/design/` klasörüne export edilmiş PDF/PNG önizlemeleriyle birlikte ekleyebilirsin.

## 5. Adım Adım Geliştirme Planı

### 5.1. Planlama ve Tasarım
- Kullanıcı akışlarını ve wireframe'leri hazırla (`docs/wireframes/`).
- Lobiler, arkadaşlık sistemi ve maç puanlaması için UML diyagramları oluştur.
- Minimum uygulanabilir ürün (MVP) kapsamını belirle: kayıt, giriş, tek lobi, maç başlatma, skor güncelleme.

### 5.2. Backend Temeli
1. Node.js projesini başlat (`apps/api`).
2. PostgreSQL şemasını planla (Users, Matches, Ratings, Friendships, Lobbies).
3. Prisma veya benzeri ORM ile veri modellerini yaz ve migrasyonları çalıştır.
4. Auth akışını (kayıt/giriş/JWT) tamamla.
5. WebSocket sunucusunu kur ve aşağıdaki olayları tanımla:
   - `lobby:join`, `lobby:leave`
   - `match:challenge`, `match:accept`, `match:result`
   - `friend:request`, `friend:accept`
6. Lobiler ve puan eşikleri için servis mantığını uygula (ör. 0–99 = Bronz, 100–199 = Gümüş, vb.).

### 5.3. Frontend Temeli
1. Vite ile React projesi oluştur (`apps/web`).
2. Tailwind veya benzeri bir UI sistemi entegre et.
3. Kimlik doğrulama sayfalarını (giriş/kayıt) hazırla.
4. Lobi görünümü: Sol tarafta oyuncu listesi, sağda sohbet, ortada meydan okuma düğmeleri.
5. Phaser sahnesini React bileşeni olarak göm.
6. WebSocket istemcisi kur ve backend olaylarına bağlan.

### 5.4. Phaser ile Pong Motoru
- Tek sahnede top, pad'ler ve skor panosu oluştur.
- Kullanıcı girişini WebSocket üzerinden senkronize et (server authoritative mantık).
- Maç sonunda backend'e sonuç gönder, puanları güncelle.
- Latency ve hile önleme için tahmin/rollback stratejilerini değerlendir.

### 5.5. İleri Özellikler
- Dereceli lobiler arası geçiş için eşik kontrolleri ve bildirimler.
- Arkadaşlık sistemi: isteği gönderme, kabul etme, sohbet kanalı açma.
- Profil sayfaları, maç geçmişi, skor grafikleri.
- Sadece arkadaşlarla özel maç açma.

### 5.6. Test ve Dağıtım
1. Birim ve entegrasyon testleri (Jest, Playwright, Supertest).
2. CI/CD boru hattı kur (GitHub Actions).
3. Docker imajları oluştur ve staging ortamında test et.
4. Üretime çıkmadan önce yük testleri yap (k6, Artillery).

## 6. Güvenlik ve Ölçeklenebilirlik Notları
- HTTPS zorunlu, güvenlik başlıkları (Helmet).
- Rate limiting, brute-force koruması.
- WebSocket bağlantıları için kimlik doğrulama.
- Loglama ve gözlemlenebilirlik (Winston, OpenTelemetry).

## 7. Yol Haritası ve Milestone Önerisi
| Milestone | Açıklama | Süre (tahmini) |
| --- | --- | --- |
| M1 | Mimari tasarım, veri modeli, temel UI wireframe'leri | 2 hafta |
| M2 | Backend MVP (auth + tek lobi + maç sonuçları) | 3 hafta |
| M3 | Frontend MVP (kayıt, lobi, Phaser ile maç) | 4 hafta |
| M4 | Dereceli lobiler, arkadaşlık, sohbet | 4 hafta |
| M5 | Testler, iyileştirmeler, dağıtım | 2 hafta |

## 8. Sonraki Adımlar
- Bu README'deki yapıyı temel alarak depo klasörlerini oluştur.
- Teknoloji seçimlerini doğrula, gerekli SDK ve kütüphaneleri kur.
- Tasarım ve mimari dokümanlarla ekibi hizala.
- MVP'yi tamamladıktan sonra kullanıcı testleri yap ve geri bildirimleri topla.

Fklavye Gaming'i gerçek dünyaya açmadan önce kapsamlı testler yapmayı, güvenlik açıklarını kapatmayı ve ölçeklenebilirliği göz önünde bulundurmayı unutma. Proje boyunca bu belgeyi güncelleyerek ilerlemeyi izle.
