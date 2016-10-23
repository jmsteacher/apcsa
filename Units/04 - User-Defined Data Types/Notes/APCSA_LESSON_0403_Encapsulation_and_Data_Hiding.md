Unit 04: User-Defined Data Types, _An Introduction to Object-Oriented-Programming_

Lesson 03: Encapsulation & Data Hiding
***

Definitions
---

**Definition: Encapsulation**

_Encapsulation_ is an object-oriented-programming concepts that suggests data and the methods that operate on that data should be "bound together" within the same class. _Encapsulation_ prevents the misuse of or interference with the data.

**Definition: Data Hiding**

_Data or Information Hiding_ is a concept closely related to the concept of _encapsulation_. In particular, it states that data should be hidden from view from parts of a system other than those objects directly responsible for the data. Access to data, therefore, should happen only through the responsible objects.
***

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

Here is a simple _getter method_ for the `Human` class:

    public String getName() {
        return name;
    }

You might be asking yourself, **what's the point of restricting access to the `name` attribute if you are just going to implement a `getName()` method?** To answer this, consider the `getAge()` method below:

    public int getAge() {
        if ((age > 25) && (gender == "female"))
            return 25;
        return age;
    }

This is a somewhat silly example, but it demonstrates a very important concept: by restricting access to an attribute's value except through a _getter_ method, you control exactly how the value is accessed! This includes restricting access under certain circumstances, such as a password not being entered correctly or an accessing client not having proper clearance to view the information.

A _setter method_ works much the same way, allowing individual attributes to be set via a method. This allows for data checking, transformations, etc. Consider the `setName()` method below:

    public void setString(String name) {
        name = name.trim();
        if (name.indexOf(" ") < 0)
            System.out.println("You must also include a surname!");
        else
            this.name = name;
    }

This example shows that we can first check for correct values (in this case, using the existance of a blank space to indicate the presence of both a first and last name) before allowing data to be assigned to an object's attribute.

_Note:_ There will often be times where you create a _getter_ method without a corresponding _setter_ method or vice versa. Additionally, you can create "phantom" attributes by creating _getter_ methods that return calculated values. For instance, consier the following method:

    public int getYearOfBirth() {
        return java.time.Year.now() - age; 
    }

Ignoring the obvious logic error in the method above, we can see that a `Human` object now has a calculated attribute: `YearOfBirth`, even though it does not contain any stored data to that effect. 

By forcing clients of our class to access attributes via _getter_ and _setter_ methods, we effectively hide implementation details of our attributes, as well as ensure proper access (both in obtaining and setting values). These benefit is well worth the added work of creating these methods for each of our attributes (or at least the ones we want to provide access to).
***

`public` vs. `private` Methods
---

You'll have noticed by now that all of our methods have been prefixed with the `public` keyword. Unsurprisingly, this means we can also make `private` methods.

Although there are a few use for which this might be useful, the most common is in the creation of "helper" methods. Suppose, for instance, that we want to ensure our `name` attribute is in "titlecase" (first letter of each word capitalized). In that case, we might create a `toTitleCase()` method as follows:

    private String toTitleCase(String str) {
        str = str.trim().toLowerCase();
        String[] substrs = str.split(" ");
        str = "";

        for (String substr : substrs) {
            str += Character.toUpperCase(substr.charAt(0)) + substr.substring(1) + " ";
        }

        return str;
    }

This method will be available to any parts of the `Human` class; however, because it is `private`, it will not be able to be invoked from outside the class.

**Why would you want to do this?** It's a simple case of allowing programmers the freedom to divide their tasks into as many different helper methods as they deem necessary without exposing those implementation details to clients of the created class. `toTitleCase()` is not a behavior of a `Human`, so there is no need to allow clients of the `Human` class to access it.

***
**Excercise:** From our work with classes in the past, you'll note that our class _constructors_ are also prefixed by the `public` keyword. What would the effects of making a `private` constructor be? Can you imagine any instances when you'll want to make a constructor `private`?
***

UML Digrams: Private Attributes & Methods
---

Private attributes with _getter_ and/or _setter_ methods are often included in the corresponding UML class diagram. To denote these attributes are private, the "+" before each is replaced with a "-". Attributes without any external way of accessing them are used for internal implementation only and, so, are often not included in the class diagrams.

Private methods are almost never included in a class diagram; however, if they are, the same change from a "+" to a "-" occurs.

***
**Exercise:** Modify the `Human` class diagram developed in previous lessons to reflect our change to `private` attributes.
***