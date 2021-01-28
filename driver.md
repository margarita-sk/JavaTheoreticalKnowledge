When we create an instace of a class using new operator, it does two things

Load the class in to memory, if it is not loaded - which means creating in-memory representation of the class from the .class file so that an instance can be created out of it. This includes initializing static variables (resolving of that class)
create an instance of that class and store the reference to the variable.

Class.forName does only the first thing. It loads the class in to memory and return that reference as an instance of Class. If we want to create an instance then, we can call newInstance method of that class. which will invoke the default constructor (no argument constructor). Note that if the default constructor is not accessible, then newInstance method will throw an IllegalAccessException. and if the class is an abstract class or interface or it does not have a default constructor, then it will throw an InstantiationException. If any exception araises during resolving of that class, it will throw an ExceptionInInitializerError.

If the default constructor is not defined, then we have to invoke the defiend constructor using reflection API.

But the main advantage with Class.forName is, it can accept the class name as a String argument. So we can pass the class name dynamically. But if we create an instance of a class using new operator, the class name can't be changed dynamically.

Class.forName() inturn will call loadClass method of the caller ClassLoader (ClassLoder of the class from where Class.forName is invoked).

By default, the Class.forName() resolve that class. which means, initialize all static variables inside that class. same can be changed using the overloaded method of Class.forName(String name,boolean initialize,ClassLoader loader)

The main reason for loading jdbc driver using Class.forName() is, the driver can change dynamically. in the static block all Drivers will create an instance of itself and register that class with DriverManager using DriverManager.registerDriver() method. Since the Class.forName(String className) by default resolve the class, it will initialize the static initializer. So when we call Class.forName("com.sun.jdbc.odbc.JdbcOdbcDriver"), the Driver class will be loaded, instanciated and registers with DriverManager

So if you are using new Operator you have to do the following things.
Code:

Driver drv = new com.sun.jdbc.odbc.JdbcOdbcDriver();
DriverManager.registerDriver(drv);
