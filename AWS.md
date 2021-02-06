# Amazon Web Services 

1. Explain what S3 is?

Amazon Simple Storage is an amazon service to store data in files. You can store files 1byte-5terabyte any quantity of files.
Files are stored in separate buckets where you can create directories and sub-directories.
Buskets are stored in different regions. 

For S3, the payment model is “pay as you go.”

2. How can you send a request to Amazon S3?
Amazon S3 is a REST service, and you can send a request by using the REST API or the AWS SDK wrapper libraries that wrap the underlying Amazon S3 REST API.


3. What EC2 is?

Amazon Elastic Compute Cloud (EC2) is a cloud service, produced virtual services (Amazon EC2 Instance), two types of storage data and a Load Balancer. 
It allows to start up configured servers with OS: Amazon Linux, Red Hat EL, Suse ES, Windows 2008, Oracle EL.
Also you can create images (AMI — Amazon Machine Image) and use any Linux. 

Also you can create rules of automatic increasing quantity of servers. 
There is one more service that control condition of servers Amazon Cloud Watch. 


4. Mention what the difference between Amazon S3 and EC2 is?
The difference between EC2 and Amazon S3 is that

EC2    It is a cloud web service used for hosting your application. It is like a huge computer machine which can run either Linux or Windows and can handle application like PHP, Python, Apache or any databases
S3  It is a data storage system where any amount of data can be stored.  It has a REST interface and uses secure HMAC-SHA1 authentication keys


5. Explain can you vertically scale an Amazon instance? How?
Yes, you can vertically scale on Amazon instance. For that

Spin up a new larger instance than the one you are currently running
Pause that instance and detach the root webs volume from the server and discard
Then stop your live instance and detach its root volume
Note the unique device ID and attach that root volume to your new server
And start it again

6. What are the storage class available in Amazon s3?
Storage classes available with Amazon s3 are:

Amazon S3 standard
Amazon S3 standard-infrequent Access
Amazon S3 Reduced Redundancy Storage
Amazon Glacier
(Нужно проверить но запоминать не надо, Просто что есть планы и какой ты юзаешь)


7. AWS RDS
Amazon Relational Database Service

RDS — is a service of databases. It contains separte VPS servers, which are opimized for work with databases.
DB engines which can be used in AWS RDS
MS-SQL DB
MariaDB
MYSQL DB
OracleDB
PostgreDB (what was chosen, what resourses and why)

Minimal size of storage is 5 gb.



### General questions
- Tell some usecase about working with AWS S3



- make Spring boot application and deploy it to EC2 
 api сохранение, получение всех и получение конкретных файлов пдф.
база данных с postgres



Про rule engine тожа рассказать
составлять аналитику. Рулы для выплаты зарплат. агрегировали и выставляли заработную плату, хранили эту информацию и мог смотреть
аналитические метрики.
отправляли уведомления о том, что работник не заполнил

We use Jira in our company for time tracking. Based on it the salary is calculated. If an employee forgot to entry working hours and if a quantity of working hours is too small, an employee receives a notification to make an entry. If an employee doesn't, the manager receive the notification to find out.

database design
bug fixing
backend development
unit and integration tests development
