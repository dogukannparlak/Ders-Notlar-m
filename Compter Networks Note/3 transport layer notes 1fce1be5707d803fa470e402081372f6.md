# 3 transport layer notes

# 🚛 Transport Layer - Taşıma Katmanı

---

> 💡 Ders Hedefi
Güvenilir veri aktarımı, akış kontrolü ve tıkanıklık kontrolü mekanizmalarını öğrenerek TCP ve UDP protokollerini derinlemesine anlamak.
> 

---

## 🎯 Giriş ve Amaçlar

### 📚 Ana Hedefler

> 🎓 Öğrenme Çıktıları
Bu bölüm sonunda şunları öğrenmiş olacaksınız:
> 

### 🔍 Temel Kavramlar

- **📋 Transport Layer Prensipleri**: Güvenilir veri aktarımı, akış kontrolü, tıkanıklık kontrolü
- **🚛 Protocol Paradigmaları**: UDP ve TCP yaklaşımları
- **🔧 Reliability Mekanizmaları**: ACK, NAK, timeout, sequence numbering
- **🌊 Flow & Congestion Control**: Performans optimizasyonu teknikleri

### 🛠️ Praktik Protokoller

- **⚡ UDP**: User Datagram Protocol - Hızlı ve basit
- **🛡️ TCP**: Transmission Control Protocol - Güvenilir ve feature-rich
- **🔄 Pipeline Protocols**: Go-Back-N ve Selective Repeat
- **📊 Congestion Algorithms**: AIMD, Slow Start, Fast Recovery

---

### 🏗️ Transport Layer’ın Rolü

- 🌟 **Transport Layer’ın Temel İşlevleri**
    
    
    | İşlev | Açıklama | Protokol Desteği |
    | --- | --- | --- |
    | **📦 Segmentation** | Uygulama mesajlarını segmentlere böler | UDP, TCP |
    | **🔄 Multiplexing** | Çoklu uygulama süreçlerini destekler | UDP, TCP |
    | **🛡️ Error Detection** | Hata algılama ve düzeltme | UDP (basic), TCP (advanced) |
    | **🌊 Flow Control** | Alıcı kapasitesine göre hız ayarlama | TCP only |
    | **🚦 Congestion Control** | Ağ durumuna göre hız ayarlama | TCP only |
    | **📋 Ordering** | Veri sıralaması garantisi | TCP only |

> 📝 Önemli Not
Transport layer, end-to-end communication sağlar ve network layer’ın üstünde çalışır.
> 

---

## 🌐 Internet Transport Protokolleri Genel Bakış

### 🔍 Protokol Karşılaştırması

> ⚖️ UDP vs TCP
İki farklı yaklaşım, farklı ihtiyaçlar
> 
- 📊 **Detaylı Protokol Karşılaştırması**
    
    
    | Özellik | ⚡ UDP | 🛡️ TCP | Kullanım Durumu |
    | --- | --- | --- | --- |
    | **Güvenilirlik** | ❌ Unreliable | ✅ Reliable | TCP: Banking, UDP: Gaming |
    | **Hız** | ⚡ Çok hızlı | 📊 Orta | UDP: Real-time, TCP: File transfer |
    | **Overhead** | 📦 8 byte header | 📦 20+ byte header | UDP: IoT, TCP: Web |
    | **Bağlantı** | 🚫 Connectionless | 🔗 Connection-oriented | UDP: DNS, TCP: HTTP |
    | **Sıralama** | ❌ No ordering | ✅ Ordered delivery | UDP: Live stream, TCP: Email |
    | **Flow Control** | ❌ None | 🌊 Yes | TCP: Büyük dosya transferi |
    | **Congestion Control** | ❌ None | 🚦 Yes | TCP: İnternet trafiği |

### ✅ Her İki Protokolde Sağlanan

- **🔢 Port-based addressing**: Process-level communication
- **📊 Basic error detection**: Checksum mekanizması
- **🔄 Multiplexing/Demultiplexing**: Çoklu uygulama desteği

### ❌ Her İki Protokolde Sağlanmayan

- **⏰ Timing guarantees**: Zaman garantisi
- **📈 Bandwidth guarantees**: Bant genişliği garantisi
- **🔒 Built-in security**: Dahili güvenlik

> 📝 Bölüm Özeti
Transport layer, application ve network layer arasında köprü görevi görür. UDP hız, TCP güvenilirlik öncelikli yaklaşımlar sunar.
> 

---

## ⚡ UDP: User Datagram Protocol

### 🎯 UDP Nedir?

> 🚀 “Best Effort” Protokolü
En basit transport protokolü - IP’nin minimal uzantısı.
> 

### 🔧 UDP Temel Özellikleri

- **📦 Connectionless**: Bağlantı kurulumu yok
- **⚡ Fast**: Minimum işlem maliyeti
- **🎯 Best-effort**: En iyi çaba yaklaşımı
- **📏 Message boundaries**: Mesaj sınırları korunur

---

### 💪 UDP’nin Avantajları

- ✅ **UDP Avantajları Detayı**
    
    ### 🚀 Performans Avantajları
    
    - **⏰ No connection setup delay**: Bağlantı kurulum gecikmesi yok
    - **📦 Small header**: Sadece 8 byte overhead
    - **🎯 Simple processing**: Basit işleme mantığı
    - **💾 No connection state**: Bağlantı durumu saklamaz
    
    ### 🔧 Implementation Avantajları
    
    - **🎮 Real-time friendly**: Gerçek zamanlı uygulamalar için ideal
    - **🔄 No flow control**: Akış kontrolü yok = maksimum hız
    - **🚦 No congestion control**: Tıkanıklık kontrolü yok = tutarlı hız
    - **📊 Predictable performance**: Öngörülebilir performans

### 🎯 UDP Kullanım Alanları

| Kategori | Uygulamalar | Neden UDP? |
| --- | --- | --- |
| **🎮 Gaming** | Online games, FPS | Düşük gecikme kritik |
| **📹 Streaming** | Video/audio streaming | Kayıp tolere edilebilir |
| **🌍 Network Services** | DNS, DHCP, SNMP | Kısa istek-yanıt |
| **📡 IoT/Sensor** | Sensor data, telemetry | Düşük kaynak kullanımı |
| **📺 Broadcasting** | Live TV, radio | Real-time delivery |

---

### 📦 UDP Segment Yapısı

> 🏗️ Basit ve Etkili Header
UDP header’ı sadece 4 alan içerir.
> 
- 📋 **UDP Header Detayları**
    
    ```
     0                   1                   2                   3
     0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |          Source Port          |       Destination Port        |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |            Length             |           Checksum            |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                        Application Data                       |
    |                             ...                               |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    ```
    
    **🔢 Field Açıklamaları**:
    - **📤 Source Port (16 bit)**: Gönderen uygulamanın port numarası
    - **📥 Destination Port (16 bit)**: Hedef uygulamanın port numarası
    - **📏 Length (16 bit)**: Header + data toplam uzunluğu (minimum 8 byte)
    - **🔍 Checksum (16 bit)**: Hata algılama için (optional IPv4’te)
    

