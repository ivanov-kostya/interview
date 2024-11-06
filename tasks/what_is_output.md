На собеседованиях часто дают примеры кода на Java, чтобы проверить знание синтаксиса, понимание работы JVM, знаний по ООП и коллекциям, а также внимательность к деталям. Ниже несколько примеров задач такого типа с объяснением:

### Пример 1: Работа с `String` и `StringBuilder`
**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");
        String str4 = "Hel" + "lo";
        
        System.out.println(str1 == str2);   // Линия 1
        System.out.println(str1 == str3);   // Линия 2
        System.out.println(str1 == str4);   // Линия 3
        System.out.println(str1.equals(str3)); // Линия 4
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Линия 1: `true` — переменные `str1` и `str2` указывают на одну и ту же строку в пуле строк (String Pool).
- Линия 2: `false` — `str3` создан с использованием `new String("Hello")`, и это новый объект, не связанный с пулом строк.
- Линия 3: `true` — компилятор объединяет литералы, поэтому `str4` указывает на ту же строку, что и `str1`.
- Линия 4: `true` — метод `equals()` сравнивает содержимое строки, а не ссылки.

**Вывод в консоль:**
```
true
false
true
true
```

### Пример 2: Автоупаковка (Autoboxing) и `==`
**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        Integer a = 127;
        Integer b = 127;
        Integer c = 128;
        Integer d = 128;
        
        System.out.println(a == b); // Линия 1
        System.out.println(c == d); // Линия 2
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Линия 1: `true` — значения от -128 до 127 кэшируются в памяти, поэтому `a` и `b` указывают на один и тот же объект.
- Линия 2: `false` — значения вне диапазона кэширования создаются как новые объекты, поэтому `c` и `d` указывают на разные объекты.

**Вывод в консоль:**
```
true
false
```

### Пример 3: Исключения и порядок выполнения
**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("A");
            int x = 5 / 0;
            System.out.println("B");
        } catch (ArithmeticException e) {
            System.out.println("C");
        } finally {
            System.out.println("D");
        }
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Сначала будет выведено `"A"`.
- При делении на ноль будет выброшено исключение `ArithmeticException`, и выполнение перейдет в блок `catch`.
- В блоке `catch` будет выведено `"C"`.
- После этого выполнится блок `finally`, который всегда выполняется, и будет выведено `"D"`.

**Вывод в консоль:**
```
A
C
D
```

### Пример 4: Полиморфизм и вызов методов
**Задание:**
```java
class A {
    void print() {
        System.out.println("A");
    }
}

class B extends A {
    void print() {
        System.out.println("B");
    }
}

public class Test {
    public static void main(String[] args) {
        A obj = new B();
        obj.print();
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Переменная `obj` имеет тип `A`, но фактический объект — это `B`.
- При вызове `obj.print()` используется полиморфизм, поэтому JVM вызывает метод `print()` класса `B`.

**Вывод в консоль:**
```
B
```

### Пример 5: Работа с `HashMap` и `null`
**Задание:**
```java
import java.util.HashMap;

public class Test {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put(null, 1);
        map.put("key", null);
        
