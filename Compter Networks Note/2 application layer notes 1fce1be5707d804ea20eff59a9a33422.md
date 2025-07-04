# 2 application layer notes

# 📱 Application Layer - Uygulama Katmanı

---

> 💡 Ders Hedefi
Ağ uygulamalarının nasıl çalıştığını, protokollerin yapısını ve socket programlama ile uygulama geliştirmeyi öğrenmek.
> 

---

## 🎯 Giriş ve Amaçlar

### 📚 Ana Hedefler

> 🎓 Öğrenme Çıktıları
Bu bölüm sonunda şunları öğrenmiş olacaksınız:
> 

### 🔍 Temel Kavramlar

- **📋 Protokol Kavramları**: Ağ uygulaması protokollerinin kavramsal ve uygulama yönleri
- **🚛 Transport Katmanı**: Servis modelleri ve gereksinimleri
- **🏗️ Mimari Paradigmaları**: Client-server ve peer-to-peer yaklaşımları
- **🌐 İçerik Dağıtımı**: CDN (Content Delivery Network) yapıları

### 🛠️ Praktik Protokoller

- **🌐 HTTP**: Web protokolü ve cache mekanizmaları
- **📁 FTP**: Dosya transfer protokolü
- **📧 E-Mail**: SMTP, POP3, IMAP protokolleri
- **🌍 DNS**: Domain Name System
- **🔌 Socket API**: Ağ uygulamaları geliştirme

---

### 📱 Ağ Uygulamaları Örnekleri

- 🌟 **Popüler Ağ Uygulamaları**
    
    
    | Kategori | Uygulamalar | Kullanım Alanı |
    | --- | --- | --- |
    | **📧 İletişim** | E-mail, WhatsApp, Telegram | Mesajlaşma |
    | **🌐 Web** | Chrome, Firefox, Safari | İnternet tarayıcıları |
    | **🎮 Oyun** | Online oyunlar, MMO | Çok kullanıcılı oyun |
    | **📺 Medya** | YouTube, Netflix, Spotify | Video/ses akışı |
    | **📞 VoIP** | Skype, Zoom, Teams | Sesli/görüntülü konuşma |
    | **📁 Dosya** | P2P, BitTorrent, FTP | Dosya paylaşımı |
    | **🔍 Arama** | Google, Bing, Yahoo | Arama motorları |
    | **👥 Sosyal** | Facebook, Twitter, Instagram | Sosyal ağlar |

> 📝 Önemli Not
Her uygulama farklı ağ gereksinimleri ve performans beklentileri olan protokoller kullanır.
> 

---

## 🏗️ Uygulama Mimarileri

### 🖥️ Client-Server Mimarisi

> 🏢 Merkezi Mimari
Geleneksel ve yaygın kullanılan ağ mimarisi türü.
> 

### 🖥️ Server Özellikleri

- **⚡ Her zaman aktif**: 7/24 hizmet veren host
- **🌐 Kalıcı IP adresi**: Sabit ağ konumu
- **🏭 Veri merkezleri**: Ölçeklendirme için server farm’ları
- **💾 Yüksek kapasite**: Büyük depolama ve işlem gücü

### 💻 Client Özellikleri

- **🔄 Aralıklı bağlantı**: İhtiyaç anında bağlanır
- **📱 Dinamik IP adresleri**: DHCP ile değişken adres
- **🚫 Direkt iletişim yok**: Client’lar birbirleriyle konuşmaz
- **📡 Server’a bağımlı**: Hizmet için server gerekli
- 📊 **Client-Server Diagram Örneği**
    
    ```
            🌐 Internet
                │
        ┌───────┴───────┐
        │   🖥️ Server   │ ← Kalıcı IP: 192.168.1.100
        │  (Port: 80)   │   Her zaman aktif
        └───────┬───────┘   Güçlü donanım
                │
        ═══════════════════
                │
        ┌───────┴───────┐
        │ 💻 Client #1  │ ← Dinamik IP
        │ 📱 Client #2  │   Aralıklı bağlantı
        │ 🖥️ Client #3  │   Server'a bağımlı
        └───────────────┘
    ```
    

### ✅ Avantajları

- **🛡️ Merkezi kontrol**: Güvenlik ve yönetim kolaylığı
- **📊 Performans**: Güçlü sunucu donanımı
- **🔒 Güvenlik**: Centralized security policies

### ❌ Dezavantajları

- **💰 Maliyet**: Pahalı sunucu altyapısı
- **⚡ Tek nokta hatası**: Server çökerse hizmet durur
- **📈 Ölçeklendirme**: Artan kullanıcı = daha güçlü server

---

### 🔄 Peer-to-Peer (P2P) Mimarisi

> 👥 Dağıtık Mimari
Eşler arası doğrudan iletişim kuran modern mimari.
> 

### 🌟 P2P Özellikleri

- **🚫 Merkezi server yok**: Her peer hem client hem server
- **🔄 Self-scalability**: Yeni peer = +kapasite +talep
- **📱 Aralıklı bağlantı**: Peer’lar gelip gidebilir
- **🌍 Dinamik IP**: Değişken ağ adresleri

### 🎯 P2P Avantajları

- **💰 Düşük maliyet**: Merkezi server gerekmez
- **📈 Ölçeklenebilirlik**: Kullanıcı artışı sistemi güçlendirir
- **🛡️ Fault tolerance**: Tek nokta hatası yok

### ⚠️ P2P Zorlukları

- **📶 Asimetrik bağlantı**: Upload < Download hızı
- **🔒 Güvenlik**: Merkezi kontrol eksikliği
- **👥 Peer bulma**: Dinamik peer discovery
- 🔄 **P2P vs Client-Server Karşılaştırması**
    
    
    | Özellik | 🖥️ Client-Server | 🔄 P2P |
    | --- | --- | --- |
    | **Merkezi Control** | ✅ Var | ❌ Yok |
    | **Ölçeklenebilirlik** | ⚠️ Sınırlı | ✅ Yüksek |
    | **Maliyet** | 💰 Yüksek | 💰 Düşük |
    | **Güvenlik** | 🛡️ Kolay | ⚠️ Zor |
    | **Performans** | ⚡ Tahmin edilebilir | 📊 Değişken |
    | **Bakım** | 🔧 Kolay | 🔧 Zor |

> 📝 Bölüm Özeti
Client-Server merkezi kontrol sunarken, P2P dağıtık ve ölçeklenebilir yapı sağlar. Her ikisinin de avantaj ve dezavantajları vardır.
> 

---

## 🔌 İşlem İletişimi ve Soketler

### 🧠 Temel Kavramlar

> 💻 Process (İşlem)
Bir host içinde çalışan program birimi.
> 

### 🏷️ Process Türleri

- **👤 Client Process**: İletişimi başlatan işlem
- **🖥️ Server Process**: İletişim için bekleyen işlem
- **📧 Example**: Web tarayıcısı (client) ↔︎ Web server (server)

### 🚪 Soketler (Sockets)

> 🚪 Socket = Kapı
İşlemlerin ağ üzerinden mesaj gönderip aldığı yazılım arayüzü.
> 

### 🔧 Socket Çalışma Prensibi

1. **📤 Mesaj gönderme**: Socket’ten dışarı
2. **🚛 Transport katmanı**: Güvenilir iletim
3. **📥 Mesaj alma**: Hedef socket’ten
4. **⚙️ OS kontrolü**: İşletim sistemi yönetimi
- 🔌 **Socket Diagram**
    
    ```
    Application Layer
         │ Mesaj
         ▼
    ┌──────────┐    📤    ┌──────────┐
    │  🚪 Socket │ ────▶ │  🚪 Socket │
    │ (Client) │         │ (Server) │
    └──────────┘    📥    └──────────┘
         │                     │
    Transport Layer      Transport Layer
         │                     │
        TCP/UDP               TCP/UDP
    ```
    

---

### 🏠 Adres Belirleme

> 📮 Ağ Adresi = IP + Port
Her network servisi benzersiz adres kombinasyonu gerektirir.
> 

### 🏷️ Adres Bileşenleri

- **🌐 IP Adresi (32-bit)**: Host’u tanımlar
- **🔢 Port Numarası (16-bit)**: Servis/process’i tanımlar

### 📊 Yaygın Port Numaraları

- 🔢 **Well-Known Port’lar**
    
    
    | Port | Protokol | Servis | Açıklama |
    | --- | --- | --- | --- |
    | **80** | HTTP | Web Server | HTTP trafiği |
    | **443** | HTTPS | Secure Web | SSL/TLS ile şifreli web |
    | **25** | SMTP | Mail Server | E-mail gönderimi |
    | **110** | POP3 | Mail Retrieval | E-mail alma |
    | **143** | IMAP | Mail Access | E-mail erişimi |
    | **53** | DNS | Name Resolution | Domain name çözümleme |
    | **21** | FTP | File Transfer | Dosya transferi |
    | **22** | SSH | Secure Shell | Güvenli uzak erişim |

### 🧮 Adres Örneği