### 🧮 UDP Length Hesaplaması

```
UDP Length = UDP Header (8 bytes) + Application Data
Minimum UDP Length = 8 bytes (header only)
Maximum UDP Length = 65,535 bytes (16-bit limit)
```

---

### 🔍 UDP Checksum Mekanizması

> 🛡️ Hata Algılama
UDP’nin tek güvenilirlik mekanizması.
> 

### 📤 Gönderen Tarafında (Sender)

1. **📊 Pseudo-header oluştur**: IP addresses + protocol + UDP length
2. **🔢 16-bit words’e böl**: Tüm UDP segment
3. **➕ Binary addition**: Tüm 16-bit değerleri topla
4. **🔄 One’s complement**: Toplamın one’s complement’i
5. **📦 Checksum field’e yerleştir**: Hesaplanan değer

### 📥 Alıcı Tarafında (Receiver)

1. **🔍 Aynı hesaplamayı yap**: Pseudo-header + UDP segment
2. **⚖️ Karşılaştır**: Hesaplanan vs gelen checksum
3. **✅ Eşitse**: Hata yok (büyük olasılıkla)
4. **❌ Farklıysa**: Hata tespit edildi → segment at
- 💡 **Checksum Örnek Hesaplaması**
    
    ```
    Örnek UDP Segment (hex):
    Source Port:      0x1234
    Dest Port:        0x5678
    Length:           0x0014 (20 bytes)
    Checksum:         0x0000 (hesaplanacak)
    Data:             0x48656C6C6F (Hello)
    
    1. Pseudo-header:
       Source IP:     192.168.1.1  → 0xC0A80101
       Dest IP:       192.168.1.2  → 0xC0A80102
       Protocol:      17 (UDP)     → 0x0011
       UDP Length:    20            → 0x0014
    
    2. Sum calculation:
       0x1234 + 0x5678 + 0x0014 + 0x48656C6C6F + pseudo-header values
    
    3. One's complement = Checksum
    ```
    

### ⚠️ Checksum Limitasyonları

- **🔍 Detects most errors**: Çoğu hatayı yakalar
- **❌ Not foolproof**: %100 garantili değil
- **🔢 16-bit limitation**: Büyük hatalar kaçabilir
- **⚡ Performance trade-off**: Hız vs güvenlik

> 📝 Bölüm Özeti
UDP basit, hızlı ve düşük overhead’li protokoldür. Checksum ile temel hata algılama sağlar ancak güvenilirlik garantisi vermez. Real-time uygulamalar için idealdir.
> 

---

## 🛡️ Reliable Data Transfer (RDT)

### 🎯 RDT Nedir?

> 🔧 Güvenilir İletim Temelleri
Güvenilmez kanal üzerinde güvenilir veri aktarımı sağlama prensipleri.
> 

### 🏗️ RDT Problem Scenarios

1. **📡 Perfect Channel**: Hata yok, kayıp yok (RDT 1.0)
2. **🔍 Bit Errors**: Hata var, kayıp yok (RDT 2.0, 2.1, 2.2)
3. **📦 Packet Loss**: Hata + kayıp var (RDT 3.0)
4. **⚡ Performance**: Pipeline protocols (GBN, SR)

---

### 🔍 RDT 2.x: Bit Hataları ile Başa Çıkma

> 🛠️ ACK/NAK Mekanizması
Hata algılama ve düzeltme için temel yaklaşım.
> 

### 📋 Temel Mekanizmalar

- **✅ Acknowledgements (ACK)**: “Paket doğru alındı”
- **❌ Negative Acknowledgements (NAK)**: “Pakette hata var”
- **🔄 Retransmission**: Hatalı paketi yeniden gönder
- **🔍 Error detection**: Checksum ile hata algılama
- 🔄 **RDT 2.0 State Machine**
    
    ```
    Sender State Machine:
    ┌─────────────────┐
    │   Wait for      │
    │   call from     │ ──rdt_send(data)──▶ create packet
    │   above         │                     send packet
    └─────────────────┘                     │
            ▲                               │
            │                               ▼
            │                     ┌─────────────────┐
            │◀──ACK received─────│   Wait for      │
            │   (do nothing)      │   ACK or NAK    │
            │                     │   from below    │
            │                     └─────────────────┘
            │                               │
            └──NAK received─────────────────┘
               retransmit packet
    
    Receiver State Machine:
    ┌─────────────────┐
    │   Wait for      │ ──packet with errors──▶ send NAK
    │   packet from   │
    │   below         │ ──packet OK─────────▶ extract data
    └─────────────────┘                      deliver to app
                                             send ACK
    ```
    

### ⚠️ RDT 2.0 Problemi

- **🔍 ACK/NAK corruption**: ACK/NAK mesajları da bozulabilir
- **🤔 Duplicate handling**: Aynı paketi iki kez gönderme riski

### 💡 RDT 2.1 Çözümü: Sequence Numbers

- **🔢 Sequence number**: Her pakete sıra numarası
- **🔄 Duplicate detection**: Tekrarlayan paket tespiti
- **📦 0/1 alternating**: İki sequence number yeterli

---

### ⏰ RDT 3.0: Packet Loss ile Başa Çıkma

> ⏱️ Timer Mekanizması
Paket kayıplarını algılama ve telafi etme.
> 

### 🔧 Temel Yaklaşım

- **⏰ Timer**: Her packet gönderiminde timer başlat
- **⏱️ Timeout**: “Makul” süre sonra timeout
- **🔄 Retransmit**: Timeout durumunda yeniden gönder
- **✅ Stop timer**: ACK geldiğinde timer durdur

### 📊 RDT 3.0 Scenarios

- 📋 **RDT 3.0 Senaryoları**
    
    **Senaryo 1: Packet Loss**
    
    ```
    Sender          Receiver
      │                │
      │──packet 0─────▶│ (LOST)
      │                │
      │ ⏰ timeout     │
      │                │
      │──packet 0─────▶│
      │ ◀────ACK 0────│
    ```
    
    **Senaryo 2: ACK Loss**
    
    ```
    Sender          Receiver
      │                │
      │──packet 0─────▶│
      │ ◀────ACK 0────│ (LOST)
      │                │
      │ ⏰ timeout     │
      │──packet 0─────▶│ (duplicate)
      │ ◀────ACK 0────│
    ```
    
    **Senaryo 3: Premature Timeout**
    
    ```
    Sender          Receiver
      │                │
      │──packet 0─────▶│
      │ ⏰ timeout     │ (early)
      │──packet 0─────▶│ (duplicate)
      │ ◀────ACK 0────│
      │ ◀────ACK 0────│ (original)
    ```
    
    ### Senaryo 4: Cumulative ACK
    
    ```
    Time   Client              Server
    0      seq=100, data ─────▶
    1      seq=120, data ──X
    2      seq=140, data ─────▶
    3      ◀─────────── ack=120 (missing 120-139)
    4      ◀─────────── ack=160 (cumulative!)
    ```
    

