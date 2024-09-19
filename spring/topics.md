# Темы по Spring для собеседований на позицию Senior Java Developer

## 1. Основы Spring Framework

- История и философия Spring Framework
- Инверсия управления (IoC) и внедрение зависимостей (DI)
- Контейнер Spring и его типы (BeanFactory, ApplicationContext)
- Жизненный цикл бинов Spring
- Конфигурация Spring (XML, аннотации, Java-конфигурация)
- Профили Spring
- Spring Expression Language (SpEL)

## 2. Аспектно-ориентированное программирование (AOP)

- Основные концепции AOP (аспект, совет, точка соединения, срез)
- Типы советов (before, after, around, after-returning, after-throwing)
- Реализация AOP в Spring (Spring AOP vs AspectJ)
- Использование аннотаций для AOP (@Aspect, @Pointcut, @Before, @After, и т.д.)
- Прокси в Spring AOP

## 3. Spring Core

- Аннотации Spring (@Component, @Service, @Repository, @Controller, @Configuration)
- Области видимости бинов (singleton, prototype, request, session, global session)
- Условные бины (@Conditional)
- События в Spring и обработка событий
- Интернационализация в Spring

## 4. Spring Boot

- Автоконфигурация Spring Boot
- Стартеры Spring Boot
- Конфигурация приложения (application.properties, application.yml)
- Профили в Spring Boot
- Встроенные серверы и развертывание Spring Boot приложений
- Actuator для мониторинга и управления
- Spring Boot DevTools

## 5. Spring MVC

- Архитектура Spring MVC
- DispatcherServlet и его роль
- Контроллеры и обработка HTTP-запросов
- Маппинг запросов (@RequestMapping, @GetMapping, @PostMapping и т.д.)
- Валидация форм и обработка ошибок
- Работа с представлениями (Thymeleaf, JSP)
- RESTful веб-сервисы с Spring MVC

## 6. Spring Data

- Spring Data JPA
- Репозитории и их типы (CrudRepository, JpaRepository, PagingAndSortingRepository)
- Запросы в Spring Data (Query Methods, @Query)
- Спецификации и QBE (Query by Example)
- Аудит с Spring Data
- Транзакции в Spring (@Transactional)

## 7. Spring Security

- Аутентификация и авторизация в Spring Security
- Конфигурация безопасности (Java config vs XML)
- UserDetailsService и его реализация
- Работа с JWT в Spring Security
- Защита от CSRF, XSS и других атак
- Методы обеспечения безопасности (@Secured, @PreAuthorize, @PostAuthorize)
- OAuth2 и OpenID Connect в Spring Security

## 8. Тестирование в Spring

- Модульное тестирование с использованием Spring Test
- Интеграционное тестирование Spring приложений
- Мокирование и стабирование в Spring
- Тестирование Spring Boot приложений
- Тестирование Spring MVC контроллеров
- Тестирование безопасности

## 9. Spring Cloud

- Микросервисная архитектура с Spring Cloud
- Service Discovery (Eureka)
- Конфигурационный сервер
- API Gateway (Spring Cloud Gateway)
- Circuit Breaker (Resilience4j)
- Distributed Tracing (Spring Cloud Sleuth, Zipkin)

## 10. Реактивное программирование в Spring

- Spring WebFlux
- Реактивные репозитории Spring Data
- Reactor Core
- Реактивная безопасность

## 11. Производительность и оптимизация

- Кэширование в Spring (@Cacheable, @CachePut, @CacheEvict)
- Оптимизация работы с базой данных
- Профилирование Spring приложений
- Масштабирование Spring приложений

## 12. Интеграция и взаимодействие

- Spring Integration
- Очереди сообщений (JMS, AMQP) с Spring
- Batch-обработка с Spring Batch
- WebSocket в Spring

## 13. Паттерны проектирования и лучшие практики

- Паттерны в контексте Spring (Singleton, Factory, Proxy, Template Method и др.)
- SOLID принципы в Spring приложениях
- Чистая архитектура и Spring
- Обработка исключений в Spring приложениях

## 14. Новые возможности и тренды

- Нативные образы с Spring Native
- Реактивное программирование и Spring
- Kotlin и Spring
- Spring для облачных платформ (Spring Cloud)
