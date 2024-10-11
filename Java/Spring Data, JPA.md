
**Spring Data**

Project within the larger Spring framework that aims to simplify working 
with different kind of databases.
Provides a reposotory pattern with predifined methods save, findById, delete


**Jpa (Java Persistence API)**

Jpa is a specification provided by java to manage relational data.
Defines the set of interfaces, annotations needed to map java objects to db tables
Is not an implementation, but a specification that orm frameworks implement


**Spring Data JPA**
Part of Spring data project that provides support for JPA based access layers. 
Add intergation with jpa to provide repository support for db operations without boilerplate coide

- Extends the JPA repository pattern by providing built in repository interfaces
- Automatic implementation for common operations (save, delete, fetch)


**Spring Data - Hibernate**

Hibernate is the most popular implementation of JPA specification
Spring can use HIbernate as a JPA provider

- JPA abstraction
Jpa data rely on Jpa specification, we can use hibernate as the orm implementation

- Hibernate implementation.
Hibernate will handle low level details of interacting with the database

- Spring Data JPA
Provides the repository pattern to abstract away the complexities of interacting with jpa, hibernate

- Spring framework
Manages the lifecycle of sessionFactory, Entity manager, injects dependenices, handles transactions



### Example Flow:

1. You define an **entity class** annotated with JPA annotations, which Hibernate will map to the database.
2. You create a **repository interface** extending `JpaRepository` or `CrudRepository`.
3. Spring Data JPA generates the implementation at runtime.
4. Hibernate, as the JPA provider, interacts with the database for CRUD operations.


**Lazy loading:** Fetch part of the data, not every linked item to it as well

**Eager fetching:** Fetch the entirety of the data at once, saving you from back and fourth operations

**Cascading** Delete child tables 

**Distributed Caching**


#### Hibernate With Spring

Setup LocalSessionFactory 

1. dataSource - connects to a DataSource bean
2. mappingResources - specifies Hibernate mapping files for persistence strategy
3. hibernateProperties - configures hibernate settings

1,3 specfy where to find db connection
we can specify all the app's peristent classes in the `AnnotatedClasses` property OR define `packagesToScan` to auto pick the annotated classes


Annotation-based mapping
```
@Bean 
public AnnotationSessionFactoryBean 
sessionFactory(DataSource ds) { 

AnnotationSessionFactoryBean sfb = new AnnotationSessionFactoryBean(); sfb.setDataSource(ds); 
sfb.setPackagesToScan(new String[] { "com.habuma.spittr.domain" }); Properties props = new Properties(); 

props.setProperty("dialect", "org.hibernate.dialect.H2Dialect"); sfb.setHibernateProperties(props); 

return sfb; 

}

```

Spring-tied hibernate ensures that only one session can be used per transaction

**JPA entity managers** (Interface for interacting with the database)

**Application managed** ->Entity managers are created when explicitly needed, used in standalnle apps

**Container managed**->Entity managers are managed by Java EE ,used when using java ee container

Injecting a repository with a proxy to Entity Manager

```
@Repository 
@Transactional 
public class JpaSpitterRepository implements SpitterRepository
	@Persistence
	Context private EntityManager em; 
	public void addSpitter(Spitter spitter) { 
		em.persist(spitter); 
} 

	public Spitter getSpitterById(long id) {
		return em.find(Spitter.class, id); 
} 

	public void saveSpitter(Spitter spitter) {
		em.merge(spitter); 
	}
}
```

jpa:repositories

given a package to scan, scans all classes thath extend jpa's repository interface, if found it generate an  implementation of that interface 
@EnableJpaRepositories to scan packages

e.g
provided the following class:

```
public interface SpitterRepository extends JpaRepository<Spitter, Long> {
    List<Spitter> findByUsername(String username);
}
```
spring jpa will automatically generate an implementation for this repository for comon methods like findAll, save, delete etc and create the corresponding queries based on custom methods

configured through the following xml 

```
<jpa:repositories base-package="com.habuma.spittr.db" />
```


spring jpa can read method name and split it down:

1. find,read,count,delete
2. ByName,ByAge ...

examples:
**findByUsername** ->SELECT * FROM Spitter WHERE username = ?
**findByUsernameAndAge** ->SELECT * FROM Spitter WHERE username = ? AND age = ?
**findByAgeGreaterThan** -> SELECT * FROM Spitter WHERE age > ?
**findByUsernameOrderByAgeDesc** ->SELECT * FROM Spitter WHERE username = ? ORDER BY age DESC

Also , you can add your customQuery 
```
@Query("SELECT s FROM Spitter s WHERE s.username = :username")
List<Spitter> findByUsernameCustom(@Param("username") String username);
```



Spring-config.xml VS applicationConfig.xml

**Spring-Config**
Used for spring core configs
Defines beans,services, repositories,controllers,etsc
Dependency injection rules
Application wide settings

**ApplicationConfig**
Application specific
Db configs
third party intergations
testing, prod, development configs
Third party configs (jpa, hibernate)