- **🌐 www.google.com**: Host adı
- **🔢 IP: 142.250.185.46**: Numerik adres
- **🚪 Port 80**: HTTP servisi
- **📍 Full Address**: `142.250.185.46:80`

> 📝 Bölüm Özeti
Socket’ler, process’ler arası ağ iletişiminin temel arayüzüdür. IP adresi + Port numarası ile benzersiz servis adresleme sağlanır.
> 

---

## ⚡ Transport Servisi Gereksinimleri

### 🎯 Ana Gereksinimler

> 🔍 Uygulama İhtiyaçları
Farklı uygulamalar farklı network hizmet kalitesi bekler.
> 

### 1️⃣ 🛡️ Data Integrity (Veri Bütünlüğü)

- **✅ Kritik uygulamalar**: %100 güvenilir veri transferi
- **📁 Örnekler**: Dosya transferi, e-mail, web browsing
- **❌ Toleranslı uygulamalar**: Küçük kayıplar kabul edilebilir
- **🎵 Örnekler**: Ses/video streaming, online oyunlar

### 2️⃣ ⏰ Timing (Zaman Hassasiyeti)

- **🎮 Real-time uygulamalar**: < 100ms gecikme
- **📞 VoIP**: < 150ms konuşma kalitesi için
- **🎯 Online oyunlar**: < 50ms rekabetçi oyun için
- **📁 File transfer**: Timing önemli değil

### 3️⃣ 📈 Throughput (İş Hacmi)

- **🎵 Multimedia uygulamalar**: Minimum bant genişliği
- **📹 Video streaming**: 1-50 Mbps (kaliteye göre)
- **📞 VoIP**: 5-64 Kbps
- **📧 E-mail**: Elastik, düşük throughput yeterli

### 4️⃣ 🔒 Security (Güvenlik)

- **🔐 Şifreleme**: Veri gizliliği
- **✅ Authentication**: Kimlik doğrulama
- **🛡️ Integrity**: Veri bütünlüğü

---

### 📊 Uygulama Gereksinimleri Tablosu

- 📋 **Detaylı Gereksinim Analizi**
    
    
    | 📱 Uygulama | 🛡️ Veri Kaybı | 📈 Throughput | ⏰ Timing | 🔒 Security |
    | --- | --- | --- | --- | --- |
    | **📁 Dosya Transferi** | ❌ Kayıp yok | 🔄 Elastik | ❌ Hassas değil | ⚠️ Orta |
    | **📧 E-mail** | ❌ Kayıp yok | 🔄 Elastik | ❌ Hassas değil | ✅ Yüksek |
    | **🌐 Web Browsing** | ❌ Kayıp yok | 🔄 Elastik | ⚠️ Orta hassas | ✅ Yüksek |
    | **📞 VoIP** | ✅ Toleranslı | 📊 5-64 Kbps | ⚡ < 150ms | ⚠️ Orta |
    | **📹 Video Streaming** | ✅ Toleranslı | 📊 1-50 Mbps | ⚡ < 200ms | ⚠️ Orta |
    | **🎮 Online Oyun** | ✅ Toleranslı | 📊 Düşük | ⚡ < 50ms | 🛡️ Yüksek |
    | **💬 Instant Messaging** | ❌ Kayıp yok | 🔄 Çok düşük | ⚠️ Orta | ✅ Yüksek |

### 🎯 Kritik Faktörler

- **🏥 Mission-critical**: Veri bütünlüğü öncelik
- **🎮 Interactive**: Düşük gecikme öncelik
- **📺 Streaming**: Yeterli throughput öncelik
- **🔒 Financial**: Güvenlik öncelik

> 📝 Bölüm Özeti
Her uygulama türü kendine özgü ağ gereksinimleri vardır. Transport katmanı bu ihtiyaçları karşılayacak uygun servisi sağlamalıdır.
> 

---

## 🚛 Internet Transport Protokolleri

### ✅ TCP Servisi (Transmission Control Protocol)

> 🛡️ Güvenilir İletim
Internet’in ana güvenilir transport protokolü.
> 

### 🌟 TCP Özellikleri

### 🛡️ Güvenilir Transport

- **📦 Ordered delivery**: Sıralı veri teslimi
- **✅ Error detection**: Hata algılama ve düzeltme
- **🔄 Retransmission**: Kayıp paketleri yeniden gönderme
- **📋 Acknowledgment**: Teslim onayları

### 🌊 Flow Control

- **🚰 Rate matching**: Sender’ın hızını receiver’a göre ayarlama
- **📊 Window size**: Alma kapasitesine göre gönderim
- **⚖️ Buffer management**: Taşma önleme

### 🚦 Congestion Control

- **📈 Network monitoring**: Ağ durumu takibi
- **⬇️ Rate adaptation**: Tıkanıklıkta hız azaltma
- **🤝 Fair sharing**: Bant genişliği adil paylaşımı

### 🔗 Connection-Oriented

- **🤝 3-way handshake**: Bağlantı kurulumu
- **💾 State maintenance**: Bağlantı durumu takibi
- **👋 Connection termination**: Düzgün bağlantı sonlandırma

### ❌ TCP’nin Sağlamadıkları

- **⏰ Timing guarantees**: Zaman garantisi yok
- **📊 Minimum throughput**: Alt sınır throughput yok
- **🔒 Built-in security**: Dahili güvenlik yok
- 🔗 **TCP Bağlantı Kurulumu (3-Way Handshake)**
    
    ```
    Client                    Server
      │                         │
      │──── SYN ──────────────▶│  1. Bağlantı isteği
      │                         │
      │ ◀──── SYN+ACK ─────────│  2. Kabul + onay
      │                         │
      │──── ACK ──────────────▶│  3. Onay
      │                         │
      │ ◀══ Data Transfer ══▶ │  4. Veri transferi
    ```
    

---

### ⚡ UDP Servisi (User Datagram Protocol)

> 🚀 Hızlı ve Basit
Minimum özellikli, yüksek performanslı transport protokolü.
> 

### 🎯 UDP Özellikleri

- **📦 Unreliable**: Güvenilmez veri transferi
- **🔄 Connectionless**: Bağlantısız servis
- **⚡ Low latency**: Düşük gecikme
- **🎯 Best effort**: En iyi çaba yaklaşımı

### ❌ UDP’nin Sağlamadıkları

- **🛡️ Reliability**: Güvenilirlik garantisi yok
- **🌊 Flow control**: Akış kontrolü yok
- **🚦 Congestion control**: Tıkanıklık kontrolü yok
- **⏰ Timing**: Zaman garantisi yok
- **📊 Throughput**: İş hacmi garantisi yok
- **🔒 Security**: Güvenlik yok
- **🔗 Connection setup**: Bağlantı kurulumu yok

### ✅ UDP Kullanım Alanları

- **📹 Video streaming**: Hız önemli, kayıp tolere edilebilir
- **🎮 Online oyunlar**: Düşük gecikme kritik
- **🌍 DNS queries**: Kısa, tek mesaj
- **📺 Live broadcasting**: Real-time önemli
- ⚖️ **TCP vs UDP Karşılaştırması**
    
    
    | Özellik | ✅ TCP | ⚡ UDP |
    | --- | --- | --- |
    | **Güvenilirlik** | ✅ Tam | ❌ Yok |
    | **Hız** | ⚠️ Yavaş | ✅ Hızlı |
    | **Overhead** | 📊 Yüksek | 📊 Düşük |
    | **Bağlantı** | 🔗 Gerekli | 🚫 Gerekmiyor |
    | **Sıralama** | ✅ Garantili | ❌ Garantisiz |
    | **Kontrol** | 🌊 Flow + Congestion | ❌ Yok |
    | **Header boyutu** | 📦 20 byte | 📦 8 byte |

---

### 🔒 SSL (Secure Sockets Layer)

> 🛡️ TCP + Güvenlik
TCP üzerinde şifreli ve güvenli bağlantı katmanı.
> 

### 🔐 SSL/TLS Özellikleri

- **🔒 Encryption**: Veri şifreleme
- **✅ Authentication**: Kimlik doğrulama
- **🛡️ Data integrity**: Veri bütünlüğü
- **🔑 Key exchange**: Güvenli anahtar değişimi

### 🌟 SSL Avantajları

- **📱 Application layer**: Uygulama seviyesinde implement
- **🔧 Easy integration**: Mevcut TCP uygulamalarına kolay entegrasyon
- **🌐 HTTPS**: Web güvenliği için standart
- **📧 Secure email**: Güvenli e-posta

### 🏗️ SSL/TLS Katman Yapısı

- 🔒 **SSL/TLS Stack**
    
    ```
    ┌─────────────────────────┐
    │   📱 Application        │ ← HTTP, SMTP, FTP
    ├─────────────────────────┤
    │   🔒 SSL/TLS           │ ← Encryption layer
    ├─────────────────────────┤
    │   ✅ TCP               │ ← Reliable transport
    ├─────────────────────────┤
    │   🌐 IP                │ ← Network layer
    └─────────────────────────┘
    ```
    

