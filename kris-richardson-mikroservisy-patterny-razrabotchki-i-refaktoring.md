# Крис Ричардсон Микросервисы Паттерны разработки и рефакторинг

## Монолит или Микросервисы

### Монолитная система

Преимущества:  
1. Простота разработки и развертывания, так как все компоненты упакованы вместе.  
2. Эффективная межмодульная коммуникация, поскольку компоненты используют общее пространство памяти.  
3. Единообразное использование вычислительных ресурсов для всего приложения.  
4. Более простое управление транзакциями и согласованностью данных.  
5. Легкая масштабируемость путем добавления больше экземпляров приложения.

Недостатки:  
1. Жесткая связь между компонентами усложняет обновление или замену отдельных частей.  
2. Сложность внесения изменений, так как любое обновление требует перезапуска всего приложения.  
3. Увеличение размера кодовой базы с ростом функциональности усложняет управление.  
4. Сложность масштабирования отдельных компонентов независимо.  
5. Риск полного отказа системы из-за единой точки отказа.  
6. Сложность использования различных технологических стеков для разных компонентов.

### Микросервисная архитектура:

Преимущества:   
1. Децентрализованное управление и независимое развертывание сервисов.  
2. Возможность масштабирования отдельных сервисов по требованию.  
3. Облегчение внедрения новых технологий для отдельных сервисов.   
4. Повышенная отказоустойчивость за счет изолированности сервисов.  
5. Улучшенная модульность и гибкость за счет слабой связанности компонентов.  
6. Более простое тестирование и развертывание отдельных сервисов.

Недостатки:  
1. Усложненная разработка из-за распределенной природы системы.  
2. Увеличенная сложность коммуникации между сервисами и обработки ошибок.  
3. Потенциальные проблемы с согласованностью данных между сервисами.  
4. Повышенная операционная нагрузка из-за большего количества сервисов.   
5. Возможные трудности с распределенным мониторингом и управлением.  
6. Дополнительная сложность кроссплатформенного тестирования и развертывания.

Выбор архитектуры зависит от конкретных требований проекта, масштаба системы, команды разработчиков и др. факторов. Монолиты проще на начальных этапах, микросервисы обеспечивают большую гибкость и отказоустойчивость для крупных и быстрорастущих систем.

## Стратегия декомпозиции

Стратегия декомпозиции - это ключевой аспект при переходе от монолитной системы к микросервисной архитектуре. Она определяет, как большая монолитная система будет разделена на отдельные микросервисы.

Успешная стратегия декомпозиции должна учитывать следующие принципы:

1. Выделение сервисов по бизнес-возможностям (bounded context) - каждый микросервис должен охватывать определенную бизнес-область или функцию приложения.

2. Слабая связанность - микросервисы должны быть максимально независимыми и избегать сильных связей с другими сервисами. Это обеспечивает гибкость и упрощает изменения. Взаимодействие между микросервисами происходит через хорошо определенные API (часто RESTful) или асинхронные протоколы обмена сообщениями (очереди, брокеры сообщений). Это создает слабосвязанный, более универсальный способ интеграции. 

3. Изолированность данных - каждый микросервис должен иметь свою собственную модель данных и не разделять данные с другими сервисами напрямую.

4. Самодостаточность - микросервисы должны быть автономными, с собственными стеками технологий, ресурсами и возможностями развертывания.

5. Определение четких граней сервиса (service boundaries) - четкие контракты, определяющие обязанности и интерфейсы взаимодействия каждого микросервиса.

Популярные стратегии декомпозиции включают разделение по бизнес-объектам, функциям, вертикальное или горизонтальное разделение архитектуры.

Теперь определение микросервисной архитектуры:

Микросервисная архитектура - это архитектурный стиль, в котором приложение строится как набор небольших сервисов, каждый со своими процессами и способами взаимодействия через легкие механизмы, часто на основе HTTP-ресурсов. Эти сервисы построены вокруг бизнес-возможностей и могут быть самостоятельно разработаны, развернуты и масштабироваться независимо от остальной части системы.

Ключевыми характеристиками микросервисной архитектуры являются:

1. Сервис-ориентированная архитектура  
2. Децентрализованное управление данными  
3. Независимое развертывание  
4. Облегчение компонентного масштабирования  
5. Децентрализация управления  
6. Высокая степень автоматизации процессов развертывания и инфраструктурных операций

Микросервисная архитектура направлена на повышение модульности, способствует параллельной разработке, упрощая внедрение новых технологий и повышая устойчивость к сбоям за счет изолированности компонентов.

## Межпроцессное взаимодействие в микросервисной архитектуре

