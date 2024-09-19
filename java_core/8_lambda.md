Для подготовки к собеседованию на позицию Senior Java Developer по теме "Lambda-выражения и функциональные интерфейсы", рекомендуется разбить тему на следующие подтемы:

### 1. **Основы лямбда-выражений**
- **Синтаксис лямбда-выражений**:
    - Описание базового синтаксиса: `(parameters) -> expression` и `(parameters) -> {statements}`.
    - Различные варианты: лямбда с одним параметром (без скобок), с несколькими параметрами, с телом в одну строку или блоком кода.
- **Типы лямбда-выражений**:
    - Лямбда-выражения для методов с различными сигнатурами: с возвратом значения, без возврата, с несколькими параметрами.
- **Контекст использования**:
    - Как компилятор выводит типы параметров (type inference).
    - Лямбда-выражения в контексте функциональных интерфейсов.
- **Scopes и доступ к переменным**:
    - Доступ к внешним переменным из лямбда-выражения (effectively final).
    - Отличие лямбда-выражений от анонимных классов с точки зрения области видимости и доступа к переменным.
- **Сравнение с анонимными классами**:
    - Различия в синтаксисе, управлении областью видимости и производительности между лямбда-выражениями и анонимными классами.

### 2. **Функциональные интерфейсы**
- **Понятие функциональных интерфейсов**:
    - Что такое функциональный интерфейс, ключевая аннотация `@FunctionalInterface`.
    - Примеры создания собственных функциональных интерфейсов.
    - Почему функциональные интерфейсы важны для лямбда-выражений.
- **Стандартные функциональные интерфейсы из пакета `java.util.function`**:
    - **`Function<T, R>`**: принимает один аргумент, возвращает результат.
        - Примеры использования, композиция функций (методы `andThen()`, `compose()`).
    - **`Consumer<T>`**: принимает аргумент, ничего не возвращает.
        - Использование метода `accept()` для операций без возвращаемого значения.
    - **`Supplier<T>`**: не принимает аргументов, возвращает результат.
        - Пример использования, например, для ленивой инициализации.
    - **`Predicate<T>`**: принимает один аргумент и возвращает `boolean`.
        - Использование метода `test()` для фильтрации данных.
        - Логические методы `and()`, `or()`, `negate()` для составления сложных предикатов.
    - Дополнительные интерфейсы, такие как `BiFunction`, `BiConsumer`, `UnaryOperator`, `BinaryOperator`, их использование.
- **Логические операторы в `Predicate`**:
    - Как объединять предикаты для более сложных условий с помощью методов `and()`, `or()`, `negate()`.

### 3. **Method References**
- **Ссылки на методы (method references)**:
    - Описание различных видов method references:
        - Ссылка на статический метод: `ClassName::staticMethod`.
        - Ссылка на метод экземпляра: `instance::instanceMethod`.
        - Ссылка на метод экземпляра произвольного объекта конкретного типа: `ClassName::instanceMethod`.
        - Ссылка на конструктор: `ClassName::new`.
- **Примеры использования**:
    - Как method references упрощают синтаксис лямбда-выражений.
    - Примеры использования method references в стандартных функциональных интерфейсах (`Predicate`, `Function`, `Supplier` и т.д.).
- **Когда использовать method references**:
    - Когда ссылка на метод является более читаемым и предпочтительным решением по сравнению с лямбда-выражением.
    - Ограничения использования method references (например, в случаях, где нужна логика, которая не может быть выражена одним методом).

### 4. **Stream API**
- **Основы Stream API**:
    - Понятие потоков (streams): ленивое вычисление, цепочки вызовов методов.
    - Как создать поток: методы `stream()` и `of()` для коллекций, массивов и других источников.
    - Понятие промежуточных и терминальных операций.
- **Промежуточные операции**:
    - **Фильтрация (`filter()`)**:
        - Применение лямбда-выражений и `Predicate` для фильтрации данных.
    - **Отображение (`map()`)**:
        - Использование `Function` для преобразования элементов.
        - Примеры преобразования типов данных, манипуляции с объектами в потоке.
    - **Сортировка (`sorted()`)**:
        - Сортировка потоков данных: естественная сортировка и сортировка с использованием компараторов.
    - **Промежуточные операции, возвращающие потоки:**
        - Операции `flatMap()`, `limit()`, `skip()`, `distinct()`, и их примеры.
- **Терминальные операции**:
    - **forEach()**: когда использовать и проблемы с побочными эффектами.
    - **collect()**:
        - Сбор данных в коллекции, использование `Collectors`.
        - Примеры использования `Collectors.toList()`, `toSet()`, `joining()`, `groupingBy()`, `partitioningBy()`.
    - **reduce()**:
        - Пример свертки данных (агрегирование) с использованием лямбда-выражений.
        - Различия между версиями `reduce()`: с и без начального значения.
    - **findFirst() и findAny()**: когда использовать для поиска элементов в потоках.
    - **allMatch(), anyMatch(), noneMatch()**: примеры использования для проверки условий в потоках.
    - **count()**: получение количества элементов в потоке.
