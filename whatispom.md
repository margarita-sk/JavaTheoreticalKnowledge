# Maven

Apache Maven - это фреймворк для автоматизации процесса сборки проектов на основе описания их структуры в файле на языке POM (Project Object Model), который является подмножеством формата XML.


**Артефакт** — это, по сути, любая библиотека, хранящаяся в репозитории. Это может быть какая-то зависимость или плагин.

**Зависимости** — это те библиотеки, которые непосредственно используются в вашем проекте для компиляции кода или его тестирования.
**Плагины** же используются самим Maven'ом при сборке проекта или для каких-то других целей (деплоймент, создание файлов проекта для Eclipse и др.).

**Архетип** — это некая стандартная компоновка файлов и каталогов в проектах различного рода (веб, swing-проекты и прочие). Другими словами, Maven знает, как обычно строятся проекты и в соответствии с архетипом создает структуру каталогов.
Как правило, название артефакта состоит из названия группы, собственного названия и версии. К примеру Spring будет иметь вот такое название в среде Maven: org.springframework.spring:2.5.5. Последний домен означает всегда artifactId, все, что перед ним – groupId.

мавен так же диктует свою иерархию директорий, но чтобы не создавать её вручную, достаточно выполнить
 mvn archetype:create -DgroupId=com.mycompany.app -DartifactId=my-webapp -DarchetypeArtifactId=maven-archetype-webapp


## 1. What is a POM?
Это xml файл, в котором описывается структура проекта(POM – Project Object Model). Он находится в корневой папке проекта. 

При описании проекта в файле pom.xml используются следующие теги и секции :
- project	элемент верхнего уровня, описание проекта;
- GAV-параметры	параметры проекта;
- url	интернет-страница проекта;
- properties	секция свойств проекта;
- repositories	секция репозиториев;
- dependencies	секция определения зависимостей проекта;
- build	описание сборки проекта c секцией plugins в ней

Структура проекта описывается в файле pom.xml, который должен находиться в корневой папке проекта. Содержимое проектного файла имеет следующий вид :
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
     xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
     http://maven.apache.org/xsd/maven-4.0.0.xsd">
   
    <modelVersion>4.0.0</modelVersion>

    <!-- GAV параметры описания проекта -->
    <groupId>...</groupId>
    <artifactId>...</artifactId>
    <packaging>...</packaging>
    <version>...</version>

    <!-- Секция свойств -->
    <properties>
        . . .
    </properties>

    <!-- Секция репозиториев -->
    <repositories>
        . . .
    </repositories>

    <!-- Секция зависимостей -->
    <dependencies>
        . . .
    </dependencies>
  
    <!-- Секция сборки -->
    <build>
        <finalName>projectName</finalName>
        <sourceDirectory>${basedir}/src/java</sourceDirectory>
        <outputDirectory>${basedir}/targetDir</outputDirectory>
        <resources>
            <resource>
                <directory>${basedir}/src/java/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                </includes>
            </resource>
        </resources>
        <plugins>
            . . .
        </plugins>
    </build>
</project>
```
Не все секции могут присутствовать в описании pom.xml. Так секции properties и repositories часто не используются. Параметры GAV проекта являются обязательными.

**Параметры GAV**
groupId - идентификатор производителя объекта. Часто используется схема принятая в обозначении пакетов Java. Например, если производитель имеет домен domain.com, то в качестве значения groupId удобно использовать значение com.domain. То есть, groupId это по сути имя пакета.
artifactId - идентификатор объекта. Обычно это имя создаваемого модуля или приложения.
version - версия описываемого объекта. Для незавершенных проектов принято добавлять суффикс SNAPSHOT. Например 1.0.0-SNAPSHOT.

**Properties**
Отдельные настройки проекта можно определить в переменных. Это может быть связанно, к примеру, с тем, что требуется использовать семейство библиотек определенной версии. Для этого в проектном файле используется секция <properties>, в которой объявляются переменные. Обращение к переменной выглядит следующим образом : ${имя переменной}.
  
В секции <properties> также можно указать следующий код с указанием требуемой кодировки :
```
<properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