Межпроцессное взаимодействие является ключевым аспектом микросервисной архитектуры, поскольку микросервисы должны взаимодействовать друг с другом для выполнения полного набора функций приложения. Давайте подробно рассмотрим различные стратегии и модели межпроцессного взаимодействия.

Стили взаимодействия:

1. Описание API в микросервисной архитектуре: Каждый микросервис должен иметь четко определенный API (Application Programming Interface), который описывает его функциональность и способы взаимодействия. Это могут быть REST API, gRPC, SOAP или другие протоколы.  
2. Развивающиеся API: API микросервисов должны быть спроектированы для эволюционирования без нарушения обратной совместимости, используя такие методы, как управление версиями, поддержка старых версий и согласованные контракты.  
3. Форматы сообщений: Для обмена данными между микросервисами используются различные форматы сообщений, такие как JSON, XML, Protocol Buffers, Apache Avro и др.

Взаимодействие на основе удаленного вызова процедур:

1. Использование REST: Широко используется архитектурный стиль REST (Representational State Transfer) с HTTP-методами для создания, чтения, обновления и удаления ресурсов. REST API обеспечивают простоту, масштабируемость и кэширование.  
2. Использование gRPC: gRPC - современная высокопроизводительная RPC-система открытого происхождения, использующая HTTP/2, Protocol Buffers и эффективное двоичное кодирование. Популярна для внутренних микросервисных вызовов.  
3. Работа в условиях частичного отказа с применением шаблона «Предохранитель»: Шаблоны, такие как "Предохранитель", помогают обрабатывать сбои при вызовах между микросервисами, предотвращая каскадные сбои.  
4. Обнаружение сервисов: Используются системы обнаружения сервисов, такие как Consul, Zookeeper или Kubernetes DNS, чтобы микросервисы могли находить друг друга в динамической средеразвертывания.

Взаимодействие с помощью асинхронного обмена сообщениями:

1. Использование асинхронного обмена сообщениями: Микросервисы могут взаимодействовать путем посылки и получения сообщений через брокеры сообщений (RabbitMQ, Apache Kafka, Azure Service Bus и др.). Это обеспечивает отказоустойчивость, рассоединение и буферизацию.  
2. Стили асинхронного взаимодействия: Включают многоточечную рассылку сообщений, публикацию/подписку, очереди сообщений, потоки событий.  
3. Хореография и оркестрация: Микросервисы могут координировать свои действия через асинхронные сообщения, используя хореографию (прямое взаимодействие между сервисами) или оркестрацию (центральный менеджер маршрутизирует сообщения).

Эти стратегии межпроцессного взаимодействия позволяют микросервисам эффективно интегрироваться, гарантируя автономность, масштабируемость и устойчивость к сбоям. Правильный выбор зависит от конкретных требований приложения, нагрузки и латентности.

### Обнаружение микросервисов (Service Discovery)

Обнаружение микросервисов (Service Discovery) является важным аспектом в микросервисной архитектуре, поскольку микросервисы развертываются динамически и их местоположения (IP-адреса и порты) могут меняться в зависимости от масштабирования, отказов и других факторов времени выполнения. Цель обнаружения сервисов - обеспечить способ для микросервисов находить друг друга и взаимодействовать без жесткой привязки к локальным адресам.

Вот основные причины необходимости обнаружения сервисов:

1. Динамические IP-адреса и порты

Микросервисы часто развертываются с динамически назначаемыми IP-адресами и портами из пула ресурсов. Эти адреса не известны заранее другим сервисам.

2. Масштабирование экземпляров  

Количество экземпляров сервиса может динамически меняться для соответствия нагрузке. Клиенты должны знать все активные экземпляры для балансировки нагрузки.

3. Отказоустойчивость

При отказе экземпляра клиенты должны быть перенаправлены к здоровым экземплярам того же сервиса.

4. Повторное использование микросервисов

Микросервисы могут быть повторно использованы в разных приложениях. Жесткая фиксация адресов затруднила бы повторное использование.

5. Упрощение развертывания

Указывать фиксированные адреса каждого сервиса во время развертывания было бы сложно и подвержено ошибкам.

Реализация обнаружения сервисов обычно выполняется с помощью следующих компонентов:

1. Реестр сервисов

Центральный компонент, в котором регистрируются все развернутые экземпляры микросервисов со своими адресами и метаданными. Примеры: Consul, Zookeeper, etcd.

2. Клиент обнаружения сервисов

Библиотека, которую используют микросервисы для регистрации/получения адресов из реестра сервисов.

3. Сторонние сервисы 

Компоненты, уведомляющие реестр об изменениях экземпляров (появление, исчезновение, изменение здоровья).

4. Балансировка нагрузки

Клиенты микросервисов используют список адресов для распределения нагрузки между экземплярами.

