Конечно, такие задачи популярны на интервью по Java, поскольку они помогают оценить понимание ООП, полиморфизма, инкапсуляции, наследования и других основополагающих принципов. Вот несколько примеров с объяснениями:

### Пример 1: Полиморфизм и переопределение методов

```java
class Animal {
    public void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    public void sound() {
        System.out.println("Bark");
    }
}

public class Test {
    public static void main(String[] args) {
        Animal animal = new Dog();
        animal.sound();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет `Bark`.  
Это происходит потому, что метод `sound()` переопределен в классе `Dog`. При вызове `animal.sound()` используется метод `sound()` класса `Dog`, несмотря на то, что переменная `animal` имеет тип `Animal`. Это демонстрация полиморфизма, когда вызывается метод подкласса, а не суперкласса, если он переопределен.

### Пример 2: Скрытие полей и методы с одинаковыми именами

```java
class Parent {
    public String name = "Parent";

    public void printName() {
        System.out.println(name);
    }
}

class Child extends Parent {
    public String name = "Child";
}

public class Test {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.printName();
        System.out.println(obj.name);
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Parent
Parent
```

Метод `printName()` вызывается от имени объекта `obj` типа `Parent`, и хотя объект фактически является экземпляром `Child`, переменная `name` не переопределена, а скрыта. Вызов `obj.name` возвращает значение поля `name` класса `Parent`, поскольку поля не подлежат полиморфизму, как методы. В Java полиморфизм работает только для методов, но не для полей.

### Пример 3: Статические методы и наследование

```java
class A {
    public static void print() {
        System.out.println("Class A");
    }
}

class B extends A {
    public static void print() {
        System.out.println("Class B");
    }
}

public class Test {
    public static void main(String[] args) {
        A a = new B();
        a.print();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет `Class A`.

Это происходит потому, что статические методы не участвуют в механизме полиморфизма. Вызывается метод `print()` класса `A`, так как статические методы привязаны к классу, а не к экземпляру. Переменная `a` имеет тип `A`, поэтому вызов `a.print()` вызывает `A.print()`, даже если объект создан как экземпляр `B`.

### Пример 4: Конструкторы и порядок инициализации

```java
class Parent {
    public Parent() {
        System.out.println("Parent constructor");
    }
}

class Child extends Parent {
    public Child() {
        System.out.println("Child constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        new Child();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Parent constructor
Child constructor
```

Когда создается экземпляр класса `Child`, сначала вызывается конструктор класса `Parent`, а затем конструктор класса `Child`. В Java при создании объекта подкласса сначала вызываются конструкторы всех суперклассов (начиная с самого верхнего), а затем конструкторы самого подкласса.

### Пример 5: Абстрактные классы и интерфейсы

```java
interface Animal {
    void sound();
}

abstract class Dog implements Animal {
    public void sound() {
        System.out.println("Woof");
    }
}

class Labrador extends Dog {
    @Override
    public void sound() {
        System.out.println("Labrador Woof");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog dog = new Labrador();
        dog.sound();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет `Labrador Woof`.

В этом примере `Dog` — это абстрактный класс, который реализует интерфейс `Animal` и предоставляет реализацию метода `sound()`. Класс `Labrador` переопределяет метод `sound()`. При вызове `dog.sound()` используется переопределенный метод класса `Labrador`, поскольку объект создан как экземпляр `Labrador`.

### Пример 6: Конструкторы с параметрами и наследование

```java
class A {
    public A(String message) {
        System.out.println("A: " + message);
    }
}

class B extends A {
    public B() {
        super("Hello from B");
        System.out.println("B: No arguments constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        new B();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
A: Hello from B
B: No arguments constructor
```

Конструктор `B()` сначала вызывает `super("Hello from B")`, то есть конструктор класса `A` с одним аргументом, передавая ему строку `"Hello from B"`. После этого выполняется оставшийся код конструктора `B`, который выводит `B: No arguments constructor`.

Вот ещё несколько примеров задач на ООП в Java, которые подчеркивают различные аспекты, не пересекающиеся с теми, что были выше.

### Пример 7: Вызов конструктора при наследовании и порядок инициализации полей

```java
class Animal {
    String type = "Unknown Animal";

    public Animal() {
        System.out.println("Animal Constructor");
        System.out.println("Type in Animal constructor: " + type);
    }
}

class Dog extends Animal {
    String type = "Dog";

    public Dog() {
        System.out.println("Dog Constructor");
        System.out.println("Type in Dog constructor: " + type);
    }
}

public class Test {
    public static void main(String[] args) {
        new Dog();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Animal Constructor
Type in Animal constructor: Unknown Animal
Dog Constructor
Type in Dog constructor: Dog
```

Когда создается объект `Dog`, сначала вызывается конструктор суперкласса `Animal`. В этот момент переменная `type` класса `Animal` инициализирована как `"Unknown Animal"`. После выполнения конструктора `Animal` вызывается конструктор `Dog`, и используется уже определенное в `Dog` значение `type`, то есть `"Dog"`. Поля классов инициализируются до выполнения их конструкторов, и так как переменные экземпляра не подлежат полиморфизму, `type` берется из соответствующего класса.


### Пример 8: Исключения при наследовании

```java
class SuperClass {
    public void riskyMethod() throws Exception {
        System.out.println("SuperClass riskyMethod");
    }
}

class SubClass extends SuperClass {
    @Override
    public void riskyMethod() {
        System.out.println("SubClass riskyMethod");
    }
}

public class Test {
    public static void main(String[] args) {
        SuperClass obj = new SubClass();
        try {
            obj.riskyMethod();
        } catch (Exception e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
SubClass riskyMethod
```

Здесь метод `riskyMethod()` в `SubClass` не выбрасывает исключение. Java позволяет подклассу переопределять метод суперкласса без исключения или с исключением более узкого типа, чем у метода суперкласса. Так как в `SubClass` исключение не выбрасывается, блок `catch` не срабатывает. Полиморфизм позволяет вызвать метод подкласса `SubClass`, несмотря на то, что переменная `obj` имеет тип `SuperClass`.

### Пример 9: Вызов перегруженных методов

```java
class OverloadTest {
    public void print(Object obj) {
        System.out.println("Object version: " + obj);
    }

    public void print(String str) {
        System.out.println("String version: " + str);
    }
}

public class Test {
    public static void main(String[] args) {
        OverloadTest ot = new OverloadTest();
        ot.print(null);
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
String version: null
```

Метод `print` перегружен: один из них принимает `Object`, другой — `String`. Вызов `ot.print(null)` вызывает `print(String str)`, поскольку `String` является более специфичным типом для `null`, чем `Object`. Если бы метода `print(String str)` не существовало, тогда вызвался бы `print(Object obj)`.

### Пример 10: Интерфейсы и множественное наследование

```java
interface A {
    default void print() {
        System.out.println("Interface A");
    }
}

interface B {
    default void print() {
        System.out.println("Interface B");
    }
}

class C implements A, B {
    @Override
    public void print() {
        A.super.print();
        B.super.print();
        System.out.println("Class C");
    }
}

public class Test {
    public static void main(String[] args) {
        C obj = new C();
        obj.print();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Interface A
Interface B
Class C
```

Здесь класс `C` реализует два интерфейса `A` и `B`, оба из которых имеют метод `print()` с реализацией по умолчанию. Поскольку в Java нет множественного наследования классов, но интерфейсы поддерживают реализацию методов по умолчанию, возникает необходимость указать, какой именно метод вызвать. В `C` метод `print` вызывает `A.super.print()` и `B.super.print()`, затем выполняет свою логику, выводя строку `Class C`.

### Пример 11: Локальные переменные и поля класса

```java
class Counter {
    public int count = 10;

    public void updateCount(int count) {
        count = count + 1;
        this.count = this.count + 1;
    }
}

public class Test {
    public static void main(String[] args) {
        Counter counter = new Counter();
        counter.updateCount(5);
        System.out.println("Local count: 5");
        System.out.println("Instance count: " + counter.count);
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Local count: 5
Instance count: 11
```

Метод `updateCount` принимает параметр `count`, который скрывает поле `count` класса `Counter`. Когда выполняется `count = count + 1`, это увеличивает локальную переменную, а не поле экземпляра. Но `this.count = this.count + 1` увеличивает именно поле `count` класса, то есть значение поля `count` объекта `counter` увеличивается с 10 до 11.

### Пример 12: Порядок инициализации статических и нестатических блоков

```java
class InitExample {
    static {
        System.out.println("Static block");
    }

    {
        System.out.println("Instance block");
    }

    public InitExample() {
        System.out.println("Constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        System.out.println("Main method");
        new InitExample();
        new InitExample();
    }
}
```

**Вопрос:** Что выведет данный код и почему?

**Ответ:**  
Код выведет:
```
Static block
Main method
Instance block
Constructor
Instance block
Constructor
```

Объяснение:
- Сначала выполняется статический блок, который запускается один раз при загрузке класса.
- Затем запускается метод `main`.
- При создании первого экземпляра `InitExample` сначала выполняется нестатический блок `{}`, а затем конструктор.
- Для второго экземпляра вновь запускаются нестатический блок и конструктор.