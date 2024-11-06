Вот несколько примеров задач на тему **исключений в Java**, которые интервьюер может использовать на собеседовании. В каждой задаче присутствует код, и интервьюер просит объяснить, что будет выведено в консоли и почему.

### Пример 1: Обработка исключений с `try-catch`

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("Start");
            int result = 10 / 0;
            System.out.println("End");
        } catch (ArithmeticException e) {
            System.out.println("ArithmeticException caught");
        }
        System.out.println("After catch");
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Start
  ArithmeticException caught
  After catch
  ```
- **Объяснение:** Код в блоке `try` вызывает исключение `ArithmeticException` (деление на ноль), которое перехватывается в блоке `catch`. После этого программа продолжает выполнение, выводя "After catch".

### Пример 2: Порядок обработки нескольких исключений

```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = null;
            System.out.println(str.length());
        } catch (NullPointerException e) {
            System.out.println("NullPointerException caught");
        } catch (Exception e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  NullPointerException caught
  ```
- **Объяснение:** Исключение `NullPointerException` возникает, потому что переменная `str` равна `null`, и попытка вызвать метод `length()` вызывает исключение. Этот тип исключения перехватывается первым `catch`-блоком.

### Пример 3: Несовместимость исключений

```java
public class Test {
    public static void main(String[] args) {
        try {
            throw new Exception();
        } catch (NullPointerException e) {
            System.out.println("NullPointerException caught");
        } catch (Exception e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Exception caught
  ```
- **Объяснение:** Исключение типа `Exception` выбрасывается в блоке `try`, и оно перехватывается в соответствующем блоке `catch (Exception e)`. Код не попадет в блок `catch (NullPointerException e)`, потому что исключение не является `NullPointerException`.

### Пример 4: Исключения внутри и после метода

```java
public class Test {
    public static void main(String[] args) {
        try {
            method();
        } catch (Exception e) {
            System.out.println("Exception caught in main");
        }
    }

    public static void method() throws Exception {
        try {
            throw new Exception("Exception in method");
        } finally {
            System.out.println("Finally in method");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Finally in method
  Exception caught in main
  ```
- **Объяснение:** Исключение выбрасывается в методе, но прежде чем оно будет передано дальше, выполняется блок `finally`, который всегда выполняется. После этого исключение перехватывается в блоке `catch` метода `main`.

### Пример 5: Множественные исключения и их обработка

```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = "Java";
            System.out.println(str.charAt(10));
        } catch (StringIndexOutOfBoundsException e) {
            System.out.println("StringIndexOutOfBoundsException caught");
        } catch (Exception e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  StringIndexOutOfBoundsException caught
  ```
- **Объяснение:** Попытка получить символ строки по индексу 10 вызывает исключение `StringIndexOutOfBoundsException`, так как строка имеет меньше символов. Этот тип исключения перехватывается первым блоком `catch`.

### Пример 6: Пример с выбрасыванием собственного исключения

```java
class MyException extends Exception {
    public MyException(String message) {
        super(message);
    }
}

public class Test {
    public static void main(String[] args) {
        try {
            throw new MyException("Custom Exception occurred");
        } catch (MyException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Custom Exception occurred
  ```
- **Объяснение:** Исключение `MyException` выбрасывается в блоке `try` и перехватывается в соответствующем блоке `catch`. Метод `getMessage()` возвращает строку, переданную при создании исключения.

### Пример 7: Несколько блоков `catch`

```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = "Java";
            System.out.println(str.charAt(10)); // Этот код вызовет исключение
        } catch (StringIndexOutOfBoundsException e) {
            System.out.println("Caught StringIndexOutOfBoundsException");
        } catch (Exception e) {
            System.out.println("Caught Exception");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Caught StringIndexOutOfBoundsException
  ```
- **Объяснение:** Поскольку в строке `"Java"` попытка обращения к символу с индексом 10 вызывает исключение `StringIndexOutOfBoundsException`, оно перехватывается первым блоком `catch`. Второй блок `catch` не выполняется.

Эти примеры помогут интервьюеру проверить знания кандидата в области работы с исключениями, а также умение правильно объяснять, как и почему возникают те или иные результаты в Java.

Вот еще несколько примеров задач на тему **исключений в Java** с кодом, где интервьюер может попросить объяснить, что будет выведено в консоль и почему.

### Пример 8: Исключение в блоке `finally`

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("Try block");
            throw new Exception("Exception in try");
        } catch (Exception e) {
            System.out.println("Catch block");
        } finally {
            System.out.println("Finally block");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Try block
  Catch block
  Finally block
  ```
- **Объяснение:** Исключение выбрасывается в блоке `try` и перехватывается в блоке `catch`. Блок `finally` выполняется всегда, независимо от того, было ли исключение или нет.

### Пример 9: Исключение с несколькими блоками `finally`

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("Try block");
            throw new Exception("Exception in try");
        } catch (Exception e) {
            System.out.println("Catch block");
        } finally {
            System.out.println("Finally block 1");
            try {
                System.out.println("Nested try block");
                throw new Exception("Exception in nested try");
            } finally {
                System.out.println("Nested finally block");
            }
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Try block
  Catch block
  Finally block 1
  Nested try block
  Nested finally block
  ```
- **Объяснение:** Внешний блок `finally` выполняется всегда, даже если исключение выбрасывается в блоке `try`. Внутри блока `finally` также есть вложенный `try-catch-finally`, который выполняется независимо от ошибок в основном блоке `finally`.

### Пример 10: Рекурсивное исключение

```java
public class Test {
    public static void main(String[] args) {
        method();
    }

    public static void method() {
        try {
            System.out.println("Entering method");
            method(); // Рекурсивный вызов
        } catch (StackOverflowError e) {
            System.out.println("StackOverflowError caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Entering method
  Entering method
  Entering method
  ...
  StackOverflowError caught
  ```
- **Объяснение:** Рекурсивный вызов метода без базового условия приводит к переполнению стека и выбрасыванию ошибки `StackOverflowError`, которую перехватывает блок `catch`.

### Пример 11: Необработанное исключение

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("Start");
            throw new RuntimeException("Unchecked exception");
        } catch (Exception e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Start
  Exception caught
  ```
- **Объяснение:** Исключение `RuntimeException` — это необработанное исключение, которое можно выбросить без явной обработки, но оно все равно перехватывается в блоке `catch (Exception e)`.

### Пример 12: Блок `finally` после выбрасывания исключения в `try`

```java
public class Test {
    public static void main(String[] args) {
        try {
            System.out.println("In try");
            throw new Exception("Exception in try");
        } catch (Exception e) {
            System.out.println("In catch");
            return; // Прерывает выполнение метода
        } finally {
            System.out.println("In finally");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  In try
  In catch
  In finally
  ```
- **Объяснение:** Блок `finally` выполняется всегда, даже если в блоке `catch` был использован `return`. Это гарантирует выполнение финализирующего кода.

### Пример 13: Выбрасывание исключений с `throw`

```java
public class Test {
    public static void main(String[] args) {
        try {
            throw new IllegalArgumentException("Illegal Argument Exception");
        } catch (IllegalArgumentException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Caught exception: Illegal Argument Exception
  ```
- **Объяснение:** Исключение `IllegalArgumentException` выбрасывается с помощью оператора `throw`, и оно перехватывается в соответствующем блоке `catch`. Метод `getMessage()` возвращает строку, переданную при создании исключения.

### Пример 14: Перехват нескольких исключений в одном блоке

```java
public class Test {
    public static void main(String[] args) {
        try {
            String str = "Java";
            System.out.println(str.charAt(10)); // вызывает исключение
        } catch (StringIndexOutOfBoundsException | NullPointerException e) {
            System.out.println("Exception caught");
        }
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Exception caught
  ```
- **Объяснение:** Java позволяет перехватывать несколько исключений в одном блоке `catch`, если они имеют общий родительский класс (например, `Exception`). В данном случае выбрасывается исключение `StringIndexOutOfBoundsException`, которое перехватывается общим блоком `catch`.

### Пример 15: Исключения в многопоточности

```java
public class Test {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            try {
                System.out.println("Thread started");
                throw new InterruptedException("Thread interrupted");
            } catch (InterruptedException e) {
                System.out.println("Exception in thread: " + e.getMessage());
            }
        });
        thread.start();
    }
}
```

**Ответ:**
- **Вывод в консоли:**
  ```
  Thread started
  Exception in thread: Thread interrupted
  ```
- **Объяснение:** Внутри потока выбрасывается исключение `InterruptedException`, которое перехватывается в блоке `catch`. Исключение связано с прерыванием потока, и оно обрабатывается внутри потока.

Эти примеры помогут интервьюеру проверить глубину знаний кандидата по обработке исключений в различных сценариях, включая многозадачность, рекурсию, обработку разных типов исключений и работу с блоками `finally`.