Обнаружение сервисов является критически важным для построения истинно децентрализованных, распределенных, масштабируемых и отказоустойчивых микросервисных систем, избегая жестких зависимостей от фиксированных адресов.

### Хореография и оркестрация

Хореография и оркестрация - это две основные модели, используемые для координации и управления взаимодействием между несколькими микросервисами при выполнении составной бизнес-операции или конвейера обработки.

Хореография:  
В модели хореографии каждый микросервис принимает решения самостоятельно и взаимодействует с другими сервисами через асинхронный обмен сообщениями или событиями. Нет центрального координатора - вместо этого каждый сервис реагирует на события от других сервисов в соответствии с заранее определенными правилами и последовательностями.

Применяется: Хореография хорошо подходит для относительно простых сценариев с небольшим количеством участвующих микросервисов и предсказуемой логикой. Она обеспечивает высокую децентрализацию и автономность.

Плюсы:  
- Высокая степень распределения и отказоустойчивости  
- Отсутствие единой точки отказа   
- Большая гибкость и расширяемость  
- Каждый сервис имеет четкую область ответственности

Минусы:   
- Сложность отслеживания общего состояния системы  
- Трудность внесения изменений в процессы  
- При ошибках возможен неконтролируемый каскад событий  
- Сложная отладка и тестирование

Оркестрация:   
При оркестрации существует центральный компонент (оркестратор), который координирует и управляет выполнением составной операции, запуская необходимые микросервисы в правильном порядке, собирая результаты и обрабатывая ошибки.

Применяется: Оркестрация хорошо подходит для более сложных, длительных операций с четко определенными последовательностями и правилами, где требуется центральное управление.

Плюсы:  
- Централизованная логика управления потоком  
- Более простой контроль и мониторинг состояния системы    
- Более легкая отладка и изменения последовательностей  
- Централизованная обработка ошибок и компенсация

Минусы:  
- Единая точка отказа (оркестратор)  
- Потенциальное узкое место производительности  
- Меньшая автономия микросервисов  
- Потенциальная сложность масштабирования оркестратора

Выбор между хореографией и оркестрацией зависит от конкретных требований к приложению, степени сложности сценариев, необходимой гибкости и предпочтений разработчиков. Также возможны гибридные подходы, сочетающие оба стиля.

### Шаблон "Предохранитель" (Circuit Breaker)

Шаблон "Предохранитель" (Circuit Breaker) является важным шаблоном проектирования для обеспечения отказоустойчивости и устойчивости в распределенных системах, таких как микросервисная архитектура.

Суть заключается в том, чтобы предотвратить каскадные сбои, когда один микросервис пытается повторно вызвать другой сбойный сервис, потенциально вызывая его дальнейшую перегрузку. Вместо этого предохранитель обнаруживает отказы и временно блокирует дальнейшие вызовы к сбойному сервису на определенный период времени.

Принцип работы:

1. Закрытый предохранитель  
   Изначально предохранитель находится в закрытом состоянии, что позволяет операциям свободно проходить к сервису.

2. Открытый предохранитель  
   Если количество сбоев превышает заданный порог в течение определенного периода времени, предохранитель переключается в открытое состояние. Теперь все последующие вызовы немедленно отклоняются, не достигая проблемного сервиса.

3. Период полураспада  
   После периода времени в открытом состоянии, предохранитель переходит в состояние полураспада, при котором он начинает пробовать пропускать ограниченное количество вызовов к сервису, чтобы проверить его восстановление.  
     
4. Восстановление  
Если тестовые вызовы успешны, предохранитель переходит обратно в закрытое состояние, разрешая все операции. В противном случае он остается открытым.

Преимущества использования шаблона Предохранитель:

- Предотвращает каскадные отказы путем временного прерывания вызовов к проблемному сервису.  
- Улучшает отказоустойчивость всей системы, помогая изолировать и обходить сбои.  
- Дает сбойному сервису время на восстановление и не перегружает его вызовами во время проблем.  
- Позволяет реализовать стратегии деградации обслуживания для клиентов при сбоях.

Однако предохранитель также вводит дополнительную сложность и требует настройки параметров срабатывания, таких как порог сбоев, временные окна и стратегии восстановления. Но в целом этот шаблон является важной практикой для повышения устойчивости распределенных систем к частичным сбоям.

## Управление транзакциями с помощью повествований

Управление транзакциями является одной из ключевых проблем в микросервисной архитектуре, поскольку данные распределены между разными изолированными микросервисами, каждый из которых управляет своей собственной моделью данных.