- **Параллельные потоки (parallel streams)**:
    - Преимущества и ограничения использования параллельных потоков.
    - Пример создания и обработки параллельных потоков, когда целесообразно их использовать.
    - Влияние параллельных потоков на производительность.

### 5. **Класс `Optional`**
- **Понятие `Optional`**:
    - Основное назначение класса `Optional`: как избежать `NullPointerException`.
    - Создание объектов `Optional` с помощью методов `of()`, `ofNullable()`, `empty()`.
- **Работа с Optional**:
    - Использование метода `isPresent()` и `ifPresent()`.
    - Методы для работы с содержимым: `orElse()`, `orElseGet()`, `orElseThrow()`, их различия.
    - Ленивая инициализация значений с `orElseGet()`.
- **Композиция с Optional**:
    - Применение методов `map()` и `flatMap()` для работы с вложенными объектами.
    - Как комбинировать `Optional` с потоками (`Stream API`).
- **Проблемы злоупотребления `Optional`**:
    - Когда стоит и не стоит использовать `Optional`.
    - Правильное использование `Optional` в сигнатурах методов (например, в аргументах и возвращаемых значениях).

### Дополнительные подтемы:
- **Функциональные интерфейсы с исключениями**:
    - Как обрабатывать исключения в лямбда-выражениях и функциональных интерфейсах (например, создание обёрток).
- **Производительность и оптимизация**:
    - Влияние лямбда-выражений и Stream API на производительность.
    - Как избежать проблем с производительностью при использовании Stream API (например, избегание ненужных промежуточных операций).
- **Каррирование (currying)**:
    - Понятие каррирования функций и его реализация в Java.

Хорошо, давай разберём основы лямбда-выражений в Java. Это важная тема для собеседования на позицию senior Java developer, и понимание всех её аспектов поможет тебе блеснуть на интервью.

### Основы лямбда-выражений

**1. Синтаксис лямбда-выражений**

Лямбда-выражения в Java были введены в версии 8, и они предоставляют способ создать анонимные функции. Синтаксис лямбда-выражений можно разделить на несколько основных вариантов:

- **Базовый синтаксис:**
    - `(parameters) -> expression`
    - `(parameters) -> {statements}`

  Примеры:
  ```java
  (x, y) -> x + y
  ```
  Это лямбда-выражение принимает два параметра `x` и `y`, и возвращает их сумму.

  ```java
  (x, y) -> {
      int result = x + y;
      return result;
  }
  ```
  Здесь лямбда-выражение также принимает два параметра и возвращает их сумму, но в теле выражения выполняется дополнительная операция.

- **Лямбда с одним параметром:**
    - Если лямбда-выражение имеет один параметр, скобки вокруг параметра можно опустить.

  Пример:
  ```java
  x -> x * x
  ```
  Это выражение принимает один параметр `x` и возвращает его квадрат.

- **Лямбда с несколькими параметрами:**
    - В случае нескольких параметров скобки обязательно.

  Пример:
  ```java
  (a, b) -> a - b
  ```

- **Лямбда с телом в одну строку или блоком кода:**
    - В случае одной строки можно опустить фигурные скобки и оператор `return`.
    - В случае блока кода фигурные скобки и оператор `return` обязательны, если необходимо возвращать значение.

**2. Типы лямбда-выражений**

- **Лямбда-выражения для методов с различными сигнатурами:**
    - **С возвратом значения:**
      ```java
      (x, y) -> x * y
      ```
      Это выражение принимает два параметра и возвращает их произведение.

    - **Без возврата значения (например, для интерфейсов с `void` методами):**
      ```java
      (message) -> System.out.println(message)
      ```
      Это выражение выводит переданное сообщение на экран.

    - **С несколькими параметрами:**
      ```java
      (x, y) -> {
          System.out.println("Sum: " + (x + y));
      }
      ```

**3. Контекст использования**

- **Type Inference:**
    - Java компилятор может выводить типы параметров лямбда-выражений на основе контекста, в котором они используются. Например, если лямбда-выражение передается в метод, который ожидает интерфейс с определённой сигнатурой, компилятор автоматически определит типы параметров.

- **Функциональные интерфейсы:**
    - Лямбда-выражения могут быть использованы только там, где ожидается функциональный интерфейс — интерфейс с единственным абстрактным методом (например, `Runnable`, `Callable`, `Comparator`, `Function` и др.).

**4. Scopes и доступ к переменным**