### ⚡ RDT 3.0 Performance Sorunu

- **📊 Utilization**: Very low throughput
- **⏰ Stop-and-wait**: Sadece bir packet in-flight
- **🐌 Efficiency**: U = (L/R) / (RTT + L/R)

```
Örnek: 1 Gbps link, 15ms RTT, 8000-bit packet
U = (8000/10^9) / (30×10^-3 + 8×10^-6) = 0.00027
Sadece %0.027 utilization!
```

> 📝 Bölüm Özeti
RDT protokolleri güvenilir iletim için temel mekanizmaları gösterir: ACK/NAK, sequence numbers, timer. Ancak stop-and-wait yaklaşımı performans sorunları yaratır.
> 

---

## ⚡ Pipeline Protocols

### 🎯 Pipelining Nedir?

> 🚀 Performance Optimization
Birden fazla paketi aynı anda “in-flight” tutarak throughput artırma.
> 

### ✅ Pipelining Avantajları

- **📈 Increased utilization**: Çok daha yüksek throughput
- **⚡ Better link efficiency**: Bandwidth’i tam kullanma
- **🔄 Overlapped transmission**: Paralel paket gönderimi

### 🔧 Pipelining Gereksinimleri

- **🔢 Larger sequence space**: Daha fazla sequence number
- **💾 Buffering**: Sender ve/veya receiver’da buffer
- **📊 Window management**: Window boyutu yönetimi
- 📈 **Pipeline Performance Comparison**
    
    ```
    Stop-and-Wait vs Pipeline Utilization:
    
    Stop-and-Wait: U = L/R / (RTT + L/R)
    Pipeline: U ≈ N × L/R / (RTT + L/R)   (N = window size)
    
    Örnek (1 Gbps, 15ms RTT, 8000-bit packet):
    Stop-and-Wait: U = 0.00027 (0.027%)
    Pipeline (N=3): U = 0.00081 (0.081%)
    Pipeline (N=30): U = 0.0081 (0.81%)
    Pipeline (N=1000): U = 0.27 (27%)
    ```
    

---

### 🔄 Go-Back-N (GBN) Protocol

> 📦 Sliding Window with Cumulative ACK
Sender N’e kadar paket gönderebilir, receiver kümülatif ACK gönderir.
> 

### 🔧 GBN Sender Özellikleri

- **📊 Window size N**: En fazla N unacked packet
- **⏰ Single timer**: En eski unacked packet için
- **🔄 Go-back-N**: Timeout’ta tüm unacked paketleri gönder
- **📈 Sequence space**: En az 2N sequence number gerekli

### 📥 GBN Receiver Özellikleri

- **✅ Only accept in-order**: Sadece sıralı paket kabul et
- **🗑️ Discard out-of-order**: Sıra dışı paketleri at
- **📤 Cumulative ACK**: En son doğru alınan paketi ACK’le
- **💾 No buffering**: Buffer’a gerek yok
- 🔄 **GBN Example Scenario**
    
    ```
    Sender Window: [0,1,2,3] (N=4)
    Sequence: 0,1,2,3,4,5,6,7,8,9,...
    
    Time 0: Send packets 0,1,2,3
    Time 1: Receive ACK(0) → Window slides: [1,2,3,4], Send packet 4
    Time 2: Packet 1 LOST
    Time 3: Receive packet 2 → Out of order → Send ACK(0)
    Time 4: Receive packet 3 → Out of order → Send ACK(0)
    Time 5: Timeout → Retransmit 1,2,3,4
    
    Timeline:
    Sender:   0 1 2 3 4   timeout   1 2 3 4
    Receiver: 0 X 2 3 4   →discard→ 0 1 2 3 4
    ACKs:     ✓ X 0 0 0              ✓ ✓ ✓ ✓
    ```
    

### ✅ GBN Avantajları

- **💾 Simple receiver**: Receiver basit ve az buffer
- **📤 Easy implementation**: Kolay implementasyon
- **🔄 Cumulative ACK**: ACK loss’a dirençli

### ❌ GBN Dezavantajları

- **📦 Unnecessary retransmissions**: Gereksiz yeniden gönderimler
- **⏰ Single timer**: Tüm window için tek timer
- **🐌 Poor utilization**: Kayıp durumunda düşük performans

---

### 🎯 Selective Repeat (SR) Protocol

> 🔍 Individual ACK with Buffering
Her paket için ayrı ACK, sadece kayıp paketleri yeniden gönder.
> 

### 🔧 SR Sender Özellikleri

- **📊 Window size N**: En fazla N unacked packet
- **⏰ Timer per packet**: Her paket için ayrı timer
- **🎯 Selective retransmit**: Sadece timeout olan paketi gönder
- **📤 Individual ACKs**: Her paket için ayrı ACK

### 📥 SR Receiver Özellikleri

- **💾 Buffer out-of-order**: Sıra dışı paketleri buffer’la
- **✅ Individual ACK**: Her doğru paket için ACK gönder
- **📈 Deliver in-order**: Uygulamaya sıralı teslim et
- **🔄 Window sliding**: Window kayma mekanizması
- 🎯 **SR Example Scenario**
    
    ```
    Sender Window: [0,1,2,3] (N=4)
    Receiver Window: [0,1,2,3] (N=4)
    
    Time 0: Send packets 0,1,2,3
    Time 1: Receive ACK(0) → Window slides: [1,2,3,4], Send packet 4
    Time 2: Packet 1 LOST
    Time 3: Receive packet 2 → Buffer → Send ACK(2)
    Time 4: Receive packet 3 → Buffer → Send ACK(3)
    Time 5: Timeout packet 1 → Retransmit only packet 1
    
    Timeline:
    Sender:   0 1 2 3 4   timeout1   1
    Receiver: 0 X 2 3 4   →buffer→   1 → deliver 1,2,3 to app
    ACKs:     ✓ X ✓ ✓ ✓             ✓
    
    Receiver Buffer: [1:missing, 2:ready, 3:ready]
    After packet 1 arrives: deliver 1,2,3 to application
    ```
    

### ✅ SR Avantajları

- **🎯 Efficient retransmission**: Sadece kayıp paket
- **⚡ Better throughput**: Daha yüksek performans
- **🔄 Individual timers**: Paket başına optimal timeout

### ❌ SR Dezavantajları

- **💾 Complex receiver**: Karmaşık buffer yönetimi
- **📊 More memory**: Daha fazla memory gereksinimi
- **⏰ Multiple timers**: Her paket için timer

---

### ⚖️ GBN vs SR Karşılaştırması

