Задачи на тему Generics (обобщений) — это популярный тип вопросов на собеседованиях для проверки понимания кандидатами того, как работает типизация в Java, особенно с учётом различий между дженериками, ковариантностью, контравариантностью и другими аспектами. Вот несколько примеров задач с кодом и объяснениями, что и почему будет выведено на консоль.

### Задача 1: Основы Generics

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> integerBox = new Box<>(10);
        Box<String> stringBox = new Box<>("Hello");

        System.out.println(integerBox.getValue());
        System.out.println(stringBox.getValue());
    }
}
```

**Ответ:**

```
10
Hello
```

**Объяснение:**
- Класс `Box<T>` — это обобщённый тип, который может хранить значения любого типа.
- Мы создаём два объекта `Box`: один для типа `Integer`, другой — для `String`.
- В методе `main` выводятся значения, хранящиеся в этих объектах.
- Метод `getValue()` возвращает значение, которое хранится в обобщённом контейнере, и выводятся значения `10` и `"Hello"`.

---

### Задача 2: Типы и приведение типов

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<? extends Number> numberBox = new Box<>(10);
        System.out.println(numberBox.getValue());
    }
}
```

**Ответ:**

```
10
```

**Объяснение:**
- В этом примере мы используем wildcard (`? extends Number`), который ограничивает тип `T` только типами, наследующими `Number` (например, `Integer`, `Double` и т. д.).
- Мы создаём объект `Box` с типом `Integer`, который является подтипом `Number`.
- При вызове `getValue()` мы получаем `Integer` (в данном случае `10`), который успешно выводится на консоль.
- `? extends Number` позволяет работать с любыми типами, которые являются подтипами `Number`.

---

### Задача 3: Ограничения для Generics

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public void printValue() {
        System.out.println(value);
    }
}

public class Main {
    public static void main(String[] args) {
        Box<? super Integer> box = new Box<>(10);
        box.printValue();
    }
}
```

**Ответ:**

```
10
```

**Объяснение:**
- В этом примере используется wildcard `? super Integer`, который ограничивает тип `T` типами, которые могут быть родителями `Integer`, включая сам `Integer` и `Number`.
- Мы создаём объект типа `Box`, который может хранить типы, такие как `Integer` или более высокие типы, например `Number`.
- Вызов метода `printValue()` выводит значение `10`, которое хранится в объекте `Box`.

---

### Задача 4: Проблема с дженериками и типами

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public void printValue() {
        System.out.println(value);
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Number> box = new Box<>(10);
        Box<Integer> integerBox = (Box<Integer>) box; // Приведение типов
        integerBox.printValue();
    }
}
```

**Ответ:**

```
10
```

**Объяснение:**
- Здесь возникает интересная ситуация с приведением типов. Мы создаём объект `Box<Number>` и пытаемся привести его к типу `Box<Integer>`. На самом деле, это небезопасное приведение, потому что мы не можем гарантировать, что объект типа `Box<Number>` действительно является объектом типа `Box<Integer>`.
- Несмотря на это, программа компилируется и работает корректно, выводя значение `10`, потому что фактически в объекте хранится `Integer` (который является подтипом `Number`).
- Однако, в реальной практике такие приведения могут приводить к исключениям `ClassCastException`, если типы не совпадают.

---

### Задача 5: Сложные дженерики с методами

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public <U> void printValue(U value) {
        System.out.println(value);
    }
}

public class Main {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>("Hello");
        stringBox.printValue(10);
    }
}
```

**Ответ:**

```
10
```

**Объяснение:**
- Здесь метод `printValue` является обобщённым, и его параметр `value` имеет тип `U`, который не связан с типом `T` класса `Box`.
- Мы вызываем `printValue(10)` на объекте `Box<String>`, но передаем значение типа `Integer` в метод. Тип `U` может быть любым, и поэтому компилятор не даёт ошибки.
- Метод выводит значение `10`, потому что это именно то, что передано в качестве аргумента.

---

Эти примеры демонстрируют различные особенности использования Generics в Java, включая типы, ограниченные wildcard'ами, безопасное приведение типов и работу с обобщёнными методами.

Вот ещё несколько примеров задач на тему **Generics**, которые могут встречаться на собеседованиях:

### Задача 6: Проблемы с неявными типами

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

public class Main {
    public static void main(String[] args) {
        Box box = new Box(42); // Неявное определение типа
        System.out.println(box.getValue());
    }
}
```

**Ответ:**

```
42
```

**Объяснение:**
- В этом примере мы создаём объект `Box` без явного указания типа (используется сырое обобщение). Это приводит к тому, что Java компилирует `Box` как `Box<Object>`.
- Поскольку `Integer` наследует от `Object`, метод `getValue()` возвращает `Integer`, и выводится значение `42`.

