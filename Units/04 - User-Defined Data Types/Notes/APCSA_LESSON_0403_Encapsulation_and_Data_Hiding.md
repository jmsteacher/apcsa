Unit 04: User-Defined Data Types, _An Introduction to Object-Oriented-Programming_\
Lesson 03: Encapsulation & Data Hiding
***

Definitions
---

**Definition: Encapsulation**

_Encapsulation_ is an object-oriented-programming concepts that suggests data and the methods that operate on that data should be "bound together" within the same class. _Encapsulation_ prevents the misuse of or interference with the data.

**Definition: Data Hiding**

_Data or Information Hiding_ is a concept closely related to the concept of _encapsulation_. In particular, it states that data should be hidden from view from parts of a system other than those objects directly responsible for the data. Access to data, therefore, should happen only through the responsible objects.

The `private` Java Keyword
---
In Java, attributes can be marked as `private`. This indicates that only objects of the specific class should be allowed to access information stored in those attributes. The following implements the `Human` class using private attributes.

    class Human {
        private String name, gender;
        private int age;
        private double height;

        // The rest of the class implementation is not shown...
    }

Notice that "hiding information" is as simple as adding the `private` keyword during attribute declaration.

***
**Exercise:** Instantiate a `Human` object after adding the `private` keyword as in the example above. Try to access the attributes of your object; what error occurs? Why does this error occur?
***

Implementing "Getters" and "Setters"
---
Because an object's attributes will be hidden using the `private` keyword, access to the information stored within them must be explicitly allowed via what is known as a _getter method_. 

`public` vs. `private` Methods
---
