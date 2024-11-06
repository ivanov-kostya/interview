Вот несколько примеров задач на тему многопоточности в Java, которые могут встретиться на интервью. В этих задачах интервьюер предоставляет код и спрашивает, какой результат будет выведен в консоль и почему.

### Задача 1: Простое использование `Thread`
```java
public class Main {
    public static void main(String[] args) {
        Thread t = new Thread(() -> System.out.println("Hello from thread!"));
        t.start();
        System.out.println("Hello from main!");
    }
}
```

**Вопрос**: Что будет выведено в консоль и почему?

**Ответ**:
Вывод будет:
```
Hello from main!
Hello from thread!
```
Это связано с тем, что метод `t.start()` запускает новый поток, который выполняет анонимную функцию, печатающую "Hello from thread!". Однако основной поток, в котором выполняется метод `main`, не блокируется, он сразу печатает "Hello from main!" и завершает выполнение, а поток `t` печатает сообщение позднее, когда успевает выполнить свою задачу.

---

### Задача 2: Синхронизация с использованием `synchronized`
```java
public class Main {
    private int counter = 0;

    public synchronized void increment() {
        counter++;
    }

    public synchronized void decrement() {
        counter--;
    }

    public int getCounter() {
        return counter;
    }

    public static void main(String[] args) throws InterruptedException {
        Main obj = new Main();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                obj.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                obj.decrement();
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Final counter: " + obj.getCounter());
    }
}
```

**Вопрос**: Какой будет результат выполнения программы и почему?

**Ответ**:
Вывод будет:
```
Final counter: 0
```
Методы `increment()` и `decrement()` синхронизированы, что означает, что в каждый момент времени только один поток может получить доступ к этим методам. Потоки `t1` и `t2` выполняются параллельно и изменяют значение переменной `counter`. После выполнения всех инкрементов и декрементов счетчик возвращается к своему начальному значению (0).

---

### Задача 3: Безопасность при многозадачности (не синхронизированные методы)
```java
public class Main {
    private int counter = 0;

    public void increment() {
        counter++;
    }

    public void decrement() {
        counter--;
    }

    public int getCounter() {
        return counter;
    }

    public static void main(String[] args) throws InterruptedException {
        Main obj = new Main();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                obj.increment();
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                obj.decrement();
            }
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Final counter: " + obj.getCounter());
    }
}
```

**Вопрос**: Какой результат будет выведен в консоль?

**Ответ**:
Результат может быть любым, но не обязательно равным 0. Например:
```
Final counter: 2
```
В этой задаче методы `increment()` и `decrement()` не синхронизированы, и несколько потоков могут одновременно изменять значение переменной `counter`. Это приведет к гонкам данных, и результат может варьироваться. Потоки могут читать и записывать значение переменной `counter` одновременно, что приведет к некорректным результатам.

---

### Задача 4: Использование `ExecutorService`
```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        executor.submit(() -> {
            System.out.println("Task 1");
        });

        executor.submit(() -> {
            System.out.println("Task 2");
        });

        executor.shutdown();
    }
}
```

**Вопрос**: Какой будет вывод программы и почему?

**Ответ**:
Вывод будет:
```
Task 1
Task 2
```
Или наоборот:
```
Task 2
Task 1
```
Это зависит от того, как именно планировщик потоков исполнил задачи. Поскольку задачи выполняются параллельно в потоке из пула с фиксированным размером (2 потока), их порядок может быть разным.

---

### Задача 5: Пример с `join()`
```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("t1: " + i);
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 5; i++) {
                System.out.println("t2: " + i);
            }
        });

        t1.start();
        t2.start();
        
        t1.join();  // main thread waits for t1 to finish
        t2.join();  // main thread waits for t2 to finish

        System.out.println("Main thread finished");
    }
}
```

**Вопрос**: Какой будет вывод в консоль?

**Ответ**:
Вывод будет следующим:
```
t1: 0
t1: 1
t1: 2
t1: 3
t1: 4
t2: 0
t2: 1
t2: 2
t2: 3
t2: 4
Main thread finished
```
Порядок вывода сообщений от потоков `t1` и `t2` может варьироваться, потому что они работают параллельно. Однако главный поток ждет завершения обоих потоков с помощью метода `join()`, прежде чем вывести "Main thread finished".


Конечно! Вот ещё несколько примеров задач на тему многозадачности в Java, которые интервьюеры могут использовать, чтобы проверить ваше понимание работы с потоками.

### Задача 6: Пример с `volatile` переменной
```java
public class Main {
    private static volatile boolean flag = false;

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            flag = true;
            System.out.println("t1 finished");
        });

        Thread t2 = new Thread(() -> {
            while (!flag) {
                // Просто ждем изменения флага
            }
            System.out.println("t2 finished");
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Main finished");
    }
}
```

