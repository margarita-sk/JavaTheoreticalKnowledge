# The Twelve Factors

### I. Codebase
- One codebase tracked in revision control, many deploys
Одно приложение - один репозиторий, который предоставляет код для деплоя, тестирования и т.д.
Весь код должен находится в системе контроля версий.

Если несколько приложений используют один код, то он должен быть выделен в отдельный репозиторий и использоваться как зависимость.

### II. Dependencies
- Explicitly declare and isolate dependencies
Приложения не должны иметь неявных зависимостей. Зависимости должны быть изолированными. 

### III. Config
- Store config in the environment
Конфигурации должны хранится в среде выполнения

### IV. Backing services
- Treat backing services as attached resources
Сторонние службы - это отдельный ресурс, неважно, расположены они локально или удаленно

### V. Build, release, run
- Strictly separate build and run stages
Разделять сборку, релиз и выполнение

A codebase is transformed into a (non-development) deploy through three stages:
1. The build stage is a transform which converts a code repo into an executable bundle known as a build. Using a version of the code at a commit specified by the deployment process, the build stage fetches vendors dependencies and compiles binaries and assets.
2. The release stage takes the build produced by the build stage and combines it with the deploy’s current config. The resulting release contains both the build and the config and is ready for immediate execution in the execution environment.
3. The run stage (also known as “runtime”) runs the app in the execution environment, by launching some set of the app’s processes against a selected release.

### VI. Processes
- Execute the app as one or more stateless processes
Приложение - это один или несколько процессов. Оно может использовать оперативную память или диск только как временное хранилище, все постоянные данные должны находится в хранилище (подключаемом ресурсе).


### VII. Port binding
- Export services via port binding
Приложение не должно зависить от сервера. Это реализуется с помощью объявления зависимости для добавления бибилиотеки веб-сервера к приложению, например Jetty в Java.


### VIII. Concurrency
- Scale out via the process model
Масштаб с помощью процессов. Это значит, что обработкой разных задач должны заниматься разные процессы, чтобы в будущем маштабировать только те процессы, которые необходимы.

### IX. Disposability
- Maximize robustness with fast startup and graceful shutdown
Быстрый запуск и корректное завершение процессов.

### X. Dev/prod parity
- Keep development, staging, and production as similar as possible
Нужно сделать разработку и развертывание как можно ближе: по времени, по людям - разработчик должен принимать участие в развертывания своего кода, по инструментам - среда разработки должна максимально соответствовать среде тестирования.

### XI. Logs
- Treat logs as event streams
Лог - это поток событий, и обращаться к нему надо как к потоку событий. Приложение не должно само записывать данные в файло логов и тем более управлять ими


### XII. Admin processes
- Run admin/management tasks as one-off processes
Задачи администрирования должны подчинятся тем же правилам, что и остальные процессы
