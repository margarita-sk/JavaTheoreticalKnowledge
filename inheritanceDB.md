There is now straightforwad way to map class hierarchies onto DB tables.
To address this, the JPA specification provides several strategies:

**MappedSuperclass** – the parent classes, can't be entities
**Single Table** – the entities from different classes with a common ancestor are placed in a single table
**Joined Table** – each class has its table and querying a subclass entity requires joining the tables
**Table-Per-Class** – all the properties of a class, are in its table, so no join is required
Each strategy results in a different database structure.

Entity inheritance means that we can use polymorphic queries for retrieving all the sub-class entities when querying for a super-class.

## 1. MappedSuperclass strategy
Эта стратегия заключается в том, что иерархические отношения отображаются внутри класса. Класс-предок помечается аннотацией @MappedSuperclass. Аннотация @Entity не используется, и предки не являются сущностями и не будут отображены в базе данных.
Классы-наследники наследуют класс-предок и помечаются аннотацией @Entity и являются сущностями.
Таким образом, в базе данных будут существовать только таблицы, отображающие классы-наследники со своими полями и полями класса-предка.

Parent class:
```
@MappedSuperclass
public class Person {
    @Id
    private long personId;
    private String name;
...
}
```

Employee sub-class:
```
@Entity
public class MyEmployee extends Person {
    private String company;
    // constructor, getters, setters 
}
```


## 2. Single Table
Это дефолтная стратегия JPA. Согласно ней все классы, вступающие в иерархические отношения собриаются в одну таблицу, которая содержит в себе колонки со всеми полями плюс колонка, определяющая тип.
Класс-предок помечается аннотациями @Entity и @Inheritance с выбором стратегии (strategy = InheritanceType.SINGLE_TABLE). Классы-наследники - @Entity.

@DiscriminatorColumn используется на классе-предке для определения невключенных колонок. 
@DiscriminatorValue используется на классе-наследнике для определения невключенных значений. 
@Id поле должно быть только в классе-предке

Недостаток этой стратегии - столбцы с null.

```
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
public class MyProduct {
    @Id
    private long productId;
    private String name;
...
}
```

```
@Entity
public class Book extends MyProduct {
    private String author;
}
@Entity
public class Pen extends MyProduct {
    private String color;
}
```


@Entity
@DiscriminatorValue("1")
public class Book extends MyProduct {
    // ...
}
@Entity
@DiscriminatorValue("2")
public class Pen extends MyProduct {
    // ...
}
Hibernate adds two other pre-defined values that the annotation can take: “null” and “not null“:

@DiscriminatorValue(“null”) – means that any row without a discriminator value will be mapped to the entity class with this annotation; this can be applied to the root class of the hierarchy
@DiscriminatorValue(“not null”) – any row with a discriminator value not matching any of the ones associated with entity definitions will be mapped to the class with this annotation
Instead of a column, we can also use the Hibernate-specific @DiscriminatorFormula annotation to determine the differentiating values:

@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorFormula("case when author is not null then 1 else 2 end")
public class MyProduct { ... }
This strategy has the advantage of polymorphic query performance since only one table needs to be accessed when querying parent entities. On the other hand, this also means that we can no longer use NOT NULL constraints on sub-class entity properties.

## 3. Joined Table
Согласно этой стратегии каждый класс в иерархических отношениях будет иметь свою таблицу. Единственная колонка, которая будет повторятся - это id, который будет использоваться для слияния этих таблиц, если будет такая нужда. У таблицы каждого класса-наследника, id будет являтся foreign key

Преимущества этой стратегии:
- нет повторяющихся колонок
- нет колонок с null

Недостатки:
- получение сущностей требует слияние таблиц


@Entity
@Inheritance(strategy = InheritanceType.JOINED)
public class Animal {
    @Id
    private long animalId;
    private String species;

    // constructor, getters, setters 
}

@Entity
public class Pet extends Animal {
    private String name;

    // constructor, getters, setters
}

To customize this column, we can add the @PrimaryKeyJoinColumn annotation:
@Entity
@PrimaryKeyJoinColumn(name = "petId")
public class Pet extends Animal {
    // ...
}


## 4. Table per Class
Эта статегия создает каждой sub-сущности по таблице.
Результат такой же как и при использовании стратегии @MappedSuperclass, но, в отличие от нее, table per class действительно будет определеять сущность для каждого класса.
allowing associations and polymorphic queries as a result.

To use this strategy, we only need to add the @Inheritance annotation to the base class:

@Entity
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
public class Vehicle {
    @Id
    private long vehicleId;
    private String manufacturer;
...
}


This is not very different from merely mapping each entity without inheritance. The distinction is apparent when querying the base class, which will return all the sub-class records as well by using a UNION statement in the background.

The use of UNION can also lead to inferior performance when choosing this strategy. Another issue is that we can no longer use identity key generation.

## Polymorphic Queries
As mentioned, querying a base class will retrieve all the sub-class entities as well.

Let's see this behavior in action with a JUnit test:

@Test
public void givenSubclasses_whenQuerySuperclass_thenOk() {
    Book book = new Book(1, "1984", "George Orwell");
    session.save(book);
    Pen pen = new Pen(2, "my pen", "blue");
    session.save(pen);

    assertThat(session.createQuery("from MyProduct")
      .getResultList()).hasSize(2);
}
In this example, we've created two Book and Pen objects, then queried their super-class MyProduct to verify that we'll retrieve two objects.

Hibernate can also query interfaces or base classes which are not entities but are extended or implemented by entity classes. Let's see a JUnit test using our @MappedSuperclass example:

@Test
public void givenSubclasses_whenQueryMappedSuperclass_thenOk() {
    MyEmployee emp = new MyEmployee(1, "john", "baeldung");
    session.save(emp);

    assertThat(session.createQuery(
      "from com.baeldung.hibernate.pojo.inheritance.Person")
      .getResultList())
      .hasSize(1);
}
Note that this also works for any super-class or interface, whether it's a @MappedSuperclass or not. The difference from a usual HQL query is that we have to use the fully qualified name since they are not Hibernate-managed entities.

If we don't want a sub-class to be returned by this type of query, then we only need to add the Hibernate @Polymorphism annotation to its definition, with type EXPLICIT:

@Entity
@Polymorphism(type = PolymorphismType.EXPLICIT)
public class Bag implements Item { ...}
In this case, when querying for Items, the Bag records won't be returned.

7. Conclusion
In this article, we've shown the different strategies for mapping inheritance in Hibernate.

The full source code of the examples can be found over on GitHub.
