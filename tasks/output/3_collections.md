Вот несколько примеров задач на тему **Коллекций в Java**, которые могут быть заданы на интервью. В каждой задаче нужно будет понять, что выведет код и почему.

### Пример 1: Работа с HashSet
```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        HashSet<Integer> set = new HashSet<>();
        set.add(1);
        set.add(2);
        set.add(3);
        set.add(4);
        set.add(5);
        
        for (Integer num : set) {
            System.out.print(num + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет элементы множества в **непредсказуемом порядке**, так как `HashSet` не сохраняет порядок добавления элементов. Возможный вывод:
```
1 2 3 4 5
```
Но порядок может быть другим, потому что `HashSet` не гарантирует порядка.

### Пример 2: Работа с TreeSet
```java
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        TreeSet<Integer> set = new TreeSet<>();
        set.add(5);
        set.add(1);
        set.add(3);
        set.add(4);
        set.add(2);
        
        for (Integer num : set) {
            System.out.print(num + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет элементы множества в **отсортированном порядке**, так как `TreeSet` использует природный порядок или переданный компаратор. В данном случае вывод будет:
```
1 2 3 4 5
```

### Пример 3: Работа с HashMap
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("cherry", 7);
        
        for (String key : map.keySet()) {
            System.out.print(key + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет ключи в **непредсказуемом порядке**, так как `HashMap` не сохраняет порядок добавления элементов. Возможный вывод:
```
apple banana cherry
```
Однако порядок может изменяться, так как `HashMap` использует хеширование, а порядок ключей не гарантирован.

### Пример 4: Работа с LinkedHashMap
```java
import java.util.LinkedHashMap;

public class Main {
    public static void main(String[] args) {
        LinkedHashMap<String, Integer> map = new LinkedHashMap<>();
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("cherry", 7);
        
        for (String key : map.keySet()) {
            System.out.print(key + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет ключи в **порядке их добавления**, так как `LinkedHashMap` сохраняет порядок вставки. Вывод будет:
```
apple banana cherry
```

### Пример 5: Работа с ArrayList
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        
        for (int i = 0; i < list.size(); i++) {
            list.add(4); // Это изменение списка во время итерации
            System.out.print(list.get(i) + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выбросит `ConcurrentModificationException`, потому что список изменяется (добавление элементов) во время итерации. Итератор не ожидает таких изменений, и это приводит к исключению.

### Пример 6: Работа с ListIterator
```java
import java.util.ArrayList;
import java.util.ListIterator;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        
        ListIterator<Integer> iterator = list.listIterator();
        while (iterator.hasNext()) {
            Integer value = iterator.next();
            if (value == 2) {
                iterator.remove();
            }
        }
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет `[1, 3]`, так как элемент `2` будет удалён с помощью `ListIterator` во время обхода списка, что безопасно для структуры данных.

### Пример 7: Работа с PriorityQueue
```java
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        PriorityQueue<Integer> queue = new PriorityQueue<>();
        queue.add(5);
        queue.add(1);
        queue.add(3);
        
        while (!queue.isEmpty()) {
            System.out.print(queue.poll() + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет элементы в **порядке возрастания**, так как `PriorityQueue` организована как мин-кучу, где наименьший элемент находится на вершине. Вывод будет:
```
1 3 5
```

Эти примеры помогают оценить знание кандидатом принципов работы различных коллекций и их особенностей, таких как порядок элементов и модификации во время обхода.


Вот ещё несколько примеров задач на тему **Коллекций в Java** для интервью, в которых нужно будет понять, что выведет код и почему.

### Пример 8: Работа с LinkedList
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<String> list = new LinkedList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        
        list.addFirst("Z");
        list.addLast("D");
        
        for (String item : list) {
            System.out.print(item + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:** Программа выведет:
```
Z A B C D
```
**Объяснение:** `LinkedList` поддерживает методы `addFirst()` и `addLast()`, которые добавляют элементы в начало и конец списка, соответственно. Поэтому сначала в начало списка добавляется "Z", а затем в конец — "D".

### Пример 9: Работа с HashMap и getOrDefault
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 5);
        map.put("banana", 3);
        
        System.out.println(map.getOrDefault("apple", 0)); // существующий ключ
        System.out.println(map.getOrDefault("cherry", 0)); // несуществующий ключ
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
5
0
```
**Объяснение:** Метод `getOrDefault()` возвращает значение, если ключ существует в карте, или значение по умолчанию, если ключ отсутствует. В случае "apple" возвращается 5, а для "cherry" — 0, так как ключа нет в карте.

### Пример 10: Работа с ListIterator и модификация списка
```java
import java.util.ArrayList;
import java.util.ListIterator;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        
        ListIterator<Integer> iterator = list.listIterator();
        while (iterator.hasNext()) {
            Integer value = iterator.next();
            if (value == 2) {
                iterator.set(5); // заменяем элемент 2 на 5
            }
        }
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[1, 5, 3]
```
**Объяснение:** Метод `set()` в `ListIterator` заменяет текущий элемент на новый. В данном случае, когда итератор достигнет элемента со значением 2, он заменит его на 5.

### Пример 11: Работа с HashSet и дублирование элементов
```java
import java.util.HashSet;

public class Main {
    public static void main(String[] args) {
        HashSet<Integer> set = new HashSet<>();
        set.add(1);
        set.add(2);
        set.add(3);
        set.add(2); // Попытка добавить дублирующий элемент
        set.add(4);
        
        System.out.println(set);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[1, 2, 3, 4]
```
**Объяснение:** `HashSet` не позволяет хранить дублирующиеся элементы, поэтому попытка добавить второе вхождение числа 2 не повлияет на содержимое множества.

### Пример 12: Использование Iterator для удаления элементов
```java
import java.util.ArrayList;
import java.util.Iterator;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        
        Iterator<Integer> iterator = list.iterator();
        while (iterator.hasNext()) {
            Integer value = iterator.next();
            if (value % 2 == 0) {
                iterator.remove(); // Удаление чётных элементов
            }
        }
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[1, 3]
```
**Объяснение:** `Iterator` позволяет безопасно удалять элементы из коллекции во время обхода, в отличие от других методов, таких как обычный `for`-цикл, где это приведет к `ConcurrentModificationException`. В данном случае будут удалены чётные элементы, то есть 2 и 4.

### Пример 13: Работа с TreeMap
```java
import java.util.TreeMap;

public class Main {
    public static void main(String[] args) {
        TreeMap<String, Integer> map = new TreeMap<>();
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("cherry", 7);
        
        System.out.println(map);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
{apple=5, banana=3, cherry=7}
```
**Объяснение:** `TreeMap` сохраняет элементы в отсортированном порядке по ключам, используя их естественный порядок или компаратор (в данном случае по алфавиту). Поэтому элементы будут выведены в следующем порядке: "apple", "banana", "cherry".

### Пример 14: Работа с PriorityQueue и добавление элементов с разными приоритетами
```java
import java.util.PriorityQueue;

public class Main {
    public static void main(String[] args) {
        PriorityQueue<Integer> queue = new PriorityQueue<>((a, b) -> b - a); // Максимальная очередь
        queue.add(5);
        queue.add(1);
        queue.add(3);
        
        while (!queue.isEmpty()) {
            System.out.print(queue.poll() + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
5 3 1
```
**Объяснение:** В данном случае мы использовали кастомный компаратор `(a, b) -> b - a`, который делает очередь максимальной. Поэтому элементы извлекаются в порядке убывания: сначала 5, затем 3 и в конце 1.

### Пример 15: Повторное добавление элемента в ArrayList
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("apple");
        list.add("banana");
        list.add("cherry");
        
        list.add(1, "orange"); // Добавляем элемент "orange" на индекс 1
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[apple, orange, banana, cherry]
```
**Объяснение:** Метод `add(index, element)` вставляет элемент на заданную позицию, сдвигая все элементы после индекса на одну позицию вправо. В данном случае "orange" вставляется на позицию с индексом 1, а остальные элементы сдвигаются.

Эти примеры помогут глубже понять работу коллекций в Java и их особенности, такие как порядок элементов, способы добавления и удаления, а также использование различных типов коллекций.

Конечно! Вот еще несколько примеров задач на тему **Коллекций в Java**, которые могут быть заданы на интервью. В каждой задаче нужно будет понять, что выведет код и почему.

### Пример 16: Работа с `Vector` и потокобезопасность
```java
import java.util.Vector;

public class Main {
    public static void main(String[] args) {
        Vector<Integer> vector = new Vector<>();
        vector.add(1);
        vector.add(2);
        vector.add(3);
        vector.add(4);

        for (Integer num : vector) {
            if (num == 2) {
                vector.remove(Integer.valueOf(2)); // Удаление элемента во время итерации
            }
            System.out.print(num + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
1 2 3 4
```
**Объяснение:** Несмотря на то, что вектор модифицируется во время обхода с помощью метода `remove()`, программа не выбросит исключение, потому что `Vector` является потокобезопасным и поддерживает синхронизацию. Однако это не рекомендуется, так как модификация коллекции во время обхода может привести к неожиданным результатам.

### Пример 17: Использование метода `forEach` для коллекции
```java
import java.util.ArrayList;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("apple");
        list.add("banana");
        list.add("cherry");

        list.forEach(item -> System.out.print(item.toUpperCase() + " "));
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
APPLE BANANA CHERRY
```
**Объяснение:** Метод `forEach` позволяет выполнить операцию для каждого элемента коллекции. В данном случае мы вызываем метод `toUpperCase()` для каждого элемента, что приводит к выводу строк в верхнем регистре.

### Пример 18: Работа с `LinkedHashSet` и порядок добавления
```java
import java.util.LinkedHashSet;

public class Main {
    public static void main(String[] args) {
        LinkedHashSet<String> set = new LinkedHashSet<>();
        set.add("apple");
        set.add("banana");
        set.add("cherry");
        set.add("banana");  // Попытка добавить дубликат

        for (String item : set) {
            System.out.print(item + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
apple banana cherry
```
**Объяснение:** `LinkedHashSet` сохраняет порядок добавления элементов и не позволяет хранить дубликаты. Попытка добавить "banana" второй раз не изменит содержимое множества, так как элементы в `Set` уникальны.

### Пример 19: Использование `TreeMap` с кастомным компаратором
```java
import java.util.TreeMap;

public class Main {
    public static void main(String[] args) {
        TreeMap<String, Integer> map = new TreeMap<>((a, b) -> b.compareTo(a)); // Обратный порядок
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("cherry", 7);

        System.out.println(map);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
{cherry=7, banana=3, apple=5}
```
**Объяснение:** Мы передали кастомный компаратор, который сортирует ключи в обратном порядке. Таким образом, `TreeMap` будет сортировать элементы по убыванию ключей: сначала "cherry", затем "banana", и в конце "apple".

### Пример 20: Дублирование ключей в `HashMap`
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("apple", 3); // Обновление значения для существующего ключа

        System.out.println(map);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
{banana=2, apple=3}
```
**Объяснение:** В `HashMap` ключи уникальны, и если ключ уже существует, то значение для него обновляется. В данном случае, при добавлении второго элемента с ключом "apple", его значение обновляется с 1 на 3.

### Пример 21: Использование `ArrayList` с индексами
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();
        list.add("A");
        list.add("B");
        list.add("C");
        
        list.set(1, "D"); // Заменяем элемент на индексе 1
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[A, D, C]
```
**Объяснение:** Метод `set()` заменяет элемент на заданном индексе. В данном случае элемент с индексом 1 ("B") заменяется на "D".

### Пример 22: Применение метода `removeIf` для коллекции
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        
        list.removeIf(num -> num % 2 == 0); // Удаляем чётные числа
        
        System.out.println(list);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[1, 3]
```
**Объяснение:** Метод `removeIf()` удаляет элементы, удовлетворяющие заданному условию. В данном случае, чётные числа (2 и 4) будут удалены из списка.

### Пример 23: Преобразование `ArrayList` в массив
```java
import java.util.ArrayList;

public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();
        list.add(10);
        list.add(20);
        list.add(30);
        
        Integer[] array = list.toArray(new Integer[0]);
        
        for (Integer num : array) {
            System.out.print(num + " ");
        }
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
10 20 30
```
**Объяснение:** Метод `toArray()` преобразует коллекцию в массив. Параметр `new Integer[0]` необходим для создания массива нужного типа. В итоге программа выводит элементы списка, преобразованные в массив.

### Пример 24: Использование метода `computeIfAbsent` в `HashMap`
```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 1);
        map.put("banana", 2);
        
        map.computeIfAbsent("apple", k -> 3);  // Не изменится, так как "apple" уже есть
        map.computeIfAbsent("cherry", k -> 4); // Будет добавлен

        System.out.println(map);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
{apple=1, banana=2, cherry=4}
```
**Объяснение:** Метод `computeIfAbsent()` добавляет пару ключ-значение в карту, если ключ отсутствует. Для "apple" пара не добавляется, так как ключ уже существует, а для "cherry" добавляется значение 4, так как такого ключа в карте ещё нет.

### Пример 25: Преобразование `HashSet` в `TreeSet`
```java
import java.util.HashSet;
import java.util.TreeSet;

public class Main {
    public static void main(String[] args) {
        HashSet<Integer> hashSet = new HashSet<>();
        hashSet.add(5);
        hashSet.add(3);
        hashSet.add(1);
        
        TreeSet<Integer> treeSet = new TreeSet<>(hashSet);  // Преобразуем в TreeSet
        
        System.out.println(treeSet);
    }
}
```
**Что выведет программа и почему?**

**Ответ:**
```
[1, 3, 5]
```
**Объяснение:** `TreeSet` автоматически сортирует элементы, даже если они были добавлены через `HashSet`, который не гарантирует порядок. В данном случае элементы будут отсортированы по возрастанию.

Эти дополнительные примеры помогают углубить понимание работы коллекций в Java, таких как списки, множества и карты, а также демонстрируют различные способы их модификации и обработки.

