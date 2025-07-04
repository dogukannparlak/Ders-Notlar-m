# 1 networking notes

# 📡 CSE 204 - Bilgisayar Ağları: Networking’e Giriş

---

> 💡 Ders Hedefi
Bu ders notları, bilgisayar ağlarının temel kavramlarını, Internet’in yapısını ve protokollerin çalışma prensiplerini anlamanızı sağlayacaktır.
> 

---

## 🌐 Internet’in “Nuts and Bolts” Tanımı

### 🔧 Temel Bileşenler

> 🏗️ Internet’in Fiziksel Yapısı
Internet, milyarlarca cihazın birbirine bağlandığı karmaşık bir ağ sistemidir.
> 

### 💻 Bağlı Cihazlar

- **🖥️ Hosts** = **End Systems** (Son Sistemler)
    - Ağ uygulamalarını çalıştıran cihazlar
    - Masaüstü bilgisayarlar, sunucular, mobil cihazlar
    - **📱 Client**: Hizmet isteyen cihazlar
    - **🖥️ Server**: Hizmet sunan cihazlar (genellikle veri merkezlerinde)

### 🔗 İletişim Bağlantıları

- **🌊 Fiber optik**: Yüksek hız, uzun mesafe
- **🔌 Bakır kablo**: Ekonomik, yaygın kullanım
- **📡 Radyo dalgaları**: Kablosuz bağlantı
- **🛰️ Uydu**: Geniş coğrafi kapsama

> ⚡ Bandwidth (Bant Genişliği)Transmission Rate olarak da bilinir. Saniye başına iletilebilen bit miktarını ifade eder (bps - bit per second).
> 

### 🔄 Packet Switches

Paketleri yönlendiren akıllı cihazlar:
- **🌐 Routers**: Ağlar arası yönlendirme
- **🔀 Switches**: Yerel ağ içi yönlendirme

- 📊 **Diagram Önerisi: Internet Topolojisi**
    
    ```
    🏠 Ev Kullanıcısı ── 🔗 DSL/Cable ── 🌐 Router ── 🏢 ISP
                                            │
    📱 Mobil Cihaz ──── 📡 4G/5G ─────────┘
                                            │
    🏢 Şirket ──────── 🔌 Ethernet ────────┘
    ```
    

---

### 🌍 Internet’in Ağ Tanımı

> 🔗 “Network of Networks”
Internet, birbirine bağlı ağların oluşturduğu küresel bir ağ sistemidir.
> 

### 🏢 ISP’ler (Internet Service Providers)

- **Tier 1**: Global seviye ISP’ler
- **Tier 2**: Bölgesel ISP’ler
- **Tier 3**: Yerel ISP’ler

### 📋 Protokoller

Mesaj gönderme/alma süreçlerini kontrol eden kurallar:

| Protokol | Kullanım Alanı | Katman |
| --- | --- | --- |
| **TCP** | Güvenilir veri transferi | Transport |
| **IP** | Adreslemе ve yönlendirme | Network |
| **HTTP** | Web sayfası transferi | Application |
| **802.11** | WiFi iletişimi | Link |

### 🏛️ Internet Standards

- **📄 RFC**: Request for Comments
- **🔬 IETF**: Internet Engineering Task Force
- **🌐 ITU**: International Telecommunication Union

> 📝 Özet Callout
Internet = Milyarlarca cihaz + İletişim bağlantıları + Packet switches + Protokoller + Standartlar
> 

---

## 📝 Protokol Nedir?

### 👥 İnsan vs 🤖 Ağ Protokolleri

- 🔄 **Protokol Karşılaştırması**
    
    
    | 👥 İnsan Protokolleri | 🤖 Ağ Protokolleri |
    | --- | --- |
    | “Merhaba, nasılsınız?” | TCP SYN paketi |
    | “Saat kaç?” | HTTP GET request |
    | “Bir sorum var” | DNS query |
    | Tanışma selamlaşması | TCP 3-way handshake |
    | “Görüşürüz” | TCP FIN paketi |

> 🎯 Protokol Tanımı
Ağ varlıkları arasında gönderilen mesajların formatını, sırasını ve mesaj iletimi/alımında alınan eylemleri tanımlayan kurallar bütünüdür.
> 

### 🔄 Protokol Bileşenleri

1. **📝 Format**: Mesaj yapısı ve içeriği
2. **⏰ Timing**: Mesaj gönderme zamanlaması
3. **🎬 Actions**: Alınan eylemlер

---

## 🏗️ Ağ Yapısına Yakından Bakış

### 🎯 Üç Ana Bileşen

### 1️⃣ 📍 Network Edge (Ağ Kenarı)

> 🏠 Son Kullanıcı Bölgesi
- 👤 Clients: Hizmet isteyen cihazlar
- 🖥️ Servers: Hizmet sunan cihazlar (genellikle veri merkezlerinde)
> 

### 2️⃣ 🔗 Access Networks & Physical Media

> 🌉 Bağlantı Köprüsü
- Kablolu iletişim bağlantıları
- Kablosuz iletişim bağlantıları
> 

### 3️⃣ 🌐 Network Core (Ağ Çekirdeği)

