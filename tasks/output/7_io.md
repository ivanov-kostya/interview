Вот несколько примеров задач на тему ввода-вывода (I/O) в Java, которые могут быть заданы на интервью. В каждой задаче интервьюер предоставляет фрагмент кода и просит объяснить, что будет выведено в консоль и почему.

### Пример 1: Работа с файлом и BufferedReader
```java
import java.io.*;

public class FileReaderExample {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Этот код пытается читать строки из файла `test.txt` и выводить их в консоль. Если файл существует и доступен, программа выведет строки, содержащиеся в файле, по одной на каждой строке. Если файла нет или произошла ошибка, в консоль будет выведено сообщение об ошибке вида "Error: <сообщение об ошибке>", где `<сообщение об ошибке>` будет содержать описание проблемы (например, "No such file or directory").

---

### Пример 2: Чтение данных из консоли
```java
import java.io.*;

public class ConsoleInputExample {
    public static void main(String[] args) throws IOException {
        BufferedReader reader = new BufferedReader(new InputStreamReader(System.in));
        String line = reader.readLine();
        System.out.println("You entered: " + line);
    }
}
```
**Вопрос:** Что будет выведено в консоль, если пользователь введет строку "Hello World"?

**Ответ:**
Если пользователь введет строку "Hello World", программа выведет:

```
You entered: Hello World
```

Программа использует `BufferedReader` для чтения строки, введенной с клавиатуры через `System.in`, и затем выводит эту строку на экран.

---

### Пример 3: Ошибка при закрытии потока
```java
import java.io.*;

public class StreamExample {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            fos.write("Hello, World!".getBytes());
            System.out.println("Data written successfully");
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
        } finally {
            System.out.println("Finally block executed");
        }
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Программа корректно записывает строку "Hello, World!" в файл `output.txt`, а затем выводит:

```
Data written successfully
Finally block executed
```

`finally` блок всегда выполняется, независимо от того, было ли исключение или нет. Поэтому в нем также будет выведено сообщение.

---

### Пример 4: Использование PrintWriter с автозакрытием
```java
import java.io.*;

public class PrintWriterExample {
    public static void main(String[] args) {
        try (PrintWriter writer = new PrintWriter("example.txt")) {
            writer.println("Hello, PrintWriter!");
        } catch (FileNotFoundException e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```
**Вопрос:** Что будет выведено в консоль, если файл `example.txt` не существует?

**Ответ:**
Если файл `example.txt` не существует, то будет выброшено исключение `FileNotFoundException`, и в консоль будет выведено сообщение:

```
File not found: <сообщение ошибки>
```

Так как программа использует конструкцию `try-with-resources`, ресурс `PrintWriter` будет автоматически закрыт после завершения работы блока.

---

### Пример 5: Проблемы с кодировкой
```java
import java.io.*;

public class EncodingExample {
    public static void main(String[] args) throws IOException {
        String text = "Привет, мир!";
        FileOutputStream fos = new FileOutputStream("output.txt");
        fos.write(text.getBytes("UTF-8"));
        fos.close();

        FileInputStream fis = new FileInputStream("output.txt");
        byte[] data = new byte[fis.available()];
        fis.read(data);
        fis.close();

        System.out.println(new String(data, "UTF-8"));
    }
}
```
**Вопрос:** Что будет выведено в консоль, если файл `output.txt` был записан с кодировкой UTF-8, а затем прочитан обратно с использованием той же кодировки?

**Ответ:**
Если в файл записана строка `"Привет, мир!"` в кодировке UTF-8 и затем она правильно читается с той же кодировкой, программа выведет:

```
Привет, мир!
```

Если возникнут проблемы с кодировкой (например, при использовании неверной кодировки), то строка может быть отображена неправильно (с различными артефактами).

---

### Пример 6: Порядок закрытия потоков
```java
import java.io.*;

public class CloseOrderExample {
    public static void main(String[] args) {
        try (BufferedReader reader = new BufferedReader(new FileReader("test.txt"));
             BufferedWriter writer = new BufferedWriter(new FileWriter("output.txt"))) {
            String line;
            while ((line = reader.readLine()) != null) {
                writer.write(line);
                writer.newLine();
            }
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
        }
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Если файл `test.txt` существует и доступен для чтения, а файл `output.txt` создается для записи, программа скопирует содержимое одного файла в другой. Если возникнет ошибка при чтении или записи, в консоль будет выведено сообщение об исключении, например:

```
IOException: <сообщение об ошибке>
```

Потоки `BufferedReader` и `BufferedWriter` автоматически закроются после завершения работы с ними благодаря конструкции `try-with-resources`.

---

Эти задачи проверяют как основные знания по работе с файловыми потоками, так и знание конструкций для безопасного закрытия ресурсов и правильного их использования в Java.

Вот еще несколько примеров задач на тему ввода-вывода (I/O) в Java, которые могут быть заданы на интервью. Они фокусируются на различных аспектах работы с потоками, файлами и ошибками.

### Пример 7: Чтение и запись через байтовые потоки
```java
import java.io.*;

public class ByteStreamExample {
    public static void main(String[] args) throws IOException {
        FileInputStream fis = new FileInputStream("input.txt");
        FileOutputStream fos = new FileOutputStream("output.txt");
        
        int data;
        while ((data = fis.read()) != -1) {
            fos.write(data);
        }
        
        fis.close();
        fos.close();
    }
}
```
**Вопрос:** Что будет сделано и какие файлы будут изменены?

**Ответ:**
Этот код читает байты из файла `input.txt` и записывает их в файл `output.txt`. Он использует байтовые потоки для работы с данными в виде байтов. Если файл `input.txt` существует и содержит данные, то эти данные будут скопированы в файл `output.txt`. Если `input.txt` не существует, будет выброшено исключение `FileNotFoundException`.

В консоль ничего не будет выведено.

---

### Пример 8: Использование PrintWriter с автоочисткой
```java
import java.io.*;