**Dependency**
Зависимость, эта связь, которая говорит, что для некоторых фаз жизненного цикла maven проекта, требуются некоторые артефакты. Зависимости проекта описываются в секции <dependencies> файла pom.xml. Для каждого используемого в проекте артефакта необходимо указать GAV (groupId, artifactId, version), где
groupId - идентификатор производителя объекта. Часто используется схема принятая в обозначении пакетов Java. Например, если производитель имеет домен domain.com, то в качестве значения groupId удобно использовать значение com.domain. То есть, groupId это по сути имя пакета.
artifactId - идентификатор объекта. Обычно это имя создаваемого модуля или приложения.
version - версия описываемого объекта. Для незавершенных проектов принято добавлять суффикс SNAPSHOT. Например 1.0-SNAPSHOT.

Иногда при описании зависимости требуется использовать необязательный параметр <classifier>. Следующий пример демонстрирует описание зависимости библиотеки json-lib-2.4-jdk15.jar с параметром classifier.
```
<dependency>
    <groupId>net.sf.json-lib</groupId>
    <artifactId>json-lib</artifactId>
    <version>2.4</version>
    <classifier>jdk15</classifier>
</dependency>
  ```

**Build**
Секция <build> также не является обязательной, т. к. существует значение по умолчанию. Данная секция содержит информацию по самой сборке, т.е. где находятся исходные файлы, файлы ресурсов, какие плагины используются.

<finalName> - наименование результирующего файла сборки (jar, war, ear..), который создаётся в фазе package. Значение по умолчанию — «artifactId-version»;
<sourceDirectory> - определение месторасположения файлов с исходным кодом. По умолчанию файлы располагаются в директории «${basedir}/src/main/java», но можно определить и в другом месте;
<outputDirectory> - определение месторасположения директории, куда компилятор будет сохранять результаты компиляции - *.class файлы. По умолчанию определено значение «target/classes»;
<resources> и вложенные в неё тэги <resource> определяют местоположение файлов ресурсов. Ресурсы, в отличие от файлов исходного кода, при сборке просто копируются в директорию, значение по умолчанию которой равно «src/main/resources».

## 2. Maven lifecycle
## 3. Maven phases

Жизненный цикл maven проекта – это чётко определённая последовательность фаз. Когда maven начинает сборку проекта, он проходит через определённую последовательность фаз, выполняя задачи, указанные в каждой из фаз. Maven имеет 3 стандартных жизненных цикла :

- clean — жизненный цикл для очистки проекта;
- default — основной жизненный цикл;
- site — жизненный цикл генерации проектной документации.
Каждый из этих циклов имеет фазы pre и post. Они могут быть использованы для регистрации задач, которые должны быть запущены перед и после указанной фазы.

**Фазы жизненного цикла clean**
- pre-clean;
- clean;
- post-clean.

**Фазы жизненного цикла site**
- pre-site;
- site;
- post-site;
- site-deploy;

**Фазы жизненного цикла default**
- validate - выполнение проверки, является ли структура проекта полной и правильной;
- generate-sources - включение исходного кода в фазу;
- process-sources - подготовка/обработка исходного кода; например, фильтрация определенных значений;
- generate-resources - генерирование ресурсов, которые должны быть включены в пакет;
- process-resources - копирование ресурсов в указанную директорию (перед упаковкой);
- compile - компиляция исходных кодов проекта;
- process-test-sources - обработка исходных кодов тестов;
- process-test-resources - обработка ресурсов для тестов;
- test-compile - компиляция исходных кодов тестов;
- test - собранный код тестируется, используя приемлемый фреймворк типа JUnit;
- package - упаковка откомпилированных классов и прочих ресурсов в дистрибутивный формат;
- integration-test - программное обеспечение в целом или его крупные модули подвергаются интеграционному тестированию. Проверяется взаимодействие между составными частями программного продукта;
- install - установка программного обеспечения в maven-репозиторий, чтобы сделать его доступным для других проектов;
- deploy - стабильная версия программного обеспечения копируется в удаленный maven-репозиторий, чтобы сделать его доступным для других пользователей и проектов;


Стандартные жизненные циклы могут быть дополнены функционалом с помощью maven-плагинов. Плагины позволяют вставлять в стандартный цикл новые шаги (например, распределение на сервер приложений) или расширять существующие шаги.

Порядок выполнения команд maven проекта зависит от порядка вызова целей и фаз. Следующая команда

```
mvn clean dependency:copy-dependencies package
 ```
выполнит фазу clean, после этого будет выполнена задача dependency:copy-dependencies, после чего будет выполнена фаза package. Аргументы clean и package являются фазами сборки, dependency:copy-dependencies является задачей.