Микросервисная архитектура и необходимость в распределенных транзакциях:  
В монолитных приложениях транзакции обычно выполняются в рамках одной базы данных, используя ACID-свойства для обеспечения согласованности. Однако в микросервисной архитектуре бизнес-операция часто требует изменения данных в нескольких базах данных, управляемых разными микросервисами. Это требует распределенных транзакций для сохранения целостности данных.

Проблемы с распределенными транзакциями:  
- Производительность: Распределенные транзакции, такие как двухфазная фиксация, медленны и дороги из-за большого количества сетевых вызовов.  
- Доступность: Блокировка ресурсов в ходе транзакций влияет на доступность и масштабируемость.  
- Надежность: Частичные сбои в одном микросервисе могут помешать успешному завершению глобальной транзакции.

Использование шаблона "Повествование" для сохранения согласованности данных:  
Шаблон "Повествование" (Saga) предоставляет альтернативный способ управления распределенными транзакциями при сохранении согласованности данных в микросервисной архитектуре. Он разбивает операцию на серию локальных транзакций, каждая из которых обновляет данные в одном микросервисе.

Координация повествований:

Повествования, основанные на хореографии:  
Каждый сервис отвечает за публикацию событий, описывающих его локальные транзакции. Другие сервисы подписываются на эти события и выполняют соответствующие локальные транзакции в правильном порядке для поддержания согласованности.

Повествования на основе оркестрации:  
Центральный оркестратор отвечает за координацию последовательности операций в повествовании. Он отправляет команды соответствующим микросервисам для выполнения локальных транзакций и отслеживает общее состояние.

Что делать с недостаточной изолированностью:  
Иногда бизнес-операции требуют доступа к данным в разных микросервисах в рамках одной транзакции, нарушая изоляцию микросервисов. Для таких случаев можно использовать дополнительные шаблоны, такие как Шаблон "Оборотень" или "Открытая сессия".

Архитектура сервиса Order и повествования Create Order:  
Рассмотрим пример, где при создании заказа необходимо согласовать операции в сервисах Order, Customer, Product и других. Повествование Create Order координирует серию локальных транзакций, обновляющих состояния в каждом сервисе, сохраняя согласованность.

Правильное управление транзакциями с помощью повествований является критически важным для поддержания согласованности данных в микросервисной архитектуре без создания узких мест производительности и доступности. Выбор между хореографией и оркестрацией зависит от конкретных требований системы.

### Шаблон Повествование

Шаблон Повествование (Saga) - это способ управления распределенными транзакциями и обеспечения согласованности данных в микросервисной архитектуре, избегая недостатков классических распределенных транзакций.

Его необходимо применять, когда бизнес-операция требует изменения данных в нескольких микросервисах, обновляя их состояния для достижения согласованности во всей распределенной системе.

Основная идея шаблона заключается в том, чтобы разбить глобальную операцию на последовательность локальных транзакций в разных микросервисах. Повествование гарантирует, что либо все локальные транзакции будут успешно выполнены, либо при сбое будет выполнена компенсирующая операция для отмены уже произведенных изменений.

Использование повествований имеет следующие преимущества:

1. Избегание распределенных блокировок и сохранение производительности/доступности.  
2. Повышенная устойчивость к сбоям, поскольку сбой в одном сервисе не прерывает всю операцию.  
3. Поддержка отложенной согласованности данных вместо жесткой согласованности.  
4. Соответствие принципам микросервисной архитектуры за счет автономии микросервисов.

Однако есть и некоторые нюансы:

1. Управление конечными последовательностями операций может стать сложным.  
2. Требуется реализовать логику компенсации и обработки ошибок для каждой локальной транзакции.  
3. Необходимость отслеживать завершение каждого шага повествования для обеспечения согласованности.  
4. Потенциальная необходимость в централизованном мониторинге состояний повествований.

Существуют два основных подхода реализации повествований:

1. Хореография: каждый микросервис реагирует на события, публикуемые другими сервисами, и выполняет соответствующие локальные операции.

2. Оркестрация: централизованный оркестратор управляет последовательностью шагов повествования и отправляет команды соответствующим микросервисам.  

Оркестрация обеспечивает лучший центральный контроль, в то время как хореография обеспечивает большую распределенность и автономию, но усложняет отслеживание состояний.

В целом, шаблон Повествование является рекомендуемой практикой для управления распределенными транзакциями в микросервисной архитектуре, хотя и требует дополнительной реализации и осторожного проектирования для обеспечения согласованности данных.

### Пример шаблона Повествования

Конечно, рассмотрим пример использования шаблона Повествование для управления распределенной транзакцией создания заказа в системе электронной коммерции с микросервисной архитектурой.

Допустим, у нас есть следующие микросервисы:

1. Order Service - управляет заказами  
2. Product Service - управляет информацией о товарах  
3. Inventory Service - управляет складскими запасами   
4. Payment Service - обрабатывает платежи  
5. Shipping Service - управляет доставкой