- **Эффективно финальные переменные (effectively final):**
    - Лямбда-выражения могут захватывать переменные из внешнего контекста, но эти переменные должны быть эффективно финальными. Это значит, что их значение не должно изменяться после инициализации.

  Пример:
  ```java
  int factor = 2;
  Function<Integer, Integer> multiply = x -> x * factor;
  ```

  Здесь переменная `factor` является эффективно финальной.

- **Сравнение с анонимными классами:**
    - **Область видимости и доступ к переменным:**
        - Лямбда-выражения и анонимные классы имеют разные правила для доступа к внешним переменным. Лямбда-выражения могут захватывать только эффективно финальные переменные, в то время как анонимные классы могут захватывать переменные, если они являются `final`.

    - **Синтаксис и производительность:**
        - Лямбда-выражения имеют более компактный синтаксис по сравнению с анонимными классами.
        - Лямбда-выражения могут быть более эффективными, так как компилятор оптимизирует их с помощью вызовов `invokedynamic` и метапрограммирования, в то время как анонимные классы создают дополнительные классы в байт-коде.

  Пример анонимного класса:
  ```java
  Runnable r = new Runnable() {
      @Override
      public void run() {
          System.out.println("Hello, world!");
      }
  };
  ```

  И его эквивалент в лямбда-выражении:
  ```java
  Runnable r = () -> System.out.println("Hello, world!");
  ```

Функциональные интерфейсы — это ключевая концепция в Java 8 и далее, особенно в контексте лямбда-выражений и функционального программирования. Вот подробное объяснение всех аспектов функциональных интерфейсов, которые могут быть полезны для подготовки к собеседованию.

### Понятие функциональных интерфейсов

**1. Что такое функциональный интерфейс**

Функциональный интерфейс — это интерфейс, который имеет только один абстрактный метод. Такие интерфейсы могут иметь множество методов по умолчанию (default) и статических методов, но только один абстрактный метод. Функциональные интерфейсы предназначены для использования с лямбда-выражениями или методами ссылок.

**Ключевая аннотация `@FunctionalInterface`:**

Аннотация `@FunctionalInterface` используется для обозначения интерфейса как функционального. Это не обязательно, но рекомендуется, так как она помогает компилятору проверять, что интерфейс действительно соответствует требованиям функционального интерфейса.

Пример:
```java
@FunctionalInterface
public interface MyFunctionalInterface {
    void myMethod();
}
```

Если интерфейс с аннотацией `@FunctionalInterface` имеет более одного абстрактного метода, компилятор выдаст ошибку.

**2. Примеры создания собственных функциональных интерфейсов**

```java
@FunctionalInterface
public interface Transformer {
    int transform(int x);
}
```
Здесь `Transformer` — это функциональный интерфейс с одним абстрактным методом `transform`.

Использование:
```java
Transformer doubleValue = x -> x * 2;
System.out.println(doubleValue.transform(5)); // Вывод: 10
```

**3. Почему функциональные интерфейсы важны для лямбда-выражений**

Функциональные интерфейсы служат целевым типом для лямбда-выражений. Лямбда-выражения создают экземпляры функциональных интерфейсов, что упрощает код и делает его более читаемым. Лямбда-выражения и метод-референции тесно связаны с функциональными интерфейсами, так как они представляют собой конкретные реализации методов этих интерфейсов.

### Стандартные функциональные интерфейсы из пакета `java.util.function`

Java 8 и выше включают несколько стандартных функциональных интерфейсов в пакете `java.util.function`. Они часто используются вместе с лямбда-выражениями и методами ссылок.

**1. `Function<T, R>`**

- **Описание:** Принимает один аргумент типа `T` и возвращает результат типа `R`.

  ```java
  Function<Integer, String> intToString = Object::toString;
  System.out.println(intToString.apply(123)); // Вывод: "123"
  ```

- **Методы:**
    - `andThen(Function<? super R, ? extends V> after)`: Создает новую функцию, которая сначала применяет текущую функцию, а затем функцию `after`.
    - `compose(Function<? super T, ? extends V> before)`: Создает новую функцию, которая сначала применяет функцию `before`, а затем текущую функцию.

  Пример:
  ```java
  Function<Integer, Integer> multiplyBy2 = x -> x * 2;
  Function<Integer, Integer> add3 = x -> x + 3;
  Function<Integer, Integer> combined = multiplyBy2.andThen(add3);

  System.out.println(combined.apply(5)); // Вывод: 13
  ```

**2. `Consumer<T>`**

- **Описание:** Принимает один аргумент типа `T` и не возвращает результат.

  ```java
  Consumer<String> printLength = str -> System.out.println(str.length());
  printLength.accept("Hello, world!"); // Вывод: 13
  ```

**3. `Supplier<T>`**

- **Описание:** Не принимает аргументов и возвращает результат типа `T`.

  ```java
  Supplier<Double> randomValue = Math::random;
  System.out.println(randomValue.get()); // Выводит случайное число типа double
  ```

