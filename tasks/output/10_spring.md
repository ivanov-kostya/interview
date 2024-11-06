Примеры задач на тему Spring, где интервьюер может дать код и попросить объяснить, что будет выведено в консоль, могут включать различные аспекты фреймворка: конфигурация Spring, управление зависимостями, жизненный цикл бинов, аннотации и т.д. Вот несколько примеров:

### Пример 1: Жизненный цикл бинов

```java
import org.springframework.beans.factory.DisposableBean;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.stereotype.Component;

@Component
public class MyBean implements InitializingBean, DisposableBean {

    public MyBean() {
        System.out.println("Конструктор MyBean");
    }

    @Override
    public void afterPropertiesSet() throws Exception {
        System.out.println("Метод afterPropertiesSet()");
    }

    @Override
    public void destroy() throws Exception {
        System.out.println("Метод destroy()");
    }
}

public class SpringLifecycleDemo {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyBean.class);
        ((AnnotationConfigApplicationContext) context).close();
    }
}
```

**Ответ:**
```
Конструктор MyBean
Метод afterPropertiesSet()
Метод destroy()
```

**Пояснение:**
- Конструктор `MyBean` вызывается при создании бина.
- `afterPropertiesSet()` вызывается после того, как все свойства бина были установлены.
- `destroy()` вызывается при закрытии контекста Spring (вызов `((AnnotationConfigApplicationContext) context).close();`).

### Пример 2: Использование аннотации `@PostConstruct` и `@PreDestroy`

```java
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    public MyBean() {
        System.out.println("Конструктор MyBean");
    }

    @PostConstruct
    public void init() {
        System.out.println("Метод init() после создания бина");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Метод destroy() перед удалением бина");
    }
}

public class SpringPostConstructPreDestroyDemo {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyBean.class);
        ((AnnotationConfigApplicationContext) context).close();
    }
}
```

**Ответ:**
```
Конструктор MyBean
Метод init() после создания бина
Метод destroy() перед удалением бина
```

**Пояснение:**
- Конструктор вызывается при создании бина.
- `@PostConstruct` помечает метод, который вызывается после создания бина.
- `@PreDestroy` помечает метод, который вызывается перед уничтожением бина.

### Пример 3: Инъекция зависимостей

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.stereotype.Component;

@Component
class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

@Component
class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
        System.out.println("Car constructor called");
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}

public class SpringDIExample {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(Car.class, Engine.class);
        Car car = context.getBean(Car.class);
        car.drive();
    }
}
```

**Ответ:**
```
Car constructor called
Engine started
Car is driving
```

**Пояснение:**
- Spring автоматически инжектирует зависимость `Engine` в конструктор `Car`, вызывая конструктор `Car`.
- Метод `engine.start()` запускает двигатель, и затем выводится сообщение о том, что машина едет.

### Пример 4: Использование аннотации `@Value` для инъекции значений

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    @Value("${message:Default message}")
    private String message;

    public void printMessage() {
        System.out.println(message);
    }
}

public class SpringValueAnnotationDemo {
    public static void main(String[] args) {
        System.setProperty("message", "Hello, Spring!");
        ApplicationContext context = new AnnotationConfigApplicationContext(MyBean.class);
        MyBean myBean = context.getBean(MyBean.class);
        myBean.printMessage();
    }
}
```

**Ответ:**
```
Hello, Spring!
```

**Пояснение:**
- Аннотация `@Value` используется для инъекции значений в поля.
- Значение свойства `message` устанавливается через `System.setProperty()`, и это значение будет инжектировано в поле `message`.

### Пример 5: Проблемы с циклическими зависимостями

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.stereotype.Component;

@Component
class A {
    private final B b;

    @Autowired
    public A(B b) {
        this.b = b;
        System.out.println("A created");
    }
}

@Component
class B {
    private final A a;

    @Autowired
    public B(A a) {
        this.a = a;
        System.out.println("B created");
    }
}

public class CircularDependencyDemo {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(A.class, B.class);
    }
}
```

**Ответ:**
```
Exception in thread "main" org.springframework.beans.factory.BeanCurrentlyInCreationException: Error creating bean with name 'a' defined in class path resource
```

**Пояснение:**
- В данном примере создаются два бина с циклической зависимостью: `A` зависит от `B`, а `B` зависит от `A`. Это вызывает ошибку в Spring, так как Spring не может разрешить такие зависимости.

### Пример 6: @Scope и синглтон

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;

@Component
@Scope("prototype")
class MyBean {
    public MyBean() {
        System.out.println("MyBean created");
    }
}

public class ScopeExample {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(MyBean.class);
        MyBean bean1 = context.getBean(MyBean.class);
        MyBean bean2 = context.getBean(MyBean.class);
    }
}
```

**Ответ:**
```
MyBean created
MyBean created
```

**Пояснение:**
- Аннотация `@Scope("prototype")` указывает, что Spring должен создавать новый экземпляр бина каждый раз при вызове `getBean()`. Поэтому оба вызова `getBean()` создают разные экземпляры, и для каждого из них выводится сообщение о создании нового бина.

Эти примеры помогают интервьюеру проверить знания кандидата о механизмах работы Spring, таких как инъекция зависимостей, жизненный цикл бинов и обработка аннотаций.


