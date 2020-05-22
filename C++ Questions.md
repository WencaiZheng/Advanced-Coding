# C++ Questions

## Static variable 

+ The space for the static variable is allocated only one time and this is used for the entirety of the program. Once this variable is declared, it exists till the program executes.
+ 

## Constructor

* A function which every time the class initialization will be called. It is pretty much like a `__init__()` in python
* There is a default constructor if not defined
* Override the constructors as you like



## Abstract class: 

+ Declared abstract
+  Cannot be instantiated, but they can be derived

```C++
class Shapes   //抽象类
{
protected:
    int x, y;
public:
    void setvalue(int d, int w=0){x=d;y=w;}
    virtual void disp()=0;//纯虚函数
};
```



## Overloading & Overriding

+ Overloading occurs when two or more methods in __one__ class have the __same method name__ but different parameters. 
+ Overriding means having two methods with the __same method name and parameters__ (eg method signature). One of the methods is in the parent class and the other is in the child class. Derived class function can override the base class function

## Ternary Operators

```c++
if (x>3)
    y=2;
else
    y=1;
static int y = x>3?2:1;
```



## Unique Pointer





## Smart Pointer





## sort the dictionary by its keys