> 📝 Bölüm Özeti
TCP güvenilir transport sağlarken UDP hız ve basitlik sunar. SSL/TLS ise TCP üzerinde güvenlik katmanı ekler. Uygulama gereksinimlerine göre protokol seçimi yapılır.
> 

---

## 🌐 HTTP (HyperText Transfer Protocol)

### 📋 HTTP Temelleri

> 🌍 Web’in Protokolü
World Wide Web’in temel uygulama katmanı protokolü.
> 

### 🏗️ HTTP Mimarisi

- **🖥️ Client-server model**: Tarayıcı ↔︎ Web server
- **🔌 TCP kullanımı**: Port 80 (HTTP), Port 443 (HTTPS)
- **🔄 Stateless protocol**: Server istemci durumunu saklamaz
- **📝 Request-response**: İstek-yanıt tabanlı

### 🌟 HTTP’nin Temel Özellikleri

- **📄 Text-based**: İnsan okunabilir format
- **🔄 Connectionless**: Her istek bağımsız
- **📱 Platform independent**: Platform bağımsız
- **🔧 Extensible**: Genişletilebilir header’lar

---

### 📄 Web Sayfası Yapısı

> 🏗️ Web Sayfası = HTML + Objects
Modern web sayfaları birden fazla kaynak içerir.
> 

### 🧩 Web Sayfası Bileşenleri

- **📝 Base HTML file**: Ana HTML dokümanı
- **🖼️ Referenced objects**: Bağlantılı kaynaklar
    - **📸 Images**: JPEG, PNG, GIF
    - **🎨 CSS files**: Stil sayfaları
    - **⚙️ JavaScript**: Dinamik içerik
    - **🎵 Media files**: Video, audio

### 🌐 URL (Uniform Resource Locator)

**Format**: `protocol://hostname:port/pathname`

- 🔍 **URL Anatomisi**
    
    ```
    https://www.example.com:443/course/networking/chapter1.html?id=123#section2
    
    🔒 https://         ← Protocol (HTTP Secure)
    🌐 www.example.com  ← Hostname/Domain
    🔢 :443            ← Port (default için yazılmaz)
    📁 /course/networking/ ← Path
    📄 chapter1.html    ← Filename
    ❓ ?id=123          ← Query parameters
    ⚓ #section2        ← Fragment identifier
    ```
    

---

### 🔗 HTTP Bağlantı Türleri

### 1️⃣ Non-Persistent HTTP

> 🔄 Her Object için Yeni Bağlantı
HTTP/1.0’da kullanılan geleneksel yöntem.
> 

### 🔧 Çalışma Prensibi

1. **🤝 TCP bağlantı kurulumu**
2. **📤 HTTP request gönderimi**
3. **📥 HTTP response alımı**
4. **❌ TCP bağlantı kapatma**
5. **🔄 Her object için tekrar**

### ⏰ Response Time Hesaplaması

**📊 Formula**: `Response Time = 2×RTT + File transmission time`

- ⏱️ **Non-Persistent HTTP Timeline**
    
    ```
    Client                Server
      │                     │
      │────TCP SYN─────────▶│  ← RTT/2
      │◀───SYN+ACK─────────│  ← RTT/2
      │────ACK──────────────▶│
      │────HTTP Request────▶│
      │◀───HTTP Response───│  ← File transfer time
      │────TCP FIN─────────▶│
    
    Total: 2×RTT + file transfer time
    ```
    

### ❌ Dezavantajları

- **⏰ Yüksek gecikme**: Her object için 2×RTT
- **💻 OS overhead**: Çok TCP bağlantısı
- **🌐 Network traffic**: Fazla control paketleri

---

### 2️⃣ Persistent HTTP

> 🔗 Tek Bağlantı, Çoklu Object
> 
> 
> HTTP/1.1’de varsayılan olan modern yöntem.
> 

### 🔧 Çalışma Prensibi

1. **🤝 Tek TCP bağlantı kurulumu**
2. **📤 Çoklu HTTP request**
3. **📥 Çoklu HTTP response**
4. **⏰ Idle timeout sonrası kapatma**

### ⚡ Avantajları

- **🎯 Düşük gecikme**: Sonraki objectler için 1×RTT
- **💾 Resource efficiency**: Az TCP bağlantısı
- **🚀 Better performance**: Pipelining desteği

### 🔄 Pipelining

- **📦 Multiple requests**: Yanıt beklemeden istek gönderme
- **⚡ Paralel transfer**: Eş zamanlı object transferi
- **📈 Improved throughput**: Artan veri aktarım hızı
- 📈 **Persistent vs Non-Persistent Performans**
    
    
    | Metrik | 🔄 Non-Persistent | 🔗 Persistent |
    | --- | --- | --- |
    | **İlk object** | 2×RTT + file | 2×RTT + file |
    | **Sonraki objectler** | 2×RTT + file | 1×RTT + file |
    | **N object toplam** | N×(2×RTT) | 2×RTT + (N-1)×RTT |
    | **TCP connections** | N adet | 1 adet |
    | **Server load** | 📊 Yüksek | 📊 Düşük |

---

### 📨 HTTP Mesaj Formatları

### 📤 HTTP Request Message

> 📋 İstek Formatı
Client’tan server’a gönderilen mesaj yapısı.
> 

### 🏗️ Request Yapısı

```
Method URL Version
Header-Name: Header-Value
Header-Name: Header-Value
[blank line]
[message body]
```

- 📋 **HTTP Request Örneği**
    
    ```
    GET /index.html HTTP/1.1
    Host: www-net.cs.umass.edu
    User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9
    Accept-Language: tr,en;q=0.8
    Accept-Encoding: gzip, deflate, br
    Connection: keep-alive
    Cache-Control: max-age=0
    ```
    
    **📝 Header Açıklamaları**
    
    **🌐 Host**
    
    **🖥️ User-Agent**
    
    **✅ Accept**
    
    **🌍 Accept-Language**
    
    **📦 Accept-Encoding**
    
    **🔗 Connection**
    

### 🔧 HTTP Methods

| Method | Açıklama | Güvenli | Idempotent |
| --- | --- | --- | --- |
| **GET** | Kaynak alma | ✅ | ✅ |
| **POST** | Veri gönderme | ❌ | ❌ |
| **PUT** | Kaynak güncelleme | ❌ | ✅ |
| **DELETE** | Kaynak silme | ❌ | ✅ |
| **HEAD** | Sadece header alma | ✅ | ✅ |
| **OPTIONS** | Desteklenen methodlar | ✅ | ✅ |

---

### 📥 HTTP Response Message

> 📋 Yanıt Formatı
Server’dan client’a dönen mesaj yapısı.
> 

### 🏗️ Response Yapısı

```
Version Status-Code Reason-Phrase
Header-Name: Header-Value
Header-Name: Header-Value
[blank line]
[message body]
```

- 📋 **HTTP Response Örneği**
    
    ```
    HTTP/1.1 200 OK
    Date: Sun, 26 Sep 2023 20:09:20 GMT
    Server: Apache/2.4.41 (Ubuntu)
    Content-Length: 2652
    Content-Type: text/html; charset=UTF-8
    Cache-Control: public, max-age=3600
    ETag: "a1b2c3d4e5f6"
    Connection: keep-alive
    
    <!DOCTYPE html>
    <html>
    <head>
        <title>Welcome</title>
    </head>
    <body>
        <h1>Merhaba Dünya!</h1>
    </body>
    </html>
    ```
    

---

### 🚨 HTTP Status Kodları

- 📊 **Status Code Kategorileri**
    
    
    | Kategori | Range | Açıklama | Örnekler |
    | --- | --- | --- | --- |
    | **1xx** | 100-199 | 📋 Informational | 100 Continue |
    | **2xx** | 200-299 | ✅ Success | 200 OK, 201 Created |
    | **3xx** | 300-399 | 🔄 Redirection | 301 Moved, 304 Not Modified |
    | **4xx** | 400-499 | ❌ Client Error | 404 Not Found, 403 Forbidden |
    | **5xx** | 500-599 | 🔥 Server Error | 500 Internal Error, 503 Unavailable |

### 🔢 Yaygın Status Kodları

- **✅ 200 OK**: İstek başarılı, kaynak döndürüldü
- **🔄 301 Moved Permanently**: Kaynak kalıcı taşındı
- **🗂️ 304 Not Modified**: Cache’deki versi geçerli
- **❌ 400 Bad Request**: Hatalı istek formatı
- **🔒 401 Unauthorized**: Kimlik doğrulama gerekli
- **🚫 403 Forbidden**: Erişim yasak
- **❓ 404 Not Found**: Kaynak bulunamadı
- **🔥 500 Internal Server Error**: Server hatası
- **📵 503 Service Unavailable**: Servis geçici kapalı

> 📝 Bölüm Özeti
HTTP, web’in temel protokolüdür. Persistent bağlantılar performansı artırır. Request/Response formatları standardize edilmiş header ve status code sistemi kullanır.
> 

---

## 🍪 Cookies (Çerezler)

### 🎯 Cookie’lerin Amacı

> 🔄 Stateful Web
HTTP stateless olmasına rağmen, durum bilgisi saklamak için cookie mekanizması.
> 