- 📊 **Detaylı Protocol Karşılaştırması**
    
    
    | Özellik | 🔄 Go-Back-N | 🎯 Selective Repeat |
    | --- | --- | --- |
    | **Receiver Complexity** | 🟢 Simple | 🔴 Complex |
    | **Buffer Requirement** | 🟢 None at receiver | 🔴 Significant |
    | **Retransmission** | 🔴 All unacked | 🟢 Only lost |
    | **Throughput** | 🟡 Moderate | 🟢 High |
    | **Timer Management** | 🟢 Single timer | 🔴 Multiple timers |
    | **ACK Loss Tolerance** | 🟢 Good | 🟡 Moderate |
    | **Implementation** | 🟢 Easy | 🔴 Hard |
    | **Ideal Use Case** | 🌐 Internet (TCP) | 📡 High-speed links |

### 🔢 Window Size Considerations

- **GBN**: Sequence space ≥ 2N (wraparound prevention)
- **SR**: Sequence space ≥ 2N (sender + receiver windows)
- **Optimal N**: Function of bandwidth-delay product

> 📝 Bölüm Özeti
Pipeline protokolleri stop-and-wait’in performans sorunlarını çözer. GBN basit ama verimsiz, SR karmaşık ama verimli. TCP, GBN’nin modifiye edilmiş versiyonunu kullanır.
> 

---

## 🛡️ TCP: Transmission Control Protocol

### 🎯 TCP Nedir?

> 💪 İnternet’in Güvenilir Protokolü
Connection-oriented, reliable, in-order byte stream protokolü.
> 

### 🌟 TCP Ana Özellikleri

- 🔧 **TCP Comprehensive Features**
    
    
    | Özellik | Açıklama | Avantaj |
    | --- | --- | --- |
    | **🔗 Connection-oriented** | 3-way handshake ile bağlantı kurulumu | Güvenilir iletişim başlangıcı |
    | **🛡️ Reliable delivery** | Kayıpsız, hatasız veri teslimi | Data integrity garantisi |
    | **📋 In-order delivery** | Sıralı byte stream | Application’a düzenli veri |
    | **🌊 Flow control** | Receiver kapasitesine göre ayarlama | Buffer overflow önleme |
    | **🚦 Congestion control** | Network durumuna adaptasyon | Ağ performansı optimizasyonu |
    | **⚡ Full duplex** | Çift yönlü simultaneous communication | Bidirectional data flow |
    | **🎯 Point-to-point** | Sadece iki endpoint | Clear communication model |

### 🏗️ TCP Service Model

- **📦 Byte stream**: Continuous byte flow (no message boundaries)
- **🔄 Bidirectional**: Her iki yönde aynı anda veri
- **💾 Buffered**: Send ve receive buffer’ları
- **📏 MSS (Maximum Segment Size)**: Tipik 1460 bytes (Ethernet)

---

### 📦 TCP Segment Yapısı

> 🏗️ Rich Header Structure
TCP’nin güçlü özelliklerini destekleyen kapsamlı header.
> 
- 📋 **TCP Header Detaylı Analizi**
    
    ```
     0                   1                   2                   3
     0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |          Source Port          |       Destination Port        |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                        Sequence Number                        |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                    Acknowledgment Number                      |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    | Hdr  |     | | | | | | |               Window Size           |
    | Len  |     |U|A|P|R|S|F|                                     |
    |      |     |R|C|S|S|Y|I|                                     |
    |      |     |G|K|H|T|N|N|                                     |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |           Checksum            |         Urgent Pointer        |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                    Options (0-40 bytes)                      |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    |                        Application Data                       |
    +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
    ```
    
    **🔢 Field Açıklamaları**:
    
    | Field | Size | Açıklama | Kullanım |
    | --- | --- | --- | --- |
    | **📤 Source Port** | 16 bit | Gönderen port numarası | Process identification |
    | **📥 Dest Port** | 16 bit | Hedef port numarası | Service identification |
    | **🔢 Sequence Number** | 32 bit | İlk data byte’ının numarası | Ordering, reliability |
    | **✅ ACK Number** | 32 bit | Beklenen sonraki byte | Flow control |
    | **📏 Header Length** | 4 bit | TCP header uzunluğu (/4) | Variable options |
    | **🏷️ Flags** | 6 bit | Control bits | Connection management |
    | **📊 Window Size** | 16 bit | Receive window size | Flow control |
    | **🔍 Checksum** | 16 bit | Error detection | Data integrity |
    | **⚡ Urgent Pointer** | 16 bit | Urgent data offset | Priority data |

### 🏷️ TCP Flag Bits

| Flag | Tam Adı | Açıklama | Kullanım Durumu |
| --- | --- | --- | --- |
| **🔴 URG** | Urgent | Urgent data var | Nadir kullanılır |
| **✅ ACK** | Acknowledgment | ACK number geçerli | Normal data transfer |
| **📤 PSH** | Push | Data’yı hemen ilet | Interactive apps |
| **🔄 RST** | Reset | Bağlantıyı resetle | Error handling |
| **🤝 SYN** | Synchronize | Bağlantı kurulumu | Connection establishment |
| **👋 FIN** | Finish | Bağlantı sonlandırma | Connection termination |

---

### 🔢 TCP Sequence Numbers ve ACKs

> 📊 Reliable Ordering Mechanism
TCP’nin güvenilirlik ve sıralama temelini oluşturan sistem.
> 

### 🔢 Sequence Number Sistemi

- **📍 Byte-level numbering**: Her byte’a sıra numarası
- **🎲 Random initial**: ISN (Initial Sequence Number) rastgele seçilir
- **🔄 Wraparound**: 32-bit space (0 to 2^32-1)
- **📦 Segment seq num**: İlk data byte’ının numarası

### ✅ Acknowledgment Sistemi

- **📈 Next expected byte**: Alınması beklenen sonraki byte
- **📊 Cumulative**: O byte’a kadar hepsini onaylar
- **🔄 Piggybacking**: Data ile birlikte gönderilir
- 📋 **TCP Sequence Example**
    
    ```
    Host A → Host B Data Transfer:
    
    Initial State:
    A seq: 1000 (ISN)
    B seq: 2000 (ISN)
    
    Step 1: A sends data
    Segment: seq=1000, ack=2000, data="Hello" (5 bytes)
    A next seq: 1005
    
    Step 2: B responds with data
    Segment: seq=2000, ack=1005, data="World" (5 bytes)
    B next seq: 2005
    
    Step 3: A acknowledges
    Segment: seq=1005, ack=2005, no data
    
    Timeline:
    A: [1000-1004] Hello →
    B: ← [2000-2004] World, ACK 1005
    A: ACK 2005 →
    
    Sequence Spaces:
    A: ...1000|Hello|1005|next...
    B: ...2000|World|2005|next...
    ```
    

### 🔄 Cumulative ACK Özellikleri

- **✅ Efficiency**: Tek ACK birden fazla segment onaylar
- **🛡️ Loss tolerance**: ACK kaybında robust
- **⏰ Delayed ACK**: Genellikle 200ms gecikme ile gönderilir
- **📦 Fast path**: Sıralı segment’ler için optimize

---

### ⚡ TCP Sender Operations