**4. `Predicate<T>`**

- **Описание:** Принимает один аргумент типа `T` и возвращает `boolean`.

  ```java
  Predicate<String> isEmpty = String::isEmpty;
  System.out.println(isEmpty.test("")); // Вывод: true
  ```

- **Методы:**
    - `and(Predicate<? super T> other)`: Возвращает новый предикат, который является логическим И между текущим и другим предикатом.
    - `or(Predicate<? super T> other)`: Возвращает новый предикат, который является логическим ИЛИ между текущим и другим предикатом.
    - `negate()`: Возвращает новый предикат, который является отрицанием текущего предиката.

  Пример:
  ```java
  Predicate<String> isNotEmpty = isEmpty.negate();
  System.out.println(isNotEmpty.test("Non-empty")); // Вывод: true

  Predicate<String> startsWithH = str -> str.startsWith("H");
  Predicate<String> combinedPredicate = isNotEmpty.and(startsWithH);

  System.out.println(combinedPredicate.test("Hello")); // Вывод: true
  ```

**5. Дополнительные интерфейсы**

- **`BiFunction<T, U, R>`:** Принимает два аргумента (`T` и `U`) и возвращает результат (`R`).

  ```java
  BiFunction<Integer, Integer, Integer> sum = (a, b) -> a + b;
  System.out.println(sum.apply(5, 3)); // Вывод: 8
  ```

- **`BiConsumer<T, U>`:** Принимает два аргумента (`T` и `U`) и ничего не возвращает.

  ```java
  BiConsumer<String, Integer> printDetails = (name, age) -> System.out.println(name + " is " + age + " years old");
  printDetails.accept("Alice", 30); // Вывод: Alice is 30 years old
  ```

- **`UnaryOperator<T>`:** Специальный случай `Function<T, T>`, который принимает один аргумент и возвращает результат того же типа.

  ```java
  UnaryOperator<String> makeUpperCase = String::toUpperCase;
  System.out.println(makeUpperCase.apply("hello")); // Вывод: HELLO
  ```

- **`BinaryOperator<T>`:** Специальный случай `BiFunction<T, T, T>`, который принимает два аргумента и возвращает результат того же типа.

  ```java
  BinaryOperator<Integer> multiply = (a, b) -> a * b;
  System.out.println(multiply.apply(3, 4)); // Вывод: 12
  ```

### Логические операторы в `Predicate`

**1. Объединение предикатов**

- **`and(Predicate<? super T> other)`**: Возвращает новый предикат, который является логическим И (AND) между текущим предикатом и `other`.

  ```java
  Predicate<String> isLongerThan5 = str -> str.length() > 5;
  Predicate<String> isShorterThan10 = str -> str.length() < 10;
  Predicate<String> isBetween6And9 = isLongerThan5.and(isShorterThan10);

  System.out.println(isBetween6And9.test("Example")); // Вывод: true
  ```

- **`or(Predicate<? super T> other)`**: Возвращает новый предикат, который является логическим ИЛИ (OR) между текущим предикатом и `other`.

  ```java
  Predicate<String> isEmptyOrLongerThan5 = isEmpty.or(isLongerThan5);
  System.out.println(isEmptyOrLongerThan5.test("Short")); // Вывод: false
  ```

- **`negate()`**: Возвращает новый предикат, который является отрицанием текущего предиката.

  ```java
  Predicate<String> isNotEmpty = isEmpty.negate();
  System.out.println(isNotEmpty.test("Hello")); // Вывод: true
  ```
Ссылки на методы (method references) в Java — это удобный синтаксический сахар, который упрощает использование лямбда-выражений и делает код более читаемым. Они позволяют ссылаться на методы без необходимости повторного написания их тела, что особенно полезно при работе с функциональными интерфейсами.

### Описание различных видов method references

**1. Ссылка на статический метод**

Формат: `ClassName::staticMethod`

- **Пример:** У вас есть класс с статическим методом, и вы хотите использовать его в качестве функционального интерфейса.

  ```java
  public class Utils {
      public static int square(int x) {
          return x * x;
      }
  }

  Function<Integer, Integer> squareFunction = Utils::square;
  System.out.println(squareFunction.apply(5)); // Вывод: 25
  ```

  Здесь `Utils::square` является ссылкой на статический метод `square` класса `Utils`.

**2. Ссылка на метод экземпляра**

Формат: `instance::instanceMethod`

- **Пример:** Использование ссылки на метод экземпляра, где ссылка создается через конкретный объект.

  ```java
  public class Printer {
      public void print(String message) {
          System.out.println(message);
      }
  }

  Printer printer = new Printer();
  Consumer<String> printerConsumer = printer::print;
  printerConsumer.accept("Hello, world!"); // Вывод: Hello, world!
  ```

  Здесь `printer::print` является ссылкой на метод экземпляра `print` объекта `printer`.