### 🤔 Neden Cookie Gerekli?

- **🔄 HTTP stateless**: Server, client geçmişini bilmez
- **👤 User experience**: Kişiselleştirilmiş deneyim
- **🛒 Shopping cart**: Alışveriş sepeti saklar
- **🔐 Authentication**: Oturum yönetimi

---

### 🔧 Cookie Bileşenleri

> 🏗️ 4 Bileşenli Sistem
Cookie’ler dört ana bileşen ile çalışır.
> 

### 1️⃣ 📤 HTTP Response Header

```
Set-Cookie: user-id=12345; expires=Wed, 09 Jun 2024 10:18:14 GMT
```

### 2️⃣ 📥 HTTP Request Header

```
Cookie: user-id=12345
```

### 3️⃣ 💾 Client Cookie File

Tarayıcının local storage’ında saklanan cookie verileri.

### 4️⃣ 🗄️ Server Backend Database

Server’da tutulan kullanıcı session verileri.

---

### 🔄 Cookie Çalışma Mekanizması

- 🔄 **Cookie Workflow Örneği**
    
    ```
    1. İlk Ziyaret:
    Client ──────GET /──────▶ Server
           ◀─Set-Cookie:1234─  (Response + Cookie)
    
    2. Sonraki Ziyaretler:
    Client ──Cookie:1234────▶ Server
           ◀───Personalized─  (Kişiselleştirilmiş content)
    
    3. Server Database:
    ┌─────────────────────────┐
    │ Cookie ID │ User Data   │
    ├───────────┼─────────────┤
    │ 1234      │ name: Ali   │
    │           │ cart: [...]  │
    │           │ prefs: [...] │
    └─────────────────────────┘
    ```
    

---

### 🎯 Cookie Kullanım Alanları

### 🔐 Authentication (Kimlik Doğrulama)

- **👤 Login sessions**: Oturum yönetimi
- **🔑 Remember me**: “Beni hatırla” özelliği
- **🛡️ Security tokens**: Güvenlik jetonu’ları

### 🛒 Shopping Carts (Alışveriş Sepetleri)

- **📦 Item storage**: Ürün saklama
- **💰 Price tracking**: Fiyat takibi
- **🔄 Session persistence**: Oturum sürekliliği

### 🎯 Recommendations (Öneriler)

- **📊 User behavior**: Kullanıcı davranışı analizi
- **🎬 Content suggestion**: İçerik önerileri
- **📈 Personalization**: Kişiselleştirme

### 📊 Analytics (Analitik)

- **👀 Page views**: Sayfa görüntüleme
- **⏰ Time tracking**: Süre takibi
- **📍 Navigation patterns**: Gezinme kalıpları

---

### ⚖️ Cookie Privacy (Gizlilik)

### ⚠️ Privacy Endişeleri

- **🕵️ User tracking**: Kullanıcı takibi
- **📊 Data collection**: Veri toplama
- **🎯 Behavioral profiling**: Davranış profilleme
- **🏢 Third-party tracking**: Üçüncü taraf takibi

### 🛡️ Privacy Korumaları

- **⚙️ Browser settings**: Tarayıcı ayarları
- **🚫 Cookie blocking**: Cookie engelleme
- **🔄 Incognito mode**: Gizli mod
- **⏰ Automatic deletion**: Otomatik silme
- 🔧 **Cookie Types**
    
    
    | Tür | Açıklama | Privacy Level | Kullanım |
    | --- | --- | --- | --- |
    | **🏠 First-party** | Ziyaret edilen site | ✅ Güvenli | Temel işlevsellik |
    | **🏢 Third-party** | Farklı site/reklam | ⚠️ Risk | Tracking, reklamlar |
    | **⚙️ Session** | Tarayıcı kapanınca sil | ✅ Güvenli | Geçici durum |
    | **💾 Persistent** | Belirli süre sakla | ⚠️ Risk | Uzun dönem takip |
    | **🔒 Secure** | Sadece HTTPS | ✅ Güvenli | Hassas veriler |
    | **🏠 SameSite** | Aynı site kısıtı | ✅ Güvenli | CSRF koruması |

> 📝 Bölüm Özeti
Cookie’ler HTTP’nin stateless yapısına karşın durum bilgisi saklamaya olanak tanır. Authentication, shopping cart ve personalization için kullanılır ancak privacy endişeleri vardır.
> 

---

## 🗄️ Web Caches (Proxy Server)

### 🎯 Web Cache Nedir?

> ⚡ Hızlandırma Mekanizması
Sık erişilen web içeriklerini geçici olarak saklayan ara sunucu sistemi.
> 

### 🏗️ Cache Mimarisi

- **👤 User**: Tarayıcıyı cache üzerinden erişim için ayarlar
- **🗄️ Proxy Cache**: Client ile origin server arasında
- **🌐 Origin Server**: Gerçek içerik sunucusu

---

### 🔄 Web Cache Çalışma Prensibi

- ⚡ **Cache İşlem Akışı**
    
    ```
    1. Cache Hit (Bulundu):
    Client ──Request──▶ Cache ──Response──▶ Client
                         │ (Cached content)
                         └─(Origin Server'a gitmez)
    
    2. Cache Miss (Bulunamadı):
    Client ──Request──▶ Cache ──Request──▶ Origin Server
                         │ ◀─Response─┘
                         │ (Cache'e kaydet)
                         └─Response──▶ Client
    
    3. Conditional Request:
    Client ──Request──▶ Cache ──If-Modified-Since──▶ Origin
                         │ ◀─304 Not Modified─┘
                         └─Cached Response──▶ Client
    ```
    

---

### ✅ Web Cache Avantajları

### ⚡ Performance İyileştirmeleri

- **📈 Response time azalır**: Cache’den hızlı yanıt
- **🌐 Access link trafiği azalır**: ISP bant genişliği tasarrufu
- **💰 Cost reduction**: Daha az bandwidth kullanımı
- **🚀 Better user experience**: Hızlı sayfa yüklemesi

### 🌍 Global Content Delivery

- **🏢 Poor content providers**: Küçük sitelerin performansını artırır
- **🌎 Geographic distribution**: Coğrafi olarak yakın cache’ler
- **📺 Load balancing**: Yük dağıtımı

---

### 🧮 Cache Örnek Hesaplama

> 📊 Performans Analizi
Cache etkisinin sayısal değerlendirmesi.
> 

### 📋 Varsayımlar

- **📦 Ortalama nesne boyutu**: 1 Mbit
- **📈 İstek oranı**: 15 request/second
- **🌐 Access link**: 15 Mbps
- **⏰ RTT (Round Trip Time)**: 2 saniye

### ❌ Cache Olmadan

- **📊 Link utilization**: (15 req/s × 1 Mbit) / 15 Mbps = 100%
- **⏰ Queueing delay**: ∞ (link tamamen dolu)
- **📈 Total delay**: 2s + ∞ = dakikalar

### ✅ %40 Hit Rate ile Cache

- **📊 Link utilization**: (15 × 0.6 × 1 Mbit) / 15 Mbps = 60%
- **⏰ Queueing delay**: ~100ms (kabul edilebilir)
- **📈 Average delay**: 0.4 × 0.01s + 0.6 × (2s + 0.1s) = **1.26s**
- 📈 **Cache Hit Rate Etkisi**
    
    
    | Hit Rate | Link Util. | Avg Delay | Performans |
    | --- | --- | --- | --- |
    | **0%** | 100% | ∞ | 🔴 Çok kötü |
    | **20%** | 80% | ~5s | 🟠 Kötü |
    | **40%** | 60% | ~1.3s | 🟡 Orta |
    | **60%** | 40% | ~0.9s | 🟢 İyi |
    | **80%** | 20% | ~0.5s | ✅ Çok iyi |

---

### 🔄 Cache Consistency (Tutarlılık)

### 🤔 Cache Consistency Problemi

- **⏰ Stale data**: Güncel olmayan veriler
- **🔄 Update frequency**: Güncelleme sıklığı
- **⚖️ Freshness vs Performance**: Güncellik vs Performans

### 💡 Conditional GET Mekanizması

### 📋 HTTP Headers

- **📅 Last-Modified**: Son değiştirme tarihi
- **🔍 ETag**: Entity tag (veri hash’i)
- **❓ If-Modified-Since**: Conditional request
- **❓ If-None-Match**: ETag tabanlı conditional

### 🔄 İşlem Akışı

1. **📦 İlk request**: Cache origin’den veriyi alır
2. **💾 Cache storage**: Last-Modified/ETag ile saklar
3. **❓ Sonraki request**: If-Modified-Since ile kontrol
4. **✅ 304 Not Modified**: Cache’deki versi geçerli
5. **📄 200 OK**: Yeni veri, cache güncelle

> 📝 Bölüm Özeti
Web cache’ler performansı artırır ve network trafiğini azaltır. Hit rate arttıkça performans iyileşir. Conditional GET ile cache consistency sağlanır.
> 

---

## 📧 Electronic Mail

### 📮 E-mail Sistem Bileşenleri

