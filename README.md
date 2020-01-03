# quarkus-test-reflect-method-not-found

Test case for Quarkus test running into a ClassNotFoundException for java.lang.reflect.Method

This project is the getting-started project from the guide with two additional dependencies:
* io.quarkus:quarkus-hibernate-orm
* de.gedoplan:baselibs-persistence:1.8

The latter is a small utility library from our maven repository http://service.gedoplan.de/nexus/content/groups/public. Its source is deployed there, too.

Both additional dependencies are not used in the project at all, but they seem to cause an exception when running test:

$ mvn test
[INFO] Scanning for projects...
[INFO]
[INFO] -----------< org.acme:quarkus-test-reflect-method-not-found >-----------
[INFO] Building quarkus-test-reflect-method-not-found 1.0-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ quarkus-test-reflect-method-not-found ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 2 resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:compile (default-compile) @ quarkus-test-reflect-method-not-found ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ quarkus-test-reflect-method-not-found ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory C:\GEDOPLAN\projects\gedoplan\issues\quarkus-test-reflect-method-not-found\src\test\resources
[INFO]
[INFO] --- maven-compiler-plugin:3.8.1:testCompile (default-testCompile) @ quarkus-test-reflect-method-not-found ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- maven-surefire-plugin:2.22.1:test (default-test) @ quarkus-test-reflect-method-not-found ---
[INFO]
[INFO] -------------------------------------------------------
[INFO]  T E S T S
[INFO] -------------------------------------------------------
[INFO] Running org.acme.quickstart.GreetingResourceTest
15:04:18,709 INFO  [org.jbo.threads] JBoss Threads version 3.0.0.Final
15:04:18,887 WARN  [io.qua.agr.dep.AgroalProcessor] Agroal dependency is present but no driver has been defined for the default datasource
15:04:18,934 INFO  [org.hib.jpa.boo.int.PersistenceXmlParser] HHH000318: Could not find any META-INF/persistence.xml file in the classpath
15:04:19,175 INFO  [org.hib.Version] HHH000412: Hibernate Core {5.4.10.Final}
[ERROR] Tests run: 1, Failures: 0, Errors: 1, Skipped: 0, Time elapsed: 4.612 s <<< FAILURE! - in org.acme.quickstart.GreetingResourceTest
[ERROR] testHelloEndpoint  Time elapsed: 0 s  <<< ERROR!
org.junit.jupiter.api.extension.TestInstantiationException: TestInstanceFactory [io.quarkus.test.junit.QuarkusTestExtension] failed to instantiate test class [org.acme.quickstart.GreetingResourceTest]: Type java/lang/reflect/Method not present
Caused by: java.lang.TypeNotPresentException: Type java/lang/reflect/Method not present
Caused by: java.lang.ClassNotFoundException: java.lang.reflect.Method

If the dependencies are deleted from pom.xml, the tests run OK.

If Quarkus version 1.0.0.Final is used instead of 1.1.0.Final, the tests run OK.