Шаги повествования для создания заказа могут выглядеть следующим образом:

1. Клиент отправляет запрос на создание заказа в Order Service  
2. Order Service создает новый заказ и публикует событие OrderCreated  
3. Product Service получает OrderCreated и утверждает доступность запрошенных товаров   
4. Inventory Service получает OrderCreated и резервирует запасы для заказа  
5. Payment Service получает OrderCreated и инициирует платеж  
6. Если платеж успешен, публикуется событие PaymentConfirmed  
7. Shipping Service получает PaymentConfirmed и планирует доставку заказа  
8. Order Service получает PaymentConfirmed и обновляет статус заказа до "Принят"

Если на любом шаге произойдет сбой, повествование инициирует компенсирующие операции для отката изменений:

1. Если резервирование запасов не удалось, Inventory Service публикует ReservationFailed  
2. Order Service получает ReservationFailed и отменяет заказ  
3. Product Service и Payment Service получают отмену и выполняют соответствующие откаты

Таким образом, шаблон Повествование гарантирует, что либо все шаги транзакции будут успешно завершены во всех микросервисах, либо все изменения будут компенсированы, сохраняя согласованность системы.

В этом примере используется хореография, где микросервисы взаимодействуют путем публикации и обработки событий. Также возможен вариант с оркестрацией, где отдельный сервис-оркестратор управляет последовательностью шагов повествования.

Ключевыми моментами являются атомарность локальных операций в микросервисах и отслеживание общего состояния повествования для обеспечения согласованности.

## Проектирование бизнес-логики в микросервисной архитектуре

Давайте подробно рассмотрим проектирование бизнес-логики в микросервисной архитектуре и связанные с этим шаблоны и практики.

Шаблоны организации бизнес-логики:

1. Проектирование с помощью шаблона "Сценарий транзакции":  
В этом подходе бизнес-логика организована вокруг последовательностей операций, выполняемых для достижения определенной бизнес-цели, например, создания заказа. Операции инкапсулируются в классы "сценариев транзакций".

2. Проектирование с помощью шаблона "Доменная модель":   
Этот подход основан на принципах предметно-ориентированного проектирования (DDD). Бизнес-логика организована вокруг концепций предметной области, таких как сущности, агрегаты и домены, инкапсулируя поведение и данные вместе.

Проектирование доменной модели с помощью шаблона "Агрегат" из DDD:

Агрегат - это кластер связанных объектов, которые обрабатываются как единое целое в операциях. Граница агрегата обеспечивает целостность инвариантов и бизнес-правил.

- Проблемы с расплывчатыми границами: Нечеткие границы могут привести к распространению изменений и нарушению инкапсуляции.

- Агрегаты имеют четкие границы: Каждый агрегат имеет корневой объект (сущность) и четко определенные границы.

- Правила для агрегатов: Внешние объекты держат ссылки только на корневую сущность, операции применяются к агрегату как единому целому.

- Размеры агрегатов: Агрегаты должны быть достаточно маленькими, чтобы быть четко определенными, но не слишком мелкими, чтобы не потерять смысл.

Публикация доменных событий:

- Зачем публиковать события: События уведомляют другие части системы об изменениях состояния и способствуют слабой связанности.

- Доменное событие: Объект, представляющий что-то, что произошло в домене, которое может быть важно для других частей системы.

- Обогащение события: События могут содержать всю необходимую информацию для обработки, без необходимости дополнительных запросов.

- Генерация и публикация событий: События генерируются в рамках транзакций в агрегатах и публикуются в шине событий.

- Потребление событий: Другие компоненты подписываются на события и реагируют соответствующим образом.

Примеры бизнес-логики:

1. Kitchen Service - Агрегат Ticket  
   - Инкапсулирует логику создания, назначения и обновления статусов заказов  
   - Публикует события TicketCreated, TicketAssigned и др.

2. Order Service - Агрегат Order   
   - Отвечает за создание, изменение и отслеживание заказов  
   - Класс OrderService оркестрирует операции над агрегатами Order и другими

Правильное проектирование бизнес-логики с использованием шаблонов DDD, таких как Агрегаты и События, способствует модульности, согласованности и расширяемости в микросервисной архитектуре.

### Шаблон Сценарий Транзакций

Шаблон "Сценарий транзакции" (Transaction Script) - один из способов организации бизнес-логики в микросервисной архитектуре. Его основная идея заключается в инкапсуляции последовательностей операций, необходимых для выполнения определенной бизнес-задачи или использования, в отдельные классы, называемые сценариями транзакций.

Принцип работы:

1. Определение сценариев  
Бизнес-процессы разбиваются на отдельные сценарии, например, "Создание заказа", "Выполнение платежа" и т.д.

2. Классы сценариев  
Для каждого сценария создается отдельный класс, инкапсулирующий последовательность шагов для выполнения этого сценария.

3. Процедурная логика  
Внутри класса сценария бизнес-логика реализуется в виде процедурного кода, применяющего изменения к соответствующим объектам данных или вызывающего другие сервисы.

4. Отсутствие состояния  
Классы сценариев, как правило, не содержат состояния, они выполняют набор команд над входными данными.

5. Использование репозиториев  
Для доступа к данным классы сценариев используют репозитории данных, инкапсулирующие детали хранения.

Преимущества:  
- Простота понимания и реализации для разработчиков  
- Четкое разделение обязанностей между сценариями  
- Хорошо подходит для простых последовательных операций

Недостатки:  
- Процедурная природа может привести к трудноподдерживаемому коду  
- Сложность при наличии сложных бизнес-правил и инвариантов  
- Отсутствие инкапсуляции поведения вместе с данными  
- Потенциальные проблемы с параллелизмом

Шаблон "Сценарий транзакции" хорошо подходит для приложений с относительно простыми, линейными бизнес-операциями. Однако для более сложных доменов с богатым поведением часто рекомендуется использовать альтернативные подходы, такие как шаблон "Доменная модель" основанный на принципах предметно-ориентированного проектирования (DDD).

## Разработка бизнес-логики с порождением событий

Разработка бизнес-логики с порождением событий (Event Sourcing) - это архитектурный паттерн, в котором изменения состояния приложения записываются в виде последовательности событий. Вместо того, чтобы хранить текущее состояние объектов, хранится поток событий, которые привели к текущему состоянию. Этот подход помогает решить ряд проблем, возникающих при традиционном способе хранения данных.

Проблемы традиционного сохранения данных:  
- Трудности отслеживания изменений и восстановления прошлых состояний  
- Сложность реализации согласованности данных в распределенной системе  
- Необходимость создания сложных механизмов блокировки для предотвращения конкурентных обновлений

Обзор порождения событий:  
- События отражают изменения в модели данных приложения  
- Вместо обновления существующих данных, создается новое событие  
- События являются неизменяемыми и сохраняются в порядке их возникновения

Обработка конкурентных обновлений с помощью оптимистичного блокирования:  
- События используют оптимистичное блокирование для предотвращения конфликтов при параллельном обновлении   
- События публикуются только в случае успешной валидации текущей версии данных

Порождение и публикация событий:  
- События генерируются в результате действий пользователей или внешних систем  
- События публикуются в брокер сообщений или хранилище событий для их дальнейшей обработки

Улучшение производительности с помощью снимков:  
- Для восстановления текущего состояния может потребоваться воспроизведение большого количества событий  
- Снимки (Snapshots) кэшируют состояние на определенных точках для оптимизации 

Идемпотентная обработка сообщений:  
- События должны обрабатываться идемпотентно, чтобы повторная доставка не влияла на конечный результат

Развитие доменных событий:  
- Первоначально события отражают действия пользователей или внешних систем  
- По мере развития системы могут добавляться производные события для оптимизации

Преимущества порождения событий:  
- Полный аудит изменений и возможность воспроизведения прошлых состояний  
- Упрощение распределенной согласованности с использованием событий  
- Лучшая масштабируемость, так как сохранение событий является операцией добавления

Недостатки порождения событий:    
- Сложность первоначального внедрения в существующие приложения  
- Увеличение объема хранимых данных из-за накопления событий  
- Дополнительная нагрузка на производительность при публикации событий

Реализация хранилища событий:  
- Хранилище событий может быть реализовано с помощью различных решений, таких как брокеры сообщений, базы данных событий или обычные базы данных

Принцип работы хранилища событий Eventuate Local:  
- Eventuate Local - это фреймворк для реализации порождения событий и повествований в микросервисах  
- События записываются в локальные журналы транзакций БД каждого микросервиса  
- Распространение событий между микросервисами осуществляется через брокер сообщений

Клиентский фреймворк Eventuate для Java:  
- Eventuate предоставляет клиентские библиотеки для Java, упрощающие интеграцию порождения событий в приложениях  
- Включает поддержку повествований, репликации событий, снимков и идемпотентности

Совместное использование повествований и порождения событий:  
- Порождение событий часто используется совместно с шаблоном повествований для управления распределенными транзакциями

Реализация повествований на основе хореографии с помощью порождения событий:  
- Каждый микросервис публикует и реагирует на события, выполняя соответствующие локальные операции  
- Согласованность достигается путем соблюдения порядка и правил обработки событий