> 📧 E-mail Üçlüsü
Electronic mail sistemi üç ana bileşenden oluşur.
> 

### 1️⃣ 📱 User Agents (Mail Reader)

- **📨 Mail client software**: Thunderbird, Outlook, Apple Mail
- **🌐 Web-based mail**: Gmail, Yahoo Mail, Hotmail
- **📝 Compose**: E-mail yazma ve düzenleme
- **📥 Read**: E-mail okuma ve organize etme
- **📤 Send**: E-mail gönderme işlemi

### 2️⃣ 📬 Mail Servers

- **📦 Mailbox**: Kullanıcının gelen mesajlarını saklar
- **📮 Message queue**: Giden mesajları sıralar
- **🔄 Store and forward**: SMTP server’lar arası transfer
- **👤 User management**: Kullanıcı hesabı yönetimi

### 3️⃣ 📨 SMTP Protocol

- **🌐 Server-to-server**: Mail server’lar arası iletişim
- **📤 Push protocol**: Doğrudan transfer yaklaşımı
- **⏰ Real-time**: Eş zamanlı message delivery

---

### 📬 Mail Server Görevleri

- 🏗️ **Mail Server Mimarisi**
    
    ```
    User Agent ━━━━━━━━━┓
                      ▼
    ┌─────────────────────────┐
    │    📬 Mail Server       │
    ├─────────────────────────┤
    │ 📦 Mailboxes:          │
    │  ├─ user1@domain.com   │
    │  ├─ user2@domain.com   │
    │  └─ user3@domain.com   │
    ├─────────────────────────┤
    │ 📮 Message Queue:      │
    │  ├─ Outgoing msg 1     │
    │  ├─ Outgoing msg 2     │
    │  └─ Outgoing msg 3     │
    ├─────────────────────────┤
    │ 📨 SMTP Daemon         │
    └─────────────────────────┘
              ▼
        📡 Internet
              ▼
    ┌─────────────────────────┐
    │   📬 Remote Mail Server │
    └─────────────────────────┘
    ```
    

### 📦 Mailbox Management

- **👤 User accounts**: Kullanıcı hesapları
- **💾 Storage quota**: Depolama kotası
- **🗂️ Folder organization**: Klasör organizasyonu
- **🔍 Search indexing**: Arama indeksleme

### 📮 Message Queue Management

- **⏰ Delivery scheduling**: Teslimat planlaması
- **🔄 Retry mechanism**: Yeniden deneme
- **❌ Failure handling**: Hata yönetimi
- **📊 Priority queuing**: Öncelik sıralaması

---

### 📨 SMTP Protokolü

> 📤 Simple Mail Transfer Protocol
E-mail göndermek için kullanılan standart protokol.
> 

### 🔧 SMTP Özellikleri

- **🔌 TCP kullanımı**: Port 25 (standard), Port 587 (submission)
- **📤 Push protocol**: Gönderen tarafından başlatılan transfer
- **📝 ASCII format**: 7-bit ASCII character set
- **🤝 Command-response**: Komut-yanıt tabanlı

### 🔄 SMTP İletişim Aşamaları

1. **🤝 Handshaking**: Bağlantı kurma ve selamlama
2. **📤 Transfer**: Mesaj transferi işlemi
3. **👋 Closure**: Bağlantı sonlandırma

---

### 💬 SMTP Örnek İletişim

- 📨 **SMTP Session Örneği**
    
    ```
    S: 220 mail.example.com SMTP service ready
    C: HELO client.domain.com
    S: 250 Hello client.domain.com, pleased to meet you
    
    C: MAIL FROM: <ayse@source.com>
    S: 250 ayse@source.com... Sender ok
    
    C: RCPT TO: <ali@destination.com>
    S: 250 ali@destination.com... Recipient ok
    
    C: DATA
    S: 354 Enter mail, end with "." on a line by itself
    C: Subject: Merhaba
    C:
    C: Bu bir test mesajıdır.
    C: İkinci satır.
    C: .
    S: 250 Message accepted for delivery
    
    C: QUIT
    S: 221 mail.example.com Service closing
    ```
    
    **📋 SMTP Komutları**
    
    **🏠 HELO/EHLO**
    
    **📤 MAIL FROM**
    
    **📥 RCPT TO**
    
    **📝 DATA**
    
    **👋 QUIT**
    

---

### 📥 Mail Access Protokolleri

> 📬 E-mail Alma Yöntemleri
SMTP gönderim için kullanılır, alma için farklı protokoller gerekir.
> 

### 📨 POP3 (Post Office Protocol)

### 🔧 POP3 Özellikleri

- **📥 Download and delete**: İndir ve sil modeli
- **🔄 Stateless**: Oturumlar arası durum saklamaz
- **💾 Local storage**: İstemci bilgisayarda saklama
- **🔌 TCP Port 110**: Standard port

### ⚡ POP3 Avantajları

- **🚀 Simple**: Basit protokol yapısı
- **💾 Offline access**: Çevrimdışı erişim
- **📊 Low server load**: Düşük sunucu yükü

### ❌ POP3 Dezavantajları

- **📱 Single device**: Tek cihaz erişimi
- **🗂️ No server folders**: Sunucu klasörleme yok
- **🔄 No synchronization**: Senkronizasyon yok

---

### 📨 IMAP (Internet Mail Access Protocol)

### 🔧 IMAP Özellikleri

- **☁️ Server-based**: Sunucu tabanlı depolama
- **🗂️ Folder management**: Klasör yönetimi
- **🔄 Stateful**: Oturum durumu saklar
- **🔌 TCP Port 143**: Standard port

### ✅ IMAP Avantajları

- **📱 Multi-device**: Çoklu cihaz erişimi
- **☁️ Server storage**: Sunucu depolama
- **🗂️ Folder organization**: Klasör organizasyonu
- **🔄 Synchronization**: Cihazlar arası senkronizasyon

### ⚠️ IMAP Dezavantajları

- **🌐 Internet required**: İnternet bağlantısı gerekli
- **📊 Higher server load**: Yüksek sunucu yükü
- **💰 Storage costs**: Depolama maliyeti

---

### 🌐 Web-Based E-Mail

### 🔧 Web Mail Özellikleri

- **🌐 HTTP protokolü**: Tarayıcı tabanlı erişim
- **☁️ Cloud-based**: Bulut tabanlı hizmet
- **📱 Cross-platform**: Platform bağımsız
- **🔐 Integrated security**: Entegre güvenlik

### 🔄 Web Mail Mimarisi

```
User ──HTTP──▶ Web Server ──SMTP──▶ Mail Server
User ◀─HTTP──  Web Server ◀─IMAP─── Mail Server
```

- ⚖️ **Mail Protocol Karşılaştırması**
    
    
    | Özellik | 📨 POP3 | 📨 IMAP | 🌐 Web Mail |
    | --- | --- | --- | --- |
    | **Depolama** | 💾 Local | ☁️ Server | ☁️ Server |
    | **Multi-device** | ❌ Hayır | ✅ Evet | ✅ Evet |
    | **Offline access** | ✅ Evet | ⚠️ Kısmi | ❌ Hayır |
    | **Folder sync** | ❌ Hayır | ✅ Evet | ✅ Evet |
    | **Bandwidth** | 📊 Düşük | 📊 Orta | 📊 Yüksek |
    | **Setup** | 🔧 Zor | 🔧 Orta | 🔧 Kolay |

> 📝 Bölüm Özeti
E-mail sistemi user agents, mail servers ve SMTP protokolünden oluşur. POP3 basit download sağlarken, IMAP çoklu cihaz desteği sunar. Web mail ise tarayıcı tabanlı kolay erişim sağlar.
> 

---

## 🌍 DNS (Domain Name System)

### 🎯 DNS Nedir?

> 🌐 İnternet’in Telefon Rehberi
Human-readable domain names’leri IP adreslerine çeviren dağıtık veritabanı sistemi.
> 

### 🏗️ DNS’in İki Rolü

1. **🗄️ Distributed Database**: Hiyerarşik name server’lar ağı
2. **📱 Application-Layer Protocol**: İsim çözümleme protokolü

### 🔄 Temel İşlev

```
www.google.com ──DNS Query──▶ 142.250.185.46
Human readable ◀─────────────── Machine readable
```

---

### 🛠️ DNS Servisleri

### 🎯 Ana Servisler

### 1️⃣ 🌐 Hostname to IP Address Translation

- **📍 Primary function**: Ana işlev
- **🔄 Bidirectional**: İki yönlü çeviri
- **⚡ Fast resolution**: Hızlı çözümleme

### 2️⃣ 🏷️ Host Aliasing

- **📝 Canonical name**: Gerçek isim (relay1.west-coast.enterprise.com)
- **🔗 Alias names**: Takma isimler (www.enterprise.com, enterprise.com)
- **🎯 User-friendly**: Kullanıcı dostu kısa isimler

### 3️⃣ 📧 Mail Server Aliasing

- **📮 MX records**: Mail exchange kayıtları
- **📧 Email routing**: E-posta yönlendirme
- **🏢 Separate mail servers**: Ayrı mail sunucuları

