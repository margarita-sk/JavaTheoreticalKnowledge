<details>
<summary>JDK vs CGLIB</summary>
  
| JDK      | CGLIB    |
|----------|----------|
| in package java.lang | requires adding a dependency |
| can proxy only classes that impl interfaces | even with no interfaces, because its proxy mechanism is based on subclassing |
| cannot proxy final - final methods are not allowed in interfaces. | cannot proxy final - because final methods cannot be overwritten |
| cannot proxy private - because it requires method implementation.  | cannot proxy private - because private methods are not accessible in a subclass |
| cannot proxy static - because they belong to the class, not the instance. | cannot proxy static - because they belong to the class, not the instance. |
| a little bit faster | a little bit slower |
</details>


<details>
  <summary>What is diamond problem?</summary>
    A
   / \
  B   C
   \ /
    D
  In Java, there is no multiple inheritance. However, there are multiple interface implementations. In the case of default methods, the child needs to overwrite it. 
</details>

<details>
  <summary>Can static methods be overwritten?</summary>
  They are bound to their classes.
  No, because invocation by class -  ClassA.call()
</details>