> 🧠 Ağın Beyni
- Birbirine bağlı router’ların oluşturduğu mesh yapı
- Network of networks mimarisi
> 
- 📊 **Diagram Önerisi: Ağ Yapısı**
    
    ```
        🏠 Edge              🌉 Access           🌐 Core
    ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
    │ 💻 Client   │────▶│ 🔗 ISP      │────▶│ 🌐 Router   │
    │ 🖥️ Server   │     │ 📡 Wireless │     │ 🔄 Switch   │
    │ 📱 Mobile   │     │ 🔌 Cable    │     │ 🌍 Backbone │
    └─────────────┘     └─────────────┘     └─────────────┘
    ```
    

---

## 🔗 Access Networks (Erişim Ağları)

### 📞 DSL (Digital Subscriber Line)

> 🏠 Ev DSL Bağlantısı
Mevcut telefon hattını kullanarak internet erişimi sağlar.
> 

### 🔧 Teknik Özellikler

- **📞 DSLAM** (DSL Access Multiplexer) ile merkezi ofise bağlantı
- **🎵 Ses** ve **💾 veri** farklı frekanslarda iletim
- **⬆️ Upstream**: < 2.5 Mbps (genellikle < 1 Mbps)
- **⬇️ Downstream**: < 24 Mbps (genellikle < 10 Mbps)
- 📊 **DSL Frekans Bölümü**
    
    
    | Frekans Bandı | Kullanım | Hız |
    | --- | --- | --- |
    | 0-4 kHz | 📞 Ses | N/A |
    | 25-200 kHz | ⬆️ Upstream | < 2.5 Mbps |
    | 200 kHz-1 MHz | ⬇️ Downstream | < 24 Mbps |

---

### 📺 Cable Network

> 🏢 Kablo TV Altyapısı
TV kablo altyapısını kullanarak internet hizmeti sunar.
> 

### 🌊 Frequency Division Multiplexing (FDM)

- Farklı kanallar farklı frekans bantlarında
- **📺 Video kanalları**: Broadcast
- **💻 Data kanalları**: Bidirectional
- **🎛️ Kontrol kanalları**: Ağ yönetimi

### 🏠 Home Network Yapısı

- 🏠 **Tipik Ev Ağı Bileşenleri**
    
    ```
    Internet ── 📡 Modem ── 🌐 Router ── 🔀 Switch
                              │
                              ├── 💻 Laptop (WiFi)
                              ├── 📱 Phone (WiFi)
                              ├── 🖥️ PC (Ethernet)
                              └── 📺 Smart TV (Ethernet)
    ```
    

### 🔧 Bileşenler

- **📡 Cable/DSL modem**: Internet bağlantısı
- **🌐 Router**: Yönlendirme + WiFi
- **🛡️ Firewall + NAT**: Güvenlik
- **🔌 Wired Ethernet**: 1 Gbps
- **📡 Wireless Access Point**: 54-450 Mbps

---

### 🏢 Enterprise Networks (Ethernet)

> 🏢 Kurumsal Ağlar
Şirketler ve üniversiteler için yüksek performanslı ağ çözümleri.
> 

### ⚡ Transmission Rates

| Standart | Hız | Kullanım |
| --- | --- | --- |
| Fast Ethernet | 100 Mbps | 🏠 Küçük ofisler |
| Gigabit Ethernet | 1 Gbps | 🏢 Standart kurumsal |
| 10 Gigabit Ethernet | 10 Gbps | 🏭 Yüksek performans |
| 100 Gigabit Ethernet | 100 Gbps | 🌐 Backbone |

---

### 📡 Wireless Access Networks

### 📶 Wireless LANs

> 🏠 Yerel Kablosuz Ağlar
Bina içi kısa mesafe kablosuz bağlantı.
> 
- **📏 Kapsama**: ~30 metre
- **📡 802.11 Standartları**:
    - **802.11b**: 11 Mbps
    - **802.11g**: 54 Mbps
    - **802.11n**: 450 Mbps
    - **802.11ac**: 1.3 Gbps

### 📱 Wide-area Wireless

> 🗼 Geniş Alan Kablosuz
Cellular operatörler tarafından sağlanan geniş kapsama.
> 
- **📏 Kapsama**: 10’larca km
- **📊 Hız**: 1-100 Mbps
- **🔢 Teknolojiler**: 3G, 4G LTE, 5G
- 📈 **Kablosuz Teknoloji Evrimi**
    
    
    | Nesil | Teknoloji | Tipik Hız | Gecikme |
    | --- | --- | --- | --- |
    | 2G | GSM | 64 Kbps | ~500ms |
    | 3G | UMTS | 2 Mbps | ~100ms |
    | 4G | LTE | 50 Mbps | ~20ms |
    | 5G | NR | 1 Gbps | <1ms |

> 📝 Bölüm Özeti
Erişim ağları, son kullanıcıları Internet çekirdeğine bağlayan çeşitli teknolojilerdir: DSL, Cable, Ethernet, WiFi ve Cellular.
> 

---

## 🔌 Physical Media (Fiziksel Ortam)

### 🎯 Guided Media (Yönlendirilmiş Ortam)