### 4️⃣ ⚖️ Load Distribution

- **🌐 Multiple IP addresses**: Çoklu IP adresleri
- **🔄 Round-robin**: Sırayla dağıtım
- **📊 Load balancing**: Yük dengeleme

---

### 🏗️ DNS Hiyerarşisi

> 🌳 Ağaç Yapısı
DNS dünya çapında hiyerarşik yapıda organize edilmiştir.
> 

### 🌍 DNS Hiyerarşi Seviyeleri

- 🌳 **DNS Hiyerarşi Ağacı**
    
    ```
                    🌍 Root (.)
                        │
        ┌───────────────┼───────────────┐
        │               │               │
       com             org             edu            country codes
        │               │               │              │
        │            ┌──┴──┐         ┌──┴──┐         .tr .uk .de
        │           mit   pbs       mit   yale         │
        │                                              │
    google amazon                                  gov edu com
        │                                           │   │   │
       www mail                                   tbd metu garanti
    ```
    

### 1️⃣ 🌍 Root DNS Servers

- **📍 13 root server** dünya çapında (A-M etiketli)
- **🌐 Global distribution**: Coğrafi dağıtım
- **⚡ Anycast**: En yakın server’a yönlendirme
- **🛡️ High security**: Yüksek güvenlik

### 2️⃣ 🏢 Top-Level Domain (TLD) Servers

- **🌐 Generic TLDs**: .com, .org, .net, .edu, .gov
- **🇹🇷 Country-code TLDs**: .tr, .uk, .de, .jp
- **🆕 New gTLDs**: .tech, .shop, .blog
- **🏢 Verisign**: .com ve .net’i yönetir

### 3️⃣ 🏛️ Authoritative DNS Servers

- **🏢 Organization’s servers**: Kuruluşların kendi server’ları
- **📋 Definitive answers**: Kesin cevaplar
- **🛠️ Maintainable**: Kurumun kontrolünde
- **🌐 Public hosting**: DNS hosting hizmetleri

### 4️⃣ 🏠 Local DNS Servers

- **🏢 ISP servers**: İnternet servis sağlayıcı sunucuları
- **🔗 Default name server**: Varsayılan DNS server
- **⚡ Caching**: Local cache ile hızlandırma
- **🔄 Proxy function**: DNS proxy işlevi

---

### 🔍 DNS Query Türleri

### 1️⃣ 🔄 Iterative Query

> 🗺️ “Git Şu Adrese Sor”
Her server sadece bir sonraki adımı gösterir.
> 

### 🔧 Iterative Query İşleyişi

1. **👤 Client** → Local DNS: “www.cnn.com nedir?”
2. **🏠 Local DNS** → Root: “www.cnn.com nedir?”
3. **🌍 Root** → Local DNS: “.com sunucusuna sor: A.GTLD-SERVERS.NET”
4. **🏠 Local DNS** → TLD: “www.cnn.com nedir?”
5. **🏢 TLD** → Local DNS: “cnn.com sunucusuna sor: dns1.cnn.com”
6. **🏠 Local DNS** → Authoritative: “www.cnn.com nedir?”
7. **📍 Authoritative** → Local DNS: “74.125.224.147”
8. **🏠 Local DNS** → Client: “74.125.224.147”
- 🔄 **Iterative Query Diagram**
    
    ```
    Client          Local DNS       Root    TLD     Authoritative
      │                 │            │       │            │
      │──1:query(www.cnn.com)────────▶│       │            │
      │                 │──2:query─────────▶ │            │
      │                 │◀─3:ref to TLD─────│            │
      │                 │──4:query─────────────────▶     │
      │                 │◀─5:ref to auth──────────│     │
      │                 │──6:query──────────────────────▶│
      │                 │◀─7:answer─────────────────────│
      │◀8:answer────────│            │       │            │
    
    Total: 8 messages, Local DNS yapar tüm işi
    ```
    

---

### 2️⃣ 🔄 Recursive Query

> 🎯 “Benim İçin Çöz”
Her server çözümleme yükünü alır.
> 

### 🔧 Recursive Query İşleyişi

1. **👤 Client** → Local DNS: “www.cnn.com nedir?” (recursive)
2. **🏠 Local DNS** → Root: “www.cnn.com nedir?” (recursive)
3. **🌍 Root** → TLD: “www.cnn.com nedir?” (recursive)
4. **🏢 TLD** → Authoritative: “www.cnn.com nedir?”
5. **📍 Authoritative** → TLD: “74.125.224.147”
6. **🏢 TLD** → Root: “74.125.224.147”
7. **🌍 Root** → Local DNS: “74.125.224.147”
8. **🏠 Local DNS** → Client: “74.125.224.147”

### ⚠️ Recursive Query Sorunları

- **📊 High load**: Root/TLD server’larda yüksek yük
- **💰 Expensive**: Pahalı işlem maliyeti
- **🚫 Usually disabled**: Genelde kapatılmış
- ⚖️ **Iterative vs Recursive Karşılaştırması**
    
    
    | Özellik | 🔄 Iterative | 🔄 Recursive |
    | --- | --- | --- |
    | **Load dağılımı** | ✅ Client/Local DNS | ❌ Tüm server’lar |
    | **Message sayısı** | 📊 Aynı | 📊 Aynı |
    | **Implementation** | ✅ Kolay | ⚠️ Zor |
    | **Scalability** | ✅ İyi | ❌ Kötü |
    | **Caching** | ✅ Local’de | 📊 Her seviyede |
    | **Yaygınlık** | ✅ Standard | ❌ Nadir |

---

### 📄 DNS Record Türleri

> 🗄️ Resource Records (RR)
DNS veritabanındaki kayıt formatları.
> 

### 📋 RR Format

```
(Name, Value, Type, TTL)
```

### 🔢 Ana Record Türleri

- 📊 **DNS Record Types**
    
    
    | Type | Name | Value | Açıklama | Örnek |
    | --- | --- | --- | --- | --- |
    | **A** | Hostname | IP address | IPv4 adresi | (relay1.bar.com, 145.37.93.126, A) |
    | **AAAA** | Hostname | IPv6 address | IPv6 adresi | (ipv6.google.com, 2001:4860:4860::8888, AAAA, 3600) |
    | **NS** | Domain | Name server | Authoritative server | (foo.com, dns.foo.com, NS) |
    | **CNAME** | Alias | Canonical name | Takma ad | (www.ibm.com, servereast.backup2.ibm.com, CNAME) |
    | **MX** | Domain | Mail server | Mail sunucusu | (foo.com, mail.bar.foo.com, MX) |
    | **PTR** | IP address | Hostname | Reverse lookup | (126.93.37.145.in-addr.arpa, relay1.bar.com, PTR, 3600) |
    | **TXT** | Domain | Text | Metin bilgisi | (example.com, “v=spf1 include:_spf.google.com ~all”, TXT, 3600) |

### ⏰ TTL (Time To Live)

- **⏰ Cache duration**: Cache’de kalma süresi
- **🔄 Update frequency**: Güncelleme sıklığı
- **⚖️ Performance vs Freshness**: Performans vs Güncellik

---

### 💾 DNS Caching

> ⚡ Performance Optimization
Sık kullanılan DNS kayıtlarının geçici olarak saklanması.
> 

### 🔧 Caching Mekanizması

- **📊 Every name server**: Her name server cache yapar
- **⏰ TTL expiration**: TTL süresi dolunca temizle
- **🏢 TLD caching**: TLD server’lar genellikle cache’li
- **🌍 Root rarely visited**: Root server’lar nadir ziyaret

### ✅ Caching Avantajları

- **⚡ Faster response**: Hızlı yanıt
- **📉 Reduced traffic**: Azaltılmış trafik
- **💰 Lower costs**: Düşük maliyetler
- **📊 Better scalability**: Daha iyi ölçeklenebilirlik

### ⚠️ Caching Sorunları

- **📰 Stale data**: Güncel olmayan veriler
- **🔄 Propagation delay**: Değişikliklerin yayılma gecikmesi
- **⏰ TTL management**: TTL yönetimi zorluğu
- 📊 **Tipik TTL Değerleri**
    
    
    | Record Type | Tipik TTL | Açıklama |
    | --- | --- | --- |
    | **A records** | 1-24 saat | Web serverleri için orta süre |
    | **NS records** | 1-7 gün | Name server’lar nadiren değişir |
    | **MX records** | 1-24 saat | Mail server’lar için orta süre |
    | **CNAME** | 1-24 saat | Alias’lar için orta süre |
    | **TXT** | 1 saat-1 gün | İçeriğe bağlı |

### 🔄 Cache Poisoning

- **🦠 Malicious data**: Kötü niyetli veri enjeksiyonu
- **🛡️ DNSSEC**: DNS Security Extensions
- **🔐 Cryptographic verification**: Kriptografik doğrulama

> 📝 Bölüm Özeti
DNS, hiyerarşik dağıtık veritabanı sistemidir. İterative query’ler yaygın kullanılır. Çeşitli record türleri farklı ihtiyaçları karşılar. Caching performansı artırır ancak consistency sorunları yaratabilir.
> 