> 🔧 Event-Driven Sender Logic
TCP sender’ın üç ana olay türüne nasıl tepki verdiği.
> 
- 📋 **TCP Sender State Machine**
    
    ### 📥 Event 1: Data from Application
    
    ```
    Application → TCP Send Buffer → Create Segment
    
    Process:
    1. 🔢 Assign sequence number (next seq num)
    2. 📦 Create TCP segment with data
    3. ⏰ Start timer (if not running)
    4. 📤 Send to Network Layer
    5. 📊 Update next sequence number
    ```
    
    ### ⏰ Event 2: Timer Timeout
    
    ```
    Timer Expires → Retransmit Oldest Unacked Segment
    
    Process:
    1. 🔍 Identify oldest unacked segment
    2. 📦 Retransmit that segment
    3. ⏰ Restart timer
    4. 📈 Update timeout interval (exponential backoff)
    ```
    
    ### ✅ Event 3: ACK Received
    
    ```
    Receive ACK → Update Window → Maybe Send More
    
    Process:
    1. 🔍 Check if ACK for new data
    2. ✅ Update send window
    3. ⏰ If more unacked data: restart timer
    4. ⏰ If no unacked data: stop timer
    5. 📤 Send new segments if window allows
    ```
    

### 📊 TCP Send Window Management

```
Send Window Structure:
|<-- sent & acked -->|<-- sent but not acked -->|<-- can send now -->|<-- can't send -->|
1                    2                          3                   4

1: Acked data (can be discarded)
2: Sent but waiting ACK (keep for retransmission)
3: Available window space (can send immediately)
4: Future space (wait for ACKs to slide window)

Window size = min(rwnd, cwnd)
rwnd = receiver advertised window
cwnd = congestion control window
```

---

### 🔄 TCP Retransmission Scenarios

> 🛠️ Loss Recovery Mechanisms
TCP’nin çeşitli kayıp durumlarını nasıl ele aldığı.
> 
- 📊 **Retransmission Scenario Analizi**
    
    ### Senaryo 1: Lost Segment
    
    ```
    Time   Client              Server
    0      seq=100, data ──X
    1                          (timeout)
    2      seq=100, data ─────▶
    3      ◀─────────── ack=120
    ```
    
    ### Senaryo 2: Lost ACK
    
    ```
    Time   Client              Server
    0      seq=100, data ─────▶
    1      ◀──────────X ack=120
    2                          (timeout)
    3      seq=100, data ─────▶ (duplicate)
    4      ◀─────────── ack=120
    ```
    
    ### Senaryo 3: Premature Timeout
    
    ```
    Time   Client              Server
    0      seq=100, data ─────▶
    1                          (early timeout)
    2      seq=100, data ─────▶ (duplicate)
    3      ◀─────────── ack=120 (for duplicate)
    4      ◀─────────── ack=120 (for original)
    ```
    
    ### Senaryo 4: Cumulative ACK
    
    ```
    Time   Client              Server
    0      seq=100, data ─────▶
    1      seq=120, data ──X
    2      seq=140, data ─────▶
    3      ◀─────────── ack=120 (missing 120-139)
    4      ◀─────────── ack=160 (cumulative!)
    ```
    

---

### ⚡ TCP Fast Retransmit

> 🚀 Quick Loss Detection
Timeout’u beklemeden hızlı kayıp tespiti ve recovery.
> 

### 🔧 Fast Retransmit Mekanizması

1. **🔍 Duplicate ACK detection**: Aynı ACK’ı 3 kez alma
2. **📦 Immediate retransmission**: Timeout beklemeden gönderim
3. **⏰ No timer wait**: Hızlı recovery

### 📊 Triple Duplicate ACK Örneği

- ⚡ **Fast Retransmit Timeline**
    
    ```
    Sender Timeline:
    Time 0: Send seq=1000 (segment 1)
    Time 1: Send seq=1500 (segment 2) ← LOST
    Time 2: Send seq=2000 (segment 3)
    Time 3: Send seq=2500 (segment 4)
    Time 4: Send seq=3000 (segment 5)
    
    Receiver Timeline:
    Time 0: Receive seq=1000 → Send ACK=1500
    Time 1: Missing seq=1500
    Time 2: Receive seq=2000 (out of order) → Send ACK=1500 (duplicate #1)
    Time 3: Receive seq=2500 (out of order) → Send ACK=1500 (duplicate #2)
    Time 4: Receive seq=3000 (out of order) → Send ACK=1500 (duplicate #3)
    
    Fast Retransmit Trigger:
    Time 5: Sender receives 3rd duplicate ACK=1500
    Time 6: Immediately retransmit seq=1500 (don't wait for timeout)
    
    Normal Recovery:
    Time 7: Receiver gets seq=1500 → Can deliver 1500,2000,2500,3000
    Time 8: Send ACK=3500 (cumulative for all received data)
    ```
    

### ✅ Fast Retransmit Avantajları

- **⚡ Faster recovery**: Timeout’tan çok daha hızlı
- **📈 Better throughput**: Daha az interruption
- **🎯 Early detection**: Erken kayıp tespiti
- **🔄 Standard practice**: Modern TCP implementasyonlarında standart

### 🎯 Duplicate ACK Interpretasyonu

- **1-2 duplicate**: Normal network reordering
- **3 duplicate**: Probable packet loss → trigger fast retransmit
- **>3 duplicate**: Confirmation of loss, network still working

> 📝 Bölüm Özeti
TCP güvenilir, sıralı veri aktarımı sağlar. Sequence number/ACK sistemi, retransmission mekanizmaları ve fast retransmit ile robust communication sağlar.
> 

---

## 🌊 TCP Flow Control

### 🎯 Flow Control Nedir?

> ⚖️ Receiver Protection
Sender’ın receiver’ın buffer kapasitesini aşmasını önleyen mekanizma.
> 

### 🏗️ Flow Control vs Congestion Control

- **🌊 Flow Control**: Receiver’ı koruma (end-to-end)
- **🚦 Congestion Control**: Network’ü koruma (network-wide)
- **🎯 Different problems**: Farklı problemler, farklı çözümler

---

### 📊 Receive Window (rwnd) Mekanizması

> 📦 Buffer Management
Receiver’ın buffer durumunu sender’a bildirme sistemi.
> 

### 🔧 Temel Mekanizma

- **📊 Receiver advertises**: Boş buffer alanını bildir
- **📤 Sender limits**: Gönderim miktarını sınırla
- **🛡️ Overflow prevention**: Buffer overflow’u önle
- 📋 **Flow Control Buffer Management**
    
    ```
    Receiver Buffer State:
    ┌────────────────────────────────────────┐
    │ App Data │ Buffered │     Free Space   │
    │ (read)   │ (unread) │   (available)    │
    └────────────────────────────────────────┘
               ▲          ▲                  ▲
            LastByteRead LastByteRcvd    Buffer End
    
    Buffer Calculations:
    RcvBuffer = Total buffer size (örn: 4096 bytes)
    Used = LastByteRcvd - LastByteRead
    Free = RcvBuffer - Used
    rwnd = Free space advertised to sender
    
    Flow Control Constraint:
    LastByteSent - LastByteAcked ≤ rwnd
    ```
    