**3. Ссылка на метод экземпляра произвольного объекта конкретного типа**

Формат: `ClassName::instanceMethod`

- **Пример:** Если метод должен применяться к объектам произвольного типа.

  ```java
  public class StringUtils {
      public boolean isLongerThan5(String s) {
          return s.length() > 5;
      }
  }

  Predicate<String> isLongerThan5Predicate = new StringUtils()::isLongerThan5;
  System.out.println(isLongerThan5Predicate.test("Example")); // Вывод: true
  ```

  Здесь `new StringUtils()::isLongerThan5` является ссылкой на метод экземпляра `isLongerThan5` нового объекта `StringUtils`.

**4. Ссылка на конструктор**

Формат: `ClassName::new`

- **Пример:** Использование ссылки на конструктор для создания новых экземпляров.

  ```java
  public class Person {
      private String name;
      public Person(String name) {
          this.name = name;
      }
      public String getName() {
          return name;
      }
  }

  Supplier<Person> personSupplier = () -> new Person("John Doe");
  // Это можно заменить на:
  Supplier<Person> personSupplierRef = Person::new;

  Person person = personSupplierRef.get();
  System.out.println(person.getName()); // Вывод: John Doe
  ```

  Здесь `Person::new` является ссылкой на конструктор класса `Person`.

### Примеры использования method references

**1. Ссылки на статические методы**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.sort(String::compareToIgnoreCase);
System.out.println(names); // Вывод: [Alice, Bob, Charlie]
```

Здесь `String::compareToIgnoreCase` заменяет лямбда-выражение `(a, b) -> a.compareToIgnoreCase(b)`.

**2. Ссылки на методы экземпляра**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Printer printer = new Printer();
names.forEach(printer::print);
```

Здесь `printer::print` заменяет лямбда-выражение `s -> printer.print(s)`.

**3. Ссылки на методы экземпляра произвольного объекта**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
StringUtils stringUtils = new StringUtils();
names.stream().filter(stringUtils::isLongerThan5).forEach(System.out::println);
```

Здесь `stringUtils::isLongerThan5` заменяет лямбда-выражение `s -> stringUtils.isLongerThan5(s)`.

**4. Ссылки на конструкторы**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<Person> people = names.stream()
                            .map(Person::new)
                            .collect(Collectors.toList());

people.forEach(person -> System.out.println(person.getName()));
```

Здесь `Person::new` заменяет лямбда-выражение `name -> new Person(name)`.

### Когда использовать method references

**1. Когда ссылки на методы более читаемы**

Ссылки на методы делают код более компактным и читаемым, особенно когда тело лямбда-выражения просто вызывает метод. Это помогает сосредоточиться на логике использования функции, а не на её реализации.

**2. Примеры**

- Использование `ClassName::methodName` вместо `(x) -> ClassName.methodName(x)` упрощает код.
- Конструкторы часто используются для создания новых объектов в потоках и коллекциях, и `ClassName::new` делает код лаконичным.

**3. Ограничения**

- Если вам нужно выполнить сложную логику внутри метода, ссылку на метод не получится использовать. В этом случае лямбда-выражение предоставляет больше гибкости.
- Метод должен соответствовать функциональному интерфейсу. Например, метод с несколькими параметрами не может быть использован в контексте `Supplier<T>`, который ожидает метод без параметров.

### Заключение

Ссылки на методы значительно упрощают и улучшают читаемость кода, особенно когда используются с функциональными интерфейсами. Они помогают избежать излишнего кода и делают лямбда-выражения более элегантными. Тем не менее, важно помнить о случаях, когда лямбда-выражения могут быть более подходящим выбором из-за необходимости более сложной логики.

Stream API в Java предоставляет мощный и выразительный способ работы с коллекциями данных. Он упрощает обработку данных, позволяя использовать декларативный стиль программирования и обрабатывать данные в виде потоков. Давайте рассмотрим подробно все ключевые аспекты Stream API.

### Основы Stream API

**1. Понятие потоков (streams)**

Потоки (`streams`) в Java представляют собой последовательность элементов, которые можно обрабатывать. Потоки поддерживают ленивое вычисление, что означает, что элементы обрабатываются только тогда, когда это необходимо (при выполнении терминальной операции).

- **Ленивое вычисление:** Потоки не вычисляют элементы до тех пор, пока не будет выполнена терминальная операция. Это позволяет объединять несколько операций и выполнять их более эффективно.

- **Цепочки вызовов методов:** Потоки поддерживают цепочки вызовов методов, где операции применяются последовательно.

**2. Как создать поток**

- **Из коллекций:**
  ```java
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
  Stream<String> stream = names.stream();
  ```

- **Из массивов:**
  ```java
  String[] namesArray = {"Alice", "Bob", "Charlie"};
  Stream<String> stream = Arrays.stream(namesArray);
  ```

