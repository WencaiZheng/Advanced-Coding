# C++ Questions

## Pointer and dereference operator

```c++
 int x;
 int *p;  // * is used in the declaration:
          // p is a pointer to an integer, since (after dereferencing),
          // *p is an integer
 x = 0;
 // now x == 0
 p = &x;  // & takes the address of x
 // now *p == 0, since p == &x and therefore *p == x
 *p = 1;  // equivalent to x = 1, since p == &x
 // now *p == 1 and x == 1
```



## File Guards

file guards assure that when other files does not include this head file repeatedly. If no file guards, it will raise error when multiple files include this head file. 

```c++
#ifndef EURO_HPP
#define EURO_HPP
class euro
{
    // define the class
}
#endif
```



## Copy constructor & assignment operator

* The copy constructor generates a new instance of the object using the value passed in, while the assignment operator copies the value of an object to an existing instance.

## Static variable 

+ The space for the static variable is allocated only one time and this is used for the entirety of the program. Once this variable is declared, it exists till the program executes.

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



## Templates

```c++
template <typename T>
void print(T x)
{
    cout<<x<<endl;
}
void main()
{
    print(5.5);
}
```

## STL

### 

### Containers

```C++
int main() 
{ 
    vector<int> g1; 
    for (int i = 1; i <= 5; i++) 
        g1.push_back(i); 
    cout << "Output of begin and end: "; 
    for (auto i = g1.begin(); i != g1.end(); ++i) 
        cout << *i << " "; 
}
```

### Functions

### Algorithms

### Iterators



