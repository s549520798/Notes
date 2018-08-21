##Classes and objects

###Classes

class declarations can include these components, in order:  

1. Modifiers such as public, private, and a number of others that you will encounter later.
2. The class name, with the initial letter capitalized by convention.
3. The name of the class's parent (superclass), if any, preceded by the keyword extends. A class can only extend (subclass) one parent.
4. A comma-separated list of interfaces implemented by the class, if any, preceded by the keyword implements. A class can implement more than one interface.
5. The class body, surrounded by braces, {}.

There are several kinds of variables:

* Member variables in a class—these are called fields.
* Variables in a method or block of code—these are called local variables.
* Variables in method declarations—these are called parameters.

####Defining Methods
More generally, method declarations have six components, in order:
1. Modifiers—such as public, private, and others you will learn about later.
2. The return type—the data type of the value returned by the method, or void if the method does not return a value.
3. The method name—the rules for field names apply to method names as well, but the convention is a little different.
4. The parameter list in parenthesis—a comma-delimited list of input parameters, preceded by their data types, enclosed by parentheses, (). If there are no parameters, you must use empty parentheses.
5. An exception list—to be discussed later.
6. The method body, enclosed between braces—the method's code, including the declaration of local variables, goes here.

>Definition: Two of the components of a method declaration comprise the method signature—the method's name and the parameter types.(方法签名只由方法名和参数构成)

####Overloading Methods
he Java programming language supports overloading methods, and Java can distinguish between methods with different method signatures. This means that methods within a class can have the same name if they have different parameter lists (方法重载是根据方法签名个构成来区分：同一方法名可以存在多个不同参数的方法，应为根据方法签名的组成，他们属于不停的签名)

The compiler does not consider return type when differentiating methods, so you cannot declare two methods with the same signature even if they have a different return type.(重载于返回值无关)

the compiler automatically provides a no-argument, default constructor for any class without constructors. This default constructor will call the no-argument constructor of the superclass.

Parameters refers to the list of variables in a method declaration. Arguments are the actual values that are passed in when the method is invoked. When you invoke a method, the arguments used must match the declaration's parameters in type and order.

可变参数(varargs)
To use varargs, you follow the type of the last parameter by an ellipsis (three dots, ...), then a space, and the parameter name. The method can then be called with any number of that parameter, including none.
```
    public Polygon polygonFrom(Point... corners) {
    int numberOfSides = corners.length;
    double squareOfSide1, lengthOfSide1;
    squareOfSide1 = (corners[1].x - corners[0].x)
                     * (corners[1].x - corners[0].x) 
                     + (corners[1].y - corners[0].y)
                     * (corners[1].y - corners[0].y);
    lengthOfSide1 = Math.sqrt(squareOfSide1);

    // more method body code follows that creates and returns a 
    // polygon connecting the Points
}
```
note:传入的参数会被当做数组来对待

#####Passing Primitive Data Type Arguments
Primitive arguments, such as an int or a double, are passed into methods by value. This means that any changes to the values of the parameters exist only within the scope of the method. When the method returns, the parameters are gone and any changes to them are lost (String 类型也不会改变)
#####Passing Reference Data Type Arguments
Reference data type parameters, such as objects, are also passed into methods by value. This means that when the method returns, the passed-in reference still references the same object as before. However, the values of the object's fields can be changed in the method, if they have the proper access level. （数组同样受影响）

###Objects

1. **Declaration**: The code set in bold are all variable declarations that associate a variable name with an object type.
2. **Instantiation**: The new keyword is a Java operator that creates the object.(实例化)
3. **Initialization**: The new operator is followed by a call to a constructor, which initializes the new object.(初始化)

####Declaring a Variable to Refer to an Objects
####Instantiating a Classes
The new operator instantiates a class by allocating memory for a new object and returning a reference to that memory运算符通过为new 操作符分配内存并返回对该内存的引用来实例化一个类。
The new operator also invokes the object constructor.
The new operator returns a reference to the object it created. This reference is usually assigned to a variable of the appropriate type,
The reference returned by the new operator does not have to be assigned to a variable. It can also be used directly in an expression
####Initializing an Object


###Controlling Access to Members of a Class
There are two levels of access control:
* At the top level—public, or package-private (no explicit modifier).
* At the member level—public, private, protected, or package-private (no explicit modifier).

|  Modify | Class | Package | Subclass | World |
|---------|-------|---------|----------|-------|
| public  |   Y   |    Y    |    Y     |   Y   |
| private |   Y   |    N    |    N     |   N   | 
|no modify|   Y   |    Y    |    N     |   N   |
|protected|   Y   |    Y    |    Y     |   N   |

这里的subclass是指在另外包内的子类


##Interface and Inheritance

###Inheritance
A class that is derived from another class is called a subclass (also a derived class, extended class, or child class). The class from which the subclass is derived is called a superclass (also a base class or a parent class).
Excepting *Object*, which has no superclass, every class has one and only one direct superclass (single inheritance). In the absence of any other explicit superclass, every class is implicitly a subclass of *Object*.

Instance methods are preferred over interface default methods

Modifiers
The access specifier for an overriding method can allow more, but not less, access than the overridden method. For example, a protected instance method in the superclass can be made public, but not private, in the subclass.

###Numbers and Strings
####Numbers
