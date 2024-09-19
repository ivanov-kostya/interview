# I/O в Java 
## Основы I/O в Java

I/O (Input/Output) — это процесс взаимодействия программы с внешними источниками данных, такими как файлы, консоль, сеть и другие устройства. В Java операции I/O осуществляются с помощью потоков (streams). Потоки являются абстракциями, которые позволяют передавать данные из источника в приемник, и Java предоставляет мощный и гибкий API для работы с ними.

Давайте разберем более детально каждый из аспектов:

### 1. Введение в I/O

Java использует потоки для выполнения операций ввода и вывода. Поток представляет собой непрерывную последовательность данных. Потоки позволяют эффективно и просто управлять вводом и выводом данных, абстрагируя разработчика от деталей реализации работы с низкоуровневыми устройствами, такими как дисковые накопители или сетевые соединения.

Потоки I/O в Java можно разделить на две основные категории:
- **Потоки ввода (Input Streams)**: используются для чтения данных.
- **Потоки вывода (Output Streams)**: используются для записи данных.

### 2. Иерархия классов I/O в Java

Java предоставляет богатую иерархию классов для работы с вводом и выводом, сгруппированных в пакете `java.io`. Основные классы делятся на два типа: **байтовые потоки** и **символьные потоки**.

- **Байтовые потоки (Byte Streams)**: работают с данными в виде байтов (`byte`). Они полезны для работы с двоичными файлами, такими как изображения, аудио или видео.
    - Основные абстрактные классы:
        - `InputStream` — базовый класс для всех потоков ввода байтов.
        - `OutputStream` — базовый класс для всех потоков вывода байтов.
    - Основные реализации:
        - `FileInputStream` и `FileOutputStream` — для работы с файловыми потоками.
        - `BufferedInputStream` и `BufferedOutputStream` — для буферизированного ввода и вывода.
        - `DataInputStream` и `DataOutputStream` — для работы с примитивными типами данных.
        - `ObjectInputStream` и `ObjectOutputStream` — для сериализации и десериализации объектов.

- **Символьные потоки (Character Streams)**: работают с данными в виде символов (`char`). Они полезны для работы с текстовыми файлами.
    - Основные абстрактные классы:
        - `Reader` — базовый класс для всех потоков ввода символов.
        - `Writer` — базовый класс для всех потоков вывода символов.
    - Основные реализации:
        - `FileReader` и `FileWriter` — для работы с файловыми потоками.
        - `BufferedReader` и `BufferedWriter` — для буферизированного ввода и вывода.
        - `InputStreamReader` и `OutputStreamWriter` — адаптеры между байтовыми и символьными потоками.
        - `PrintWriter` — для форматированного вывода текста.

### 3. Различие между потоками ввода и вывода

- **Потоки ввода** предназначены для чтения данных из различных источников, таких как файлы, консоль, сокеты и т. д. Они читают данные и помещают их в программу.
    - Примеры: `FileInputStream`, `BufferedInputStream`, `InputStreamReader`.

- **Потоки вывода** предназначены для записи данных из программы в различные назначения, такие как файлы, консоль, сокеты и т. д. Они получают данные из программы и записывают их в заданное место.
    - Примеры: `FileOutputStream`, `BufferedOutputStream`, `PrintWriter`.

Обычно поток создается, когда объект класса `InputStream` или `OutputStream` (или их подклассов) инициализируется, и заканчивается, когда поток закрывается вызовом метода `close()`. Важно правильно управлять потоками, чтобы избежать утечек памяти или блокировок.

### 4. Байтовые и символьные потоки

#### Байтовые потоки (Byte Streams)
Байтовые потоки работают с необработанными байтами. Эти потоки полезны для работы с бинарными данными, такими как изображения или аудиофайлы, где требуется сохранять точную структуру байтов. Классы, реализующие байтовые потоки, наследуются от `InputStream` и `OutputStream`.

- **Основные байтовые потоки**:
    - `FileInputStream` и `FileOutputStream`: используются для чтения и записи данных в файл в формате байтов.
    - `BufferedInputStream` и `BufferedOutputStream`: добавляют буферизацию, что увеличивает производительность путем минимизации операций чтения и записи в файл.
    - `DataInputStream` и `DataOutputStream`: предназначены для чтения и записи примитивных типов данных (например, `int`, `double`) в формате байтов.