- **Из значений:**
  ```java
  Stream<String> stream = Stream.of("Alice", "Bob", "Charlie");
  ```

### Понятие промежуточных и терминальных операций

- **Промежуточные операции:** Операции, которые возвращают новый поток и не выполняют вычисления до тех пор, пока не будет вызвана терминальная операция. Примеры: `filter()`, `map()`, `sorted()`.

- **Терминальные операции:** Операции, которые выполняют вычисления и возвращают результат (например, коллекцию, число). Примеры: `forEach()`, `collect()`, `reduce()`.

### Промежуточные операции

**1. Фильтрация (`filter()`)**

Фильтрация позволяет выбрать элементы, которые соответствуют определенному условию.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Dave");
Stream<String> filtered = names.stream()
                                .filter(name -> name.startsWith("A"));
filtered.forEach(System.out::println); // Вывод: Alice
```

Здесь `filter()` использует лямбда-выражение для отбрасывания элементов, не удовлетворяющих условию.

**2. Отображение (`map()`)**

Операция `map()` преобразует элементы потока в другой формат.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
Stream<Integer> nameLengths = names.stream()
                                    .map(String::length);
nameLengths.forEach(System.out::println); // Вывод: 5, 3, 7
```

Здесь `map()` преобразует строки в их длину.

**3. Сортировка (`sorted()`)**

Сортировка позволяет упорядочить элементы в потоке.

```java
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");
Stream<String> sortedNames = names.stream()
                                   .sorted();
sortedNames.forEach(System.out::println); // Вывод: Alice, Bob, Charlie
```

Также можно использовать компаратор:

```java
Stream<String> sortedNames = names.stream()
                                   .sorted(Comparator.reverseOrder());
sortedNames.forEach(System.out::println); // Вывод: Charlie, Bob, Alice
```

**4. Промежуточные операции, возвращающие потоки**

- **`flatMap()`**: Применяет функцию к каждому элементу и объединяет результат в один поток.

  ```java
  List<List<String>> listOLists = Arrays.asList(
      Arrays.asList("a1", "a2"),
      Arrays.asList("b1", "b2"),
      Arrays.asList("c1", "c2")
  );
  listOLists.stream()
            .flatMap(List::stream)
            .forEach(System.out::println); // Вывод: a1, a2, b1, b2, c1, c2
  ```

- **`limit()`**: Ограничивает количество элементов в потоке.

  ```java
  Stream<String> names = Stream.of("Alice", "Bob", "Charlie", "Dave");
  names.limit(2)
       .forEach(System.out::println); // Вывод: Alice, Bob
  ```

- **`skip()`**: Пропускает указанное количество элементов в потоке.

  ```java
  Stream<String> names = Stream.of("Alice", "Bob", "Charlie", "Dave");
  names.skip(2)
       .forEach(System.out::println); // Вывод: Charlie, Dave
  ```

- **`distinct()`**: Удаляет дублирующиеся элементы.

  ```java
  Stream<String> names = Stream.of("Alice", "Bob", "Alice", "Charlie", "Bob");
  names.distinct()
       .forEach(System.out::println); // Вывод: Alice, Bob, Charlie
  ```

### Терминальные операции

**1. `forEach()`**

Применяет указанное действие к каждому элементу потока.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
names.stream()
     .forEach(System.out::println);
```

Использование `forEach()` может привести к проблемам с побочными эффектами и производительностью в параллельных потоках.

**2. `collect()`**

Собирает элементы потока в коллекцию или другую структуру данных.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> result = names.stream()
                           .collect(Collectors.toList());
```

Примеры использования `Collectors`:

- **`toList()`**: Собирает элементы в `List`.

  ```java
  List<String> list = names.stream()
                           .collect(Collectors.toList());
  ```

- **`toSet()`**: Собирает элементы в `Set`.

  ```java
  Set<String> set = names.stream()
                         .collect(Collectors.toSet());
  ```

- **`joining()`**: Объединяет элементы в строку.

  ```java
  String result = names.stream()
                       .collect(Collectors.joining(", "));
  System.out.println(result); // Вывод: Alice, Bob, Charlie
  ```

- **`groupingBy()`**: Группирует элементы по определенному критерию.

  ```java
  Map<Integer, List<String>> groupedByLength = names.stream()
                                                    .collect(Collectors.groupingBy(String::length));
  ```

- **`partitioningBy()`**: Разделяет элементы на две группы по условию.

  ```java
  Map<Boolean, List<String>> partitioned = names.stream()
                                                .collect(Collectors.partitioningBy(name -> name.length() > 3));
  ```

**3. `reduce()`**

Агрегирует элементы потока в одно значение.

- **Пример без начального значения:**

  ```java
  int sum = Stream.of(1, 2, 3, 4, 5)
                  .reduce((a, b) -> a + b)
                  .orElse(0);
  System.out.println(sum); // Вывод: 15
  ```

