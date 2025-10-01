# Fklavye Gaming Proje Rehberi

Bu depo, Fklavye Gaming adındaki çevrimiçi arkadaşlık ve oyun platformunu geliştirmek için başlangıç dokümantasyonunu içerir. Platformun temel özellikleri arasında Phaser tabanlı Pong oyunu, puan ve lobi sistemi, arkadaşlık/sohbet fonksiyonları ve görsel varlık yönetimi bulunur.

## Genel Vizyon
- **Platform Teması:** Lichess benzeri sade bir arayüz fakat Pong üzerine odaklı.
- **Oyun Mekaniği:** Phaser kullanılarak geliştirilen gerçek zamanlı Pong.
- **Puan Sistemi:** Herkes 50 puanla başlar; kazanan kaybedenden 5 puan alır.
- **Lobi Sistemi:** Oyuncular başlangıç lobisinde başlar, puan sınırlarını geçtikçe üst lobiler açılır. Arkadaşlık ve sohbet sadece aynı lobideki kişilerle mümkündür.
- **Gerçek Dünya Yayını:** Proje en baştan üretim ortamına açılabilecek yapıda planlanmalıdır.

## Yol Haritası
Adım adım neler yapmanız gerektiğini görmek için [`docs/roadmap.md`](docs/roadmap.md) dosyasına bakın. Bu dosya; planlama, teknik altyapı kurulumu, arayüz tasarımı, oyun geliştirme, backend ve dağıtım hazırlıklarını detaylandırır.

## Klasör Yapısı
Aşağıdaki klasörler oluşturuldu ve proje ilerledikçe genişletilmelidir:

```
FklavyeGaming/
├── assets/
│   ├── icons/
│   │   └── README.md        # Simge dosyaları için rehber
│   ├── logos/
│   │   └── README.md        # Logo dosyaları için rehber
│   └── ui/
│       └── README.md        # Arayüzde kullanılacak illüstrasyonlar ve görseller
├── docs/
│   └── roadmap.md           # Projenin adım adım geliştirme planı
└── README.md                # Bu dosya
```

## Varlık (Asset) Yükleme Talimatları
- **Logo Dosyaları:** `assets/logos/` klasörüne ekleyin. SVG tercih edilir; gerektiğinde PNG alternatifleri ekleyin. Dosya isimleri `fklavye-logo-dark.svg`, `fklavye-logo-light.svg` gibi temaya göre düzenlenmelidir.
- **İkonlar:** `assets/icons/` klasörüne yerleştirin. Boyut/tema bilgisi için `assets/icons/README.md` dosyasındaki talimatlara uyun.
- **UI Görselleri:** Arka plan, lobi illüstrasyonları gibi görselleri `assets/ui/` klasörüne ekleyin.

Her klasördeki README dosyaları, kabul edilen dosya formatları, boyutlar ve isimlendirme konvansiyonlarını açıklar.

## Ek Kaynaklar
- [Phaser 3 Dokümantasyonu](https://newdocs.phaser.io/) – Pong oyununun motorunu geliştirmek için.
- [Socket.io](https://socket.io/) veya WebRTC gibi gerçek zamanlı iletişim teknolojileri – oyuncular arasında oyun ve sohbet senkronizasyonu için.
- [Tailwind CSS](https://tailwindcss.com/) veya benzeri – Lichess benzeri minimalist arayüz için stil kütüphanesi.

Sorularınız veya yeni özellik önerileriniz için `docs/roadmap.md` üzerinden notlar ekleyebilirsiniz.