### 🌀 Twisted Pair (TP)

> 🔗 Bükümlü Çift Kablo
İki yalıtılmış bakır telin birbirine bükülmesiyle oluşan kablo.
> 
- **🏷️ Category 5**: 100 Mbps, 1 Gbps Ethernet
- **🏷️ Category 6**: 10 Gbps
- **💰 Maliyet**: Düşük
- **📏 Mesafe**: Kısa-orta (100m)

### 🔄 Coaxial Cable

> 📺 Eş Eksenli Kablo
TV ve internet için kullanılan kalın kablo.
> 
- **🔧 Yapı**: İki eş merkezli bakır iletken
- **↔︎️ İletim**: Çift yönlü
- **📡 Kullanım**: Broadband, kabel TV
- **🌊 Özellik**: Kabel üzerinde çoklu kanal

### 💎 Fiber Optic Cable

> ✨ Işık Hızında İletim
Cam fiber üzerinden ışık darbeleriyle veri iletimi.
> 

### ⚡ Avantajları

- **🚀 Yüksek Hız**: 10-100 Gbps
- **🎯 Düşük Hata**: Minimal bit error
- **🛡️ Bağışıklık**: Elektromanyetik gürültüye karşı
- **📏 Uzun Mesafe**: Km’lerce kayıpsız iletim

### ⚠️ Dezavantajları

- **💰 Yüksek Maliyet**: Kablo + ekipman
- **🔧 Zor Kurulum**: Özel tekniker gerekli

---

### 📡 Unguided Media (Yönlendirilmemiş Ortam)

### 📻 Radio Waves

> 🌊 Elektromanyetik Spectrum
Fiziksel kablo gerektirmeyen kablosuz iletim.
> 

### 🔧 Özellikler

- **🌊 Sinyal**: Elektromanyetik spektrumda
- **🚫 Kablo**: Fiziksel bağlantı yok
- **↔︎️ İletim**: Çift yönlü
- **🌍 Kapsama**: Metre’den km’ye değişken

### ⚠️ Sorunlar

- **🪞 Yansıma**: Duvarlar, binalar
- **🚧 Engelleme**: Fiziksel objeler
- **📡 Parazit**: Diğer sinyallerle karışma
- 📊 **Radio Link Türleri Karşılaştırması**
    
    
    | Tip | Hız | Kapsama | Gecikme | Kullanım |
    | --- | --- | --- | --- | --- |
    | 📶 **WiFi** | 54-1300 Mbps | 30m | <1ms | 🏠 LAN |
    | 📱 **Cellular** | 1-100 Mbps | 10km | 20ms | 📱 Mobile |
    | 🗼 **Microwave** | 45 Mbps | 50km | <1ms | 🏢 P2P |
    | 🛰️ **Satellite** | 1-45 Mbps | Global | 270ms | 🌍 Remote |

> 📝 Bölüm Özeti
Fiziksel medya, veriyi aktaran ortamdır. Guided media (TP, Coax, Fiber) kablo kullanırken, unguided media (Radio) kablosuz iletim sağlar.
> 

---

## 🧠 Network Core (Ağ Çekirdeği)

### 📦 Packet Switching Temelleri

> 📬 Paket Mantığı
Büyük mesajlar küçük paketlere bölünerek daha verimli iletim sağlanır.
> 

### 🔄 İşlem Adımları

1. **📝 Hosts**: Uygulama mesajlarını **paketlere** böler
2. **🌐 Routers**: Paketleri router’dan router’a iletir
3. **⚡ Capacity**: Her paket tam link kapasitesinde iletilir
4. **🎯 Destination**: Hedefte paketler birleştirilir

---

### 📥 Store-and-Forward Prensibi

> ⏳ Bekle ve İlet
Router, paketi tamamen alana kadar sonraki link’e iletemez.
> 

### 🧮 Gecikme Hesabı

- **📏 L**: Paket uzunluğu (bit)
- **⚡ R**: Link hızı (bps)
- **⏱️ İletim Süresi**: L/R saniye
- 📊 **Store-and-Forward Örneği**
    
    ```
    Kaynak ──[L/R]── Router ──[L/R]── Hedef
       📦               📦              📦
    
    End-to-end gecikme = 2L/R
    (propagation delay = 0 varsayımıyla)
    ```
    

### 🔢 Örnek Hesaplama

- **📦 L = 7.5 Mbits**
- **⚡ R = 1.5 Mbps**
- **⏱️ İletim gecikmesi = 15 saniye**

---

### 📊 Queueing ve Loss

### 🚦 Queueing (Kuyruk Oluşma)

> ⏳ Trafik Sıkışması
Gelen trafik > çıkan kapasitesi durumunda paketler kuyrukta bekler.
> 
- **📈 Sebep**: Arrival rate > transmission rate
- **⏰ Sonuç**: Paketler buffer’da bekler
- **📏 Buffer**: Sınırlı kapasiteli geçici depolama

### ❌ Packet Loss

> 🗑️ Paket Kaybı
Buffer dolduğunda yeni gelen paketler atılır.
> 

**Loss durumları**:
- Buffer tamamen dolu
- Yeni paket gelir → **DROP!**
- İletim kalitesi düşer