При этом все шаги последовательны. И если, к примеру, выполнить $ mvn package, то фактически будут выполнены шаги: validate, compile, test и package. Таким образом использовать мавен довольно просто.


## 4. Goals in maven
Использование maven часто сводится к выполнению одной из команды следующего набора, которые можно назвать целями:

validate — проверка корректности метаинформации о проекте;
compile — компилиляция исходников;
test — прогонка тестов классов;
package — упаковка скомпилированнных классов в заданный формат (jar или war, к примеру);
integration-test — отправка упакованных классов в среду интеграционного тестирования и прогонка тестов;
verify — проверка корректности пакета и удовлетворение требованиям качества;
install — отправка пакета в локальный репозиторий, где он будет доступен для использования как зависимость в других проектах;
deploy — отправка пакета на удаленный production сервер, где доступ к нему будет открыт другим разработчикам.
В общем случае для выполнения команды maven необходимо выполнить следующий код : «mvn цель». В качестве параметров указываются не только имена фаз, но и имена и цели плагинов в формате «mvn плагин:цель». Например, вызов фазы цикла «mvn clean» эквивалентен вызову плагина «mvn clean:clean».

Каждая фаза - это послоедовательность целей, каждая цель ответственна за выполенние специфического задания.
Когда мы запускаем определенную фазу - все цели, привязанные к этой фазе начинают по порядку выполнятся.


## 5. What is profile in maven, can we bound profiles to phases or goals?
В maven существует возможность изменять настройки проекта в зависимости от окружения, это реализовано через профили проекта. Профиль содержит в себе настройки, которые будут добавлены к основным настройкам, или, наоборот, заместят их
  ```
<project>
 ...
 <profiles>
  <profile>
   <id>test</id>
   <activation>...</activation>
   <build>...</build>
   <modules>...</modules>
   <repositories>...</repositories>
   <pluginRepositories>...</pluginRepositories>
   <dependencies>...</dependencies>
   <reporting>...</reporting>
   <dependencyManagement>...</dependencyManagement>
   <distributionManagement>...</distributionManagement>
  </profile>
 </profiles>
</project>
  ```


Профиль можно активировать (включить) явно, указав в строке запуска мейвена имя профиля через опцию -P:
  ```
mvn -Pимя_профиля
  ```
Либо указав условия активации. Профиль будет активирован, если выполнилось хотя бы одно условие активации. Условием активации может быть наличие или значение определенной переменной окружения, версия JDK, версия или тип операционной системы, наличие или отсутствие определенного файла.
  ```
<project>
 ...
 <profiles>
  <profile>
   <id>test</id>
   <activation>
    <activeByDefault>false</activeByDefault>
    <jdk>1.5</jdk>
    <os>
     <name>Windows XP</name>
     <family>Windows</family>
     <arch>x86</arch>
     <version>5.1.2600</version>
    </os>
    <property>
     <name>mavenVersion</name>
     <value>2.0.3</value>
    </property>
    <file>
     <exists>${basedir}/file2.properties</exists>
     <missing>${basedir}/file1.properties</missing>
    </file>
   </activation>
   ...
  </profile>
 </profiles>
</project>
  ```
  ```
<project>
 <modelVersion>4.0.0</modelVersion>
 <groupId>habr</groupId>
 <artifactId>aggr</artifactId>
 <version>1.0.0-SNAPSHOT</version>
 <packaging>pom</packaging>
 <name>Profiles Demo - Top</name>
 
 <modules>
  <module>module1</module>
  <module>selenium-tests</module>
 </modules>
 
 <profiles>
  <profile>
   <id>it</id>
   <modules>
    <module>integration-tests</module>
   </modules>   
  </profile>
 </profiles>  
</project>
  ```
Per Project
- Defined in the POM itself (pom.xml).

Per User
- Defined in the Maven-settings (%USER_HOME%/.m2/settings.xml).

Global
- Defined in the global Maven-settings (${maven.home}/conf/settings.xml).

Profile descriptor
- a descriptor located in project basedir (profiles.xml) (unsupported in Maven 3.0: see Maven 3 compatibility notes)

**How can a profile be triggered? How does this vary according to the type of profile being used?**

- From the command line
- Through Maven settings
- Based on environment variables
- OS settings
- Present or missing files



## 6. What is local and remout repositories and how to work with them

