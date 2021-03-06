## ACID 
Atomicity - атомарность, Consistency - консистентность, Isolation - изолированность, Durability - стойкость.

Атомарность гарантирует, что никакая транзакция не будет зафиксирована в системе частично

Консистентность (согласованность)
каждая успешная транзакция по определению фиксирует только допустимые результаты. Это условие является необходимым для поддержки четвёртого свойства.

Изоляция
Во время выполнения транзакции параллельные транзакции не должны оказывать влияния на её результат.

Долговечность
Другими словами, если пользователь получил подтверждение от системы, что транзакция выполнена, он может быть уверен, что сделанные им изменения не будут отменены из-за какого-либо сбоя.


## Уровни изолированности

- READ_UNCOMMITTED
- READ_COMMITTED
- REPEATABLE_READ
- SERIALIZABLE
Самый высокий уровень изолированности; транзакции полностью изолируются друг от друга, каждая выполняется так, как будто параллельных транзакций не существует. Только на этом уровне параллельные транзакции не подвержены эффекту «фантомного чтения».


При параллельном выполнении транзакций возможны следующие проблемы:

- потерянное обновление (англ. lost update) — при одновременном изменении одного блока данных разными транзакциями теряются все изменения, кроме последнего;
- «грязное» чтение (англ. dirty read) — чтение данных, добавленных или изменённых транзакцией, которая впоследствии не подтвердится (откатится);
- неповторяющееся чтение (англ. non-repeatable read) — при повторном чтении в рамках одной транзакции ранее прочитанные данные оказываются изменёнными;
- фантомное чтение (англ. phantom reads) — одна транзакция в ходе своего выполнения несколько раз выбирает множество строк по одним и тем же критериям. Другая транзакция в интервалах между этими выборками добавляет строки или изменяет столбцы некоторых строк, используемых в критериях выборки первой транзакции, и успешно заканчивается. В результате получится, что одни и те же выборки в первой транзакции дают разные множества строк.


## Распространение транзакций
Когда вызывается метод с @Transactional proxy, который создал Spring, создаёт persistence context (или соединение с базой), открывает в нём транзакцию и сохраняет всё это в контексте нити исполнения (натурально, в ThreadLocal). По мере надобности всё сохранённое достаётся и внедряется в бины. Привязка транзакций к нитям (threads) позволяет использовать семантику серверов приложений J2EE, в которой гарантируется, что каждый запрос получает свою собственную нить.

Таким образом, если в вашем коде есть несколько параллельных нитей, у вас будет и несколько параллельных транзакций, которые будут взаимодействовать друг с другом согласно уровням изоляции. Но что произойдёт, если один метод с @Transactional вызовет другой метод с @Transactional? В Spring можно задать несколько вариантов поведения, которые называются правилами распространения.

Propagation.REQUIRED — применяется по умолчанию. При входе в @Transactional метод будет использована уже существующая транзакция или создана новая транзакция, если никакой ещё нет
Propagation.REQUIRES_NEW — второе по распространённости правило. Транзакция всегда создаётся при входе метод с Propagation.REQUIRES_NEW, ранее созданные транзакции приостанавливаются до момента возврата из метода.
Propagation.NESTED — корректно работает только с базами данных, которые умеют savepoints. При входе в метод в уже существующей транзакции создаётся savepoint, который по результатам выполнения метода будет либо сохранён, либо откачен. Все изменения, внесённые методом, подтвердятся только поздее, с подтверждением всей транзакции. Если текущей транзакции не существует, будет создана новая.
Propagation.MANDATORY — обратный по отношению к Propagation.REQUIRES_NEW: всегда используется существующая транзакция и кидается исключение, если текущей транзакции нет.
Propagation.SUPPORTS — метод с этим правилом будет использовать текущую транзакцию, если она есть, либо будет исполнятся без транзакции, если её нет.
Propagation.NOT_SUPPORTED — одно из самых забавных правил. При входе в метод текущая транзакция, если она есть, будет приостановлена и метод будет выполняться без транзакции.
Propagation.NEVER — правило, которое явно запрещает исполнение в контексте транзакции. Если при входе в метод будет существовать транзакция, будет выброшено исключение.


## Spring JPA Exceptions
Spring has built-in exception translation mechanism, so that all exceptions thrown by the JPA persistence providers are converted into Spring's DataAccessException - for all beans annotated with @Repository (or configured).

There are four main groups -

- NonTransientDataAccessException - это исключения, при которых повторная попытка той же операции завершится неудачно, если причина исключения не будет исправлена. Поэтому, если вы передадите, например, несуществующий идентификатор, он не удастся, если идентификатор не существует в базе данных.

- RecoverableDataAccessException - это «противоположность» предыдущему - исключения, которые можно исправить - после некоторых шагов восстановления. Подробнее в документации API.

- ScriptException - исключения, связанные с SQL, например, при попытке обработать неверно сформированный скрипт.

- TransientDataAccessException - это исключение, когда восстановление возможно без какого-либо явного шага, например если для базы данных истекло время, вы пытаетесь повторить попытку через несколько секунд.


That said, the ideal place to find documentation about all exceptions - is in the API itself - just go through the hierarchy of DataAccessException.



