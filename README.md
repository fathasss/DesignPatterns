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

---

## Creational Design Patterns

### Singleton Pattern

Amaç: Bir sınıftan yalnızca bir nesne oluşturmak ve bu nesneye global erişim sağlamak.

Kullanım senaryosu:

- Logger sınıfları
- Configuration ayarları
- Database Bağlantısı

```csharp
public class Singleton{
    private string Singleton _instance;

    private Singleton(){}

    public static Singleton Instance{
        get{
            if (_instance is null)
                _instance = new Singleton();
            return _instance;
        }
    }

    public void DoSomething(){
        Console.WriteLine("Singleton çalıştı!");
    }
}

class Program{
    static void Main(){
        Singleton s1 = Singleton.Instance;
        Singleton s2 = Singleton.Instance;

        Console.WriteLine(ReferanceEquals(s1,s2));
        s1.DoSomething();
    }
}

```

**Singleton** sayesinde sadece bir instance oluşur ve ReferanceEquals ile iki değişkenin aynı nesneyi işaret ettiği görülebilir.

### Factory Method Pattern

Amaç: Nesne yaratmayı alt sınıflara bırakmak, hangi nesnenin oluşturulacağını runtime' da karar vermek.

Kullanım senaryosu:

- Farklı tipte ürünlerin üretildiği sistemler
- GUI toolkitlerde farklı platformlara göre widget üretmek

```csharp
public abstract class Product{
    public abstract void Operation();
}

public class ConcreteProductA : Product {
    public override void Operation() {
        Console.WirteLine("ConcreteProductA çalıştı!");
    } 
}

public class ConcreteProdcutB : Product{
    public override void Operation(){
        Console.WriteLine("ConcreteProductB çalıştı!");
    }
}

public abstract class Creator{
    public abstract Product FactoryMethod();
}

public class ConcreteCreatorA : Creator{
    public override Product FactoryMethod(){
        return new ConcreteProductA();
    }
}

public class ConcreteCreatorB : Creator{
    public override Product FactoryMethod(){
        return new ConcreteProductB();
    }
}

class Program{
    static void Main(){
        Creator creatorA = new ConcreteCreatorA();
        Product productA = creatorA.FactoryMethod();
        productA.Operation();

        Creator creatorB = new ConcreteCreatorB();
        Product productB = creatorB.FactoryMethod();
        productB.Operation();
    }
}

```

**Factory Method**, nesne yaratmayı bağımlılıklardan ayırır ve esnekliği artırır.

### Anstract Factory Pattern

Amaç: Birbirleriyle ilişkili nesne ailelerini üretmek ve somut sınıflara bağımlılığı azaltmak.

Kullanım senaryosu:

- UI elementlerinin platforma göre (Windows/ Linux/ Mac) üretilmesi
- Tema veya skin sistemleri

```csharp
public interface IButton{
    void Paint();
}

public interface ICheckbox{
    void Paint();
}

// Concrete Product -> Windows
public class WindowsButton : IButton{
    public void Paint(){
        Console.WriteLine("Windows button!");
    }
}

public class WindowsCheckbox : ICheckbox {
    public void Paint(){
        Console.WriteLine("Windows checkbox");
    }
}

// Concrete Product -> Mac

public class MacButton : IButton{
    public void Paint(){
        Console.WriteLine("Mac button!");
    }
}

public class MacCheckbox : ICheckbox {
    public void Paint(){
        Console.WriteLine("Mac checkbox");
    }
}

// Abstract Factory
public interface IGUIFactory{
    IButton CreateButton();
    ICheckbox CreateCheckbox();
}

public class WindowsFactory : IGUIFactory{
    public IButton CreateButton(){
        new WindowsButton();
    }
    public ICheckbox CreateCheckbox(){
        new WindowsCheckbox();
    }
}

public class MacFactory : IGUIFactory{
    public IButton CreateButton(){
        new MacButton();
    }
    public ICheckbox CreateCheckbox(){
        new MacCheckbox();
    }
}

class Program {
    static void Main(){
        IGUIFactory factory = new WindowsFactory();
        IButton button = factory.CreateButton();
        ICheckbox checkbox = facetory.CrateCheckbox();
        button.Paint();
        checkbox.Paint();

        factory = new  MacFactory();
        button = factory.CreateButton();
        checkbox = factory.CreateCheckbox();
        button.Paint();
        checkbox.Paint();
    }
}

```

**Abstract Factory**, grup halinde nesneleri üretip sistemin platforma veya türe bağlı olmasını önler.

### Builder Pattern

Amaç: Karmaşık nesneleri adım adım oluşturmak ve farklı varyasyonlar yaratmak.

Kullanım senaryosu:

- Karmaşık rapor veya döküman üretimi
- Sipariş veya konfigurasyon sistemleri

```csharp
public class Car{
    public string Engine { get; set; }
    public string Seats { get; set; }
    public string GPS { get; set; }

    public void Show(){
        Console.WriteLine($"Engine: {Engine}, Seats: {Seats}, GPS: {GPS}");
    }
}

// Builder
public abstract class CarBuilder{
    protected Car car = new Car();
    public abstract void BuildEngine();
    public abstract void BuildSeats();
    public abstract void BuildGPS();
    public Car GetCar(){
        return car;
    }
}

// Concrete Builder
public class SportsCarBuilder : CarBuilder{
    public override void BuildEngine(){
        car.Engine = "V8";
    }
    public override void BuildSeats(){
        car.Seats = "2";
    }
    public override void BuildGPS(){
        car.GPS = "Premium GPS";
    }
}

// Director
public class Director{
    public void Construct(Carbuilder builder){
        builder.BuildEngine();
        builder.BuildSeats();
        builder.BuildGPS();
    }
}

class Program{
    static void Main(){
        CarBuilder builder = new SportsCarBuilder();
        Director director = new Director();
        director.Construct(builder);
        Car car = builder.GetCar();
        car.Show();
    }
}

```

**Builder Pattern**,nesneyi adım adım inşa eder, farklı varyasyonlar için aynı süreci kullanabiliriz.

### Prototype Pattern

Amaç: Var olan bir nesneyi kopyalarak yeni nesne oluşturmak.

Kullanım senaryosu:

- Karmaşık nesneleri hızlıca kopyalamak
- Nesne klonlama ve undo/ redo işlemleri

```csharp

public abstract class Prototype{
    public abstract Prototype Clone();
}

public class ConcretePrototype : Prototype{
    public string Data { get; set; }
    public override Prototype Clone(){
        return (Prototype)this.MemberwiseClone();
    }
}

class Program{
    static void Main(){
        ConcretePrototype original = new ConcretePrototype { Data = "Orijinal"};
        ConcretePrototype clone = (ConcretePrototype)original.Clone();
        Console.WriteLine(clone.Data);
    }
}

```

**Prototype**, nesne oluşturmayı kopyalama ile yapar, maliyetli yeni nesne yaratmayı önler.