- **Пример с начальным значением:**

  ```java
  int sum = Stream.of(1, 2, 3, 4, 5)
                  .reduce(0, (a, b) -> a + b);
  System.out.println(sum); // Вывод: 15
  ```

**4. `findFirst()` и `findAny()`**

- **`findFirst()`**: Возвращает первый элемент в потоке.

  ```java
  Optional<String> first = names.stream().findFirst();
  first.ifPresent(System.out::println);
  ```

- **`findAny()`**: Возвращает любой элемент в потоке, часто используется в параллельных потоках.

  ```java
  Optional<String> any = names.stream().findAny();
  any.ifPresent(System.out::println);
  ```

**5. `allMatch()`, `anyMatch()`, `noneMatch()`**

- **`allMatch()`**: Проверяет, соответствует ли каждый элемент условию.

  ```java
  boolean allLongerThan3 = names.stream().allMatch(name -> name.length() > 3);
  System.out.println(allLongerThan3); // Вывод: true
  ```

- **`anyMatch()`**: Проверяет, соответствует ли хотя бы один элемент условию.

  ```java
  boolean anyLongerThan3 = names.stream().anyMatch(name -> name.length() > 3);
  System.out.println(anyLongerThan3); // Вывод: true
  ```

- **`noneMatch()`**: Проверяет, не соответствует ли ни один элемент условию.

  ```java
  boolean noneLongerThan10 = names.stream().noneMatch(name -> name.length() > 10);
  System.out.println(noneLongerThan10); // Вывод: true
  ```

**6. `count()`**

Возвращает количество элементов в потоке.

```java
long count = names.stream().count();
System.out.println(count); // Вывод: 3
```

###

Параллельные потоки (parallel streams)

Параллельные потоки позволяют обрабатывать элементы в параллельных потоках, что может улучшить производительность при работе с большими объемами данных.

**1. Преимущества и ограничения**

- **Преимущества:** Улучшение производительности при обработке больших объемов данных благодаря использованию нескольких потоков процессора.

- **Ограничения:** Не все операции могут быть эффективно распараллелены. Использование параллельных потоков может привести к накладным расходам на управление потоками и синхронизацию.

**2. Пример создания и обработки параллельных потоков**

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Dave");
names.parallelStream()
     .filter(name -> name.length() > 3)
     .forEach(System.out::println);