- 📊 **Queueing Örnek Senaryo**
    
    ```
    Gelen: 📦📦📦📦 (100 Mbps)
          ↓
       [Buffer: 📦📦📦]
          ↓
    Çıkan: 📦 (10 Mbps)
    
    Sonuç: Queueing delay + Buffer overflow riski
    ```
    

---

### 🧭 Routing vs Forwarding

### 🗺️ Routing (Yönlendirme)

> 🎯 Rota Planlama
Source-destination arası en iyi yolu belirleme süreci.
> 
- **🧠 Routing Algorithms**: Dijkstra, Bellman-Ford
- **📋 Routing Table**: Router’daki yol tablosu
- **🔄 Dynamic**: Ağ durumuna göre güncellenir

### ➡️ Forwarding (İletme)

> 🚀 Paket Yönlendirme
Gelen paketi uygun çıkış portuna yönlendirme.
> 
- **⚡ Hız**: Nanosaniye seviyesinde
- **📋 Forwarding Table**: Yerel arama tablosu
- **🎯 Lookup**: Destination IP → Output port
- 🔄 **Routing vs Forwarding Analojisi**
    
    
    | 🗺️ Routing | ➡️ Forwarding |
    | --- | --- |
    | GPS ile rota planla | Kavşakta sağa dön |
    | Şehirler arası yol | Sokak içi yönlendirme |
    | Stratejik karar | Operasyonel eylem |
    | Dakikalar/saatler | Mikrosaniyeler |

> 📝 Bölüm Özeti
Network Core, packet switching prensibini kullanarak store-and-forward, queueing/loss yönetimi ve routing/forwarding işlemlerini gerçekleştirir.
> 

---

## 🌍 Internet Yapısı: Network of Networks

### 🏗️ Evrim Süreci

### 1️⃣ 🤔 Problem: ISP Bağlantısı

> ❓ Soru: Milyonlarca access ISP nasıl birbirine bağlanır?
> 

### 2️⃣ ❌ Çözüm 1: Mesh Topoloji

- **🔗 Yaklaşım**: Her ISP diğer hepsine bağlansın
- **📊 Sonuç**: O(N²) bağlantı sayısı
- **⚠️ Problem**: Ölçeklenmiyor!

### 3️⃣ ✅ Çözüm 2: Hub Yaklaşımı

- **🌐 Global Transit ISP**: Merkezi bağlantı sağlayıcı
- **💰 Rekabet**: Multiple global ISP’ler
- **🔗 Interconnection**: ISP’ler arası bağlantı

### 4️⃣ 🎯 Modern Internet Yapısı

- 🏗️ **Internet Hiyerarşisi**
    
    ```
            🌍 Tier-1 ISPs (Global)
                  │
            🌎 Tier-2 ISPs (Regional)
                  │
            🏙️ Tier-3 ISPs (Local)
                  │
            🏠 End Users (Access)
    
    🔗 IXP (Internet Exchange Points)
    🤝 Peering Links (Direct connections)
    ```
    

### 🔗 Bağlantı Mekanizmaları

### 🏢 IXP (Internet Exchange Point)

> 🤝 Buluşma Noktası
ISP’lerin trafiklerini değiştireceği fiziksel lokasyonlar.
> 
- **📍 Lokasyon**: Büyük şehirlerde veri merkezleri
- **💱 İşlev**: Trafik değişimi (peering)
- **💰 Maliyet**: Transit maliyetlerini azaltır

### 🤝 Peering Links

> 🔗 Doğrudan Bağlantı
İki ISP arasında doğrudan kurulan özel bağlantılar.
> 

**Peering türleri**:
- **🆓 Settlement-free**: Ücretsiz trafik değişimi
- **💰 Paid peering**: Ücretli anlaşmalar
- **🚫 Selective peering**: Seçici partnerlık

### 📊 Content Provider Networks

> 🏢 İçerik Devi Stratejisi
Google, Netflix, Facebook gibi şirketlerin özel ağ stratejisi.
> 

### 🎯 Motivasyon

- **💰 Maliyet**: Transit ISP ücretlerinden kaçınma
- **⚡ Performans**: Son kullanıcıya daha yakın içerik
- **🎛️ Kontrol**: Trafiği kendi ağında yönetme

### 🌐 CDN (Content Delivery Network)

- **📍 Edge Servers**: Kullanıcılara yakın sunucular
- **📦 Cache**: Popüler içeriklerin yerel kopyaları
- **🚀 Hız**: Azaltılmış gecikme ve yük

> 📝 Bölüm Özeti
Internet, hiyerarşik ISP yapısından evrimleşerek karmaşık bir “network of networks” haline gelmiştir. IXP’ler ve peering linkler verimli bağlantı sağlarken, content provider’lar kendi ağlarını kurarak kontrolü artırmaktadır.
> 

---

## ⏰ Delay (Gecikme) ve Loss (Kayıp)

### 🧮 Dört Gecikme Türü

> ⏱️ Toplam Nodal Gecikmed_nodal = d_proc + d_queue + d_trans + d_prop
> 

### 1️⃣ 🔍 Processing Delay (d_proc)

