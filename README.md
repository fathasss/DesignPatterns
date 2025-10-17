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

> Concrete Nedir ?

- **Abstract (soyut)**: Sadece bir iskelet (veya imza) sağlar, doğrudan kullanılamaz. İçinde bazı methodlar tanımlı ama gövdesi olmayabilir veya alt sınıfları override etmek zorunda olabilir.
- **Concreate (somut)**: Soyut sınıf veya interface' i implement eden ve tam olarak işleyen sınıftır. Yani gerçek bir nesne oluşturulabilir.

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

### Abstract Factory Pattern

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

## Structural Design Patterns

Amaç: Sınıflar ve nesneler arasındaki ilişkileri ve yapıyı düzenlemek, karmaşık sistemleri daha basit ve esnek hale getirmek.

### Adapter Pattern

Amaç: Farklı arayüzleri birbirine uyumlu hale getirmek.

Kullanım senaryosu:

- Eski bir sistemle yeni sistemi bağlamak
- Farklı API' leri aynı interface ile kullanmak

```csharp

public interface ITarget{
    void Request();
}

public class Adaptee{
    public void SpecificRequest(){
        Console.WriteLine("Adaptee çalıştı!");
    }
}

public class Adapter : ITarget {
    private readonly Adaptee _adaptee;

    public Adapter(Adaptee adaptee) {
        _adaptee = adaptee;
    }

    public void Request(){
        _adaptee.SpecificRequest();
    }
}

class Program {
    static void Main(){
        ITarget target = new Adapter(new Adaptee());
        target.Request(); //Adaptee çalıştı.
    }
}
```

**Adapter**, uyumsuz arayüzleri köprüler.

### Decorator Pattern

Amaç: Nesnelere çalışma zamanında yeni davranış eklemek.

Kullanım senaryosu:

- UI bileşenlerine ekstra özellik eklemek (border,scroll vb.)
- Nesneye dinamik yetenek eklemek

```csharp
public abstract class Coffee{
    public abstract double GetCost();
    public abstract string GetDescription();
}

//Concrete Component
public class SimpleCoffee : Coffee {
    public override double GetCost() {
        return 5;
    }

    public override string GetDescription(){
        return "Light coffee";
    }
}

//Decorator
public abstract class CoffeeDecorator : Coffee {
    protected Coffee _coffee;
    protected CoffeeDecorator(Coffee coffee){
        _coffee = coffee;
    }
}

//Concrete Decorators
public class MilkDecorator : CoffeeDecorator {
    public MilkDecorator(Coffee coffee) : base(coffee) { }
    public override double GetCost(){
        return _coffee.GetCost();
    }
    public override string GetDescription(){
        return _coffee.GetDescription() + ", Milk";
    }
}

public class SugarDecorator : CoffeeDecorator {
    public SugarDecorator(Coffee coffee) : base(coffee) { }
    public override double GetCost() => _coffee.GetCost() + 1;
    public override string GetDescription() => _coffee.GetDescription() + ", Sugar";
}

class Program{
    static void Main(){
        Coffee coffee = new SimpleCoffee();
        coffee = new MilkDecorator(coffee);
        coffee = new SugarDecorator(coffee);

        Console.WriteLine($"{coffee.GetDescription()} = {coffee.GetCost()} TL");       
    }
}

```

**Decorator** ile nesneye yeni özellikler eklemek için sınıfları değiştirmeye gerek yok.

### Facade Pattern

Amaç: Karmaşık sistemi basit bir arayüz ile sunmak.

Kullanım senaryosu:

- Büyük kütüphane veya API' yi kolay kullanmak
- Karmaşık iş akışlarını tek bir sınıf üzerinden yönetmek

```csharp

//Subsystem
public class CPU {
    public void Start(){
        Console.WriteLine("CPU started");
    }
}

public class Memory{
    public void Load(){
        Console.WriteLine("Memory loaded");
    }
}

public class Disk{
    public void Read(){
        Console.WriteLine("Disk readed");
    }
}

//Facade
public class ComputerFacade{
    private CPU cpu = new CPU();
    private Memory memory = new Memory();
    private Disk disk = new Disk();

    public void Start(){
        cpu.Start();
        memory.Load();
        disk.Read();
        Console.WriteLine("Computer ready!");
    }
}

class Program {
    static void Main(){
        ComputerFacade computer = new ComputerFacade();
        computer.Start();
    }
}

```

