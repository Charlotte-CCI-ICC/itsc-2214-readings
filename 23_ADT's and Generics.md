---
title: Abstract Data Types and Generics
---

In computer science, Abstract Data Types (ADTs) and generics are foundational concepts that allow for the creation of flexible, reusable, and robust software. ADTs provide a theoretical framework for data structures, focusing on what operations are possible and what their behaviors are, while generics enhance the flexibility and reusability of code by allowing data structures and algorithms to operate on different types without sacrificing type safety. The chapter starts by introducing the concept of data types and their importance in programming. It explains how data is stored as bits (0s and 1s) on computers and how data types provide a way to interpret these bits in a specific manner, allowing programmers to work with higher-level concepts like numbers, strings, or custom data structures.

## Abstract Data Types (ADTs)

An Abstract Data Type (ADT) is a mathematical model for data types. It defines a data structure in terms of its behavior from the point of view of a user, specifically in terms of possible values and operations on the data, without considering how these operations are implemented.

1. **Encapsulation**: ADTs encapsulate data and the operations that can be performed on the data. This means users interact with the data only through a specified set of operations.
2. **Abstraction**: ADTs provide a level of abstraction that allows users to manipulate the data without needing to understand the underlying implementation.
3. **Interface and Implementation Separation**: The definition of an ADT includes a clear distinction between the interface (the set of operations) and the implementation (how the operations are performed).

There are some limitations of working with fixed data types, as programmers often need to write separate implementations of the same operations for different data types, even when the operations are conceptually similar. This leads to code duplication and increased effort. To address this issue, the idea of introducing a placeholder type (called "AnyType") that can represent any data type. This would allow programmers to write generic code that can work with various data types without needing separate implementations. However, the potential issues with this approach, such as ensuring the validity of operations performed on the placeholder type and the methods that can be called on it. The presenter explores possible solutions, like constraining the placeholder type to only work with types that support certain operations or implement specific traits/interfaces.

Below we discuss the different types of data types, placeholder etc. 

1. Data Types
   
   | Data Type                    | Description                                                              |
   | ---------------------------- | ------------------------------------------------------------------------ |
   | Primitive Data Types         | Built-in data types like `short`, `int`, `long`, `char`, etc.            |
   | Reference/User-defined Types | Any class created by the programmer is a reference or user-defined type. |

2. Perspectives on Data Types

   | Perspective                   | Description                                                                                             |
   | ----------------------------- | ------------------------------------------------------------------------------------------------------- |
   | User/Programmer's Perspective | Data types allow encapsulation, code reuse, and implementation of concepts like numbers or collections. |
   | Compiler's Perspective        | Data types help the compiler keep track of how to interpret and operate on different bit patterns.      |

3. Limitations of Fixed Data Types

   | Limitation          | Description                                                                                                                                  |
   | ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
   | Code Duplication    | Programmers need to write separate implementations for the same operations on different data types, even when they are conceptually similar. |
   | Lack of Reusability | It's difficult to write generic code that can work with various data types without duplication.                                              |

4. Potential Issues with a Placeholder Type (AnyType)

   | Issue                | Description                                                                                                                 |
   | -------------------- | --------------------------------------------------------------------------------------------------------------------------- |
   | Invalid Operations   | Ensuring that the operations being performed on the placeholder type are valid for all the types it represents.             |
   | Incompatible Methods | Ensuring that the methods being called on the placeholder type are present and compatible with all the types it represents. |

5. Examples of Trait Constraints in Rust

   ```rust
   fn add<AnyType: Add>(a: AnyType, b: AnyType) -> AnyType
     where AnyType: Add<Output = AnyType>
   {
     a + b
   }
   ```

   ```rust
   fn math<T>(a: T, b: T, c: T) -> T
     where
       T: Add<Output = T> + Mul<Output = T> + Sub<Output = T> + Div<Output = T>,
   {
     (a + b) * (c - a) / b
   }
   ```
   
 ## Generics
   
Generics enable the definition of classes, interfaces, and methods with placeholders for types that can be specified later. This allows for the creation of components that can operate on different types while ensuring type safety at compile time.

## Benefits of Generics
1. **Type Safety**: Generics provide compile-time type checking, reducing the likelihood of runtime errors.
2. **Code Reusability**: Generics allow for the creation of functions and classes that can operate on any data type, making code more reusable.
3. **Performance**: Using generics can eliminate the need for type casting and boxing/unboxing, leading to better performance.

###Generic Classes
A generic class is a class that can operate on objects of various types. For example, a generic Box class might look like this in Java:

```java
public class Box<T> {
    private T content;

    public void setContent(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }
}
```
In this example, T is a type parameter that will be replaced with a specific type when an instance of Box is created.


###Generic Methods
A generic method is a method that can operate on objects of various types. Here's an example of a generic method in Java:

```java
public <T> void printArray(T[] array) {
    for (T element : array) {
        System.out.println(element);
    }
}

```
In this example, T is a type parameter that will be replaced with a specific type when an instance of Box is created.

###Bounded Type Parameters
Sometimes it's useful to limit the types that can be used as type arguments. This is done using bounded type parameters. For example, if a method should only accept instances of Number or its subclasses, it can be defined as follows:

```java
public <T extends Number> void process(T number) {
    System.out.println(number.doubleValue());
}

```
###Generics in Collections
Generics are heavily used in the Java Collections Framework, which includes classes like ArrayList, HashMap, and HashSet. For instance, an ArrayList of strings is declared as follows:

```java
ArrayList<String> stringList = new ArrayList<>();
```
This ensures that only String objects can be added to the list, providing type safety.

digraph G {
    node [shape=record, fontname=Helvetica, fontsize=10];
    edge [fontname=Helvetica, fontsize=10];

    GenericClass [label="{GenericClass|+ genericMethod(T extends t)}"];
    Interface [label="{Interface|+ method1()\l+ method2()\l}"];
    ConcreteClass [label="{ConcreteClass|+ method1()\l+ method2()\l+ method3()\l}"];

    GenericClass -> Interface [arrowhead=empty, arrowtail=none];
    ConcreteClass -> Interface [arrowhead=empty, arrowtail=none];
}

This diagram shows a generic class GenericClass that takes a type parameter T with a type bound Interface. The Interface defines two methods, method1 and method2, which must be implemented by any concrete class that serves as a type argument for GenericClass, such as ConcreteClass.



Abstract Data Types and generics are fundamental concepts in computer science that enhance the design and implementation of flexible, reusable, and type-safe software components. ADTs focus on defining what operations can be performed on data, abstracting away the implementation details. Generics, on the other hand, allow these operations to be applied to different types without compromising type safety. Together, they provide powerful tools for building robust software systems.