Пример использования байтовых потоков:
```java
try (FileInputStream fis = new FileInputStream("example.txt");
     FileOutputStream fos = new FileOutputStream("output.txt")) {
    int byteData;
    while ((byteData = fis.read()) != -1) {
        fos.write(byteData);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

#### Символьные потоки (Character Streams)
Символьные потоки работают с символами, то есть данными типа `char`. Они полезны при работе с текстовыми данными, так как учитывают кодировку символов и могут работать с многобайтовыми кодировками. Классы символьных потоков наследуются от `Reader` и `Writer`.

- **Основные символьные потоки**:
    - `FileReader` и `FileWriter`: используются для чтения и записи текстовых данных в файлы.
    - `BufferedReader` и `BufferedWriter`: добавляют буферизацию для увеличения производительности и предоставляют методы для эффективного чтения строк, такие как `readLine()`.
    - `InputStreamReader` и `OutputStreamWriter`: используются для преобразования байтовых потоков в символьные, позволяя работать с различными кодировками.

Пример использования символьных потоков:
```java
try (BufferedReader br = new BufferedReader(new FileReader("example.txt"));
     BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        bw.write(line);
        bw.newLine();
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### Заключение

Понимание основ ввода-вывода в Java и знание различных классов и их иерархии являются фундаментальными навыками для разработки надежных и эффективных приложений. Потоки — это мощный инструмент для работы с данными, и правильное использование байтовых и символьных потоков помогает создать оптимизированные и масштабируемые программы.

## Байтовые потокм
### Байтовые потоки (Byte Streams) в Java

Байтовые потоки (Byte Streams) в Java предназначены для работы с данными в их «сырых» форматах — байтах. Эти потоки позволяют считывать и записывать данные по байтам, что делает их подходящими для работы с файлами, изображениями, аудио и другими типами бинарных данных.

Давайте разберем каждый из аспектов байтовых потоков более подробно:

### 1. Классы `InputStream` и `OutputStream`

`InputStream` и `OutputStream` — это абстрактные базовые классы, от которых наследуются все байтовые потоки. Эти классы обеспечивают основные методы для чтения и записи байтов.

- **`InputStream`**:
    - Основной класс для всех потоков ввода байтов. Он предоставляет методы для чтения данных из различных источников.
    - **Основные методы**:
        - `int read()`: Читает один байт данных и возвращает его в виде `int`. Возвращает `-1`, если достигнут конец потока.
        - `int read(byte[] b)`: Читает данные в массив байтов `b` и возвращает количество прочитанных байтов или `-1`, если достигнут конец потока.
        - `int read(byte[] b, int off, int len)`: Читает до `len` байтов в массив `b`, начиная с `off`.
        - `void close()`: Закрывает поток и освобождает ресурсы.

- **`OutputStream`**:
    - Основной класс для всех потоков вывода байтов. Он предоставляет методы для записи данных в различные источники.
    - **Основные методы**:
        - `void write(int b)`: Записывает один байт данных.
        - `void write(byte[] b)`: Записывает все байты из массива `b`.
        - `void write(byte[] b, int off, int len)`: Записывает `len` байтов из массива `b`, начиная с `off`.
        - `void flush()`: Очищает буфер вывода и записывает все буферизированные данные.
        - `void close()`: Закрывает поток и освобождает ресурсы.

### 2. Работа с файлами через `FileInputStream` и `FileOutputStream`

`FileInputStream` и `FileOutputStream` — классы, которые предоставляют средства для чтения и записи данных в файлы. Они являются конкретными реализациями классов `InputStream` и `OutputStream`.

- **`FileInputStream`**:
    - Используется для чтения данных из файла.
    - Конструкторы:
        - `FileInputStream(File file)`: Создает поток ввода для чтения из файла.
        - `FileInputStream(String name)`: Создает поток ввода для чтения из файла по имени.

Пример чтения данных из файла:
```java
try (FileInputStream fis = new FileInputStream("example.txt")) {
    int data;
    while ((data = fis.read()) != -1) {
        System.out.print((char) data);  // Чтение и вывод каждого символа
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

- **`FileOutputStream`**:
    - Используется для записи данных в файл.
    - Конструкторы:
        - `FileOutputStream(File file)`: Создает поток вывода для записи в файл.
        - `FileOutputStream(String name)`: Создает поток вывода для записи в файл по имени.

Пример записи данных в файл:
```java
try (FileOutputStream fos = new FileOutputStream("output.txt")) {
    String text = "Hello, World!";
    fos.write(text.getBytes());  // Запись строки в файл
} catch (IOException e) {
    e.printStackTrace();
}
```

### 3. Буферизация байтовых потоков: `BufferedInputStream` и `BufferedOutputStream`

Буферизация потоков ввода-вывода позволяет повысить производительность путем уменьшения количества операций чтения/записи. `BufferedInputStream` и `BufferedOutputStream` предоставляют такие возможности, добавляя буфер между программой и потоком данных.

- **`BufferedInputStream`**:
    - Буферизированный поток ввода, который увеличивает производительность за счет уменьшения числа обращений к источнику данных.
    - Конструкторы:
        - `BufferedInputStream(InputStream in)`: Создает буферизированный поток ввода с буфером по умолчанию.
        - `BufferedInputStream(InputStream in, int size)`: Создает буферизированный поток ввода с заданным размером буфера.

- **`BufferedOutputStream`**:
    - Буферизированный поток вывода, который повышает производительность, буферизируя данные перед их записью.
    - Конструкторы:
        - `BufferedOutputStream(OutputStream out)`: Создает буферизированный поток вывода с буфером по умолчанию.
        - `BufferedOutputStream(OutputStream out, int size)`: Создает буферизированный поток вывода с заданным размером буфера.

Пример использования буферизированных потоков:
```java
try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("example.txt"));
     BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("output.txt"))) {

    int data;
    while ((data = bis.read()) != -1) {
        bos.write(data);  // Чтение и запись данных с буферизацией
    }
    bos.flush();  // Явное освобождение буфера
} catch (IOException e) {
    e.printStackTrace();
}
```

### 4. Чтение и запись массивов байтов

В Java можно легко работать с массивами байтов для выполнения операций ввода-вывода. Это полезно для повышения производительности и уменьшения количества системных вызовов.

Пример чтения и записи массива байтов:
```java
try (FileInputStream fis = new FileInputStream("example.txt");
     FileOutputStream fos = new FileOutputStream("output.txt")) {

    byte[] buffer = new byte[1024];  // Буфер размером 1 КБ
    int bytesRead;
    while ((bytesRead = fis.read(buffer)) != -1) {
        fos.write(buffer, 0, bytesRead);  // Запись считанных байтов
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### 5. Работа с данными примитивных типов: `DataInputStream` и `DataOutputStream`

Классы `DataInputStream` и `DataOutputStream` позволяют читать и записывать данные примитивных типов (`int`, `double`, `boolean`, и т. д.) в формате байтов. Это полезно для записи и чтения бинарных данных в форматах, независимых от платформы.

- **`DataInputStream`**:
    - Расширяет `FilterInputStream` и позволяет читать данные примитивных типов из потока.
    - Примеры методов: `readInt()`, `readDouble()`, `readBoolean()`.

- **`DataOutputStream`**:
    - Расширяет `FilterOutputStream` и позволяет записывать данные примитивных типов в поток.
    - Примеры методов: `writeInt(int v)`, `writeDouble(double v)`, `writeBoolean(boolean v)`.

Пример использования `DataInputStream` и `DataOutputStream`:
```java
try (DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.bin"))) {
    dos.writeInt(123);  // Запись целого числа
    dos.writeDouble(45.67);  // Запись числа с плавающей точкой
} catch (IOException e) {
    e.printStackTrace();
}

try (DataInputStream dis = new DataInputStream(new FileInputStream("data.bin"))) {
    int number = dis.readInt();  // Чтение целого числа
    double decimal = dis.readDouble();  // Чтение числа с плавающей точкой
    System.out.println("Число: " + number + ", Дробное число: " + decimal);
} catch (IOException e) {
    e.printStackTrace();
}
```

### 6. Сериализация объектов: `ObjectInputStream` и `ObjectOutputStream`

Сериализация в Java позволяет сохранять объекты в поток и затем восстанавливать их из потока. Классы `ObjectInputStream` и `ObjectOutputStream` используются для сериализации и десериализации объектов.

- **`ObjectOutputStream`**:
    - Записывает объекты в поток и сериализует их.
    - Метод `writeObject(Object obj)` записывает объект в поток.

- **`ObjectInputStream`**:
    - Читает объекты из потока и десериализует их.
    - Метод `readObject()` читает объект из потока и возвращает его.

Пример сериализации и десериализации объекта:
```java
import java.io.*;

class Person implements Serializable {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{name='" + name + "', age=" + age + "}";
    }
}

public class SerializationExample {


    public static void main(String[] args) {
        Person person = new Person("Alice", 30);

        // Сериализация
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.ser"))) {
            oos.writeObject(person);  // Запись объекта в файл
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Десериализация
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.ser"))) {
            Person deserializedPerson = (Person) ois.readObject();  // Чтение объекта из файла
            System.out.println("Десериализованный объект: " + deserializedPerson);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

### Заключение

Байтовые потоки в Java предоставляют мощные инструменты для работы с бинарными данными. Они охватывают широкий спектр задач — от работы с файлами до сериализации объектов и передачи данных по сети. Понимание того, как использовать эти потоки, позволяет разработчику эффективно управлять вводом-выводом данных, обеспечивая производительность и надежность приложений.

## Символьные потоки (Character Streams)