**Repository** - это хранилище библиотек, место, где хранятся файлы jar, pom, javadoc, исходники и т.д. 

В проекте могут быть использованы :
- центральный репозиторий, доступный на чтение для всех пользователей в интернете;
- внутренний «корпоративный» репозиторий - дополнительный репозиторий группы разработчиков;
- локальный репозиторий, по умолчанию расположен в ${user.home}/.m2/repository - персональный для каждого пользователя.

Дополнительные репозитории, необходимые для сборки проекта, перечисляются в секции <repositories> проектного файла pom.xml :
  
```
<project>
    ...
    <repositories>
        <repository>
            <id>repo1.maven.org</id>
            <url>http://repo1.maven.org/maven2</url>
        </repository>
    </repositories>
    ...
</project>
 ```
Можно создать и подключать к проектам свой репозиторий, содержимое которого можно полностью контролировать и сделать его доступным для ограниченного количества пользователей. Доступ к содержимому репозитория можно ограничивать настройками безопасности сервера так, что код ваших проектов не будет доступен из вне. Существуют несколько реализаций серверов - репозиториев maven; к наиболее известным относятся artifactory, continuum, nexus.
Для добавления, к примеру, библиотеки carousel-lib.jar в локальный репозиторий можно использовать команду mvn install (команда должна быть однострочной) :
  
```
mvn install:install-file -Dfile=${FILE_PATH}/carousel-lib.jar -DgroupId=ru.carousel -DartifactId=carousel-lib -Dversion=1.0 -Dpackaging=jar -DgeneratePom=true
```
В локальном репозитории «.m2» maven создаст директорию ru/carousel, в которой разместит данную библиотеку и создаст к ней описание в виде pom.xml.
By default, maven local repository is %USER_HOME%/.m2 directory

## 7. What is maven plugins, how to run it from command line

**Plugins**
Maven базируется на plugin-архитектуре, которая позволяет использовать плагины для различных задач (test, compile, build, deploy и т.п). Иными словами, maven запускает определенные плагины, которые выполняют всю работу. То есть, если мы хотим научить maven особенным сборкам проекта, то необходимо добавить в pom.xml указание на запуск нужного плагина в нужную фазу и с нужными параметрами. Это возможно за счет того, что информация поступает плагину через стандартный вход, а результаты пишутся в его стандартный выход.

Количество доступных плагинов очень велико и включает разнотипные плагины, позволяющие непосредственно из maven запускать web-приложение для тестирования его в браузере, генерировать Web Services. Главной задачей разработчика в этой ситуации является найти и применить наиболее подходящий набор плагинов.

В простейшем случае запустить плагин просто - для этого необходимо выполнить команду в определенном формате. Например, чтобы запустить плагин «maven-checkstyle-plugin» (artifactId) с groupId равным «org.apache.maven.plugins» необходимо выполнить следующую команду :
``` 
mvn org.apache.maven.plugins:maven-checkstyle-plugin:check
 ```
Целью (goal) выполнения данного плагина является проверка "check". Можно запустить в более краткой форме :
```
mvn maven-checkstyle-plugin:check
 ```
Объявление плагина в проекте похоже на объявление зависимости. Плагины также идентифицируется с помощью GAV (groupId, artifactId, version). 

В случае необходимости выполнения нестандартных действий в определенной фазе, например, на стадии генерации исходников «generate-sources», можно добавить вызов соответствующего плагина в файле pom.xml :
 ```
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>имя-плагина</artifactId>
  <executions>
    <execution>
      <id>customTask</id>
      <phase>generate-sources</phase>
      <goals>
         <goal>pluginGoal</goal>
      </goals>
...
 ```
Самое важное в данном случае – это определить для плагина наименование фазы «execution/phase», в которую нужно встроить вызов цели плагина «goal». Фаза «generate-sources» располагается перед вызовом фазы compile и очень удобна для генерирования части исходных кодов проекта.

## 8. Transitivity dependencies

Начиная со второй версии фреймворка maven были введены транзитивные зависимости, которые позволяет избегать необходимости изучения и определения библиотек, которые требуются для самой зависимости. Maven включает их автоматически. В общем случае, все зависимости, используемые в проекте, наследуются от родителей. Ограничений по уровню наследований не существует, что, в свою очередь, может вызвать их сильный рост. В качестве примера можно рассмотреть создание проекта «A», который зависит от проекта «B». Но проект «B», в свою очередь, зависит от проекта «C». Подобная цепочка зависимостей может быть сколь угодно длинной. Проблемы могут возникнуть только в случае циклических зависимостей.

