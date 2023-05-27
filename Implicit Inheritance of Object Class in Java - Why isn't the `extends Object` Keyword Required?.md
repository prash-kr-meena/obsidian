In Java, every class implicitly extends the `Object` class if no explicit inheritance is specified using the `extends` keyword. The `Object` class is the root class of all classes in Java, and it provides a set of common methods and behaviors that are inherited by all other classes.

The reason why you don't see the `extends Object` keyword explicitly mentioned in your code is because it is optional. If you don't provide an explicit superclass using the `extends` keyword, Java assumes that your class inherits from `Object` by default.

Here's an example to illustrate this:

javaCopy code

``` java
public class MyClass {     
	// Class implementation 
}
```


In the above code, the `MyClass` implicitly extends the `Object` class, even though it's not explicitly mentioned.

You can confirm this by checking the Java Language Specification (JLS), which defines the syntax and semantics of the Java programming language. According to JLS Section 8.1.4:

> If a class declaration does not declare an explicit superclass, then it implicitly declares `Object` as the superclass.

You can refer to the Java Language Specification for more detailed information:

-   [Java Language Specification, Section 8.1.4: Superclasses and Subclasses](https://docs.oracle.com/javase/specs/jls/se16/html/jls-8.html#jls-8.1.4)

Additionally, you can also check the Java API documentation for the `Object` class, which describes the methods and behaviors inherited by all Java classes:

-   [Java Platform SE 16 API Specification: java.lang.Object](https://docs.oracle.com/en/java/javase/16/docs/api/java.base/java/lang/Object.html)