        System.out.println(map.get(null)); // Линия 1
        System.out.println(map.get("key")); // Линия 2
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Линия 1: `1` — в `HashMap` ключ `null` допустим, и значение `1` будет возвращено.
- Линия 2: `null` — также допустимо хранить `null` в значении.

**Вывод в консоль:**
```
1
null
```

### Пример 6: Статические и нестатические методы
**Задание:**
```java
class Parent {
    static void staticMethod() {
        System.out.println("Static method in Parent");
    }
    
    void instanceMethod() {
        System.out.println("Instance method in Parent");
    }
}

class Child extends Parent {
    static void staticMethod() {
        System.out.println("Static method in Child");
    }
    
    @Override
    void instanceMethod() {
        System.out.println("Instance method in Child");
    }
}

public class Test {
    public static void main(String[] args) {
        Parent obj = new Child();
        obj.staticMethod(); // Линия 1
        obj.instanceMethod(); // Линия 2
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Линия 1: `Static method in Parent` — статические методы не переопределяются, вызов зависит от типа переменной (`Parent`).
- Линия 2: `Instance method in Child` — нестатический метод вызывается на основе фактического типа объекта, который является `Child`.

**Вывод в консоль:**
```
Static method in Parent
Instance method in Child
```

Эти примеры демонстрируют разные аспекты Java, которые часто тестируются на собеседованиях: понимание ссылок, автоупаковки, исключений, полиморфизма, работы с коллекциями и статическими методами.


Конечно! Вот ещё несколько популярных примеров задач на Java, которые часто встречаются на собеседованиях. Эти задачи позволяют проверять знания по конструкциям языка, многопоточности и нюансам Java.

---

### Пример 7: Многопоточность и `synchronized`

**Задание:**
```java
public class Test {
    private static int counter = 0;

    public static synchronized void increment() {
        counter++;
    }

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                increment();
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println(counter); // Линия 1
    }
}
```

**Вопрос:** Какое значение выведется в консоль?

**Ответ:**

Поскольку метод `increment()` синхронизирован, `counter` увеличивается правильно при каждом вызове, и в конечном итоге выводится значение `2000`, так как оба потока увеличивают счётчик по 1000 раз.

**Вывод в консоль:**
```
2000
```

---

### Пример 8: Неявное приведение типов и потеря данных

**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        int largeValue = 130;
        byte smallValue = (byte) largeValue;
        
        System.out.println(smallValue); // Линия 1
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Здесь происходит приведение `int` к `byte`, но значение `130` выходит за пределы диапазона типа `byte` (-128 до 127). При приведении происходит переполнение, и значение `130` преобразуется в `-126`.

**Вывод в консоль:**
```
-126
```

---

### Пример 9: Инициализация статических и нестатических блоков

**Задание:**
```java
class A {
    static {
        System.out.println("Static Block A");
    }

    {
        System.out.println("Instance Block A");
    }

    public A() {
        System.out.println("Constructor A");
    }
}

class B extends A {
    static {
        System.out.println("Static Block B");
    }

    {
        System.out.println("Instance Block B");
    }

    public B() {
        System.out.println("Constructor B");
    }
}

public class Test {
    public static void main(String[] args) {
        new B();
    }
}
```

**Вопрос:** В каком порядке будут выведены строки?

**Ответ:**

Порядок выполнения следующий:
1. Выполняется статический блок класса `A`, затем статический блок класса `B`.
2. Выполняются нестатические блоки в порядке иерархии от родителя к потомку: сначала `A`, затем `B`.
3. Выполняется конструктор родительского класса `A`, затем конструктор класса `B`.

**Вывод в консоль:**
```
Static Block A
Static Block B
Instance Block A
Constructor A
Instance Block B
Constructor B
```

---

### Пример 10: Пример с интерфейсами и default-методами

**Задание:**
```java
interface InterfaceA {
    default void print() {
        System.out.println("InterfaceA");
    }
}

interface InterfaceB {
    default void print() {
        System.out.println("InterfaceB");
    }
}

public class Test implements InterfaceA, InterfaceB {
    public void print() {
        InterfaceA.super.print();
        InterfaceB.super.print();
    }

