Вот несколько примеров задач на тему Stream и Lambda в Java, которые могут быть заданы на интервью. В этих примерах интервьюер может попросить объяснить, что будет выведено в консоли и почему.

### Задача 1: Пример с использованием `filter()` и `map()`

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9);

        numbers.stream()
               .filter(n -> n % 2 == 0)
               .map(n -> n * n)
               .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует Stream для обработки списка чисел. Описание шагов:
1. `filter(n -> n % 2 == 0)` — отфильтровывает только четные числа (2, 4, 6, 8).
2. `map(n -> n * n)` — возводит каждое четное число в квадрат (4, 16, 36, 64).
3. `forEach(System.out::println)` — выводит каждый результат в консоль.

**Результат:**
```
4
16
36
64
```

### Задача 2: Пример с `reduce()` для вычисления суммы

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        int sum = numbers.stream()
                         .reduce(0, (a, b) -> a + b);

        System.out.println(sum);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `reduce()` для вычисления суммы всех чисел в списке.
1. `reduce(0, (a, b) -> a + b)` — начинает с начального значения 0 и последовательно прибавляет каждое число из списка.
2. После выполнения метода сумма чисел от 1 до 5 будет равна 15.

**Результат:**
```
15
```

### Задача 3: Пример с `distinct()` для удаления дубликатов

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 2, 3, 3, 3, 4, 4, 4, 4);

        numbers.stream()
               .distinct()
               .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `distinct()` для удаления дубликатов из списка.
1. `distinct()` удаляет повторяющиеся элементы в потоке.
2. Оставшиеся уникальные элементы будут выведены в консоль.

**Результат:**
```
1
2
3
4
```

### Задача 4: Пример с `sorted()` для сортировки чисел

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(5, 3, 8, 1, 7, 2, 4, 6);

        numbers.stream()
               .sorted()
               .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `sorted()` для сортировки чисел в порядке возрастания.
1. Метод `sorted()` сортирует элементы в естественном порядке (по возрастанию).
2. Все элементы выводятся по одному в отсортированном порядке.

**Результат:**
```
1
2
3
4
5
6
7
8
```

### Задача 5: Пример с использованием `anyMatch()` и `noneMatch()`

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        boolean anyMatch = numbers.stream().anyMatch(n -> n > 4);
        boolean noneMatch = numbers.stream().noneMatch(n -> n > 5);

        System.out.println("anyMatch > 4: " + anyMatch);
        System.out.println("noneMatch > 5: " + noneMatch);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует методы `anyMatch()` и `noneMatch()` для проверки условий на элементы потока.
1. `anyMatch(n -> n > 4)` проверяет, есть ли хотя бы одно число больше 4. Это условие выполняется для чисел 5.
2. `noneMatch(n -> n > 5)` проверяет, нет ли чисел больше 5. Это условие выполняется, так как в списке нет чисел больше 5.

**Результат:**
```
anyMatch > 4: true
noneMatch > 5: true
```

### Задача 6: Пример с использованием `flatMap()`

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<List<Integer>> listOfLists = Arrays.asList(
            Arrays.asList(1, 2, 3),
            Arrays.asList(4, 5),
            Arrays.asList(6, 7, 8)
        );

        listOfLists.stream()
                   .flatMap(List::stream)
                   .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `flatMap()`, который "расплющивает" вложенные списки в один поток.
1. `flatMap(List::stream)` превращает каждый вложенный список в поток и объединяет их в один.
2. Каждый элемент из всех вложенных списков выводится в консоль.

**Результат:**
```
1
2
3
4
5
6
7
8
```

Эти примеры охватывают базовые операции с Stream API и могут быть полезны на интервью для проверки знаний о функциональных методах в Java.

Конечно, вот ещё несколько примеров задач на тему **Stream** и **Lambda** в Java, которые могут быть заданы на интервью. Задачи направлены на понимание использования различных методов Stream API и применения лямбда-выражений.

### Задача 7: Пример с `collect()` для группировки элементов

**Код:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "cherry", "avocado", "blueberry");

        Map<Character, List<String>> groupedByFirstLetter = words.stream()
                .collect(Collectors.groupingBy(word -> word.charAt(0)));

        groupedByFirstLetter.forEach((key, value) -> 
            System.out.println(key + ": " + value));
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `collect()` с коллектором `Collectors.groupingBy()`, чтобы сгруппировать строки по первой букве.
1. Строки из списка группируются по их первой букве.
2. Каждая группа выводится в консоль, где ключ — это первая буква, а значение — список слов, начинающихся с этой буквы.

**Результат:**
```
a: [apple, avocado]
b: [banana, blueberry]
c: [cherry]
```