**Facade**, karmaşık sistemi basit bir arayüz ile kontrol etmemizi sağlar.

### Composite Pattern 

Amaç: Nesneleri ağaç yapısında gruplamak ve tek bir nesne gibi işlem yapmak.

Kullanım senaryosu:

- Dosya ve klasör yapıları
- UI elementleri (Panel içinde düğmeler, textboxlar vb.)

```csharp

//Component
public abstract class Graphic {
    public abstract void Draw();
}

//Leaf
public class Dot : Graphic {
    public override void Draw(){
        Console.WriteLine("Dot çizildi.");
    }
}

//Composite
public class CompoundGraphic : Graphic {
    private List<Graphic> _children = new List<Graphic>();

    public void Add(Graphic g){
        _children.Add(g);
    }

    public override void Draw(){
        foreach(var child in _children){
            child.Draw();
        }
    }
}

class Program {
    static void Main(){
        CompoundGraphic picture = new CompoundGraphic();
        picture.Add(new Dot());
        picture.Add(new Dot());

        CompoundGraphic group = new CompundGraphic();
        group.add(new Dot());
        picture.Add(group);

        picture.Draw();
    }
}

```

**Composite**, tekil nesne veya nesne grubunu aynı şekilde kullanmayı sağlar.

### Proxy Pattern

Amaç: Başka bir nesneye erişimi kontrol etmek veya geciktirmek.

Kullanım senaryosu:

- Uzak nesnelere erişim (Remote Proxy)
- Ağ veya maliyetli nesneleri yükleme (Virtual Proxy)
- Erişim kontrolü (Protection Proxy)

```csharp
//Subject
public interface IImage{
    void Display();
}

//Real Subject
public class RealImage : IImage {
    private string _filename;

    public RealImage(string filename) {
        _filename = filename;
        LoadFromDisk();
    }

    private void LoadFromDisk(){
        Console.WriteLine($"{_filename} loading...");
    }

    public void Display(){
        Console.WriteLine($"{_filename} showing...");
    }
}

//Proxy
public class ProxyImage : IImage {
    private RealImage _realimage;
    private string _filename;

    public ProxyImage(string filename){
        _filename = filename;
    }

    public void Display(){
        if (_realimage is null){
            _realimage = new RealImage(_filename);
        }
        
        _realimage.Display();
    }
}

class Program{
    static void Main(){
        IImage image = new ProxyImage("photo.jpg");
        image.Display(); //loaded and showed
        image.Display(); //just showed
    }
}
```

**Proxy**, gerçek nesnenin yaratılmasını ve kullanımını kontrol eder.

### Bridge Pattern

Amaç: Abstraction ve implementasyonu ayırmak, bağımlılığı azaltmak.

Kullanım senaryosu:

- Farklı platformlarda çalışacak sistemler.
- Arayüz ve iş mantığını birbirinden bağımsız geliştirmek.

```csharp

//Implementor
public interface IRenderer {
    void RenderCircle(float radius);
}

//Concrete Implementor
public class VectorRenderer : IRenderer {

    public void RenderCircle(float radius){
        Console.WriteLine($"Vector circle with radius {radius}");
    }
}

public class RasterRenderer : IRenderer {

    public void RenderCircle(float radius){
        Console.WriteLine($"Raster circle with radius {radius}");
    }
}

//Abstraction
public abstract class Shape{
    protected IRenderer renderer;
    protected Shape(IRenderer renderer){
        this.renderer = renderer;
    }

    public abstract void Draw();
}

//Refined Abstraction
public class Circle : Shape {
    private float radius;
    public Circle(IRenderer renderer, float radius): base(renderer){
        this.radius = radius;
    }

    public override void Draw(){
        renderer.RenderCircle(radius);
    }
}

class Program {
    static void Main(){
        Shape circle1 = new Circle(new VectorRenderer(),5);
        circle1.Draw(); // Vector circle with radius 5

        Shape circle2 = new Circle(new RasterRenderer(),7);
        circle2.Draw(); // Raster circle with radius 7
    }
}

```

**Bridge**, abstraction ve implementasyonu bağımsız yaparak sistemi enek kılar.

### Flyweight Pattern

