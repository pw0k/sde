### OLTP (Online Transaction Processing) / OLAP(Online Analytical Processing)

OLTP **системы** характеризуются большим количеством коротких транзакций, требующих высокой скорости обработки и надежности. OLAP **системы** предназначены для выполнения сложных аналитических запросов на больших объемах данных. 

### Рассмотрим представителей  

| Параметр               | PostgreSQL (OLTP)                   | [[ClickHouse]] (OLAP)                   |
| ---------------------- | ----------------------------------- | --------------------------------------- |
| **Тип хранения**       | Строковое (Row-oriented)            | Колоночное (Column-oriented)            |
| **Транзакции**         | Полная поддержка ACID               | Ограниченная поддержка транзакций       |
| **Запросы**            | CRUD операции, сложные транзакции   | Агрегации, аналитические запросы        |
| **Производительность** | Оптимизирован для операций записи   | Оптимизирован для операций чтения       |
| **Масштабирование**    | Вертикальное и горизонтальное       | Горизонтальное (кластеризация)          |
| **Применение**         | Банковские системы, e-commerce, CRM | BI, аналитика, обработка больших данных |

### ACID (Atomicity, Consistency, Isolation, Durability)

- **Atomicity (Атомарность)**: Транзакция выполняется полностью или не выполняется вовсе. Если какая-либо часть транзакции не проходит, все изменения откатываются.
    
- **Consistency (Согласованность)**: Транзакция переводит базу данных из одного согласованного состояния в другое, соблюдая все определенные правила целостности данных (constraints). На практике этот пункт обычно реализуется именно в приложении 
    
- **Isolation (Изоляция)**: Одновременные транзакции выполняются так, будто они работают последовательно, не влияя друг на друга. Это достигается через уровни изоляции транзакций (MVCC + isolation level)
    
- **Durability (Долговечность)**: После подтверждения транзакции ее результаты сохраняются даже при сбое системы. Это обеспечивается механизмом WAL.

### WAL (Write-Ahead Logging)
- **Журналирование**: Все изменения данных сначала записываются в WAL, прежде чем быть применены к основным файлам данных.
- **Синхронизация на диск**: PostgreSQL гарантирует, что записи WAL сброшены на диск при подтверждении транзакции (`COMMIT`).

**Также WAL используется для восстановлении:**
- **Crash Recovery (Восстановление после сбоя)**: При перезапуске после сбоя PostgreSQL воспроизводит журнал WAL, чтобы восстановить базу данных до консистентного состояния.
- **Point-in-Time Recovery (Восстановление до точки во времени)**: Позволяет восстановить базу данных до конкретного момента времени, используя архивные журналы WAL.

### [Уровни изоляции транзакций в PostgreSQL](transaction)

#### Курсы PostgreSQL DBA от компании Postgres Professional
[https://www.youtube.com/watch?v=yevXLP2LA4Q](https://www.youtube.com/watch?v=yevXLP2LA4Q) - запись курса DBA1 для PostgreSQL версии 13
#### Курс молодого бойца от команды PostgreSQL DBA в Ozon

[https://www.youtube.com/playlist?list=PLCV5pSK-WYy85UmYUusizyZw0MUkYIWdH](https://www.youtube.com/playlist?list=PLCV5pSK-WYy85UmYUusizyZw0MUkYIWdH)
#### Про типичные ошибки и как делать не надо, про практики

[Типовые ошибки в приложениях, которые ведут к bloat в postgresq](http://backendconf.ru/2018/abstracts/3391)

[PostgreSQL. Плохие запросы, примеры и их поиск](https://www.highload.ru/spb/2020/abstracts/6683)

[Типичные ошибки при разработке приложений, работающих с PostgreSQL](https://www.highload.ru/spb/2019/abstracts/4833)

[Как устроить хайлоад на ровном месте](https://www.highload.ru/moscow/2018/abstracts/4181)

[Postgres Highload Checklist](https://www.highload.ru/spb/2019/abstracts/4433)

#### Про оптимизации запросов

[PostgreSQL Query Optimization Step by step techniques](https://www.postgresql.eu/events/nordicpgday2018/sessions/session/1858/slides/68/query-optimization-techniques_talk.pdf)

[Учим слона танцевать рок-н-ролл](https://pgday.ru/presentation/232/5964945ea4142.pdf)

[Неклассические приемы оптимизации запросов](https://pgday.ru/files/pgmaster14/max.boguk.query.optimization.pdf)

#### Про VACUUM

[https://www.interdb.jp/pg/pgsql06.html](https://www.interdb.jp/pg/pgsql06.html) — как работает VACUUM

[https://habr.com/ru/post/501516/](https://habr.com/ru/post/501516/) — еще про VACUUM
#### Книги

PostgreSQL 15 изнутри - [https://postgrespro.ru/education/books/internals](https://postgrespro.ru/education/books/internals)