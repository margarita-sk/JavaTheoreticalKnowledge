# Docker

#1. docker ps — смотрим список запущенных контейнеров
Ей можно передать несколько параметров, вот самые полезные из них:
-q — «тихий» режим, в котором команда выводит только id контейнеров (полезно, когда вам нужно знать только id или же при использовании этой команды в сценариях).
-a — показывает все контейнеры, а не только запущенные.

#2. docker pull — загрузка образа
Как правило, образы создаются на основе базового — из Docker Hub, где есть множество уже готовых образов и которые ты можешь использовать, 
а не тратить время на создание собственного. Для загрузки образа используется команда docker pull.

#3. docker build — собирает образ
Данная команда собирает образ Docker из файла докера (dockerfile) и контекста сборки. Контекст сборки — это набор файлов, расположенных по определенному пути. 
Для задания имени образа используйте параметр -t, например, «docker build -t my.». 
Собирает образ из текущего каталога (».«) — последний параметр это имя каталога, в нашем случае точка указывает, что каталог — текущий.

#4. docker logs — смотрим логи
Позволяет просмотреть логи указанного контейнера. Можно использовать флаг -follow, чтобы следить за логами работающего контейнера, например, docker logs -follow my.

#5. docker run — запускаем контейнер
Запускает контейнер на основе указанного образа. Пример команды docker run my -it bash В данном случае будет запущен контейнер из образа my, а после в нем будет запущен bash.

#6. docker stop — останавливает контейнер
Используется для «мягкой» остановки контейнера. Пример: docker stop my_cont. Можно остановить не конкретный контейнер, а все запущенные — docker stop $(docker ps -a -q).

#7. docker kill — «убивает» контейнер
Не пытается аккуратно завершить процесс, подобна системной команде kill. Как и в предыдущем случае, можно «убить» все контейнеры: docker kill $(ps -a -q).

#8. docker rm — удаляет контейнер
Для удаления контейнера используется команда docker rm, например, docker rm my_cont.

#9. docker rmi — удаляет образ
Команда docker rmi (i от image) удаляет образ, например, docker rmi my.

#10. docker volume ls — список томов
Данная команда показывает список томов, которые являются основным механизмом для хранения данных, генерируемых контейнерами Docker.



- FROM — задаёт базовый (родительский) образ.
- LABEL — описывает метаданные. Например — сведения о том, кто создал и поддерживает образ.
- ENV — устанавливает постоянные переменные среды.
- RUN — выполняет команду и создаёт слой образа. Используется для установки в контейнер пакетов.

- COPY — копирует в контейнер файлы и папки.
The COPY instruction lets us copy a file (or files) from the host system into the image. This means the files become a part of every container that is created from that image. The syntax for the COPY instruction is similar to other copy commands we saw above: COPY <SRC> <DEST>
Just like the other copy commands, SRC can be either a single file or a directory on the host machine. It can also include wildcard characters to match multiple files.

This will copy a single from the current Docker build context into the image: COPY properties.ini /config/
And this will copy all XML files into the Docker image:

COPY *.xml /config/
The main downside of this approach is that we cannot use it for running Docker containers. Docker images are not Docker containers, so this approach only makes sense to use when the set of files needed inside the image is known ahead of time.

COPY and ADD are both Dockerfile instructions that serve similar purposes. They let you copy files from a specific location into a Docker image.
COPY takes in a src and destination. It only lets you copy in a local file or directory from your host (the machine building the Docker image) into the Docker image itself.

ADD lets you do that too, but it also supports 2 other sources. First, you can use a URL instead of a local file / directory. Secondly, you can extract a tar file from the source directly into the destination
A valid use case for ADD is when you want to extract a local tar file into a specific directory in your Docker image.
If you’re copying in local files to your Docker image, always use COPY because it’s more explicit.

ADD — копирует файлы и папки в контейнер, может распаковывать локальные .tar-файлы.
CMD — описывает команду с аргументами, которую нужно выполнить когда контейнер будет запущен. Аргументы могут быть переопределены при запуске контейнера. В файле может присутствовать лишь одна инструкция CMD.
WORKDIR — задаёт рабочую директорию для следующей инструкции.
ARG — задаёт переменные для передачи Docker во время сборки образа.
ENTRYPOINT — предоставляет команду с аргументами для вызова во время выполнения контейнера. Аргументы не переопределяются.
EXPOSE — указывает на необходимость открыть порт.
VOLUME — создаёт точку монтирования для работы с постоянным хранилищем.
