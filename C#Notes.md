# Basic

Under .Net framework, everything is an object.

string 

```c#
//string is refrence type, behave like value type
```



ref and out

```c#
public void aa(a)
{
	a = 2;
}
// if no keyword ref or out, the local variable a is copy by value
```



Struct and Class

```c#
public Struct A;
var a = new A();
//a is the value type
punlic Class A;
var a = new A();
//a is the reference type
```



Switch statement:

```c#
Switch(a)
{
    case var d when d>=90:
    	result = 'A';
    	break;
    case var d when d>=80:
    	result = 'B';
    	break;
}
```

throw and catch exception

```c#
throw new ArgumentException($"Invalid {nameof(grade)}");
```

```c#
try
{
    abc;
}
catch(Exception ex)//catch any type of Exception
{
    Console.WriteLine(ex.Message);
}    
catch(ArgumentException ex)//catch Argument Exception
{
    Console.WriteLine(ex.Message);
}   
```

```c#
try
{
    abc;
}
catch(FormatException ex)//catch Format Exception
{
    Console.WriteLine(ex.Message);
}    
catch(ArgumentException ex)//catch Argument Exception
{
    Console.WriteLine(ex.Message);
}
finally
{
    console.WriteLine("**")
}
```

property or field

```c#
public string Name//property
{
	get;
    private set;
}
public string Name;//field
readonly string Name;
const string NAME;//All Cap 
```

delegate and multi-cast delegates

```c#

```

Event

 add event or substract an event

```

```

# OOP

Encapsulation, Inheritance, Polymorphism

```c#
public class Child:People
{
    public Child(string name):base(name)
}
```

interface

```c#
public interface IBook
{
    //...
}
```

abstract and virtual

```c#
public abstract class Book:
{
    public virtual event ABCDelegate ABC;
    public abstract void Aa(double a);
    public override Bb(double b);
}
//child class need to override all the abstract method from base class
```

using

```c#
using()
{
    //..
}//tell .Net to dispose the object after using it
```

non-nullable reference type

```c#
Book? onebook = null;
```

static member

The static member is callable on a class even when no instance of the class has been created. The static member is always accessed by the class name, not the instance name. Only one copy of a static member exists, regardless of how many instances of the class are created. Static methods and properties cannot access non-static fields and events in their containing type, and they cannot access an instance variable of any object unless it's explicitly passed in a method parameter.

Static methods can be overloaded but not overridden, because they belong to the class, and not to any instance of the class.