> 🧠 İşlem Gecikmesi
Router’ın paketi analiz etmesi için gereken süre.
> 

**İşlemler**:
- **🔍 Bit hata kontrolü**: Checksum verification
- **🗺️ Routing table lookup**: Çıkış link belirleme
- **📊 Header processing**: Paket başlığı analizi

**⏰ Süre**: Genellikle < 1 msec

### 2️⃣ 📊 Queueing Delay (d_queue)

> 🚦 Kuyruk Gecikmesi
Çıkış link’te iletim için bekleme süresi.
> 

**Faktörler**:
- **📈 Trafik yoğunluğu**: Router’daki paket sayısı
- **⚡ Link kapasitesi**: Çıkış bandwith’i
- **📦 Paket boyutu**: Büyük paketler = uzun bekleme

**⏰ Süre**: 0 msec’den saniye’lere değişken

### 3️⃣ 📡 Transmission Delay (d_trans)

> 🚀 İletim Gecikmesi
Paketi link’e tamamen gönderme süresi.
> 

**📊 Formül**: `d_trans = L/R`
- **L**: Paket uzunluğu (bit)
- **R**: Link bandwidth (bps)

- 🧮 **Transmission Delay Örnekleri**
    
    
    | Paket Boyutu | Link Hızı | İletim Gecikmesi |
    | --- | --- | --- |
    | 1000 bit | 1 Mbps | 1 ms |
    | 1000 bit | 100 Mbps | 0.01 ms |
    | 1 MB (8×10⁶ bit) | 1 Gbps | 8 ms |

### 4️⃣ 🌊 Propagation Delay (d_prop)

> 💨 Yayılma Gecikmesi
Sinyalin link boyunca yayılma süresi.
> 

**📊 Formül**: `d_prop = d/s`
- **d**: Fiziksel link uzunluğu (metre)
- **s**: Yayılma hızı (~2×10⁸ m/sec)

- 🌍 **Propagation Delay Örnekleri**
    
    
    | Mesafe | Ortam | Yayılma Gecikmesi |
    | --- | --- | --- |
    | 100m | Ethernet | 0.5 μs |
    | 3000km | Fiber | 15 ms |
    | 36000km | Uydu | 180 ms |

---

### 📊 Queueing Delay Detayı

### 🔢 Traffic Intensity

> 📈 Trafik Yoğunluğuρ = La/R
> 

**Parametreler**:
- **L**: Ortalama paket uzunluğu (bit)
- **a**: Ortalama paket geliş oranı (paket/sn)
- **R**: Link bandwidth (bps)

### 📊 Yoğunluk Kuralları

- 📈 **Traffic Intensity Davranışı**
    
    
    | Traffic Intensity | Queueing Delay | Durum |
    | --- | --- | --- |
    | **ρ ~ 0** | ≈ 0 | 🟢 İdeal |
    | **ρ = 0.5** | Küçük | 🟡 Normal |
    | **ρ = 0.8** | Orta | 🟠 Dikkat |
    | **ρ ≥ 0.9** | Büyük | 🔴 Kritik |
    | **ρ ≥ 1** | ∞ | ⚫ Tıkanma |

> ⚠️ Kritik Nokta
ρ ≥ 1 durumunda sistem kararsızlaşır ve ortalama gecikme sonsuza gider!
> 

---

### 🔍 Traceroute Aracı

> 🛠️ Ağ Tanılama
Kaynak-hedef arası gerçek gecikmeleri ölçen araç.
> 

### 🔧 Çalışma Prensibi

1. **📡 3 Probe**: Her router’a 3 test paketi gönder
2. **⏰ TTL**: Time-To-Live değeri ile hop sayısını kontrol et
3. **📥 Response**: Router’dan gelen yanıt süresini ölç
4. **📊 Report**: Her hop için min/avg/max gecikme
- 🖥️ **Traceroute Örnek Çıktı**
    
    ```bash
    traceroute google.com
    1  gateway (192.168.1.1)  1.2ms  1.1ms  1.3ms
    2  isp-router (10.0.0.1)  15.2ms  14.8ms  15.5ms
    3  regional (203.123.45.1)  45.3ms  44.9ms  46.1ms
    4  backbone (8.8.8.8)  78.2ms  77.8ms  79.1ms
    ```
    

> 📝 Bölüm Özeti
Ağ gecikmesi dört bileşenden oluşur: processing, queueing, transmission ve propagation. Traffic intensity queueing delay’in ana belirleyicisidir ve 1’e yaklaştıkça sistem kararsızlaşır.
> 

---

## 📈 Throughput (İş Hacmi)

### 🎯 Throughput Tanımı

> 📊 Veri Transfer Oranı
Gönderici/alıcı arası gerçek bit transfer hızı.
> 

### 📏 Ölçüm Türleri

- **⚡ Instantaneous**: Belirli andaki anlık oran
- **📊 Average**: Uzun süre boyunca ortalama oran
- **🏁 End-to-end**: Kaynak-hedef arası toplam performans

### 🔗 Bottleneck Link Kavramı

> 🚧 Darboğaz
End-to-end path’teki en yavaş link throughput’u sınırlar.
> 

### 🔍 Basit Senaryo

