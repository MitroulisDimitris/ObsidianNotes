Most popular frameqork for ORM is hibernate


**ORM frameworks**
ORM is used to map objects directly to relational databases for crud operations.
Queries are often otpimized

Used for:
- Databse interaction
- Object relational mapping (Bridge the gap between OOP java and relational SQL)
- Preformace tuning (caching lazy loading, techniques for preformance)

**Key compoments in ORM:**
1. **Entry class:**
- Class that represents a table in the databse 
```
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    
    private String name;
    private String email;
    // Getters and setters
}

```

2. **SessionFactory/EntityManager**
Session manager is used to manage the lifecycle of entity objects, preform database operations

3. **Configuration.**
Conncetion to db is configured through an xml file (hibernate.cfg.xml)

**Example Usage**
```
SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
Session session = sessionFactory.openSession();
Transaction transaction = session.beginTransaction();

// Creating a new user and saving to the database
User user = new User();
user.setName("John Doe");
user.setEmail("john@example.com");
session.save(user);

// Committing the transaction
transaction.commit();
session.close();

```



**JPA**
Java persistence API is a specification for ORM. defines a standard way to map java objects to db tables. It's a set of guidelines/rules that ORM frameworks implement

**Key features**
1. Entity mapping: Allows to define how java obj(entities) map to DB tables using annotations or xml configs
2. Entity Lifecycle ManagmentL Handles the lifecycle of entity objects
3. Queries: Provides the JPQL for quering entities
4. Transaction Managment: 
5. Cascading OperationsL 
6. Lazy/Eager Loading: JPA allows to control when associated data is loaded 


**Annotations**
@Entity -> Marks the class as a hibernate table
@ Table (name = "users") -> Specifies the name of the table in the database
@ ID -> Marks the given attribute as a primary Key
@ GeneratedValue(strategy = GenerationType.IDENTITY) -> Atrtibute is autoincremented
@ Column -> Maps the attribute as a column in the databse
@ Temporal(TemporalType.DATE) -> Specify date format
@ Lob -> large object type Blob/clob
@ManyToOne, OneToMany, etc -> defines relationships between entities
@ JoinColumn ->Specifies the Foreign key Column
@ @Table(name = "USERS", uniqueConstraints = {@UniqueConstraint(columnNames = "email")}) -> Ensures a colum, set of columns must be unique