*Важно*: Это не рекомендуется делать, так как использование "сырых" типов (`raw types`) нарушает безопасность типов и может привести к ошибкам во время выполнения.

---

### Задача 7: Несовместимость типов с дженериками

```java
class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public void setValue(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Number> box = new Box<>(10);  // Box<Number> с типом Integer
        box.setValue(3.14); // Пытаемся установить значение типа Double

        System.out.println(box.getValue());
    }
}
```

**Ответ:**

```
3.14
```

**Объяснение:**
- В этом примере создаётся объект `Box<Number>`, и начальное значение устанавливается как `Integer`.
- Затем мы устанавливаем значение типа `Double` в тот же контейнер, что допускается, потому что `Double` также является подтипом `Number`.
- Метод `getValue()` возвращает значение типа `Number`, и в данном случае это `Double` (значение `3.14`), которое и выводится на консоль.

---

### Задача 8: Проблемы с типами в коллекциях

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<? extends Number> list = new ArrayList<Integer>();
        list.add(42); // Ошибка компиляции
    }
}
```

**Ответ:**

**Ошибка компиляции**

**Объяснение:**
- В этом примере мы пытаемся добавить элемент в список, где тип ограничен wildcard `? extends Number`.
- `? extends Number` означает, что список может содержать объекты типа `Number` или его подтипы, но мы не можем точно знать, какой именно тип в коллекции.
- Java не позволяет добавлять элементы в коллекцию с таким wildcard'ом, потому что тип может быть, например, `Integer` или `Double`, и компилятор не может гарантировать, что тип `42` совместим с этим списком.

---

### Задача 9: Ковариантность и контравариантность с wildcard'ами

```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<? extends Number> list1 = new ArrayList<Integer>();
        List<? super Integer> list2 = new ArrayList<Number>();

        // list1.add(10); // Ошибка компиляции
        list2.add(10); // Без ошибок

        System.out.println(list2.get(0)); // Выведет Integer
    }
}
```

**Ответ:**

```
10
```

**Объяснение:**
- В `list1`, тип ограничен wildcard `? extends Number`, что означает, что в список можно добавить элементы только определённого типа, но тип элемента неизвестен. Из-за этого мы не можем добавить значение типа `Integer` или `Number`, так как это может нарушить типизацию.
- В `list2`, тип ограничен wildcard `? super Integer`, что позволяет добавлять объекты типа `Integer` или его суперклассы (`Number`, `Object`). Мы можем добавить `10` в список, но извлечение элемента из этого списка будет проблематично, так как мы не можем точно знать, какого типа объект мы получим.
- Метод `get(0)` в `list2` вернёт объект типа `Integer`, так как мы добавили `10` (тип `Integer`).

---

### Задача 10: Взаимодействие обобщённых классов и методов

```java
class Pair<K, V> {
    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public K getKey() {
        return key;
    }

    public V getValue() {
        return value;
    }

    public <T> void printValue(T t) {
        System.out.println(t);
    }
}

public class Main {
    public static void main(String[] args) {
        Pair<Integer, String> pair = new Pair<>(1, "One");
        pair.printValue(pair.getKey()); // Печатает Integer
        pair.printValue(pair.getValue()); // Печатает String
    }
}
```

**Ответ:**

```
1
One
```

**Объяснение:**
- Класс `Pair` — это обобщённый класс, который хранит пару значений: ключ типа `K` и значение типа `V`.
- Метод `printValue(T t)` является обобщённым и не зависит от типа `K` или `V`, поэтому его можно использовать с любым типом.
- В методе `main` мы создаём пару с типами `Integer` и `String`.
- Мы выводим сначала ключ (`pair.getKey()`, который равен `1`, тип `Integer`), а затем значение (`pair.getValue()`, которое равно `"One"`, тип `String`).

---

### Задача 11: Обобщённые типы с наследованием

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

class Box<T extends Animal> {
    private T animal;

    public Box(T animal) {
        this.animal = animal;
    }

    public void makeSound() {
        animal.sound();
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Dog> dogBox = new Box<>(new Dog());
        dogBox.makeSound();
    }
}
```

**Ответ:**

```
Bark
```

**Объяснение:**
- В этом примере класс `Box` ограничен типом `T extends Animal`, что означает, что мы можем использовать только объекты, которые являются подтипами класса `Animal` (например, `Dog`).
- Мы создаём объект `Box<Dog>`, который хранит экземпляр класса `Dog`.
- Метод `makeSound()` вызывает метод `sound()` для объекта `Dog`, и выводится строка `"Bark"`, так как метод был переопределён в классе `Dog`.

---

Эти примеры иллюстрируют различные аспекты работы с обобщениями (Generics) в Java: от базовых операций с типами до более сложных случаев с wildcard'ами, ограничениями типов и дженериками с наследованием.