```

**3. Влияние на производительность**

Параллельные потоки могут значительно улучшить производительность, но это зависит от задачи и объема данных. Важно тестировать производительность в вашем конкретном случае, чтобы понять, стоит ли использовать параллельные потоки.

### Заключение

Stream API предлагает мощный и гибкий способ обработки коллекций данных в Java. Использование потоков упрощает работу с данными и делает код более выразительным. Понимание основ потоков, промежуточных и терминальных операций, а также особенностей параллельных потоков поможет вам эффективно использовать Stream API в вашей работе.

### Класс `Optional`

`Optional` — это контейнер, который может содержать значение или быть пустым. Он был введен в Java 8 для улучшения работы с возможными `null` значениями и для избежания распространенных ошибок, таких как `NullPointerException`. Давайте разберем основные аспекты использования `Optional`.

#### Понятие `Optional`

**1. Основное назначение класса `Optional`**

- **Избежание `NullPointerException`:** `Optional` предоставляет способ явно обозначить, что значение может отсутствовать, и предлагает безопасные способы обработки таких случаев без явного использования `null`.

**2. Создание объектов `Optional`**

- **`Optional.of(T value)`**: Создает `Optional` с ненулевым значением. Если значение `null`, выбрасывается `NullPointerException`.

  ```java
  Optional<String> optional = Optional.of("Hello");
  ```

- **`Optional.ofNullable(T value)`**: Создает `Optional`, который может содержать значение или быть пустым. Если значение `null`, создается пустой `Optional`.

  ```java
  Optional<String> optional = Optional.ofNullable(null); // Пустой Optional
  ```

- **`Optional.empty()`**: Создает пустой `Optional`, который не содержит значения.

  ```java
  Optional<String> emptyOptional = Optional.empty();
  ```

#### Работа с `Optional`

**1. Использование метода `isPresent()` и `ifPresent()`**

- **`isPresent()`**: Проверяет, содержит ли `Optional` значение.

  ```java
  if (optional.isPresent()) {
      System.out.println(optional.get());
  }
  ```

- **`ifPresent(Consumer<? super T> action)`**: Выполняет действие, если значение присутствует.

  ```java
  optional.ifPresent(value -> System.out.println(value));
  ```

**2. Методы для работы с содержимым**

- **`orElse(T other)`**: Возвращает значение, если оно присутствует, иначе возвращает указанное значение по умолчанию.

  ```java
  String result = optional.orElse("Default Value");
  ```

- **`orElseGet(Supplier<? extends T> other)`**: Возвращает значение, если оно присутствует, иначе вызывает `Supplier` для получения значения по умолчанию. Это позволяет избежать лишних вычислений, если значение присутствует.

  ```java
  String result = optional.orElseGet(() -> "Default Value");
  ```

- **`orElseThrow(Supplier<? extends X> exceptionSupplier)`**: Возвращает значение, если оно присутствует, иначе выбрасывает исключение, которое предоставляет `Supplier`.

  ```java
  String result = optional.orElseThrow(() -> new IllegalArgumentException("Value is missing"));
  ```

**3. Ленивая инициализация значений с `orElseGet()`**

Использование `orElseGet()` позволяет избегать ненужных вычислений, так как `Supplier` вызывается только если значение отсутствует. Это полезно, когда создание значения по умолчанию требует сложных вычислений.

  ```java
  String result = optional.orElseGet(() -> {
      // сложные вычисления
      return "Default Value";
  });
  ```

#### Композиция с `Optional`

**1. Применение методов `map()` и `flatMap()`**

- **`map(Function<? super T, ? extends U> mapper)`**: Преобразует значение в `Optional`, если оно присутствует, или возвращает пустой `Optional`, если значение отсутствует.

  ```java
  Optional<String> uppercase = optional.map(String::toUpperCase);
  ```

- **`flatMap(Function<? super T, Optional<U>> mapper)`**: Преобразует значение в другой `Optional`, если оно присутствует. Полезно для работы с вложенными `Optional`.

  ```java
  Optional<String> result = optional.flatMap(value -> Optional.of(value.toUpperCase()));
  ```

**2. Комбинирование `Optional` с потоками (`Stream API`)**

- **Пример преобразования `Optional` в поток:**

  ```java
  Stream<String> stream = optional.stream();
  ```

- **Пример использования `Optional` в потоке:**

  ```java
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
  Optional<String> result = names.stream()
                                 .filter(name -> name.startsWith("A"))
                                 .findFirst();
  ```

#### Проблемы злоупотребления `Optional`

**1. Когда использовать `Optional`**

- **Используйте `Optional`** для возвращаемых значений методов, когда отсутствие значения является ожидаемым и нормальным состоянием, и когда вы хотите явно указать на это.

**2. Не используйте `Optional`**

- **Не используйте `Optional`** для параметров методов или полей класса. Это не предназначено для использования в качестве замены для `null` в таких ситуациях.
- **Не используйте `Optional`** для коллекций или массивов. Используйте его только для случаев, когда наличие или отсутствие значения является частью логики метода.

#### Дополнительные подтемы

**1. Функциональные интерфейсы с исключениями**

Обработка исключений в лямбда-выражениях может быть сложной. Один из подходов — создание оберток, которые позволяют обрабатывать исключения:

```java
@FunctionalInterface
public interface CheckedFunction<T, R> {
    R apply(T t) throws Exception;

    static <T, R> Function<T, R> wrap(CheckedFunction<T, R> checkedFunction) {
        return t -> {
            try {
                return checkedFunction.apply(t);
            } catch (Exception e) {
                throw new RuntimeException(e);
            }
        };
    }
}
```

**2. Производительность и оптимизация**

- **Лямбда-выражения и Stream API**: Лямбда-выражения и Stream API могут иногда вызывать накладные расходы, особенно в случаях большого количества промежуточных операций. Важно избегать ненужных операций и использовать параллельные потоки осознанно.

- **Оптимизация Stream API**: Используйте ленивые операции, избегайте промежуточных операций, которые могут быть дорогостоящими, и тестируйте производительность для вашего конкретного случая.

**3. Каррирование (currying)**

Каррирование — это процесс преобразования функции, принимающей несколько аргументов, в функцию, которая принимает один аргумент и возвращает функцию, принимающую оставшиеся аргументы. В Java нет встроенной поддержки каррирования, но его можно реализовать вручную.

**Пример каррирования в Java:**

```java
public class CurryingExample {
    public static Function<Integer, Function<Integer, Integer>> add = x -> y -> x + y;

    public static void main(String[] args) {
        Function<Integer, Integer> add5 = add.apply(5);
        System.out.println(add5.apply(10)); // Вывод: 15
    }
}
```

Здесь `add` — это функция, которая возвращает другую функцию, и так далее, что соответствует концепции каррирования.

### Заключение

Класс `Optional` в Java помогает избежать проблем с `null`, делает код более читаемым и безопасным. Знание его возможностей, методов и правильного использования поможет вам эффективно управлять значениями и избежать распространенных ошибок. Также важно понимать, когда и как применять функциональные интерфейсы, оптимизировать использование Stream API и применять концепции, такие как каррирование, для более эффективного и выразительного программирования.

