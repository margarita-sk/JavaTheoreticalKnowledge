Project Lombok is a Java library or tool that helps us to avoid writing certain parts of coding. Therefore, these days, developers cannot write code without including it in their projects. It is not essential but thanks to its features and benefits, it has almost become essential for developers who are using it in all their Java projects. 

It magically injects code in a Java class at the time of compilation. 
To understand its working, you need to have some idea about Java compilation.

**The Process Of Java Compilation**  
There are basically three stages of compilation in Java namely, 
1. Parse and Enter, 
2. Annotation Processing and 
3. Analyze and Generate. 

In the first phase, the compiler takes the source files and generates what is referred to as Abstract Source Tree(AST). If you have an idea of DOM, you can consider AST as DOM-equivalent. In this parse, only the syntax errors are checked. 

In phase 2 which is also referred to as the pre-compilation phase, this is where the classes are validated and new resources are generated. They can generate errors that can fail the entire compilation process. If a new source file is generated in this phase, the compilation goes back to the first phase and the process is repeated. 

The last phase is the Analyze and Generate phase where the compiler generates the class files from AST. AST is analyzed where the references, flow, and various other aspects are checked. When everything goes successfully, the class files are written. 

The Working Of Project Lombok – Project Lombok puts itself in the second phase of annotation processing as an annotation processor. But it is quite different from a normal annotation processor. The job of a normal annotation processor is to generate new files while that of Project Lombok is to modify the existing one. This is possible by modifying the AST and the changes made in the AST will be visible in the Analyze and Generate phase. Therefore, the generated class file will reflect the changes. Project Lombok can do things like generating new methods as well as injecting code into an existing method. There are many who call this as hacking which is somewhat true technically speaking. What Project Lombok Provides – There are a lot of annotations provided by Lombok and the most important ones are listed below. Mutable Entities – These contain a lot of boilerplate code and the typical examples are constructors, setters, getter, toString, hashcode, and equals. Immutable Classes – Except fields declarations, you can modify everything with just one annotation. Apart from these, for loggers and final local variables, there are annotations present. With the help of Project Lombok, you can avoid coding so many lines and get rid of repetitive works pretty easily. Besides, the code will be cleaner and much more. If not already, you should incorporate Project Lombok in your Java project.