    public static void main(String[] args) {
        Test test = new Test();
        test.print();
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Здесь класс `Test` реализует два интерфейса с одинаковым методом `print()`. Поэтому необходимо явно указать, какой именно метод вызвать из каждого интерфейса, используя `InterfaceA.super.print()` и `InterfaceB.super.print()`. В результате оба метода будут вызваны последовательно.

**Вывод в консоль:**
```
InterfaceA
InterfaceB
```

---

### Пример 11: Перегрузка методов с `null`

**Задание:**
```java
public class Test {
    public static void print(Object obj) {
        System.out.println("Object");
    }

    public static void print(String str) {
        System.out.println("String");
    }

    public static void main(String[] args) {
        print(null); // Линия 1
    }
}
```

**Вопрос:** Какой метод будет вызван и что будет выведено?

**Ответ:**

Компилятор выберет перегруженный метод с наиболее специфичным типом. Поскольку `String` является более специфичным типом, чем `Object`, будет вызван метод `print(String str)`.

**Вывод в консоль:**
```
String
```

---

### Пример 12: Неизменяемость объекта и `final`

**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        final StringBuilder sb = new StringBuilder("Hello");
        sb.append(", World!");
        System.out.println(sb); // Линия 1
    }
}
```

**Вопрос:** Будет ли ошибка компиляции? И что будет выведено в консоль?

**Ответ:**

Ключевое слово `final` указывает, что переменная `sb` не может быть переназначена, но сам объект `StringBuilder` остаётся изменяемым. Поэтому `sb.append(", World!")` изменит содержимое `StringBuilder`, и в консоль будет выведено `Hello, World!`.

**Вывод в консоль:**
```
Hello, World!
```

---

### Пример 13: Вложенные классы и доступ к переменным

**Задание:**
```java
public class Outer {
    private int x = 10;

    class Inner {
        private int x = 20;

        public void print() {
            int x = 30;
            System.out.println(x);           // Линия 1
            System.out.println(this.x);      // Линия 2
            System.out.println(Outer.this.x);// Линия 3
        }
    }

    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner();
        inner.print();
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**
- Линия 1: Локальная переменная `x` внутри метода `print()` имеет значение `30`, так что будет выведено `30`.
- Линия 2: Используется `this.x`, где `this` указывает на текущий экземпляр `Inner`, поэтому будет выведено `20`.
- Линия 3: Используется `Outer.this.x`, чтобы получить доступ к переменной `x` внешнего класса `Outer`, её значение `10`.

**Вывод в консоль:**
```
30
20
10
```

Эти примеры демонстрируют более глубокие концепции Java, такие как многопоточность, работа с типами и методами, вложенные классы и модификаторы доступа, что полезно проверять на собеседованиях для выявления уровня понимания внутренней работы Java.


Конечно, вот ещё несколько интересных примеров задач на Java, которые проверяют тонкости работы с особенностями языка, коллекциями, исключениями и потоками.

---

### Пример 14: Поведение `ArrayList` при изменении размера в цикле

**Задание:**
```java
import java.util.ArrayList;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        for (int i = 1; i <= 5; i++) {
            list.add(i);
        }
        
        for (int i = 0; i < list.size(); i++) {
            if (list.get(i) % 2 == 0) {
                list.remove(i);
            }
        }
        
        System.out.println(list);
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Здесь мы удаляем элементы из `ArrayList` во время итерации. При удалении элемента сдвигаются индексы последующих элементов, из-за чего элементы пропускаются.

Этапы выполнения:
1. `i = 0`: Удаление не происходит (`1 % 2 != 0`).
2. `i = 1`: Удаляется `2`, и индексы сдвигаются.
3. `i = 2`: Пропускается `4` из-за смещения индексов.

**Результат**:
```
[1, 3, 5]
```

---

### Пример 15: Проблема с `HashSet` и переопределение `equals()` и `hashCode()`

**Задание:**
```java
import java.util.HashSet;
import java.util.Set;

class Point {
    int x, y;

    Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Point point = (Point) obj;
        return x == point.x && y == point.y;
    }
}