---

## 🔄 P2P File Distribution

### 🌟 BitTorrent Protokolü

> 👥 Peer-to-Peer Dosya Paylaşımı
Merkezi server olmadan dosya dağıtımını sağlayan popüler P2P protokolü.
> 

### 🏗️ BitTorrent Bileşenleri

### 🗂️ Torrent

- **👥 Peer grubu**: Aynı dosyayı paylaşan kullanıcılar
- **📦 File chunks**: Dosya 256KB parçalara bölünür
- **📋 Metadata**: .torrent dosyasında torrent bilgileri

### 📡 Tracker

- **📊 Peer tracking**: Torrent’teki peer’ları takip eder
- **📋 Peer list**: Aktif peer listesi sağlar
- **💾 Centralized coordination**: Merkezi koordinasyon noktası

### 👤 Peers

- **📥 Leechers**: Dosya indiren kullanıcılar
- **📤 Seeders**: Tam dosyaya sahip, sadece upload yapan kullanıcılar
- **⚖️ Peers**: Hem indiren hem upload yapan kullanıcılar

---

### 🔄 BitTorrent Çalışma Prensibi

- 🔄 **BitTorrent İşlem Akışı**
    
    ```
    1. 🎯 Torrent Discovery:
       User ──.torrent file──▶ BitTorrent Client
    
    2. 📡 Tracker Contact:
       Client ──peer list request──▶ Tracker
       Client ◀─peer list response─── Tracker
    
    3. 👥 Peer Connection:
       Client ←─────TCP handshake─────▶ Other Peers
    
    4. 📦 Chunk Exchange:
       Client ←─────chunk trading─────▶ Other Peers
    
    5. 🔄 Continuous Process:
       - Request rarest chunks first
       - Upload to fastest downloaders
       - Maintain peer connections
    ```
    

### 🎯 BitTorrent Stratejileri

### 📦 Rarest First

- **🔍 Chunk popularity**: En nadir chunk’ları önce iste
- **⚖️ Load balancing**: Yük dengeleme sağlar
- **📈 Availability**: Chunk availability’sini artırır

### 🤝 Tit-for-Tat

- **⚡ Top 4 uploaders**: En hızlı 4 uploader’a chunk gönder
- **🔄 Reciprocal altruism**: Karşılıklı yardımlaşma
- **🚫 Free riders**: Bedavacıları engeller

### 🎲 Optimistic Unchoking

- **🆕 Random peer**: Rastgele yeni peer’a şans ver
- **📊 Better partners**: Daha iyi partner keşfi
- **🔄 Periodic**: Periyodik olarak değiştir

---

### 📊 Client-Server vs P2P Karşılaştırması

> 📈 Ölçeklenebilirlik Analizi
File distribution sürelerinin karşılaştırmalı analizi.
> 

### 🖥️ Client-Server Model

- **📤 Server upload**: us (server upload bandwidth)
- **📥 Client download**: di (client i download bandwidth)
- **⏰ Distribution time**:
    
    ```
    Dcs ≥ max{NF/us, F/dmin}
    ```
    

### 🔄 P2P Model

- **📤 Total upload**: us + Σdi (server + all clients)
- **📥 Each client**: Must download F bits
- **⏰ Distribution time**:
    
    ```
    DP2P ≥ max{F/us, F/dmin, NF/(us + Σui)}
    ```
    
- 📈 **Scalability Comparison**
    
    
    | N (Peers) | Client-Server Time | P2P Time | P2P Advantage |
    | --- | --- | --- | --- |
    | **10** | 10×F/us | ~F/us | 🟢 10x faster |
    | **100** | 100×F/us | ~2×F/us | 🟢 50x faster |
    | **1000** | 1000×F/us | ~3×F/us | 🟢 300x faster |
    
    **📊 Grafik trend**
    
    **Client-Server**
    
    **P2P**
    

### ✅ P2P Avantajları

- **📈 Self-scaling**: Kullanıcı artışı kapasiteyi artırır
- **💰 Cost effective**: Merkezi server maliyeti yok
- **🛡️ Fault tolerant**: Tek nokta hatası yok
- **🌍 Global distribution**: Coğrafi dağıtım

### ⚠️ P2P Zorlukları

- **🔒 Security**: Güvenlik endişeleri
- **⚖️ Legal issues**: Telif hakkı sorunları
- **📊 Variable performance**: Değişken performans
- **👤 User dependency**: Kullanıcıya bağımlılık

> 📝 Bölüm Özeti
BitTorrent, rarest-first ve tit-for-tat stratejileri ile etkili P2P dosya dağıtımı sağlar. P2P modeli client-server’a göre çok daha iyi ölçeklenebilirlik sunar.
> 

---

## 🔌 Socket Programming

### 🎯 Socket Türleri

> 🚪 İki Ana Socket Türü
Ağ uygulamaları için iki farklı communication paradigması.
> 

### 1️⃣ 📦 UDP Socket

- **🚀 Connectionless**: Bağlantısız datagram servis
- **⚡ Fast**: Hızlı, düşük gecikme
- **🎯 Best-effort**: En iyi çaba yaklaşımı
- **📏 Message boundaries**: Mesaj sınırları korunur

### 2️⃣ 🔗 TCP Socket

- **🔗 Connection-oriented**: Bağlantı tabanlı
- **🛡️ Reliable**: Güvenilir byte-stream
- **📊 Flow control**: Akış kontrolü
- **🤝 Handshake required**: Bağlantı kurulumu gerekli

---

### 📦 UDP Socket Programming

> ⚡ Basit ve Hızlı
UDP ile socket programlama temel adımları.
> 

### 📤 UDP Client Örneği

- 💻 **UDP Client Code (Python)**
    
    ```python
    from socket import *serverName = 'hostname'serverPort = 12000clientSocket = socket(AF_INET, SOCK_DGRAM)
    message = input('Input lowercase sentence:')
    clientSocket.sendto(message.encode(), (serverName, serverPort))
    modifiedMessage, serverAddress = clientSocket.recvfrom(2048)
    print(modifiedMessage.decode())
    clientSocket.close()
    ```
    
    **🔧 UDP Client Adımları**
    
    **🔌 Socket creation**
    
    ```
    socket(AF_INET, SOCK_DGRAM)
    ```
    
    **📤 Send data**
    
    ```
    sendto(data, (host, port))
    ```
    
    **📥 Receive data**
    
    ```
    recvfrom(buffer_size)
    ```
    
    **🔒 Close socket**
    
    ```
    close()
    ```
    

---

### 📥 UDP Server Örneği

- 💻 **UDP Server Code (Python)**
    
    ```python
    from socket import *serverPort = 12000serverSocket = socket(AF_INET, SOCK_DGRAM)
    serverSocket.bind(('', serverPort))
    print("The server is ready to receive")
    while True:
        message, clientAddress = serverSocket.recvfrom(2048)
        modifiedMessage = message.decode().upper()
        serverSocket.sendto(modifiedMessage.encode(), clientAddress)
    ```
    
    **🔧 UDP Server Adımları**
    
    **🔌 Socket creation**
    
    ```
    socket(AF_INET, SOCK_DGRAM)
    ```
    
    **📍 Bind to port**
    
    ```
    bind(('', port))
    ```
    
    **📥 Receive data**
    
    ```
    recvfrom(buffer_size)
    ```
    
    **🔄 Process data**
    
    **📤 Send response**
    
    ```
    sendto(response, client_address)
    ```
    

---

### 🔗 TCP Socket Programming

> 🛡️ Güvenilir Bağlantı
TCP ile socket programlama ve connection management.
> 

### 📤 TCP Client Örneği

- 💻 **TCP Client Code (Python)**
    
    ```python
    from socket import *serverName = 'servername'serverPort = 12000clientSocket = socket(AF_INET, SOCK_STREAM)
    clientSocket.connect((serverName, serverPort))
    sentence = input('Input lowercase sentence:')
    clientSocket.send(sentence.encode())
    modifiedSentence = clientSocket.recv(2048)
    print('From Server:', modifiedSentence.decode())
    clientSocket.close()
    ```
    
    **🔧 TCP Client Adımları**
    
    **🔌 Socket creation**
    
    ```
    socket(AF_INET, SOCK_STREAM)
    ```
    
    **🤝 Connect**
    
    ```
    connect((host, port))
    ```
    
    **📤 Send data**
    
    ```
    send(data)
    ```
    
    **📥 Receive data**
    
    ```
    recv(buffer_size)
    ```
    
    **🔒 Close connection**
    
    ```
    close()
    ```
    

---

### 📥 TCP Server Örneği