### Задача 8: Пример с использованием `count()` для подсчета элементов

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "cherry", "avocado", "blueberry");

        long count = words.stream()
                          .filter(word -> word.length() > 5)
                          .count();

        System.out.println(count);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `count()` для подсчета количества строк, длина которых больше 5 символов.
1. `filter(word -> word.length() > 5)` отбирает только те слова, длина которых больше 5 символов.
2. После фильтрации считается количество таких слов.

**Результат:**
```
3
```
(Слова: "banana", "cherry", "blueberry" имеют длину больше 5.)

### Задача 9: Пример с использованием `anyMatch()` и `allMatch()`

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        boolean anyMatch = numbers.stream().anyMatch(n -> n > 3);
        boolean allMatch = numbers.stream().allMatch(n -> n < 6);

        System.out.println("anyMatch > 3: " + anyMatch);
        System.out.println("allMatch < 6: " + allMatch);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует методы `anyMatch()` и `allMatch()`:
1. `anyMatch(n -> n > 3)` проверяет, есть ли хотя бы одно число больше 3. Условие выполняется для чисел 4 и 5.
2. `allMatch(n -> n < 6)` проверяет, все ли числа меньше 6. Все числа в списке меньше 6, так что условие выполняется.

**Результат:**
```
anyMatch > 3: true
allMatch < 6: true
```

### Задача 10: Пример с `peek()` для промежуточной обработки

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        numbers.stream()
               .peek(n -> System.out.println("Before doubling: " + n))
               .map(n -> n * 2)
               .peek(n -> System.out.println("After doubling: " + n))
               .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует метод `peek()` для промежуточной обработки элементов в потоке.
1. `peek(n -> System.out.println("Before doubling: " + n))` — печатает значение до умножения на 2.
2. `map(n -> n * 2)` — умножает числа на 2.
3. `peek(n -> System.out.println("After doubling: " + n))` — печатает значение после умножения.
4. `forEach(System.out::println)` — выводит результаты.

**Результат:**
```
Before doubling: 1
After doubling: 2
2
Before doubling: 2
After doubling: 4
4
Before doubling: 3
After doubling: 6
6
Before doubling: 4
After doubling: 8
8
Before doubling: 5
After doubling: 10
10
```

### Задача 11: Пример с использованием `max()` и `min()`

**Код:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 3, 5, 7, 9);

        Optional<Integer> max = numbers.stream().max(Integer::compareTo);
        Optional<Integer> min = numbers.stream().min(Integer::compareTo);

        System.out.println("Max: " + max.orElseThrow());
        System.out.println("Min: " + min.orElseThrow());
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует методы `max()` и `min()` для нахождения максимального и минимального значений в списке:
1. `max(Integer::compareTo)` находит максимальное число.
2. `min(Integer::compareTo)` находит минимальное число.
3. `orElseThrow()` выбрасывает исключение, если поток пуст, но в данном случае поток не пуст.

**Результат:**
```
Max: 9
Min: 1
```

### Задача 12: Пример с комбинированным использованием нескольких операций Stream

**Код:**

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<String> words = Arrays.asList("apple", "banana", "cherry", "avocado", "blueberry");

        String result = words.stream()
                             .filter(word -> word.startsWith("b"))
                             .map(String::toUpperCase)
                             .sorted()
                             .collect(Collectors.joining(", "));

        System.out.println(result);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код выполняет несколько операций Stream:
1. `filter(word -> word.startsWith("b"))` — оставляет только слова, начинающиеся с буквы "b".
2. `map(String::toUpperCase)` — переводит все слова в верхний регистр.
3. `sorted()` — сортирует слова по алфавиту.
4. `collect(Collectors.joining(", "))` — собирает все слова в строку, разделенную запятой.

**Результат:**
```
BANANA, BLUEBERRY
```

### Задача 13: Пример с `flatMap()` для преобразования строк

**Код:**

```java
import java.util.Arrays;
import java.util.List;

public class StreamExample {
    public static void main(String[] args) {
        List<String> sentences = Arrays.asList("Hello world", "Java stream", "Lambda expressions");

        sentences.stream()
                 .flatMap(sentence -> Arrays.stream(sentence.split(" ")))
                 .distinct()
                 .forEach(System.out::println);
    }
}
```

**Вопрос:** Что будет выведено в консоли?

**Ответ:**

Этот код использует `flatMap()` для разделения строк на слова и удаления дубликатов:
1. `flatMap(sentence -> Arrays.stream(sentence.split(" ")))` — разделяет каждое предложение на отдельные слова.
2. `distinct()` — убирает повторяющиеся слова.
3. `forEach(System.out::println)` — выводит уникальные слова.

**Результат:**
```
Hello
world
Java
stream
Lambda
expressions
```

Эти примеры позволяют проверить понимание различных методов Stream API и их применение в различных ситуациях.

