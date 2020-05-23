# C++ Questions

## Call by reference / value

always pass the object use `const` call by reference

```c++
void PrintString(const string& string)
{
    std::cout<<string<<std::endl;
}
```

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

## Dynamic allocation

ask for a specific block of memory ahead of time, new is an operator

```c++
class Entity
{    
 //   
}
int* b = new int[50]; // array with 4*50 bytes and the address of which is b
Entity* e = new Entity(); // this will call the constructor
Entity* e = (Entity*)malloc(sizeof(Entity)); //do the same above but no calling constructor
delete[] b; //release the address in the heap
delete e; //call the destructor
```

## Function template

```C++
template <typename T>]
void print(T x)
{
    std::cout<<x<<endl;
}
```

## Class template

```C++
template <class T>
class Stack { 
  private: 
    vector<T> elems;     // 元素 
 
  public: 
    void push(T const&);  // 入栈
    void pop();               // 出栈
    T top() const;            // 返回栈顶元素
    bool empty() const
    {       // 如果为空则返回真。
        return elems.empty(); 
    } 
}; 
template <class T>
void Stack<T>::push (T const& elem) 
{ 
    elems.push_back(elem);    
} 
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

## Inheritance and Polymorphism

- When derived class overrides the base class, the function of the base needs to be virtual. If there is not meaning to instantiate the base class, the class should be set to abstract class, because it includes pure virtual function. 

```C++
class Shapes
{
    protected:
    int x, y;
    public:
    void setvalue(int d, int w=0){x=d;y=w;}
    virtual void disp()=0;//pure virtual
};
```

- polymorphism means the multiple derived classes override the based class's virtual function in different ways.

```C++
class Shape {
protected:
	int width, height;
public:
	Shape(int a = 0, int b = 0)
	{width = a; height = b;}
	virtual int area() = 0;
};
class Rectangle : public Shape {
	public:
		Rectangle(int a = 0, int b = 0) :Shape(a, b) { }
		int area() { return (width * height); }
	};
class Triangle : public Shape{
public:
	Triangle(int a = 0, int b = 0) :Shape(a, b) { }
	int area() { return (width * height / 2); }
};
```

## Encapsulation 

```c++
class Adder{
   public:
      // 构造函数
      Adder(int i = 0)
      {
        total = i;
      }
      // 对外的接口
      void addNum(int number)
      {
          total += number;
      }
      // 对外的接口
      int getTotal()
      {
          return total;
      };
   private:
      // 对外隐藏的数据
      int total;
};
int main( )
{
   Adder a;
   
   a.addNum(10);
   a.addNum(20);
   a.addNum(30);
 
   cout << "Total " << a.getTotal() <<endl;
   return 0;
}
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

## Static member and static member function

- Static member always have one copy no matter how many instances are initialized. 
- The static member are shared in all the objects.  
- Can't initialize the static member inside class, only allowed outside using ::, if no initialization, it is at first object being created.
- if announce function as static, it could be used without creating any object.
- static member function cannot use this pointer, can only access to static member and other static member functions.

```C++
class Box
{
   public:
      static int objectCount;
      // 构造函数定义
      Box(double l=2.0, double b=2.0, double h=2.0)
      {
         cout <<"Constructor called." << endl;
         length = l;
         breadth = b;
         height = h;
         // 每次创建对象时增加 1
         objectCount++;
      }
      double Volume()
      {
         return length * breadth * height;
      }
      static int getCount()
      {
         return objectCount;
      }
   private:
      double length;     // 长度
      double breadth;    // 宽度
      double height;     // 高度
};
// 初始化类 Box 的静态成员
int Box::objectCount = 0;
int main(void)
{
   cout << "Final Stage Count: " << Box::getCount() << endl;//0
   Box Box1(3.3, 1.2, 1.5);    // 声明 box1
   Box Box2(8.5, 6.0, 2.0);    // 声明 box2
   // 输出对象的总数
   cout << "Total objects: " << Box::objectCount << endl;// 2 
   return 0;
}
```





## Singleton

Initiated once only, such as random number generator. It is used to organize a bunch of global variables and include them in a single name space. Similar to using a namespace.

```c++
class Singleton
{
    public:
    Singleton(const Singleton&) = delete;//copy constructor as delete
    static Singleton& Get()
    {
        return s_Instance;
    }
    void Function() {}
    private:
    Singleton() {}
    static Singleton s_Instance;
}
Singleton Singleton::s_Instance;
int main()
{
    Singleton::Get().Function();
}
```





## Unique Pointer





## Smart Pointer





## 

## STL

Four kinds

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

```C++
list<string> mylist({ "3","2" });
mylist.sort();
```



### Functions

### Algorithms

```C++ #include <algorithm>
#include <algorithm>
int myarray[5] = { 1,9,2,22,3 };
vector<int> myvector(myarray, myarray + 4);
sort(myvector.begin(), myvector.end());
list<string> mylist({ "3","2" });
mylist.sort();
```

### Iterators



