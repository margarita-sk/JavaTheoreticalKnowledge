### Redis 
резидентная система управления базами данных класса NoSQL с открытым исходным кодом, работающая со структурами данных типа «ключ — значение». 
Используется как для баз данных, так и для реализации кэшей, брокеров сообщений.
Самые распространенные примеры использования Redis включают кэширование, управление сессиями, системы «издатель-подписчик» и таблицы лидеров. Это самое популярное на текущий момент хранилище пар «ключ-значение». Название Redis является акронимом от REmote DIctionary Server.

Ориентирована на достижение максимальной производительности на атомарных операциях. Написана на Си, интерфейсы доступа созданы для большинства основных языков программирования.

Хранит базу данных в оперативной памяти, снабжена механизмами снимков и журналирования для обеспечения постоянного хранения (на дисках, твердотельных накопителях). Также предоставляет операции для реализации механизма обмена сообщениями в шаблоне «издатель-подписчик»: с его помощью приложения могут создавать каналы, подписываться на них и помещать в каналы сообщения, которые будут получены всеми подписчиками (как IRC-чат). Поддерживает репликацию данных с основных узлов на несколько подчинённых (англ. master — slave replication). Также поддерживает транзакции и пакетную обработку команд (выполнение пакета команд, получение пакета результатов).

Все данные Redis хранит в виде словаря, в котором ключи связаны со своими значениями. Одно из ключевых отличий Redis от других хранилищ данных заключается в том, что значения этих ключей не ограничиваются строками. Поддерживаются следующие абстрактные типы данных: строки, списки, множества, хеш-таблицы, упорядоченные множества.

Тип данных значения определяет, какие операции (команды) доступны для него; поддерживаются такие высокоуровневые операции, как объединение и разность наборов, сортировка наборов.


Преимущества:
Высочайшая производительность
Все данные Redis находятся в оперативной памяти сервера, в отличие от большинства систем управления базами данных, в которых данные хранятся на жестких дисках или твердотельных накопителях (SSD).

Структуры данных в памяти
Redis позволяет пользователям хранить ключи, привязанные к различным типам данных. Основной тип данных – это строка, которая может состоять из текстовых или двоичных данных размером до 512 МБ. Redis также поддерживает списки строк (List of Strings), упорядоченные в порядке вставки; множества неупорядоченных строк (Sets of unordered Strings); упорядоченные по результату множества (Sorted Sets); хеш-таблицы (Hashes), содержащие список полей и значений, и тип данных HyperLogLogs для подсчета уникальных элементов в наборе данных. С помощью Redis в памяти можно хранить практически любые типы данных.