**İki Link**: Rs (kaynak) ↔︎ Rc (hedef)

- ⚖️ **Bottleneck Analizi**
    
    
    | Durum | Throughput | Darboğaz |
    | --- | --- | --- |
    | **Rs < Rc** | Rs | 📡 Kaynak link |
    | **Rs > Rc** | Rc | 🎯 Hedef link |
    | **Rs = Rc** | Rs = Rc | ⚖️ Dengeli |

### 🧮 Örnek Hesaplama

- **📡 Rs = 2 Mbps** (DSL upstream)
- **🎯 Rc = 1 Gbps** (Ethernet)
- **📊 Sonuç**: Throughput = 2 Mbps (DSL bottleneck)

### 🌐 Internet Senaryosu

> 🛣️ Çoklu Link Yapısı
Gerçek Internet’te çok sayıda bağlantı ve router bulunur.
> 

### 🔢 N-Connection Modeli

- **🏢 10 bağlantı** backbone link R’yi paylaşır
- **📊 Her bağlantı** için throughput hesabı

**📊 Formül**: `Per-connection throughput = min(Rc, Rs, R/10)`

- 📊 **Gerçek Dünya Senaryoları**
    
    
    | Bağlantı Türü | Tipik Rc | Tipik Rs | Backbone R | Bottleneck |
    | --- | --- | --- | --- | --- |
    | 🏠 Home | 100 Mbps | 10 Mbps | 1 Gbps | 📡 Upload |
    | 🏢 Office | 1 Gbps | 1 Gbps | 10 Gbps | 🌐 Backbone |
    | 📱 Mobile | 50 Mbps | 10 Mbps | 1 Gbps | 📡 Cellular |

### 🎯 Pratik Sonuç

> 💡 Gerçek Hayat
Çoğu durumda Rc veya Rs bottleneck olur, backbone değil!
> 

**Nedenler**:
- **💰 Maliyet**: Access link’ler backbone’dan pahalı
- **📏 Mesafe**: “Last mile” problemi
- **🏠 Kullanıcı**: Ev internet paketleri sınırlı

> 📝 Bölüm Özeti
Throughput, darboğaz (bottleneck) link tarafından belirlenir. Gerçek hayatta genellikle access link’ler (DSL, cable, cellular) backbone’dan yavaş olduğu için bottleneck oluştururlar.
> 

---

## 📚 Protocol Layers (Protokol Katmanları)

### 🏗️ Internet Protocol Stack

> 🏛️ 5 Katmanlı Mimari
Her katman belirli sorumlulukları olan modüler yapı.
> 

### 5️⃣ 📱 Application Layer

> 🎯 Ağ Uygulamaları
Son kullanıcı uygulamalarını destekler.
> 

**🛠️ Protokoller**:
- **🌐 HTTP/HTTPS**: Web sayfası transferi
- **📧 SMTP**: E-mail gönderimi
- **📨 IMAP/POP3**: E-mail alma
- **📁 FTP**: Dosya transferi
- **🌍 DNS**: Domain name çözümleme

### 4️⃣ 🚛 Transport Layer

> 📦 Process-to-Process İletim
Uygulamalar arası güvenilir veri transferi.
> 

**🛠️ Protokoller**:
- **✅ TCP**: Güvenilir, sıralı, hata kontrolü
- **⚡ UDP**: Hızlı, basit, güvenilirlik yok

### 3️⃣ 🗺️ Network Layer

> 🧭 End-to-End Routing
Kaynak-hedef arası yol bulma ve adreslemе.
> 

**🛠️ Protokoller**:
- **🌐 IP**: Internet Protocol (IPv4/IPv6)
- **🗺️ OSPF**: Open Shortest Path First
- **🔄 BGP**: Border Gateway Protocol

### 2️⃣ 🔗 Link Layer

> 🤝 Hop-to-Hop İletim
Komşu ağ elemanları arası veri transferi.
> 

**🛠️ Protokoller**:
- **🔌 Ethernet**: Kablolu LAN
- **📡 802.11**: WiFi
- **📞 PPP**: Point-to-Point Protocol

### 1️⃣ ⚡ Physical Layer

> 🔌 Bit İletimi
Elektriksel/optik sinyaller üzerinde raw bit transferi.
> 

**🛠️ Media**:
- **🔌 Ethernet cable**: Elektriksel sinyal
- **📡 WiFi**: Radyo dalgaları

- **💎 Fiber**: Işık darbeleri

- 📊 **Katman Sorumlulukları Tablosu**
    
    
    | Katman | Temel Sorumluluk | Veri Birimi | Örnek |
    | --- | --- | --- | --- |
    | **Application** | Uygulamaya özel protokoller | Message | HTTP GET |
    | **Transport** | Process-to-process teslimat | Segment | TCP segment |
    | **Network** | Host-to-host yönlendirme | Datagram | IP packet |
    | **Link** | Node-to-node iletim | Frame | Ethernet frame |
    | **Physical** | Bit iletimi | Bit | Elektrik sinyali |

---

### 🏛️ ISO/OSI Reference Model

> 📚 7 Katmanlı Model
Internet stack’ten daha detaylı teorik model.
> 