Создание повествования на основе оркестрации:  
- Центральный оркестратор управляет последовательностью шагов повествования  
- Оркестратор отправляет команды соответствующим микросервисам через события или сообщения

Реализация участника повествования на основе порождения событий:  
- Микросервис реагирует на события, инициирующие его участие в повествовании  
- Выполняет локальные операции, генерируя и публикуя события о своем прогрессе

Реализация оркестраторов повествований с помощью порождения событий:  
- Оркестратор публикует события, инициирующие повествования  
- Отслеживает прогресс повествования, обрабатывая события от участвующих микросервисов  
- Координирует дальнейшие шаги, публикуя новые события-команды

Порождение событий в сочетании с повествованиями предоставляет мощный подход к разработке распределенных систем с сохранением согласованности данных, аудита изменений и возможностью воспроизведения прошлых состояний.

## Реализация запросов в микросервисной архитектуре

Реализация запросов в микросервисной архитектуре - важный аспект, поскольку данные часто распределены между несколькими микросервисами. Рассмотрим два основных подхода: объединение API и шаблон CQRS (Command Query Responsibility Segregation).

Выполнение запросов с помощью объединения API:

Обзор шаблона "Объединение API":  
- Создается специальный микросервис (API Gateway), выполняющий роль входной точки  
- API Gateway отвечает за маршрутизацию запросов к соответствующим микросервисам  
- Полученные данные от разных микросервисов объединяются и возвращаются клиенту как единый ответ

Архитектурные проблемы объединения API:  
- API Gateway становится узким местом производительности и единой точкой отказа  
- Сложность в масштабировании API Gateway при высоких нагрузках  
- Возможная избыточность данных в ответах из-за недостатка согласованности

Преимущества объединения API:  
- Клиенты взаимодействуют с одной входной точкой, не зная о внутренней структуре системы  
- Упрощается разработка клиентов за счет скрытия распределенной природы системы  
- Централизованное управление маршрутизацией и другими межсервисными озаботами  

Недостатки объединения API:  
- Увеличение сложности и риск создания антипаттерна "распределенной монолитной системы"  
- Объединение API может стать узким местом при больших нагрузках  
- Потенциальные проблемы производительности из-за избыточных сетевых вызовов

CQRS - это архитектурный паттерн, при котором операции чтения данных (запросы) полностью отделены от операций записи/изменения данных (команды). Вместо использования единой модели данных, применяются две разные модели:

1. Модель записи (Write Model) - оптимизирована для операций обновления данных, таких как создание, обновление и удаление. Здесь основной акцент на согласованность данных и выполнение бизнес-правил.

2. Модель чтения (Read Model) - оптимизирована для эффективного извлечения данных для операций чтения/запросов. Эта модель часто денормализована для упрощения сложных запросов.

CQRS применяется в системах, где:  
- Существуют сложные запросы для чтения, требующие объединения данных из нескольких источников  
- Требуется высокая производительность для операций чтения при большом количестве запросов  
- Необходимо масштабировать операции чтения отдельно от операций записи

Основные преимущества:  
- Оптимизация моделей данных для разных нагрузок чтения/записи  
- Более простые и производительные запросы благодаря денормализации  
- Независимое масштабирование систем чтения и записи

Недостатки:  
- Увеличение сложности архитектуры с двумя разными моделями  
- Необходимость синхронизации данных между моделями записи и чтения  
- Может возникать задержка в согласованности данных между операциями записи и чтения

Пример использования CQRS:

Рассмотрим интернет-магазин. Модель записи может включать сущности Заказ, Товар, Клиент и бизнес-правила для создания и обработки заказов. 

Модель чтения может быть денормализованной представлением, объединяющим детали заказов, товаров и клиентов для эффективного выполнения запросов, таких как "Получить все заказы клиента с указанием товаров и статусов доставки".

Операции создания/обновления заказов будут применяться к модели записи, в то время как получение списка всех заказов будет использовать оптимизированную для чтения модель.

CQRS хорошо подходит для систем с интенсивными операциями чтения при необходимости сложных запросов, особенно когда требования к производительности чтения и записи сильно различаются.

И объединение API, и CQRS имеют свои плюсы и минусы. Выбор зависит от конкретных требований приложения, сложности запросов, нагрузки и важности согласованности. Объединение API может быть хорошим решением для простых случаев, а CQRS лучше подходит для более сложных сценариев чтения и высоких нагрузок.

### Проектирование CQRS-представлений

Рассмотрим более детально проектирование CQRS-представлений (Read Model) в микросервисной архитектуре.

