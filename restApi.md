# REST api

## What is restApi?
REST означает REpresentational State Transfer (передача состояния представления). 
Это популярный архитектурный подход для создания API.
Был создан одним из создателей протокола HTTP. Отличительной особенностью сервисов REST является то, что они позволяют наилучшим образом использовать протокол HTTP. 

Вот как обычно реализуется служба REST:
*Формат обмена данными*: здесь нет никаких ограничений. JSON — очень популярный формат, хотя можно использовать и другие, такие как XML
*Транспорт*: всегда HTTP. REST полностью построен на основе HTTP.
*Определение сервиса*: не существует стандарта для этого, а REST является гибким. Это может быть недостатком в некоторых сценариях, поскольку потребляющему приложению может быть необходимо понимать форматы запросов и ответов. Однако широко используются такие языки определения веб-приложений, как WADL (Web Application Definition Language) и Swagger.

REST фокусируется на ресурсах и на том, насколько эффективно вы выполняете операции с ними, используя HTTP.

REST - это архитектурный подход, который определяет стиль выполнения запросов и получения ответов в клиент-серверных приложениях.
Он работает на основе HTTP - формируются запросы. Формат обмена данными чаще всего json, однако может быть и xml

## @Controller 

HandlerMapping

## @RestController vs. @Controller

Spring MVC и REST 
Spring - MVC фреймфорк, использующий аннотации, которые позволяют облегчить процесс создания RESTfull веб-сервиса. Основная разница между традиционным Spring MVC контроллером и RESTfull веб-сервис контроллером заключается в способе создания тела HTTP ответа. MVC контроллер опирается на технологию View, а RESTfull веб сервис контроллер  возвращает объект, который представляется в HTTP ответе  в виде JSON или XML. 

Схема работы Spring MVC
Клиент отправляет запрос к веб-сервису.
Запрос перехватывается DispatcherServlet, который ищет Handler Mappings и соответствующий тип.
Запрос обрабатывается контроллером и результат передается DispatcherServlet, а потом перенаправляется во view.
Использование @ResponseBody 
Когда вы используете аннотацию @ResponseBody для метода, Spring автоматически записывает результат в тело http ответа. Каждый метод в контроллере должен иметь данную аннотацию. 

Что происходит внутри
У Spring есть список HttpMessageConverters. HttpMessageConverter обязан конвертировать тело запроса к определенному классу и и класс к телу ответа, в зависимости от типа. Каждый раз, когда происходит запрос с аннотацией @ResponseBody, Spring ищет  среди всех HttpMessageConverters подходящий и использует его.

Использование аннотации @RestController
В Spring 4.0 была представлена аннотация @RestController. Применив ее к контроллеру добавляются аннотации @Controller, а так же @ResponseBody применяется ко всем методам. 

## HTTP methods 

HTTP defines a set of request methods to indicate the desired action to be performed for a given resource. Although they can also be nouns, these request methods are sometimes referred to as HTTP verbs.

**GET**
The GET method requests a representation of the specified resource. Requests using GET should only retrieve data.

**HEAD**
The HEAD method asks for a response identical to that of a GET request, but without the response body.

**POST**
The POST method is used to submit an entity to the specified resource, often causing a change in state or side effects on the server.

**PUT**
The PUT method replaces all current representations of the target resource with the request payload.

**DELETE**
The DELETE method deletes the specified resource.

**CONNECT**
The CONNECT method establishes a tunnel to the server identified by the target resource.

**OPTIONS**
The OPTIONS method is used to describe the communication options for the target resource.

**TRACE**
The TRACE method performs a message loop-back test along the path to the target resource.

**PATCH**
The PATCH method is used to apply partial modifications to a resource.


## Status codes

HTTP response status codes indicate whether a specific HTTP request has been successfully completed. Responses are grouped in five classes:

Informational responses (100–199)
Successful responses (200–299)
Redirects (300–399)
Client errors (400–499)
Server errors (500–599)

1xx: Informational (информационные):
100 Continue («продолжай»)[2][3];
101 Switching Protocols («переключение протоколов»)[2][3];
102 Processing («идёт обработка»);

2xx: Success (успешно):
200 OK («хорошо») успешный запрос
201 Created («создано») ресурс создан
202 Accepted («принято»)запрос был принят на обработку, но она не завершена. 

3xx: Redirection (перенаправление):
300 Multiple Choices («множество выборов»)[2][7];
301 Moved Permanently («перемещено навсегда»)[2][7];
302 Moved Temporarily («перемещено временно»)[2][7];
302 Found («найдено»)
303 See Other («смотреть другое»)[2][7];
304 Not Modified («не изменялось»)[2][7];
305 Use Proxy («использовать прокси»)[2][7];
306 — зарезервировано (код использовался только в ранних спецификациях)[7];
307 Temporary Redirect («временное перенаправление»)[7];
308 Permanent Redirect («постоянное перенаправление»)[8].

4xx: Client Error (ошибка клиента):
400 Bad Request («неправильный, некорректный запрос»)[2][3][4];
401 Unauthorized («не авторизован (не представился)»)[2][3];
402 Payment Required («необходима оплата»)[2][3];
403 Forbidden («запрещено (не уполномочен)»)[2][3];
404 Not Found («не найдено»)[2][3];
405 Method Not Allowed («метод не поддерживается»)[2][3];
406 Not Acceptable («неприемлемо») запрошенный URI не может удовлетворить переданным в заголовке характеристикам
407 Proxy Authentication Required («необходима аутентификация прокси»)[2][3];
408 Request Timeout («истекло время ожидания»)[2][3];
409 Conflict («конфликт»)[2][3][4];
410 Gone («удалён»)[2][3];

5xx: Server Error (ошибка сервера):
500 Internal Server Error («внутренняя ошибка сервера»)[2][3];
501 Not Implemented («не реализовано»)[2][3];
502 Bad Gateway («плохой, ошибочный шлюз»)[2][3];
503 Service Unavailable («сервис недоступен»)[2][3];
504 Gateway Timeout («шлюз не отвечает»)[2][3];
505 HTTP Version Not Supported («версия HTTP не поддерживается»)[2][3];
520 Unknown Error («неизвестная ошибка»)[15];
524 A Timeout Occurred («время ожидания истекло»)[15];