### 🆚 Internet vs OSI Karşılaştırması

- 📊 **Model Karşılaştırması**
    
    
    | OSI Katmanı | Internet Katmanı | Açıklama |
    | --- | --- | --- |
    | **Application** | **Application** | ✅ Aynı |
    | **Presentation** | *(Application içinde)* | 🔐 Şifreleme, sıkıştırma |
    | **Session** | *(Application içinde)* | 🔄 Oturum yönetimi |
    | **Transport** | **Transport** | ✅ Aynı |
    | **Network** | **Network** | ✅ Aynı |
    | **Data Link** | **Link** | ✅ Aynı |
    | **Physical** | **Physical** | ✅ Aynı |

### 📋 Eksik Katmanlar

**🔐 Presentation Layer**:
- Şifreleme/deşifreleme
- Data compression
- Makine-spesifik veri formatları

**🔄 Session Layer**:
- Dialog kontrolü
- Checkpointing
- Recovery mechanisms

> 💡 Internet Yaklaşımı
Bu servisler gerekirse application layer’da implement edilir!
> 

---

### 📦 Encapsulation (Kapsülleme)

> 🎁 Sarma Süreci
Her katman kendi header’ını ekleyerek veriyi kapsüller.
> 

### 🔄 Encapsulation Süreci

- 📦 **Veri Dönüşüm Süreci**
    
    ```
    Application: 📄 Message
         ↓ +Header
    Transport:   📦 Segment [Ht|📄]
         ↓ +Header
    Network:     📮 Datagram [Hn|Ht|📄]
         ↓ +Header
    Link:        📬 Frame [Hl|Hn|Ht|📄|Tl]
         ↓
    Physical:    ⚡ Bits 01101001...
    ```
    

### 🏷️ Header İçerikleri

- **🌐 Network (Hn)**: Source/destination IP
- **🚛 Transport (Ht)**: Source/destination port, sequence#
- **🔗 Link (Hl)**: Source/destination MAC address
- **🔚 Link Trailer (Tl)**: Error detection

### 🔧 Cihaz İşlem Seviyeleri

- 🖥️ **Cihaz Protokol İşleme**
    
    
    | Cihaz | İşlenen Katmanlar | Sebep |
    | --- | --- | --- |
    | **🏠 Host** | 1-5 (Tümü) | Full stack implementation |
    | **🌐 Router** | 1-3 (Physical-Network) | Routing decisions |
    | **🔀 Switch** | 1-2 (Physical-Link) | MAC address forwarding |
    | **🔌 Hub** | 1 (Physical) | Simple bit repeater |

> 📝 Bölüm Özeti
Protocol layers modüler tasarım sağlar. Internet 5-layer stack kullanırken OSI 7-layer theoretical model’dir. Encapsulation her katmanın header eklemesi ile gerçekleşir.
> 

---

## 🛡️ Network Security (Ağ Güvenliği)

### 🎯 Güvenlik Alanları

> 🔒 3 Ana Hedef
Ağ güvenliğinin kapsamlı yaklaşımı.
> 
1. **🔍 Saldırı Analizi**: Kötü niyetli saldırılar nasıl yapılır?
2. **🛡️ Koruma**: Ağlar nasıl korunur?
3. **🏗️ Güvenli Tasarım**: Saldırılara karşı bağışık mimariler

---

### 🦠 Malware Saldırıları

### 🦠 Malware Türleri

- 🦠 **Malware Sınıflandırması**
    
    
    | Tür | Bulaşma | Çalışma | Zarar |
    | --- | --- | --- | --- |
    | **🦠 Virus** | 📧 E-mail eki | 👤 Kullanıcı çalıştırır | 📁 Dosya hasar |
    | **🐛 Worm** | 🌐 Ağ otomatik | 🤖 Kendini çalıştırır | 🌊 Ağ yayılması |
    | **🕵️ Spyware** | 🎭 Gizli kurulum | 👀 Gizli çalışır | 🔍 Bilgi çalma |

### 🦠 Virus

> 📧 E-mail Eki Saldırısı
Kullanıcı etkileşimi gerektiren kötü niyetli kod.
> 

**Özellikler**:
- **📎 Taşıyıcı**: E-mail eki, USB, indirilen dosya
- **👤 Aktivasyon**: Kullanıcı çalıştırması gerekli
- **🎯 Hedef**: Dosya sistemi hasar, veri çalma

### 🐛 Worm

> 🌊 Kendini Yayan Kod
Ağ üzerinden otomatik yayılan kötü niyetli yazılım.
> 

**Özellikler**:
- **🤖 Otomatik**: Kullanıcı etkileşimi gerektirmez
- **🌐 Yayılma**: Ağ zafiyetlerini kullanır
- **⚡ Hız**: Eksponansiyel yayılma

### 🕵️ Spyware

> 👀 Gizli Gözetleme
Kullanıcı faaliyetlerini gizlice kaydetmе.
> 

**Toplanan veriler**:
- **⌨️ Keylogger**: Tuş vuruşları
- **🌐 Browser**: Ziyaret edilen siteler

- **💳 Credentials**: Kullanıcı adı/şifre
- **📊 Habits**: Kullanım alışkanlıkları