Выбор хранилища данных для представления:  
- Представление данных оптимизировано для чтения, поэтому может использовать другое хранилище данных, отличное от хранилища модели записи  
- Популярные варианты: реляционные БД, NoSQL БД (MongoDB, Cassandra), кэши данных (Redis), поисковые движки (Elasticsearch)  
- Выбор зависит от характера данных, сложности запросов и требований к производительности

Структура модуля доступа к данным:  
- Модуль доступа к модели чтения часто отделен от модуля записи  
- Может содержать репозитории, сервисы для работы с представлениями и события/подписчики для синхронизации

Добавление и обновление CQRS-представлений:  
- При выполнении команд в модели записи публикуются события об изменениях данных  
- События подписываются на эти события и синхронизируют представления путем создания, обновления или удаления записей

Реализация CQRS с использованием AWS DynamoDB:  
- DynamoDB - это полностью управляемая NoSQL база данных AWS, подходящая для больших объемов данных и высокой производительности  
- Хорошо подходит для создания оптимизированных моделей чтения CQRS

Модуль OrderHistoryEventHandlers:   
- В качестве примера, рассмотрим модуль для получения истории заказов пользователя с помощью DynamoDB  
- Модуль OrderHistoryEventHandlers подписывается на события создания, изменения и отмены заказов из модели записи  
- При получении событий, создает/обновляет записи в DynamoDB для быстрого доступа к истории заказов

Моделирование данных и проектирование запросов с DynamoDB:  
- В DynamoDB данные моделируются с помощью таблиц, состоящих из элементов (записей)  
- Каждый элемент имеет обязательный ключ раздела (Partition Key) и необязательный ключ сортировки (Sort Key)  
- Структура данных и типы ключей определяют эффективность запросов  
- Например, для получения истории заказов пользователя:  
  - Partition Key - userId (для группировки заказов по пользователю)  
  - Sort Key - orderTimestamp (для сортировки заказов по времени)  
- Дополнительные атрибуты (столбцы) могут включать детали заказа, товары и статусы  
- Такая модель позволяет эффективно запрашивать историю заказов для конкретного пользователя

Преимущества использования DynamoDB для CQRS-представлений:  
- Высокая производительность благодаря горизонтальному масштабированию и кэшированию  
- Гибкое моделирование данных с возможностью денормализации  
- Интеграция с AWS Lambda и DynamoDB Streams для обработки событий

Таким образом, при проектировании CQRS необходимо тщательно спроектировать модель чтения, выбрать подходящее хранилище данных и определить способ синхронизации представлений на основе событий из модели записи. Правильное проектирование обеспечит производительные запросы чтения и масштабируемость в микросервисной архитектуре.

## Шаблоны внешних API

Книга подробно рассматривает шаблоны проектирования внешних API и паттерн API Gateway. Вот ключевые моменты:

Шаблоны внешних API:

Проблемы с проектированием внешних API:  
- Необходимость предоставления удобного интерфейса для разных типов клиентов (веб, мобильные и т.д.)  
- Обеспечение безопасности и контроля доступа  
- Версионирование и эволюция API без нарушения обратной совместимости  
- Производительность и масштабируемость

Проблемы для мобильных клиентов FTGO (системы заказа еды):  
- Эффективная доставка данных на устройства с ограниченными ресурсами  
- Минимизация количества раундтрипов  
- Оптимизация использования полосы пропускания

Проблемы для клиентов другого рода:  
- Агрегация данных из нескольких сервисов  
- Адаптация форматов данных и протоколов для разных клиентов

Шаблон API Gateway:

Обзор:  
- API Gateway - единая входная точка для клиентов  
- Инкапсулирует внутреннюю систему микросервисов от клиентов  
- Предоставляет единообразный API на стороне клиента

Преимущества:  
- Клиенты взаимодействуют только с API Gateway, не зная о внутренних микросервисах  
- Упрощает клиентский код  
- Обеспечивает дополнительные уровни безопасности, мониторинга, кэширования

Недостатки:   
- Потенциальная точка отказа  
- Необходимо масштабирования для высокой нагрузки  
- Увеличение сложности разработки

Netflix как пример:  
- Одним из первых внедрил API Gateway (Zuul)  
- Обеспечивает динамическое маршрутизирование, мониторинг, резилиентность и безопасность

Трудности проектирования:  
- Эффективная маршрутизация запросов к соответствующим микросервисам  
- Агрегация данных из нескольких источников  
- Обработка ошибок и время ожидания  
- Кэширование и производительность

Реализация:  
- Существуют решения с открытым кодом (Netflix Zuul, Nginx, Kong и др.)  
- Позволяют разработчикам сосредоточиться на бизнес-логике  
- Часто API Gateway реализуется как кластер для отказоустойчивости

Книга детально описывает эти паттерны с помощью примеров кода и архитектурных решений.