Существуют специальные методы ограничивать включение зависимостей.

**Посредничество зависимостей** определяет версию артификата, который будет выбран. Мавен берет ближайший в древе к родительскому. 
  A
  ├── B
  │   └── C
  │       └── D 2.0
  └── E
      └── D 1.0
D 1.0 будет использован в данном случае для сборки.
   
**Управление зависимостями** позволяет авторам проекта прямо указвать версию артификата, который будет использован при возникновении транзитивных зависимостей.



## 9. Parent and child pom

Чтобы объединить несколько maven-проектов в один связанный проект необходимо использовать наследование, которое определяет включение дополнительных секций в pom.xml (POM - Project Object Model).

Допустим необходимо разработать два взаимосвязанных проекта (project1, project2), которые должны быть объединены в едином родительском проекте project. Физически проекты необходимо расположить в одной родительской директории, в которой дочерние maven-проекты являются поддиректориями. Родительский файл pom.xml располагается в корневой директории.

В pom.xml родительского проекта необходимо определить параметры GAV (groupId, artifactId, version) и в теге <packaging> указать значение «pom». Дополнительно вводится секция <modules>, в которой перечисляются все дочерние проекты.

```
<groupId>com.example</groupId>
<artifactId>project</artifactId>
<version>0.0.1</version>
<packaging>pom</packaging>
. . .
<modules>
    <module>project1</module>
    <module>project2</module>
</modules>
```

В pom.xml дочерних проектов необходимо ввести секцию <parent> и определить GAV-параметры родительского проекта.
  
```
<parent>
    <groupId>com.example</groupId>
    <artifactId>project</artifactId>
    <version>0.0.1</version>
</parent>
```
На этом можно сказать, что все дочерние проекты привязаны к родительскому.


Наследование в maven-проектах широко используется при разработке плагинов/бандлов для контейнеров OSGi (Open Services Gateway Initiative) и компонентов EJB (Enterprise JavaBeans). Также можно использовать «преимущества» наследования и в простых проектах.

Зачем объединять проекты?
В связанных многомодульных проектах можно исключить дублирование свойств и зависимостей, а также использовать централизованное управление и контролировать зависимости.

1. Общие свойства проектов
Связанные проекты позволяют определить общие свойства проектов, зависимости и разместить их в родительском pom.xml. Дочерние проекты будут автоматически наследовать свойства родителя. 
Дочерние объекты наследуют значения следующих GAV-параметров родителя : <groupId>, <version>, но их можно при необходимости переопределить.

2. Централизованное управление проектами
Выполняя maven-команды в родительском проекте, они автоматически будут выполнены для каждого из подпроектов. В следующем примере выполняется команда install, согласно которой после сборки всех проектов они будут размещены в локальном репозитории.


Чтобы посмотреть список зависимостей проекта/ов, необходимо выполнить команду «mvn dependency:tree» :

Maven сначала выводит в консоль зависимости главного проекта, а потом зависимости для каждого из дочерних проектов. Как видно в примере значения groupId (com.example) и version (0.0.1) дочерних проектов совпадают с родительским. Они теперь необязательны и берутся по умолчанию у parent проекта, хотя можно определить собственные значения для каждого подпроекта.

Кроме свойств <properties> и зависимостей <dependencies> в родительском проекте часто объявляют необходимые для сборки плагины и репозитории.
  
  

## 10. Scope of dependencies
Область действия scope определяет этап жизненного цикла проекта, в котором эта зависимость будет использоваться.

test
Если зависимость junit имеет область действия test, то эта зависимость будет использована maven'ом при выполнении компиляции той части проекта, которая содержит тесты, а также при запуске тестов на выполнение и построении отчета с результатами тестирования кода. Попытка сослаться на какой-либо класс или функцию библиотеки junit в основной части приложения (каталог src/main) вызовет ошибку.

compile (дефолтный)
К наиболее часто используемой зависимости относится compile (используется по умолчанию). Т.е. dependency, помеченная как compile, или для которой не указано scope, будет доступна как для компиляции основного приложения и его тестов, так и на стадиях запуска основного приложения или тестов. Чтобы инициировать запуск тестов из управляемого maven-проекта можно выполнив команду "mvn test", а для запуска приложения используется плагин exec.

