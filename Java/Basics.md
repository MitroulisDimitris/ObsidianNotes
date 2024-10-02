Folder structure in default build:


```
project-root/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/
│   │   │       └── example/
│   │   │           └── app/
│   │   │               └── Main.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── app/
│       │               └── MainTest.java
│       └── resources/
│           └── test-config.properties

```
scr/main/java contains java source code.
Directory structure under src.main.java should mirror the package structure of java classes

if package is com.exampe.app, should be located at scr/main/java/xom/example/app