### 📈 Dynamic Window Size

- **📊 rwnd value**: TCP header’da 16-bit field
- **🔄 Continuously updated**: Her segment’te güncellenir
- **📉 Decreases**: Application data okumadığında azalır
- **📈 Increases**: Application data okuduğunda artar

---

### ⚠️ Zero Window Problem

> 🛑 Window Size = 0
Receiver buffer’ı dolduğunda karşılaşılan durum.
> 

### 🔧 Problem Senaryosu

1. **📦 Receiver buffer full**: rwnd = 0 advertisement
2. **⏸️ Sender stops**: Gönderim durur
3. **📥 Application reads**: Buffer’da yer açılır
4. **❌ No data to send**: Sender’a bildirecek veri yok
5. **🔄 Deadlock**: İkisi de bekler

### 💡 Çözüm: Zero Window Probing

- **⏰ Persistence timer**: Sender’da timer
- **📦 1-byte probe**: Küçük segment gönder
- **📊 Force window update**: Receiver’ı rwnd güncellemesi için zorla
- **🔄 Periodic probing**: Düzenli kontrol
- ⚡ **Zero Window Probe Example**
    
    ```
    Scenario Timeline:
    
    Time 0: Receiver buffer full
    Receiver → Sender: rwnd = 0
    
    Time 1: Sender stops transmission
    Sender state: Waiting for window update
    
    Time 2: Application reads data
    Receiver buffer: Free space = 1000 bytes
    BUT: No data to send to trigger window update
    
    Time 3: Sender persistence timer expires
    Sender → Receiver: 1-byte probe segment
    
    Time 4: Receiver responds
    Receiver → Sender: ACK with rwnd = 1000
    
    Time 5: Normal transmission resumes
    Sender: Can send up to 1000 bytes
    ```
    

---

### 🔧 Flow Control Implementation

### 📊 Buffer Size Management

- **⚙️ Socket options**: SO_RCVBUF setting
- **🖥️ OS auto-tuning**: Modern systems auto-adjust
- **📈 Dynamic scaling**: Buffer size adaptation
- **💾 Default sizes**: Tipik 32KB-128KB range

### 🎯 Window Update Strategies

- **📤 Immediate**: Her ACK’ta window update
- **⏰ Delayed**: Birleştirme için gecikme
- **🎯 Threshold-based**: Belirli threshold’dan sonra update
- **📊 Advertised vs Available**: Gerçek vs advertised space
- 📊 **Flow Control Performance Metrics**
    
    
    | Metric | Açıklama | İdeal Değer |
    | --- | --- | --- |
    | **Buffer Utilization** | Kullanılan/Total buffer | %70-90 |
    | **Window Size** | Ortalama advertised window | BDP (Bandwidth-Delay Product) |
    | **Zero Window Events** | rwnd=0 olma sıklığı | Minimize |
    | **Application Read Rate** | App’in veri okuma hızı | ≥ Network arrival rate |
    | **Buffer Overflow** | Dropped segment count | 0 |

### 🎯 Flow Control Best Practices

- **📏 Right-size buffers**: Uygun buffer boyutu
- **⚡ Fast application reads**: Hızlı data consumption
- **📊 Monitor window size**: Window size takibi
- **🔄 Avoid silly window**: Küçük window’lar önle

> 📝 Bölüm Özeti
TCP flow control, receiver buffer overflow’unu önler. rwnd mekanizması ile dynamic window management sağlar. Zero window durumlarında persistence timer ile deadlock’u önler.
> 

---

## 🤝 TCP Connection Management

### 🎯 Connection Lifecycle

> 🔄 State-Based Protocol
TCP bağlantıları well-defined state machine ile yönetilir.
> 

### 🏗️ Connection Phases

1. **🤝 Establishment**: 3-way handshake
2. **📊 Data Transfer**: Bidirectional communication
3. **👋 Termination**: Graceful connection closure

---

### 🤝 TCP 3-Way Handshake

> 🔧 Connection Establishment
Güvenilir bağlantı kurulumu için standardize edilmiş süreç.
> 
- 📋 **3-Way Handshake Detayları**
    
    ### Step 1: SYN (Client → Server)
    
    ```
    TCP Segment:
    - SYN = 1
    - seq = client_isn (initial sequence number)
    - ack = 0 (no acknowledgment yet)
    - Data = none
    
    Client State: CLOSED → SYN_SENT
    ```
    
    ### Step 2: SYN+ACK (Server → Client)
    
    ```
    TCP Segment:
    - SYN = 1, ACK = 1
    - seq = server_isn
    - ack = client_isn + 1
    - Data = none
    
    Server State: LISTEN → SYN_RCVD
    ```
    
    ### Step 3: ACK (Client → Server)
    
    ```
    TCP Segment:
    - SYN = 0, ACK = 1
    - seq = client_isn + 1
    - ack = server_isn + 1
    - Data = can contain data
    
    Client State: SYN_SENT → ESTABLISHED
    Server State: SYN_RCVD → ESTABLISHED
    ```
    

### 🔢 Initial Sequence Number (ISN)

- **🎲 Random selection**: Security için rastgele seçim
- **⏰ Time-based**: Genellikle time-based algorithm
- **🔒 Security**: Sequence number prediction attacks önleme
- **🔄 Different for each connection**: Her bağlantı farklı ISN

### ⏰ Handshake Timing

```
Total connection establishment time = 1.5 RTT
- SYN: 0.5 RTT
- SYN+ACK: 0.5 RTT
- ACK: 0.5 RTT (can carry data)
```

---

### 👋 TCP Connection Termination

> 🔚 Graceful Closure
Her iki tarafın da bağlantıyı düzgün şekilde sonlandırması.
> 

### 🔧 4-Way Handshake (Normal Termination)

- 👋 **Connection Termination Sequence**
    
    ### Step 1: FIN (Initiator → Responder)
    
    ```
    Active Close:
    - FIN = 1, ACK = 1
    - seq = last_seq_used
    - ack = last_ack_sent
    
    State: ESTABLISHED → FIN_WAIT_1
    ```
    
    ### Step 2: ACK (Responder → Initiator)
    
    ```
    Acknowledge FIN:
    - FIN = 0, ACK = 1
    - seq = current_seq
    - ack = received_fin_seq + 1
    
    Initiator: FIN_WAIT_1 → FIN_WAIT_2
    Responder: ESTABLISHED → CLOSE_WAIT
    ```
    
    ### Step 3: FIN (Responder → Initiator)
    
    ```
    Passive Close:
    - FIN = 1, ACK = 1
    - seq = current_seq
    - ack = received_fin_seq + 1
    
    Responder: CLOSE_WAIT → LAST_ACK
    ```
    
    ### Step 4: ACK (Initiator → Responder)
    
    ```
    Final Acknowledgment:
    - FIN = 0, ACK = 1
    - seq = current_seq
    - ack = received_fin_seq + 1
    
    Initiator: FIN_WAIT_2 → TIME_WAIT → CLOSED
    Responder: LAST_ACK → CLOSED
    ```
    