### 🤖 Botnet

> 🕷️ Zombie Ağı
Ele geçirilmiş bilgisayarların oluşturduğu kontrollü ağ.
> 

### 🔧 Botnet Mimarisi

1. **🎯 Enfeksiyon**: Malware ile host ele geçirme
2. **📡 C&C Server**: Command & Control sunucusu
3. **🤖 Bot**: Kontrol edilebilen zombie host
4. **👤 Botmaster**: Ağı kontrol eden saldırgan

**🎭 Kullanım alanları**:
- **📧 Spam**: Toplu e-mail gönderimi
- **⚔️ DDoS**: Distributed Denial of Service
- **🔍 Mining**: Kripto para madenciliği
- **💳 Banking**: Finansal bilgi çalma

---

### ⚔️ DoS (Denial of Service) Saldırıları

> 🚫 Hizmet Engelleme
Meşru kullanıcıların hizmete erişimini engelleme.
> 

### 🎯 DDoS (Distributed DoS) Süreci

- ⚔️ **DDoS Saldırı Adımları**
    
    ```
    1. 🎯 Hedef Seçimi
       Target: web server, DNS server
    
    2. 🤖 Botnet Hazırlama
       1000'lerce enfekte host
    
    3. ⚔️ Koordineli Saldırı
       📦📦📦 → 🎯 Target
       📦📦📦 → 🎯 Target
       📦📦📦 → 🎯 Target
    
    4. 🚫 Hizmet Çökmesi
       Server overload → legitimate users rejected
    ```
    

### 📊 DDoS Türleri

| Saldırı Türü | Hedef | Yöntem | Savunma |
| --- | --- | --- | --- |
| **🌊 Volume** | Bandwidth | UDP flood | Rate limiting |
| **📦 Protocol** | Routing tables | SYN flood | SYN cookies |
| **🎯 Application** | Web services | HTTP requests | Application firewalls |

---

### 🕵️ Diğer Saldırı Türleri

### 📡 Packet Sniffing

> 👂 Ağ Dinleme
Ağ trafiğini gizlice dinleyerek veri toplama.
> 

**Çalışma prensibi**:
- **📡 Broadcast ortam**: Ethernet, WiFi
- **🔍 Promiscuous mode**: Tüm paketleri oku
- **📊 Analysis**: Hassas veri arama

**🛡️ Korunma**:
- **🔐 Encryption**: HTTPS, VPN
- **🔀 Switched networks**: Broadcast trafiği azalt
- **🕵️ Detection**: Network monitoring

### 🎭 IP Spoofing

> 🎪 Kimlik Sahteciliği
Sahte kaynak IP adresi ile paket gönderme.
> 

**Saldırı senaryoları**:
- **🛡️ Firewall bypass**: Güvenlik duvarı atlatma
- **🤝 Trust exploitation**: Güven ilişkisi suistimali

- **🔄 Reflection attacks**: Yansıtma saldırıları

- 🎭 **IP Spoofing Örneği**
    
    ```
    Gerçek:
    🏠 Attacker (10.0.0.5) → 🎯 Target
    
    Sahte paket:
    📦 [Src: 192.168.1.100, Dst: Target, Data: Payload]
    🏠 Attacker → 🎯 Target
    
    Target görür:
    📦 Trusted source (192.168.1.100) → Target
    ```
    

**🛡️ Korunma**:
- **🔍 Ingress filtering**: ISP seviyesinde
- **🤝 Authentication**: Kuvvetli kimlik doğrulama
- **🔐 Cryptographic verification**: Digital signatures

> 📝 Bölüm Özeti
Network security, malware (virus, worm, spyware), DDoS saldırıları, packet sniffing ve IP spoofing gibi tehditlere karşı çok katmanlı savunma stratejisi gerektirir.
> 

---

## 📋 Özet ve Genel Değerlendirme

### ✅ Kapsanan Ana Konular

> 🎯 Öğrenme Hedefleri
Bu ders ile bilgisayar ağlarının temel kavramlarını ve çalışma prensiplerini öğrendiniz.
> 

### 🌐 Internet’e Genel Bakış

- **🔧 Nuts & Bolts**: Fiziksel bileşenler
- **🏗️ Network of Networks**: Hiyerarşik yapı
- **📋 Protocols**: İletişim kuralları

### 🏗️ Ağ Mimarisi

- **📍 Network Edge**: End systems
- **🌉 Access Networks**: Bağlantı teknolojileri
- **🧠 Network Core**: Packet switching

### ⚡ Performans Analizi

- **⏰ Delay**: Processing, queueing, transmission, propagation
- **❌ Loss**: Buffer overflow
- **📈 Throughput**: Bottleneck link analizi

### 📚 Protocol Stack

- **🏛️ Layering**: Modüler tasarım
- **📦 Encapsulation**: Header ekleme süreci
- **🔄 Service models**: Katmanlar arası ilişki

### 🛡️ Güvenlik Temelleri

- **🦠 Malware**: Virus, worm, spyware
- **⚔️ DDoS**: Hizmet engelleme saldırıları
- **🎭 Spoofing**: Kimlik sahteciliği

---