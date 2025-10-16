# Design Patterns

Design Pattern' ler yani Tasarım Desenleri, yazılımda tekrar eden problemlere çözüm getiren, kanıtlanmış yöntemlerdir. Tekrar kullanılabilir ve yazılımın bakımını, okunabilirliğini kolaylaştırır. Temel olarak 3 ana kategoriye ayrılır.

**1️⃣ Creational (Yaratıcı) Desenler**

Amaç: Nesnelerin oluşturulmasını kontrol altına almak, esnekliği artırmak.

| `Desen` | `Açıklama` |
| --- | --- | 
| **Singleton** | Bir sınıftan yalnızca bir nesne oluşturulmasını garanti eder. |
| **Factory Method** | Nesne oluşturmayı alt sınıflara bırakır, hangi sınıfın oluşturalacağını belirler. |
| **Abstract Factory** | İlgili nesne gruplarını üretir, somut sınıflara bağımlılığı azaltır. |
| **Builder** | Karmaşık nesneler adım adım oluşturmayı sağlar, aynı inşa sürecinden farklı nesneler yaratılabilir. | 
| **Prototype** | Var olan bir nesneyi kopyalayarak yeni nesne üretir. | 

**2️⃣ Structural (Yapısal) Desenler**

Amaç: Sınıflar ve nesneler arasındaki ilişkiyi düzenlemek ve yapıyı kolaylaştırmak.

| `Desen` | `Açıklama` |
| --- | --- | 
| **Adapter** | Farklı arayüzleri birbirlerine uyumlu hale getirir. |
| **Decorator** | Nesnelere çalışma zamanında davranış ekler. |
| **Facade** | Karmaşık sistemleri basit bir arayüzle sunar. |
| **Composite** | Nesneleri ağaç yapısında gruplayarak tek bir nesne gibi işlem yapmayı sağlar. |
| **Proxy** | Başka bir nesneye erişimi kontrol eder veya geciktirir. | 
| **Bridge** | Abstraction ve implementasyonu ayırır, bağımlılığı azaltır. |
| **Flyweight** | Çok sayıda benzer nesneyi hafızada paylaşarak performansı artırır. |

**3️⃣ Behavioral (Davranışsal) Desenler** 

Amaç: Nesneler arasındaki iletişimi ve sorumlulukları düzenlemek.

| `Desen` | `Açıklama` |
| --- | --- | 
| **Observer** | Bir nesnedeki değişiklikleri bağlı nesnelere bildirir. |
| **Strategy** | Bir algoritmayı çalıştırma zamanında değiştirmeyi sağlar. |
| **Command** | İşlemleri nesne olarak kapsüller, geri almayı kolaylaştırır. |
| **Chain of Responsibility** | bir isteği zincir üzerinde bir nesne işleyebilir. |
| **Iterator** | Koleksiyon üzerindeki elemanları tek tek dolaşmayı sağlar. | 
| **Mediator** | Nesneler arasındaki iletişimi merkezi bir nesne üzerinden yönetir. |
| **State** | Nesnenin durumuna göre davranışını değiştirir. |
| **Template Method** | Algoritmanın iskeletini tanımlar, alt sınıflar adımlarını değiştirir. |
| **Visitor** | Nesne yapısına yeni operasyonlar ekler, sınıfları değiştirmeden. |
| **Memento** | Nesnenin önceki durumunu kaydedip geri almayı sağlar. |

**Özetle:**
- Creational : Nesne oluşturma.
- Structural : Nesneler arası ilişki.
- Behavioral : Nesnelerin davranışı ve iletişimi.