provided
Область действия зависимости provided аналогична compile, за исключением того, что артефакт используется на этапе компиляции и тестирования, а в сборку не включается. Предполагается, что среда исполнения (JDK или WEB-контейнер) предоставят данный артефакт во время выполнения программы. Наглядным примером подобных артефактов являются такие библиотеки, как hibernate или jsf, которые необходимы на этапе разработки приложения.

runtime
Область действия зависимости runtime не нужна для компиляции проекта и используется только на стадии выполнения приложения.

system
Область действия зависимости system аналогична provided за исключением того, что содержащий зависимость артефакт указывается явно в виде абсолютного пути к файлу, определенному в теге systemPath. Обычно к таким артефактам относятся собственные наработки, и искать их в центральном репозитории, куда Вы его не размещали, не имеет смысла :
```
<dependencies>
    <dependency>
        <groupId>ru.carousel</groupId>
        <artifactId>carousel-lib</artifactId>
        <version>1.0</version>
        <scope>system</scope>
        <systemPath>
               /projects/libs/carousel-lib.jar
        </systemPath>
    </dependency>
</dependencies>
```
Если версия модуля определяется как SNAPSHOT (версия 2.0.0-SNAPSHOT), то maven будет либо пересобирать его каждый раз заново вместо того, чтобы подгружать из локального репозитория, либо каждый раз загружать из public-репозитория. Указывать версию как SNAPSHOT нужно в том случае, если проект в работе и всегда нужна самая последняя версия.

## 11. What is import scope?
<scope>import</scope>
использутся для импорта зависимостей из других артефактов и управлением зависимостями в сложных пакетах, состоящих из нескольких артефактов.
Эта область действия поддерживается только pom в секции <dependencyManagement>. Он указывает, что зависимость должна быть заменена действующим списком зависимостей в указанном разделе POM <dependencyManagement>. Поскольку они заменяются, зависимости с областью импорта фактически не участвуют в ограничении транзитивности зависимости.

  

## 12. What are bom files?

Bill Of Materials (спецификация материалов). BOM - это особый вид pom файла, который контролирует версии зависимостей проекта и предоставляет центральное место для определения и обновления этих версий. Он привносит гибкость с помощью возможности добавлять зависимости в модуль и не думать об их версии.

When we have a set of projects that inherit a common parent, we can put all dependency information in a shared POM file called BOM.

Following is an example of how to write a BOM file:
```
<project ...>
	
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Baeldung-BOM</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>BaelDung-BOM</name>
    <description>parent pom</description>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>test</groupId>
                <artifactId>a</artifactId>
                <version>1.2</version>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>b</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
            <dependency>
                <groupId>test</groupId>
                <artifactId>c</artifactId>
                <version>1.0</version>
                <scope>compile</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>
```
As we can see, the BOM is a normal POM file with a dependencyManagement section where we can include all an artifact's information and versions.



There are 2 ways to use the previous BOM file in our project and then we will be ready to declare our dependencies without having to worry about version numbers.

We can inherit from the parent:

<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
    <parent>
        <groupId>baeldung</groupId>
        <artifactId>Baeldung-BOM</artifactId>
        <version>0.0.1-SNAPSHOT</version>
    </parent>
</project>
As we can see our project Test inherits the Baeldung-BOM.

We can also import the BOM.

In larger projects, the approach of inheritance is not efficient because the project can inherit only a single parent. Importing is the alternative as we can import as many BOMs as we need.

Let's see how we can import a BOM file into our project POM:

<project ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>baeldung</groupId>
    <artifactId>Test</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <packaging>pom</packaging>
    <name>Test</name>
    
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>baeldung</groupId>
                <artifactId>Baeldung-BOM</artifactId>
                <version>0.0.1-SNAPSHOT</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
</project>



Overwriting BOM Dependency
The order of precedence of the artifact's version is:

The version of the artifact's direct declaration in our project pom
The version of the artifact in the parent project
The version in the imported pom, taking into consideration the order of importing files
dependency mediation
We can overwrite the artifact's version by explicitly defining the artifact in our project's pom with the desired version
If the same artifact is defined with different versions in 2 imported BOMs, then the version in the BOM file that was declared first will win


## Super POM
The Super POM is Maven's default POM. All POMs extend the Super POM unless explicitly set, meaning the configuration specified in the Super POM is inherited by the POMs you created for your projects.