**Вопрос**: Какой результат будет выведен в консоль?

**Ответ**:
```
t1 finished
t2 finished
Main finished
```
Поток `t2` будет постоянно проверять значение переменной `flag`. Переменная `flag` объявлена как `volatile`, что означает, что изменения этой переменной видны всем потокам немедленно. После того как поток `t1` изменит значение флага на `true`, поток `t2` завершит свою работу и выведет "t2 finished".

---

### Задача 7: Пример с гонкой потоков
```java
public class Main {
    private static int counter = 0;

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter++;
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                counter++;
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final counter: " + counter);
    }
}
```

**Вопрос**: Какой результат будет выведен в консоль?

**Ответ**:
Результат может быть любым, но он, скорее всего, будет меньше 2000, например:
```
Final counter: 1997
```
Поскольку переменная `counter` не синхронизирована, несколько потоков могут одновременно модифицировать её, что приведет к гонке данных. При таком параллельном изменении переменной `counter` результат может быть неожиданным и отличается от 2000, так как обновления не происходят атомарно.

---

### Задача 8: Использование `ReentrantLock`
```java
import java.util.concurrent.locks.ReentrantLock;

public class Main {
    private static int counter = 0;
    private static final ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                lock.lock();
                try {
                    counter++;
                } finally {
                    lock.unlock();
                }
            }
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) {
                lock.lock();
                try {
                    counter++;
                } finally {
                    lock.unlock();
                }
            }
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Final counter: " + counter);
    }
}
```

**Вопрос**: Какой результат будет выведен в консоль и почему?

**Ответ**:
```
Final counter: 2000
```
Потоки `t1` и `t2` используют `ReentrantLock` для синхронизации доступа к переменной `counter`. Благодаря блокировке, каждый поток будет получать доступ к переменной поочередно, предотвращая гонки данных. Таким образом, значение `counter` корректно увеличивается до 2000.

---

### Задача 9: Использование `ExecutorService` с `Callable`
```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Callable<Integer> task1 = () -> {
            Thread.sleep(1000);
            return 100;
        };

        Callable<Integer> task2 = () -> {
            Thread.sleep(500);
            return 200;
        };

        Future<Integer> result1 = executor.submit(task1);
        Future<Integer> result2 = executor.submit(task2);

        System.out.println("Task 1 result: " + result1.get());
        System.out.println("Task 2 result: " + result2.get());

        executor.shutdown();
    }
}
```

**Вопрос**: Какой будет вывод программы и почему?

**Ответ**:
```
Task 2 result: 200
Task 1 result: 100
```
Потоки выполняются параллельно, и задача `task2` завершится быстрее, потому что она засыпает на меньшее время (500 миллисекунд). Метод `get()` блокирует основной поток до получения результата, поэтому вывод будет в порядке завершения задач. Результаты будут выведены в том порядке, в котором задачи завершатся.

---

### Задача 10: Использование `CountDownLatch`
```java
import java.util.concurrent.CountDownLatch;

public class Main {
    public static void main(String[] args) throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(2);

        Thread t1 = new Thread(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 1 finished");
            latch.countDown();
        });

        Thread t2 = new Thread(() -> {
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 2 finished");
            latch.countDown();
        });

        t1.start();
        t2.start();

        latch.await();  // Ожидаем, пока оба потока завершатся
        System.out.println("Both threads finished, main thread proceeds");
    }
}
```

**Вопрос**: Какой будет результат выполнения программы?

**Ответ**:
```
Thread 2 finished
Thread 1 finished
Both threads finished, main thread proceeds
```
`CountDownLatch` ожидает, пока оба потока не уменьшат счетчик до 0 с помощью метода `countDown()`. Поток `main` будет заблокирован на методе `await()` до тех пор, пока оба потока не завершат свою работу, после чего он продолжит выполнение.

---

### Задача 11: Пример с `Thread.sleep()`
```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        Thread t1 = new Thread(() -> {
            System.out.println("Thread 1 start");
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 1 end");
        });

        Thread t2 = new Thread(() -> {
            System.out.println("Thread 2 start");
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread 2 end");
        });

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Main thread finished");
    }
}
```

**Вопрос**: Какой будет вывод в консоль?

**Ответ**:
```
Thread 1 start
Thread 2 start
Thread 2 end
Thread 1 end
Main thread finished
```
Потоки выполняются параллельно, но так как поток `t2` засыпает на 1 секунду, он завершится первым. После завершения потоков, основной поток завершит выполнение и выведет "Main thread finished".

--- 

Эти примеры проверяют различные аспекты работы с многозадачностью в Java, включая синхронизацию, управление потоками, обработку исключений и использование стандартных библиотек.