Amaç: Çok sayıda benzer nesneyi hafızada paylaşarak performansı artırmak.

Kullanım senaryosu: 

- Oyunlardaki çok sayıda aynı tip objeler (ağaç, düşman, taş vb.)
- Grafik objelerinin paylaşımı

```csharp

//Flyweight
public class TreeType{
    public string Name { get; }
    public string Color { get; }

    public TreeType(string name, string color){
        Name = name;
        Color = color;
    }

    public void Display(int x, int y){
        Console.WriteLine($"Tree {Name} ({Color}) at ({x},{y})")
    }
}

//Flyweight Factory
public class TreeFactory{

    private Dictionary<string,TreeType> _treeTypes = new Dictionary<string,TreeType>();

    public TreeType GetTreeType(string name, string color){
        string key = $"{name}_{color}";
        if(!_treeTypes.ContainsKey(key))
            _treeTypes[key] = new TreeType(name,color);
        
        return _treeTypes[key];
    }
}

class Program{
    static void Main(){
        TreeFactory factory = new TreeFactory();

        TreeType oak1 = factory.GetTreeType("Oak","Green");
        TreeType oak2 = factory.GetTreeType("Oak","Green");
        TreeType pine = factory.GetTreeType("Pine","DarkGreen");

        //oak1 ve oak2 aynı instance
        Console.WriteLine(ReferenceEquals(oak1,oak2)); //true
        Console.WriteLine(ReferenceEquals(oak1,pine)); //false

        oak1.Display();
        pine.Display();
    }
}

```

**Flyweight** ile benzer nesneleri paylaşarak hafızayı ve performansı optimize edebiliriz.

#### Structural Patterns Özeti

| `Pattern` | `Amaç/ Kısa Açıklama` |
| --- | --- |
| Adapter | Farklı arayüzleri uyumlu hale getirir. |
| Decorator | Nesnelere dinamik olarak özellik ekler. |
| Facade | Karmaşık sistemi basit bir arayüz ile sunar. |
| Composite | Nesneleri ağaç yapısında gruplayıp tek nesne gibi kullanmayı sağlar. | 
| Proxy | Nesneye erişimi kontrol eder ve geciktirir. |
| Bridge | Abstraction ve implementastonu ayırır, bağımlılığı azaltır. |
| Flyweight | Çok sayıda benzer nesneyi hafızada paylaşır, performansı artırır. |

## Behavioral Patterns

Amaç: Nesnelerin davranışlarını ve birbirleriyle iletişimini düzenlemek, esnek ve sürdürülebilir sistemler tasarlamaktır.

Behavioral Patterns' ler "nesneler ne yapar ve birbiri ile nasıl iletişim kurar?" sorularını çözmek için kullanılır.

### Observer Pattern

Amaç: Bir nesnedeki değişiklikleri ona bağlı diğer nesnelere otomatik olarak bildirmek.

Kullanım senaryosu:

