# java9-jigsaw-documentation

## Hello world example

We followed https://dzone.com/articles/a-javafx-helloworld-using-java-9s-project-jigsaw-i example to make a module and expose the package containing a main module.

How to structure the modules in IntelliJ is not entirely clear yet.

## What we do know

Each module must define a module-info.java.
Example
```
           module com.mycompany.helloworld {
               requires javafx.base;
               requires javafx.graphics;
               requires javafx.controls;
               exports com.mycompany.helloworld;
           }
```

A module can be looked at as a good old java-jar. The main difference with Java 8 is that you can choose which packages to expose and use,
defining a more fine-grained access control.

* **module**: the module definition file starts with this keyword followed by its name and definition
* **requires**: is used to indicate the modules it depends on; a module name has to be specified after this keyword
* **transitive**: is specified after the requires keyword; this means that any module that depends on the module defining requires transitive \<modulename> gets an implicit dependence on the \<modulename>
* **exports**: is used to indicate the packages within the module available publicly; a package name has to be specified after this keyword
* **opens**: is used to indicate the packages that are accessible only at runtime and also available for introspection via Reflection APIs; this is quite significant to libraries like Spring and Hibernate, highly rely on Reflection APIs; opens can also be used at the module level in which case the entire module is accessible at runtime
* **uses**: is used to indicate the service interface that this module is using; a type name, i.e., complete class/interface name, has to specified after this keyword
* **provides … with ...**: they are used to indicate that it provides implementations, identified after the with keyword, for the service interface identified after the provides keyword

See also http://www.baeldung.com/project-jigsaw-java-modularity