- 💻 **TCP Server Code (Python)**
    
    ```python
    from socket import *serverPort = 12000serverSocket = socket(AF_INET, SOCK_STREAM)
    serverSocket.bind(('', serverPort))
    serverSocket.listen(1)
    print('The server is ready to receive')
    while True:
        connectionSocket, addr = serverSocket.accept()
        sentence = connectionSocket.recv(2048).decode()
        capitalizedSentence = sentence.upper()
        connectionSocket.send(capitalizedSentence.encode())
        connectionSocket.close()
    ```
    
    **🔧 TCP Server Adımları**
    
    **🔌 Socket creation**
    
    ```
    socket(AF_INET, SOCK_STREAM)
    ```
    
    **📍 Bind to port**
    
    ```
    bind(('', port))
    ```
    
    **👂 Listen**
    
    ```
    listen(queue_size)
    ```
    
    **🤝 Accept connections**
    
    ```
    accept()
    ```
    
    **📥📤 Data exchange**
    
    ```
    recv()
    ```
    
    ```
    send()
    ```
    
    **🔒 Close connection**
    
    ```
    close()
    ```
    

---

### ⚖️ UDP vs TCP Farkları

- 📊 **Detaylı Karşılaştırma**
    
    
    | Özellik | 📦 UDP | 🔗 TCP |
    | --- | --- | --- |
    | **Bağlantı** | ❌ Connectionless | ✅ Connection-oriented |
    | **Güvenilirlik** | ❌ Unreliable | ✅ Reliable |
    | **Sıralama** | ❌ No ordering | ✅ Ordered delivery |
    | **Hata kontrolü** | ⚠️ Basic checksum | ✅ Full error recovery |
    | **Flow control** | ❌ None | ✅ Yes |
    | **Congestion control** | ❌ None | ✅ Yes |
    | **Header overhead** | 📦 8 bytes | 📦 20+ bytes |
    | **Performance** | ⚡ Fast | 📊 Moderate |
    | **Use cases** | 🎮 Gaming, 📹 Streaming | 🌐 Web, 📧 Email, 📁 FTP |

### 🎯 Kullanım Alanları

### 📦 UDP İçin Uygun

- **🎮 Online games**: Düşük gecikme kritik
- **📹 Video streaming**: Kayıp tolere edilebilir
- **🌍 DNS queries**: Kısa, hızlı sorgular
- **📡 IoT devices**: Düşük kaynak kullanımı

### 🔗 TCP İçin Uygun

- **🌐 Web browsing**: Güvenilir veri gerekli
- **📧 Email**: Kayıp kabul edilemez
- **📁 File transfer**: Bütünlük şart
- **💬 Chat applications**: Message ordering önemli

### 🔧 Socket API Temel Fonksiyonları

- 📋 **Socket Functions Reference**
    
    
    | Function | UDP | TCP | Açıklama |
    | --- | --- | --- | --- |
    | **socket()** | ✅ | ✅ | Socket oluştur |
    | **bind()** | ✅ | ✅ | Port’a bağla |
    | **listen()** | ❌ | ✅ | Bağlantı dinle |
    | **accept()** | ❌ | ✅ | Bağlantı kabul et |
    | **connect()** | ❌ | ✅ | Server’a bağlan |
    | **send()** | ❌ | ✅ | Veri gönder |
    | **recv()** | ❌ | ✅ | Veri al |
    | **sendto()** | ✅ | ❌ | Adresli veri gönder |
    | **recvfrom()** | ✅ | ❌ | Adresli veri al |
    | **close()** | ✅ | ✅ | Socket kapat |

> 📝 Bölüm Özeti
Socket programming, network uygulamaları geliştirmek için temel API’dir. UDP basit ve hızlı, TCP güvenilir ve feature-rich yaklaşım sunar. Uygulama gereksinimlerine göre protokol seçimi yapılmalıdır.
> 

---

## 📋 Özet ve Genel Değerlendirme

### ✅ Kapsanan Ana Konular

> 🎓 Application Layer Mastery
Bu kapsamlı bölümde application layer’ın tüm önemli konularını öğrendiniz.
> 

### 🏗️ Temel Mimari Yapılar

- **🖥️ Client-Server**: Merkezi mimari yaklaşımı
- **🔄 P2P**: Dağıtık peer-to-peer yaklaşımı
- **🔌 Socket Programming**: Network aplikasyon geliştirme
- **🚛 Transport Requirements**: Uygulama gereksinimleri

### 🌐 Önemli Protokoller

- **🌍 HTTP**: Web protokolü ve cache mekanizmaları
- **📧 Email**: SMTP, POP3, IMAP protokolleri
- **🌍 DNS**: Domain name resolution sistemi
- **🔄 BitTorrent**: P2P file distribution

### 🔧 Pratik Uygulamalar

- **🍪 Cookies**: Web durum yönetimi
- **🗄️ Web Caches**: Performance optimization
- **📱 Socket API**: TCP/UDP programming

---

### 🔮 İlerleyen Konular

> 📚 Sonraki Adımlar
Application layer temelinde transport layer detaylarına geçiş.
> 
- 📖 **Gelecek Ders Planı**
    
    
    | Hafta | Konu | Detay | Prerequisites |
    | --- | --- | --- | --- |
    | **4-5** | **🚛 Transport Layer** | TCP/UDP deep dive, reliability | Application layer |
    | **6-7** | **🌐 Network Layer** | IP, routing algorithms, forwarding | Transport layer |
    | **8-9** | **🔗 Link Layer** | Ethernet, WiFi, switching | Network layer |
    | **10-11** | **🛡️ Advanced Security** | Cryptography, TLS/SSL | All layers |
    | **12-13** | **📡 Wireless & Mobile** | 802.11, cellular, mobility | Physical concepts |

---

### 🎯 Notion Veritabanı Önerileri

### 📚 Protocol Reference Database

> 📋 Protokol Hızlı Referansı
> 

**Önerilen alanlar**:
- **📋 Protocol Name**: HTTP, SMTP, DNS, etc.
- **🔢 Port Number**: 80, 25, 53, etc.
- **🏗️ Architecture**: Client-server, P2P
- **🚛 Transport**: TCP/UDP
- **🎯 Use Case**: Web, email, name resolution
- **⭐ Importance**: Critical/Important/Optional

### 💻 Code Snippets Database

> 🔧 Socket Programming Örnekleri
> 

**Önerilen alanlar**:
- **👨‍💻 Code Type**: UDP Client, TCP Server, etc.
- **🐍 Language**: Python, Java, C++
- **📝 Description**: Kod açıklaması
- **💾 Code**: Gerçek kod snippet
- **🎯 Use Case**: Hangi durumda kullanılır
- **⭐ Difficulty**: Beginner/Intermediate/Advanced

### ❓ Protocol Quiz Database

> 🧠 Protokol Bilgi Testi
> 

**Önerilen alanlar**:
- **❓ Question**: Soru metni
- **📊 Protocol**: Hangi protokol
- **✅ Answer**: Doğru yanıt
- **💡 Explanation**: Açıklama
- **⭐ Level**: Basic/Medium/Hard
- **📅 Last Attempted**: Son deneme tarihi

---

### 🎨 Visual Hierarchy Rehberi

### 🏷️ Renk Kodlama Sistemi

- **🔴 Kritik Protokoller**: HTTP, DNS, SMTP
- **🟠 Önemli Kavramlar**: Socket, Client-Server, P2P
- **🟡 Implementation**: Code examples, syntax
- **🟢 Performance**: Caching, optimization
- **🔵 Security**: Cookies, privacy, TLS

### 📊 Performans Metrikleri

- **⚡ Speed**: Response time, throughput
- **🛡️ Reliability**: Error rates, availability
- **📈 Scalability**: User capacity, growth
- **💰 Cost**: Infrastructure, maintenance

---

### 🔍 Gerçek Dünya Uygulamaları

### 🌐 Web Teknolojileri

- **⚡ HTTP/2 ve HTTP/3**: Modern web protocols
- **🔒 HTTPS Everywhere**: Security best practices
- **📱 Progressive Web Apps**: Mobile-first design
- **🚀 CDN Optimization**: Global content delivery

### 📧 Modern Email

- **☁️ Cloud Email**: Gmail, Outlook architecture
- **🛡️ Email Security**: SPF, DKIM, DMARC
- **📱 Mobile Email**: IMAP optimization
- **🤖 Email Automation**: APIs and integration

### 🎮 Real-time Applications

- **🎮 Gaming**: Low-latency networking
- **📹 Video Conferencing**: WebRTC, protocols
- **💬 Messaging**: WhatsApp, Telegram architecture
- **📺 Streaming**: Netflix, YouTube systems

---

> 🎓 Final Assessment
Application layer, end-user’ların ağ ile etkileşimde bulunduğu en üst seviyedir. Bu katmandaki protokoller ve teknolojiler modern internet deneyiminin temelini oluşturur.
> 

### 🌟 Önemli Çıkarımlar

1. **🏗️ Architecture Matters**: Client-server vs P2P seçimi uygulamanın ölçeklenebilirliğini belirler
2. **⚡ Performance vs Reliability**: UDP hız, TCP güvenilirlik öncelikli
3. **🔒 Security Integration**: Modern uygulamalar security-by-design yaklaşımı benimser
4. **📱 Mobile-First**: Uygulamalar mobil cihazlar için optimize edilmelidir
5. **🌍 Global Scale**: CDN ve caching stratejileri global performans için kritik