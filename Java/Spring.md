Open source framework
Features like:
- Dependency injection
- Aspect oriented programming
- Microservices
- Tools for web applications
Spring is widely used in enterprise environments because it reduces boilerplate code, encourages best practices, and is flexible for various use cases.

**Sping boot**
Framework built upon the Spring that simplifies the development of java based web applications

1. Autoconfiguration: Automatically configures the app based on given dependencies
2. Embedded servers: Comes with embedded servers (Tomcat, Jetty)
3. Convention over Cenfiguration: Embraces the principle of providing default configurations for common tasks
4. Microservices: Used widely for microservices
5. Starter POMs: Provides starter dependencies


### Spring In Action (Book)

Pojos

DI enables for object to be given their dependencies at creation time by a third party
Objects aren't expected to create/obtain these dependencies

**Constructor injections** -> Dependencies on constructor 
**Wiring** ->Act of creating associations between application components

---
**Beans** ->Object that's instantiated,managed,configured by the Spring IoC container
Beans are defined using config metadata:
- XML config
- Java Annotations (@Component, @Service, @Repository, @Bean)
- Java Config Classes (@Configuration.@Bean)
By default singletons


**Bean Lifecycle**
![[Pasted image 20241008141505.png]]

1. Spring instantiates the bean. 
2. Spring injects values and bean references into the bean’s properties. 
3. If the bean implements BeanNameAware, Spring passes the bean’s ID to the setBeanName() method. 
4. If the bean implements BeanFactoryAware, Spring calls the setBeanFactory() method, passing in the bean factory itself. 
5. If the bean implements ApplicationContextAware, Spring calls the setApplicationContext() method, passing in a reference to the enclosing application context. 
6. If the bean implements the BeanPostProcessor interface, Spring calls its postProcessBeforeInitialization() method. 
7. If the bean implements the InitializingBean interface, Spring calls its afterPropertiesSet() method. Similarly, if the bean was declared with an initmethod, then the specified initialization method is called. 
8. If the bean implements BeanPostProcessor, Spring calls its postProcessAfterInitialization() method. 
9. At this point, the bean is ready to be used by the application and remains in the application context until the application context is destroyed. 
10. If the bean implements the DisposableBean interface, Spring calls its destroy() method. Likewise, if the bean was declared with a destroy-method, the specified method is called

**Properties:**
- All beans are given an ID
By using @Named(\*CustomName\*) or @Component(\*CustomName\*)

@ComponentScan annotation suggests thath Spring **should** scan for Components,Service, repository and Controller annotations 

@Autowire/@Inject -> Automatically resolve dependencies into a class
Works on classes, methods. 
set (**required=false**) to not throw error when not finding dependencies



**Application Context** loads bean definitions and wires them together.
Is the Central interface to Spring IoC container


```
package com.springinaction.knights; 
import org.springframework.context.support. 

ClassPathXmlApplicationContext; 

public class KnightMain { public static void main(String[] args) throws Exception { 
	ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext( "META-INF/spring/knight.xml"); 
	Knight knight = context.getBean(Knight.class); knight.embarkOnQuest(); context.close(); 
	} 
}
```

**Aspects**
Captures functionality that's used thoughout the application

**Templates** eliminate duplicate, boilerplate code

```
public Employee getEmployeeById(long id) { 

return jdbcTemplate.queryForObject( "select id, firstname, lastname, salary " + "from employee where id=?", new RowMapper() { 

public Employee mapRow(ResultSet rs, int rowNum) throws SQLException { 

Employee employee = new Employee(); employee.setId(rs.getLong("id")); employee.setFirstName(rs.getString("firstname")); employee.setLastName(rs.getString("lastname")); employee.setSalary(rs.getBigDecimal("salary")); 
return employee;  
} 
}, id);
```

In spring applications, Objects live in the ==Spring container==
**Container** creates, wires, configures objects together


Bean Factories (low level)

Application Contexts(Prefered)


Load application context using `FileSystemXmlApplicationContext` 

### Spring framework preinstalled ibraries
![[Pasted image 20241008141929.png]]


## Implementation

 Automatic bean wiring:
- Component scanning -> Automatically discovers Beans, creation in application context
- Autowiring ->Auto satisfaction of bean dependencies

```
@Component public class SgtPeppers implements CompactDisc { 

	private String title = "Sgt. Pepper's Lonely Hearts Club Band"; 
	private String artist = "The Beatles"; public void play() { System.out.println("Playing " + title + " by " + artist); 
	} 
}
```

With the `@Component` Annotation, Spring will configure a SgtPeppers Bean



---

### Configuration Classes

  
```
package soundsystem; 
import org.springframework.context.annotation.Configuration; 

@Configuration public class CDPlayerConfig { }
```

---

### Annotations

@Component
Spring-managed componend (Bean)
Used on any class to mark it for component scanning

@Controller
Marks a class as a web controller. web request handler

@Service
Holds Bussness logic, service layer componend
is a specialization of @Component

@Repository
Data Access Object,  interacts with database
Specialization of @Component, provides automatic database related exceptions, transactions

@Autowired
Injects class dependencies automatically
Used in Fields, constructors, setters

@Qualifier
Specifieas the excact bean to inject when ambiguity arises

```
@Autowired
@Qualifier('SpecificService')
private Service my Service;
```

@Bean
Declares a method as a Spring Bean provider
Used in config classes to define beans

```
@Bean
public MyService myService(){
	return new MyServiceImpl;
}
```

@Configuration
Indicates that a Class declares one or more @Bean methods
To define application level configurations

@Transactional
Mark a method for transaction managment
When applied to a class, method spring creates a transaction around the method, handling rollback logic
Options:
	- Propagation ->required,requires_new
	- isolation -> Read_commited,serializable
	- timeout
	- readOnly


@RestController
Marks a class as a RESTful 


@RequestMapping
Map to Urls

@PathVariable
Extracts values from the URI path
```
@RequestMapping("/user/{id}")
public String getUser(@PathVariable("id") String id) { ... }

```


@RequestParam
Extracts query parameters from the request URL
```
@RequestMapping("/search")
public String search(@RequestParam("q") String query) { ... }

```

@ExceptionHandler
Handles exceptions thrown from Controller methods