### ⏰ TIME_WAIT State

- **🕐 2×MSL duration**: 2 × Maximum Segment Lifetime
- **🛡️ Prevent confusion**: Eski segment’lerin karışmasını önle
- **✅ Reliable termination**: Son ACK’ın ulaştığından emin ol
- **💾 Resource holding**: Socket resource’u tutar

### 🔄 Simultaneous Close

- **👥 Both sides initiate**: Her iki taraf da aynı anda FIN gönderir
- **🔄 State transitions**: Farklı state sequence
- **✅ Still works**: Protocol robust enough to handle

---

### 📊 TCP State Diagram

- 🔄 **Complete TCP State Machine**
    
    ```
    Connection Establishment:
    CLOSED → SYN_SENT → ESTABLISHED (client)
    CLOSED → LISTEN → SYN_RCVD → ESTABLISHED (server)
    
    Normal Termination (Active close):
    ESTABLISHED → FIN_WAIT_1 → FIN_WAIT_2 → TIME_WAIT → CLOSED
    
    Normal Termination (Passive close):
    ESTABLISHED → CLOSE_WAIT → LAST_ACK → CLOSED
    
    Simultaneous Close:
    ESTABLISHED → FIN_WAIT_1 → CLOSING → TIME_WAIT → CLOSED
    
    Reset Connection:
    Any State → CLOSED (RST received/sent)
    
    Key States:
    - LISTEN: Server waiting for connections
    - SYN_SENT: Client sent SYN, waiting for SYN+ACK
    - SYN_RCVD: Server received SYN, sent SYN+ACK
    - ESTABLISHED: Connection active, data transfer
    - FIN_WAIT_1: Sent FIN, waiting for ACK
    - FIN_WAIT_2: FIN ACKed, waiting for peer FIN
    - CLOSE_WAIT: Received FIN, waiting for app close
    - LAST_ACK: Sent FIN, waiting for final ACK
    - TIME_WAIT: Waiting for old segments to expire
    - CLOSED: No connection
    ```
    

### 🔴 Connection Reset (RST)

- **⚡ Immediate termination**: Abrupt connection close
- **❌ Error conditions**: Protocol violations, port unreachable
- **🚫 No data delivery**: Pending data lost
- **🛠️ Recovery mechanism**: Clean up corrupted connections
- ⚠️ **Common RST Scenarios**
    
    
    | Durum | RST Nedeni | Çözüm |
    | --- | --- | --- |
    | **Port closed** | Hedef port’ta dinleyen servis yok | Servisi başlat |
    | **Invalid state** | Unexpected segment | Connection state kontrol |
    | **Resource exhaustion** | Server overwhelmed | Load balancing |
    | **Firewall** | Connection blocked | Firewall rules |
    | **Application error** | Socket forcefully closed | Graceful termination |

> 📝 Bölüm Özeti
TCP connection management 3-way handshake ile başlar, veri transferi yapar, 4-way handshake ile sonlanır. State machine robust connection lifecycle yönetimi sağlar.
> 

---

## 🚦 Congestion Control

### 🎯 Congestion Nedir?

> 🚧 Network Overload
Ağ kaynaklarının kapasitesini aşan trafik durumu.
> 

### 🔍 Congestion vs Flow Control

- **🌊 Flow Control**: Receiver’ı koruma (endpoint problem)
- **🚦 Congestion Control**: Network’ü koruma (network-wide problem)
- **🎯 Different solutions**: Farklı mekanizmalar gerekli

---

### 📊 Congestion Indicators

> 🚨 Network Stress Signals
Ağ tıkanıklığının belirtileri ve etkileri.
> 

### 🔍 Congestion Symptoms

- **📦 Packet loss**: Router buffer overflow
- **⏰ Increased delay**: Queueing delay artışı
- **📉 Throughput degradation**: Effective throughput azalması
- **🔄 Retransmissions**: Artan yeniden gönderimler
- 📈 **Congestion Cost Analysis**
    
    ### Senaryo 1: Sonsuz Buffer
    
    ```
    Configuration: 2 senders → 1 router → 2 receivers
    Router: Infinite buffer, capacity R
    
    Results:
    - Maximum throughput: R/2 per connection
    - Problem: Arrival rate → R/2 ⟹ delay → ∞
    - Cost: Infinite queueing delay
    ```
    
    ### Senaryo 2: Finite Buffer + Packet Loss
    
    ```
    Configuration: Finite buffer + retransmissions
    Real traffic: λ (application data)
    Offered traffic: λ' (including retransmissions)
    
    Cases:
    1. Perfect retransmission: λ' = λ (no unnecessary retrans)
    2. Duplicate retransmission: λ' > λ (duplicate packets)
    3. Premature timeout: λ' >> λ (multiply retransmitted)
    
    Cost: More work for same "goodput"
    ```
    
    ### Senaryo 3: Multi-hop Network
    
    ```
    Configuration: Multiple router network
    Effect: Upstream transmission capacity wasted
    
    Example:
    A → R1 → R2 → B
    C → R2 → D
    
    If R2 drops A's packet:
    - Wasted: A→R1 transmission
    - Wasted: R1→R2 transmission
    - Result: Upstream capacity waste when packet dropped
    ```
    

---

### 🔧 TCP Congestion Control Principles

> 📊 AIMD Algorithm
Additive Increase, Multiplicative Decrease yaklaşımı.
> 

### 🎯 Temel Prensipler

1. **📈 Bandwidth probing**: Kullanılabilir bant genişliğini test et
2. **🚨 Loss-based**: Packet loss = congestion signal
3. **⚖️ Rate adjustment**: ACK = artır, Loss = azalt
4. **🤝 Fair sharing**: Adil bandwidth paylaşımı

### 🔧 Congestion Window (cwnd)

```
Constraint: LastByteSent - LastByteAcked ≤ min(cwnd, rwnd)

Sending Rate ≈ cwnd / RTT

cwnd: Congestion control window (sender-side)
rwnd: Receive window (receiver-side)
Effective window = min(cwnd, rwnd)
```

---

### 📈 TCP Congestion Control Algorithm

> 🔄 Three-Phase Algorithm
Slow Start, Congestion Avoidance, Fast Recovery.
> 

### 🚀 Phase 1: Slow Start

- **🎯 Goal**: Quickly reach available bandwidth
- **📈 Growth**: Exponential increase
- **🔢 Mechanism**: cwnd = cwnd × 2 per RTT
- **⏰ Trigger**: Connection start or timeout
- 🚀 **Slow Start Detailed**
    
    ```
    Slow Start Behavior:
    Initial: cwnd = 1 MSS
    After 1 RTT: cwnd = 2 MSS
    After 2 RTT: cwnd = 4 MSS
    After 3 RTT: cwnd = 8 MSS
    ...
    After n RTT: cwnd = 2^n MSS
    
    Implementation:
    - For each ACK received: cwnd += 1 MSS
    - Effective: cwnd doubles per RTT
    - Continue until: loss event OR cwnd ≥ ssthresh
    
    Example Timeline:
    RTT 1: Send 1 segment → receive 1 ACK → cwnd = 2
    RTT 2: Send 2 segments → receive 2 ACKs → cwnd = 4
    RTT 3: Send 4 segments → receive 4 ACKs → cwnd = 8
    ```
    

