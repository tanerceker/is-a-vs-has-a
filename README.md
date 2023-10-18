<br/>

# is-a vs has-a

Nesne-yönelimli programlamada (OOP) "is-a" ve "has-a" ilişkileri, sınıflar ve nesneler arasındaki ilişkileri modellemek için kullanılan temel kavramlardır. Bu ilişkiler, sınıfların ve nesnelerin birbirleriyle nasıl etkileşime girdiğini tanımlamaya yardımcı olur. Bu kavramları Typescript kullanarak açıklayacağım ve bunları göstermek için birçok örnek vereceğim.

<br/>

---

<br/>

## "is-a" ilişkisi (Inheritance — Kalıtım)

"is-a" ilişkisi, bir sınıfın başka bir sınıfın özelleşmiş bir sürümü olduğu kalıtımı (inheritance) temsil eder. Typescript'te, sınıf kalıtımını kullanarak bunu başarabilirsiniz. Bir alt sınıf (subclass), üst sınıfından (superclass) özellikleri ve yöntemleri miras alır. İşte bir örnek:

```tsx
class Animal {
  constructor(public name: string) {}

  makeSound() {
    console.log("Animal makes a sound");
  }
}

class Dog extends Animal {
  constructor(name: string) {
    super(name);
  }

  makeSound() {
    console.log("Dog barks");
  }
}

const myDog = new Dog("Buddy");
console.log(myDog.name); // Output: Buddy
myDog.makeSound(); // Output: Dog barks
```

Bu örnekte, Dog, Animal'ın bir alt sınıfıdır (subclass). Name özelliğini ve makeSound yöntemini Animal'dan kalıtım (inheritance) alır. Son olarak Dog sınıfında makeSound yöntemi geçersiz kılınır (override) ve kendi mantığını uygular.

<br/>

---

<br/>

## "has-a" ilişkisi (Composition — Bileşim)

"has-a" ilişkisi, bir sınıfın kendi iç yapısının bir parçası olarak başka bir sınıfın örneğini (instance) içerdiği bileşimi (composition) temsil eder. Typescript'te, sınıfınızın içinde başka bir sınıfın örneğini (instance) oluşturarak bunu başarabilirsiniz. İşte bir örnek:

```tsx
class Engine {
  start() {
    console.log("Engine started");
  }
}

class Car {
  private engine: Engine;

  constructor() {
    this.engine = new Engine();
  }

  start() {
    console.log("Car started");
    this.engine.start();
  }
}

const myCar = new Car();
myCar.start();
```

Bu örnekte, Car sınıfının Engine sınıfıyla bir "has-a" ilişkisi vardır. Private üye olarak Engine sınıfının bir örneğini (instance) içerir ve arabayı çalıştırdığınızda motoru da çalıştırır.

**Not:** Yukarıdaki kod bloğu tamamen konu anlatımını netleştirmek için basit tutulmuştur. Ancak ileri düzeyde bazı sorunlar yaratmaktadır;

1. Yapıcıdaki (constructor) engine değişkeni sıkı bağlantı (tight coupled) sorunu yaratmaktadır.
2. Engine sınıfı somut bir uygulamadır (concrete implementation) buda aslında genel olarak bir başka sorundur.

SOLID ilkelerini kullanarak tüm bu sorunların üstesinden gelebilir, gevşek bağlantı (loose coupled) ve soyut uygulama (abstract implementation) sağlayabiliriz.

<br/>

---

<br/>

## "is-a" ve "has-a" birlikte (Hibrit — Hybrid)

Bazen kodunuzda hem "is-a" hem de "has-a" ilişkilerini kullanırsınız.

Örneğin, bir Person sınıfınız ve bir Job sınıfınız olduğu bir senaryoyu düşünün:

```tsx
class Person {
  constructor(public name: string) {}
}

class Job {
  private title: string;
  private salary: number;

  constructor(title: string, salary: number) {
    this.title = title;
    this.salary = salary;
  }

  getInfo() {
    return `Title: ${this.title}, Salary: ${this.salary}`;
  }
}

// inheritance — kalıtım
class Employee extends Person {
  private job: Job; // composition — bileşim

  constructor(name: string, jobTitle: string, salary: number) {
    super(name); // inheritance — kalıtım
    this.job = new Job(jobTitle, salary); // composition — bileşim
  }

  getJobInfo() {
    return this.job.getInfo(); // composition — bileşim
  }
}

const john = new Employee("John", "Software Developer", 10000);
console.log(john.name);
// Output: John
console.log(john.getJobInfo());
// Output: Title: Software Developer, Salary: 10000
```

Bu örnekte, Employee sınıfı Person'ın bir alt sınıfıdır (subclass) ("is-a" ilişkisini temsil eder). Ve iç yapısının bir parçası olarak bir Job nesnesine sahiptir ("has-a" ilişkisini temsil eder).

<br/>
<br/>

Tüm bu örnekler, sınıflar arasındaki farklı ilişki türlerini modellemek için Typescript'te
"is-a" (inheritance — kalıtım) ve "has-a" (composition — bileşim) ilişkilerinin nasıl kullanılacağını göstermektedir.

---

— Taner Çeker tarafından hazırlanmıştır.