public class Test {
    public static void main(String[] args) {
        Set<Point> points = new HashSet<>();
        points.add(new Point(1, 2));
        points.add(new Point(1, 2));
        
        System.out.println(points.size());
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

У `Point` переопределён метод `equals()`, но `hashCode()` не переопределён, что нарушает контракт `equals()` и `hashCode()`. `HashSet` использует `hashCode()` для сравнения, и так как он не переопределён, два объекта считаются разными.

**Вывод в консоль:**
```
2
```

---

### Пример 16: Особенности работы с `try` и `finally`

**Задание:**
```java
public class Test {
    public static int testMethod() {
        try {
            return 1;
        } finally {
            return 2;
        }
    }

    public static void main(String[] args) {
        System.out.println(testMethod());
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Когда `return` выполняется в `try`, результат сохраняется, но затем выполняется `finally`. Если `finally` также содержит `return`, то возвращаемое значение будет перезаписано и вернётся `2`.

**Вывод в консоль:**
```
2
```

---

### Пример 17: Использование `Optional` и `orElse`

**Задание:**
```java
import java.util.Optional;

public class Test {
    public static void main(String[] args) {
        String value = null;
        String result = Optional.ofNullable(value).orElse(getDefault());
        System.out.println(result);
    }

    public static String getDefault() {
        System.out.println("Calling getDefault()");
        return "Default Value";
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Метод `getDefault()` будет вызван и вернёт значение `"Default Value"`, так как `value` равен `null`. `orElse` вызывает метод `getDefault()`, даже если значение присутствует.

**Вывод в консоль:**
```
Calling getDefault()
Default Value
```

---

### Пример 18: Вложенные циклы и `continue` с метками

**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        outer:
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (j == 1) {
                    continue outer;
                }
                System.out.println("i = " + i + ", j = " + j);
            }
        }
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Когда `j == 1`, выполняется `continue outer`, который продолжает итерацию внешнего цикла, пропуская остальные шаги внутреннего. В результате строки, где `j >= 1`, пропускаются.

**Вывод в консоль:**
```
i = 0, j = 0
i = 1, j = 0
i = 2, j = 0
```

---

### Пример 19: Ковариантность возвращаемых значений

**Задание:**
```java
class Parent {
    Parent get() {
        return this;
    }
}

class Child extends Parent {
    @Override
    Child get() {
        return this;
    }
    
    void message() {
        System.out.println("Hello from Child");
    }
}

public class Test {
    public static void main(String[] args) {
        new Child().get().message();
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Ковариантность позволяет `Child` возвращать `Child` вместо `Parent`. Метод `get()` у `Child` возвращает `Child`, поэтому `message()` доступен.

**Вывод в консоль:**
```
Hello from Child
```

---

### Пример 20: Многопоточность и гонка потоков

**Задание:**
```java
public class Test {
    private int count = 0;

    public void increment() {
        count++;
    }

    public static void main(String[] args) throws InterruptedException {
        Test test = new Test();
        
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                test.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                test.increment();
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();
        
        System.out.println(test.count);
    }
}
```

**Вопрос:** Какое значение может быть выведено в консоль?

**Ответ:**

Здесь не используется синхронизация для метода `increment()`, поэтому при параллельном выполнении возникают состояния гонки. Ожидаемое значение — `2000`, но фактическое может быть меньше из-за непредсказуемых операций `count++`.

**Пример вывода:**
```
1800  // или любое другое значение от 1000 до 2000
```

---

### Пример 21: `Integer` и `==` с `new`

**Задание:**
```java
public class Test {
    public static void main(String[] args) {
        Integer a = new Integer(100);
        Integer b = new Integer(100);
        System.out.println(a == b);   // Линия 1
        System.out.println(a.equals(b)); // Линия 2
    }
}
```

**Вопрос:** Что будет выведено в консоль?

**Ответ:**

Использование `new` создаёт разные объекты, даже если их значения равны.
- Линия 1: `false` — так как `a` и `b` указывают на разные объекты.
- Линия 2: `true` — метод `equals()` сравнивает значения.

**Вывод в консоль:**
```
false
true
```

---

Эти примеры затрагивают такие аспекты, как особенности работы `continue` с метками, ошибки в многопоточности, нюансы работы `Integer` с операторами сравнения, `ArrayList` в циклах и использование меток.