### ⚖️ Phase 2: Congestion Avoidance

- **🎯 Goal**: Stable operation near capacity
- **📊 Growth**: Linear increase
- **🔢 Mechanism**: cwnd += 1 MSS per RTT
- **⏰ Trigger**: cwnd ≥ ssthresh
- ⚖️ **Congestion Avoidance Detailed**
    
    ```
    Congestion Avoidance Behavior:
    Growth: +1 MSS per RTT (additive increase)
    
    Implementation:
    - For each ACK: cwnd += MSS²/cwnd
    - Effective: cwnd increases by 1 MSS per RTT
    - Continue until: loss event
    
    Example:
    RTT 1: cwnd = 8 → receive 8 ACKs → cwnd = 9
    RTT 2: cwnd = 9 → receive 9 ACKs → cwnd = 10
    RTT 3: cwnd = 10 → receive 10 ACKs → cwnd = 11
    
    Linear Growth vs Exponential in Slow Start
    ```
    

### ⚡ Phase 3: Fast Recovery (TCP Reno)

- **🎯 Goal**: Quick recovery from single packet loss
- **🔢 Mechanism**: cwnd = cwnd/2 + 3
- **⏰ Trigger**: 3 duplicate ACKs received

---

### 🎛️ Loss Detection and Response

> 🚨 Congestion Signal Processing
Farklı loss türlerine farklı tepkiler.
> 
- 📊 **Loss Type Analysis**
    
    ### Timeout Loss (Severe Congestion)
    
    ```
    Action:
    1. ssthresh = cwnd / 2
    2. cwnd = 1 MSS
    3. Enter Slow Start
    4. Exponential backoff on retransmission timer
    
    Interpretation: Network heavily congested
    Recovery: Conservative restart
    ```
    
    ### Triple Duplicate ACK (Mild Congestion)
    
    ```
    TCP Reno Response:
    1. ssthresh = cwnd / 2
    2. cwnd = ssthresh
    3. Retransmit missing segment
    4. Enter Congestion Avoidance
    
    TCP Tahoe Response:
    1. ssthresh = cwnd / 2
    2. cwnd = 1 MSS
    3. Enter Slow Start
    
    Interpretation: Network still delivering packets
    Recovery: Less aggressive reduction
    ```
    

### 🔄 AIMD Pattern

- **➕ Additive Increase**: +1 MSS per RTT during Congestion Avoidance
- **✖️ Multiplicative Decrease**: ÷2 during Fast Recovery
- **📈 Sawtooth pattern**: Characteristic bandwidth probing behavior
- 📈 **AIMD Visualization**
    
    ```
    Congestion Window over Time:
    
    cwnd
     ^
     |     /\      /\      /\
     |    /  \    /  \    /  \
     |   /    \  /    \  /    \
     |  /      \/      \/      \
     | /                        \
     |/                          \____
     +--------------------------------> time
    
    Phases:
    /: Slow Start (exponential)
    —: Congestion Avoidance (linear)
    \: Multiplicative Decrease (÷2)
    
    Pattern:
    - Probe for bandwidth (increase)
    - Hit congestion (loss)
    - Back off (decrease)
    - Repeat (fairness + efficiency)
    ```
    

---

### 🎯 TCP Variants Comparison

- ⚖️ **TCP Algorithm Variants**
    
    
    | Variant | Loss Response | Performance | Use Case |
    | --- | --- | --- | --- |
    | **TCP Tahoe** | Always slow start | Conservative | Stable networks |
    | **TCP Reno** | Fast recovery on 3-dup-ACK | Better | Most common |
    | **TCP New Reno** | Improved fast recovery | Good | Multiple losses |
    | **TCP CUBIC** | Cubic growth function | High-speed | Long fat networks |
    | **TCP BBR** | RTT + bandwidth based | Modern | Google’s approach |

### 🚀 Modern Developments

- **📊 Explicit Congestion Notification (ECN)**: Router feedback
- **⚡ TCP BBR**: Bottleneck Bandwidth and Round-trip propagation time
- **🔍 Compound TCP**: Microsoft’s hybrid approach
- **📈 TCP CUBIC**: High-speed networks için optimize

---

### 🤝 Fairness and Efficiency

> ⚖️ Network Resource Sharing
Adil ve verimli bandwidth paylaşımı.
> 

### 🎯 Fairness Goals

- **⚖️ Equal sharing**: Aynı RTT’deki connectionlar eşit pay
- **🚀 Efficiency**: Toplam throughput maksimize
- **⚡ Fast convergence**: Hızla fair state’e ulaşma
- **🛡️ Stable operation**: Oscillation minimize

### 📊 AIMD Fairness Analysis

```
Two connections sharing bottleneck:

Fair line: x = y (equal bandwidth)
Efficient line: x + y = C (total capacity)

AIMD behavior:
- Additive increase: parallel movement to efficient line
- Multiplicative decrease: movement toward fair line
- Converges to fair and efficient point

Fairness = (Σxi)² / (n × Σ(xi²))
Perfect fairness = 1.0
```

> 📝 Bölüm Özeti
TCP congestion control AIMD algoritması ile ağ tıkanıklığını yönetir. Slow Start, Congestion Avoidance ve Fast Recovery fazları ile bandwidth probing yapar. Adil ve verimli resource sharing sağlar.
> 

---

## 📋 Özet ve Genel Değerlendirme

### ✅ Kapsanan Ana Konular

> 🎓 Transport Layer Mastery
Bu kapsamlı bölümde transport layer’ın tüm önemli konularını öğrendiniz.
> 

### 🔧 Temel Mekanizmalar

- **⚡ UDP**: Basit, hızlı, connectionless protokol
- **🛡️ TCP**: Güvenilir, connection-oriented protokol
- **🔄 Reliable Data Transfer**: RDT principles ve pipeline protokolleri
- **🌊 Flow Control**: Receiver protection mekanizması
- **🚦 Congestion Control**: Network protection algoritmaları

### 📊 Protocol Features

- **📦 Segmentation**: Message’ları segment’lere bölme
- **🔍 Error Detection**: Checksum mekanizmaları
- **🔢 Sequence Numbering**: Ordering ve duplicate detection
- **⏰ Timer Management**: Timeout ve retransmission
- **🤝 Connection Management**: 3-way handshake, termination

### 🎯 Performance Optimization

- **⚡ Pipeline Protocols**: GBN ve Selective Repeat
- **🚀 Fast Retransmit**: Quick loss recovery
- **📈 AIMD**: Additive Increase Multiplicative Decrease
- **📊 Window Management**: Flow ve congestion control

---

###