Build automation tool 
Manages: dependencies, compile, packaging, test, more
Uses xlm configuration **pom.xlm** to describe the given project

Features: 
- Downloads/manages dependencies
- Compiles,testspackages,deploys code
- Standardized directory structure
- Plugins
- Build lifecycle (Create and run a pipeline on project run)


Used for:
- Large projects
- CI/CID
-  Extend Vanilla Java

**Project Structure:**
```
my-app/
├── pom.xml
└── src/
    ├── main/
    │   └── java/
    └── test/
        └── java/

```

### **Maven lifecycle commands:** 

- **Clean**: removes all files from previous builds 
- **Validate**: Checks if the project is correct and all necessary information is availabe
- **Complile**: Compiles source code
- **Test**: Runs unit tests (Do not require code deployment)
- **Package**: Packages compiled code in a jara/war
- **Verify**: Runs all checks to verify validity of project
- **Install**: Installs the package into local mvn repo
- **Site**: Creates documentation for the project based on source code and configutaion
- **Deploy**: Copies the final package to a remote repo so that it can be deployed/used elsewere etc.