- Event sistemleri (UI' daki buton tıklamaları)
- Stock market veya fiyat değişikliklerini takip eden sistemler
- Chat uygulamalarında mesaj güncellemeleri

> Özet: **Subject (gözlenen)** bir nesnedir. **Observer (gözlemci)** ise değişiklikleri takip eden nesnedir.

```csharp

public interface IInvestor{
    void Update(Stock stock);
}

//Concrete Observer
public class Investor : IInvestor {
    public string Name { get; }

    public Investor(string name){
        Name = name;
    }

    public void Update(Stock stock){
        Console.WriteLine($"Merhaba {name}, {stock.Symbol} fiyatı değişti: {stock.Price}");
    }
}

//Subject
public class Stock {
    private List<IInvestor> _investors = new List<IInvestor>();
    public string Symbol { get; }
    private double _price;

    public Stock(string symbol, double price){
        Symbol = symbol;
        _price = price;
    }

    public double Price{
        get{
            return _price;
        }
        set{
            if(_price != value){
                _price = value;
                Notify();
            }
        }
    }

    public void Attach(IInvestor investor) {
        _investors.Add(investor);
    }

    public void Detach(IInvestor investor){
        _investors.Remove(investor);
    }

    private void Notify(){
        foreach (var investor in _inverstors){
            investor.Update(this);
        }
    }
}

class Program {
    static void Main(){
        Stock apple = new Stock("AAPL",150);
        Investor investor1 = new Investor("Ali");
        Investor investor2 = new Investor("Ayşe");

        apple.Attach(investor1);
        apple.Attach(investor2);

        apple.Price = 155;
        apple.Price = 160;
    }
}

```

```less

Merhaba Ali, AAPL fiyatı değişti: 155
Merhaba Ayşe, AAPL fiyatı değişti: 155
Merhaba Ali, AAPL fiyatı değişti: 160
Merhaba Ayşe, AAPL fiyatı değişti: 160

```

**Stock** -> Subject, fiyat değişikliklerini gözlemcilere bildiriyor.
**Investor** -> Observer, değişikilkleri alıyor ve tepki veriyor.
Observer pattern, loosely coupled bir yapı sağlar; yani subject ve observer birbirine sıkı bağlı değildir.

- Gevşek Bağlılık (loosely coupled): Subject, observer' ın detaylarını bilmez.
- Dinamik İlişki: Çalışma zamanında observer eklenip çıkarılabilir.
- Otomatik güncelleme: Değişiklik olduğunda herkes bilgilendirilir.

**4️⃣ Gerçek dünya analojisi**
Diyelim ki sen bir YouTube kanalına abonesin:
* Kanal = Subject
* Sen = Observer
* Kanala video yüklendiğinde (state değiştiğinde) sen otomatik bildirim alırsın (Update çağırılır.)
* Başka biri de abone olursa aynı şekilde o da bilgilendirilir.

Kısaca Observer Pattern = **publish-subscribe** mekanizması.

### Strategy Pattern

Amaç: Bir algoritmayı veya davranışı çalışma zamanında değiştirmek, farklı yöntemleri aynı interface üzerinden uygulamak.

Kullanım senaryosu:

- Ödeme Yöntemleri (Kredi Kartı, PayPal, Havale)
- Sıralama Algoritmaları (BubbleSort, QuickSort, MergeSort)
- Filtreleme veya hesaplama seçenekleri

> Özet: **Algoritmaları encapsulate edip, çalışma zamanında seçilebilir hale getirebiliriz.**

```csharp

//Stractegy
public interface IPaymentStrategy {
    void Pay(decimal amount);
}

//Concrete Strategy
public class CreaditCardStrategy : IPaymentStrategy {
    public void Pay(decimal amount){
        Console.WriteLine($"{amount} TL Kredi Kartı ile ödendi.");
    }
}

public class PayPalStrategy : IPaymentStrategy {
    public void Pay(decimal amount){
        Console.WriteLine($"{amount} TL PayPal ile ödendi.");
    }
}

//Context
public class ShoppingCart {
    private IPaymentStrategy _paymentStrategy;

    public void SetPaymentStrategy(IPaymentStrategy strategy){
        _paymentStrategy = strategy;
    }

    public void Checkout(decimal amount){
        _paymentStrategy.Pay(amount);
    }
}

class Program{
    static void Main(){
        ShoppingCart cart = new ShoppingCart();

        cart.SetPaymentStrategy(new CreditCardStrategy());
        cart.Chekout(200); // 200 TL kredi kartı ile ödendi.

        cart.SetPaymentStrategy(new PayPalStrategy());
        cart.Checkout(150); // 150 TL PayPal ile ödendi.
    }
}

```

`IPaymentStrategy` -> Algoritmayı tanımlar (interface).
`CreditCardPayment`, `PayPalPayment` -> Concrete strategy, algoritmanın farklı versiyonları.
`ShoppingCart` -> Context, strategy'i çalışma zamanında seçer.

**Avantaj:**
* Yeni ödeme yöntemi eklemek kolaydır. (Yeni ConcreteStrategy ekle.)
* Contect kodunu değiştirmeye gerek yok -> (**Open/ Closed Principle**' a uygun)

---

> Open/Closed Principle Nedir ? 

**Yazılım var olan davranışları değiştirmeye gerek kalmadan yeni işlevler eklemeye açık, mevcut kod değişikliğine kapalı olmalıdır.**

* Open (Açık): Yeni özellik eklemeye açık.
* Closed (Kapalı): Mevcut kodu değiştirmeye kapalı.

Amaç: Kodun yeniden kullanılabilirliğini artırmak ve hataları azaltmak.

**Özet Mantık:**
- Kod değiştirmeden genişletilebilir olmalı.
- Yeni davranış eklemek mevcut kodu kırmadan yapılmalı.

---

### Command Pattern

Amaç: bir işlemi nesne olarak kapsülleyip, çağrı ve yürütme zamanını ayırmak.

Kullanım senaryosu:

- Undo/Redo işlemleri (metin editörü)
- Task scheduling/ job queue
- GUI butonları ve event handling

> Özet: **Komutları nesne olarak paketleriz ve onları istediğimiz zaman çağırabiliriz.**

```csharp

//Command Interface
public interface ICommand{
    void Execute();
}

//Receiver
public class Light{
    public void On(){
        Console.WriteLine("Light opened!");
    }

    public void Off(){
        Console.WriteLine("Light closed!");
    }
}

//Concrete Commands
public class LightOnCommand : ICommand {
    private Light _light;
    public LightCommand(Light light){
        _light = light;
    }
    public void Execute(){
        _light.On();
    }
}

public class LightOffCommand : ICommand {
    private Light _light;
    public LightCommand(Light light){
        _light = light;
    }
    public void Execute(){
        _light.Off();
    }
}


//Invoker
public class RemoteControl{
    private ICommand _command;
    public void SetCommand(ICommand command){
        _command = command;
    }
    public void PressButton(){
        _command.Execute();
    } 
}

class Program{
    static void Main(){
        Light livingRoomLight = new Light();
        ICommand lightOn = new LightOnCommand(livingRoomLight);
        ICommand lightOff = new LightOffCommand(livingRoomLight);

        RemoteControl remote = new RemoteControl();

        remote.SetCommand(lightOn);
        remote.PressButton(); //Light opened!

        remote.SetCommand(lightOff);
        remote.PressButton(); //Light closed!
    }
}

```

`ICommand` -> Komutları tanımlar.
`LightOnCommand`, `LightOffCommand` -> Concrete Command, receiver' ı çağırır.
`RemoteControl` -> Invoker, komutları çalıştırır.

**Avantaj:**
* İşlemler nesne olarak saklanır -> queue, undo/redo veya logging kolay olur.
* Invoker ve receiver loosely coupled.

### Chain of Responsibilility Pattern

Amaç: Bir isteği bir zincir boyunca iletip, isteği işleyebilecek uygun nesnenin işlemesini sağlamak.

Kullanım senaryosu:

- Hata/ Exception yönetimi
- Event Handling
- Yetki kontrolü/ Access Control

> Özet: **İstekleri zincir boyunca iletir, hangi nesne uygun ise o işleme alır.**

```csharp
//Handler (abstract)

public abstract class Handler {
    protected Handler _next;
    public void SetNext(Handler next){
        _next = next;
    }
    public abstract void Handle(string request);
}

//Concreate Handlers
public class AdminHandler : Handler {

    public override void Handle(string request){
        if(request == "Admin")
            Console.WriteLine("Admin isteği işlendi!");
        else if (_next != null)
            _next.Handle(request);
    }
}

public class UserHandler : Handler {

    public override void Handle(string request){
        if(request == "User")
            Console.WriteLine("User isteği işlendi.");
        else if (_next != null)
            _next.Handle(request);
    }
}

public class GuestHandler : Handler {

    public override void Handle(string request){
        if(request == "Guest")
            Console.WriteLine("Guest isteği işlendi");
        else
            Console.WriteLine("İstek işlenemedi");
    }
}

class Program {
    static void Main(){
        Handler admin = new AdminHandler();
        Handler user = new UserHandler();
        Handler guest = new GuestHandler();

        admin.SetNext(user);
        user.SetNext(guest);

        admin.Handle("User"); // User isteği işlendi
        admin.Handle("Guest"); // Guest isteği işlendi
        admin.Handle("Super"); // İstek işlenemedi
    }
}

```

* `Handler` -> abstract sınıf, isteği işleyebilir veya bir sonraki handler' a iletir.
* Concrete Handler' lar -> kendilerine uygun isteği işleyip, uygun değilse zincirdeki diğer handler' a iletir.

**Avantaj:**
* İstekler nesneler arası zincir boyunca akabilir. -> loosely coupled.
* Zincire yeni handler eklemek kolaydır.