public class PrintWriterFlushExample {
    public static void main(String[] args) {
        try (PrintWriter writer = new PrintWriter(new FileWriter("example.txt"))) {
            writer.print("Hello, ");
            writer.print("World!");
            writer.flush();  // явный вызов flush
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
        }
    }
}
```
**Вопрос:** Что произойдет, если файл `example.txt` не существует, и что будет записано в этот файл?

**Ответ:**
Программа откроет файл `example.txt` для записи, запишет в него строку "Hello, World!" и явно вызовет метод `flush()` для немедленного сброса данных на диск. После выполнения кода файл `example.txt` будет содержать:

```
Hello, World!
```

Если файл не существует, он будет создан. В консоль ничего не будет выведено, так как программа не вызывает `System.out.println()`.

---

### Пример 9: Чтение строк из файла с помощью Files API
```java
import java.nio.file.*;
import java.io.IOException;
import java.util.List;

public class NIOExample {
    public static void main(String[] args) {
        try {
            List<String> lines = Files.readAllLines(Paths.get("test.txt"));
            for (String line : lines) {
                System.out.println(line);
            }
        } catch (IOException e) {
            System.out.println("IOException: " + e.getMessage());
        }
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Этот код использует NIO (New Input/Output) API для чтения всех строк из файла `test.txt` и вывода их в консоль. Если файл существует и содержит несколько строк, программа выведет их поочередно. Если файл не существует или произошла ошибка, в консоль будет выведено сообщение об ошибке вида:

```
IOException: <сообщение ошибки>
```

Пример вывода:

```
Hello
World
```

---

### Пример 10: Работа с файлом с использованием DataInputStream и DataOutputStream
```java
import java.io.*;

public class DataStreamExample {
    public static void main(String[] args) throws IOException {
        DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.dat"));
        dos.writeInt(42);
        dos.writeDouble(3.14);
        dos.writeUTF("Hello, Data Streams!");
        dos.close();

        DataInputStream dis = new DataInputStream(new FileInputStream("data.dat"));
        System.out.println(dis.readInt());
        System.out.println(dis.readDouble());
        System.out.println(dis.readUTF());
        dis.close();
    }
}
```
**Вопрос:** Что будет выведено в консоль, если файл `data.dat` был успешно создан и содержит данные?

**Ответ:**
Программа записывает в файл `data.dat` три значения: целое число (42), число с плавающей точкой (3.14) и строку ("Hello, Data Streams!"). Затем она читает эти данные и выводит их на консоль. Вывод будет следующим:

```
42
3.14
Hello, Data Streams!
```

Если файл `data.dat` не существует или возникнет ошибка при чтении/записи, программа выведет сообщение об ошибке в консоль.

---

### Пример 11: Работа с RandomAccessFile
```java
import java.io.*;

public class RandomAccessFileExample {
    public static void main(String[] args) throws IOException {
        RandomAccessFile file = new RandomAccessFile("random.dat", "rw");
        file.writeInt(123);
        file.writeDouble(45.67);
        file.seek(0);  // перемещение указателя на начало
        System.out.println(file.readInt());
        System.out.println(file.readDouble());
        file.close();
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Этот код использует `RandomAccessFile`, чтобы записать целое число и число с плавающей точкой в файл `random.dat`. Затем программа перемещает указатель в начало файла и читает эти данные. Вывод будет:

```
123
45.67
```

Если файл не существует, он будет создан. В случае ошибок при чтении или записи, будет выброшено исключение.

---

### Пример 12: Работа с FileReader и FileWriter
```java
import java.io.*;

public class FileReaderWriterExample {
    public static void main(String[] args) throws IOException {
        FileWriter writer = new FileWriter("file.txt");
        writer.write("Hello, World!");
        writer.close();

        FileReader reader = new FileReader("file.txt");
        int data;
        while ((data = reader.read()) != -1) {
            System.out.print((char) data);
        }
        reader.close();
    }
}
```
**Вопрос:** Что будет выведено в консоль?

**Ответ:**
Программа сначала записывает строку "Hello, World!" в файл `file.txt`, а затем считывает этот файл и выводит содержимое в консоль. Вывод будет:

```
Hello, World!
```

Если файл не существует, он будет создан. В случае ошибки при записи или чтении будет выброшено исключение.

---

### Пример 13: Проблемы с ресурсами в потоке
```java
import java.io.*;

public class ResourceLeakExample {
    public static void main(String[] args) {
        BufferedReader reader = null;
        try {
            reader = new BufferedReader(new FileReader("test.txt"));
            String line = reader.readLine();
            System.out.println(line);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            // Поток не закрывается здесь, утечка ресурса
        }
    }
}
```
**Вопрос:** Какие проблемы могут возникнуть при выполнении этого кода?

**Ответ:**
Этот код пытается прочитать строку из файла `test.txt`, но он не закрывает поток `BufferedReader` в блоке `finally`. Это может привести к утечке ресурса, так как поток не будет закрыт, даже если произошла ошибка или выполнение завершилось успешно. Чтобы исправить это, нужно либо явно закрыть поток в блоке `finally`, либо использовать конструкцию `try-with-resources`.

---

Эти примеры охватывают различные темы работы с потоками ввода/вывода, от базового чтения и записи файлов до работы с более сложными потоками, такими как `RandomAccessFile`, а также проблемы утечек ресурсов и ошибок при работе с файлами.

