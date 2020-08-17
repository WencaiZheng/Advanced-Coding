# C++ Notes

# Basics

## Type size

| Type                                                   | Size        |
| ------------------------------------------------------ | ----------- |
| bool, char, unsigned char, signed char, __int8         | 1 **byte**  |
| __int16, short, unsigned short, wchar_t, __wchar_t     | 2 **bytes** |
| float, __int32, int, unsigned int, long, unsigned long | 4 **bytes** |
| **double**, __int64, long **double**, long long        | 8 **bytes** |

## Call by reference / value

always pass the object use `const` call by reference

```c++
void PrintString(const string& string)
{
    std::cout<<string<<std::endl;
}
```

## Pointer 

- Derived class pointer cannot point to base class
- Pointer to a constant: cannot change the value that is pointed at.

```C++
const double taxRates[] = {0.65, 0.8, 0.75};
const double *ratePtr; // ratePtr points to a const double value
```

- Constant pointer: address in pointer cannot change once pointer is initialized.

  * Must be initialized when defined

  - Can be used without initialization as a function parameter
  - Initialized by argument when function is called
  - Function can receive different arguments on different calls
  - While the address in the pointer cannot change, the data at that address may be changed

```c++
int classSize = 24;
int * const classPtr = &classSize; //
```

```c++
 int x;
 int *p;  // * is used in the declaration:
          // p is a pointer to an integer, since (after dereferencing),
          // *p is an integer
 x = 0; // now x == 0
 p = &x;  // & takes the address of x // now *p == 0, since p == &x and therefore *p == x
 *p = 1;  // equivalent to x = 1, since p == &x// now *p == 1 and x == 1
```

## Reference

- You must always be able to assume that a **reference is** connected to a legitimate piece of storage. Once a **reference is initialized** to an object, it cannot be changed to refer to another object. 
- A reference must be initialized on declaration while pointers **can** be pointed to another object at any time.
- References are used to refer an existing variable in another name whereas pointers are used to store address of variable.
- References cannot have a null value assigned but pointer can.
- A reference variable can be referenced by pass by value whereas a pointer can be referenced but pass by reference.
- 
- A reference shares the same memory address with the original variable but also takes up some space on the stack whereas a pointer has its own memory address and size on the stack.

```C++
int b =13;
int &ref = b;
```



## Dynamic Memory Allocation

Uses`new` operator to allocate memory. Can allocate storage for a variable while program is running

```C++
double *dptr;
dptr = new double; //new returns address of memory location
int* b = new int[50]; // array with 4*50 bytes and the address of which is b
delete[] b; //release the address in the heap
```

`new ` returns address of memory location

```c++
class Entity{}
Entity* e = new Entity(); // this will call the constructor
Entity* e = (Entity*)malloc(sizeof(Entity)); //do the same above but no calling constructor
delete e; //call the destructor
```

## Dangling Pointers and Memory Leaks

- A pointer is dangling if it contains the address of memory that has been freed by a call to **delete**.
- Solution: set such pointers to 0 as soon as memory is freed.
- A memory leak occurs if no-longer-needed dynamic memory is not freed. The memory is unavailable for reuse within the program.
- Solution: free up dynamic memory after use

## Returning Pointers from Functions

- Pointer can be return type of function

``` c++
int* newNum();
```

- Function must not return a pointer to a local variable in the function
- Function should only return a pointer
  - to data that was passed to the function as an argument
  - to dynamically allocated memory

## **Pointers to Class Objects** 

- Derived class pointer cannot point to base class

```C++
class Student{}
Student stu1;
Student *stuPtr = &stu1;
(*stuPtr).age = 3;stuPtr->age =3 ;//equal

struct GradeList
  { 	string courseNum;
    	int * grades;
  }
GradeList test1; *testPtr = &test1;
testPtr->grades;// Access the grades pointer in test1.  This is the same as (*testPtr).grades
*testPtr->grades; //Access the value pointed at by testPtr->grades.  This is the same as *(*testPtr).grades
*test1.grades; //Access the value pointed at by test1.grades
```

## Template

template <typename T> and template <class T> are equivalent and interchangeable

```C++
template <typename T> //python print
void print(T x)
{
    std::cout<<x<<endl;
}

template <class T> //define stack using vector
class Stack
{ 
  private: 
    vector<T> elems;     // 元素 
  public: 
    void push(T const&);  // 入栈
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


# OOP

## Inheritance, Polymorphism, Encapsulation

- **Inheritance:** Ability to derive new objects from old ones
- **Polymorphism:** Ability for different objects to interpret functions differently
- **Encapsulation:** Combining data structure with actions

## Static and Non-static member 

+ **non-static** data member
  - Each class object has its own copy

- **static** data member
  - Acts as a global variable
  - One copy per class type, e.g. counter

## const member function

```C++
void print(string x) const{}//Makes no modification about the data members (safe function). It is illegal for a const member function to modify a class data member
```

## Access control

- public
  - may be accessible from anywhere within a program
- private
  - may be accessed only by the member functions, and friends of this class
- protected
  - acts as public for derived classes
  - behaves as private for the rest of the program

## Constructor

- A function which every time the class initialization will be called. **no return type**; **different signatures**; **public access**
- The default constructor and the destructor of the base class are always called when a new object of a derived class is created or destroyed.

```C++
class Rectangle
{
	private:
	   int width;
	   int length;
	public:
	   Rectangle();//Default constructor
	   Rectangle(const Rectangle &r);//Copy constructor
	   Rectangle(int w, int l);//Constructor with parameters
	   void set(int w, int l);
	   int area();
}
Rectangle :: Rectangle() { };//default
Rectangle :: Rectangle (const Rectangle & r) //default copy
{ width = r.width;  length = r.length;};

```

## Virtual destructor

-  **Virtual destructor** is to destruct the resources in a proper order, when you delete a **base class** pointer pointing to derived **class** object. **Virtual base class destructors** are "best practice" - you **should** always use them to avoid (hard to detect) memory leaks.

## Access method

```C++
class Point{
	protected:
	   int x, y;
	public:
	   void set(int a, int b)
		{x=a; y=b;}
	   void foo ();
	   void print();
};
class Circle : public Point{
  private:  double r;
  public:
	void set (int a, int b, double c) {
	     Point :: set(a, b); //same name function call
	     r = c;}
	void print(); };
```

## Virtual function

- By default, C++ matches a function call with the correct function definition at compile time. This is called **static binding**. You can specify that the compiler match a function call with the correct function definition at run time; this is called **dynamic binding**. You declare a function with the keyword **virtual** if you want the compiler to use dynamic binding for that specific function.
- A virtual function is a member function you may redefine for other derived classes, and can ensure that the compiler will call the redefined virtual function for an object of the corresponding derived class, even if you call that function with a pointer or reference to a base class of the object.
- A class that declares or inherits a virtual function is called a **polymorphic** class.

## Abstract class

When derived class overrides the base class, the function of the base needs to be virtual. If there is not meaning to instantiate the base class, the class should be set to abstract class, because it includes pure virtual function. 

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
    Singleton(const Singleton&) = delete; //copy constructor as delete
    void operator=(const Singleton &) = delete;
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



## Smart Pointer

- auto_ptr: smart pointer that manages an object obtained via new expression and deletes that object when auto_ptr itself is destroyed.
- unique_ptr: similar functionality with auto_ptr, but with improved security (no fake copy assignments), added features (deleters) and support for arrays. 

```c++
class A { 
public: 
    void show() 
    { 
        cout << "A::show()" << endl; 
    } 
}; 
  
int main() 
{ 
    unique_ptr<A> p1(new A); 
    p1->show(); 
  
    // returns the memory address of p1 
    cout << p1.get() << endl; 
  
    // transfers ownership to p2 
    unique_ptr<A> p2 = move(p1); 
    p2->show(); 
    cout << p1.get() << endl; 
    cout << p2.get() << endl; 
  
    // transfers ownership to p3 
    unique_ptr<A> p3 = move(p2); 
    p3->show(); 
    cout << p1.get() << endl; 
    cout << p2.get() << endl; 
    cout << p3.get() << endl; 
  
    return 0; 
} 
```

- shared_ptr

  a container for raw pointers. It is a **reference counting ownership model** i.e. it maintains the reference count of its contained pointer in cooperation with all copies of the shared_ptr. So, the counter is incremented each time a new pointer points to the resource and decremented when the destructor of the object is called.

- weak_ptr

  A weak_ptr is created as a copy of shared_ptr. It provides access to an object that is owned by one or more shared_ptr instances but does not participate in reference counting. The existence or destruction of weak_ptr has no effect on the shared_ptr or its other copies. It is required in some cases to break circular references between shared_ptr instances.



## Typeof 

give data type a new short name

```C++
typedef vector<double> vecd;
typedef vector<vector<double>> metrix;
```

# STL

### Containers

- Sequence Containers: implement data structures which can be accessed in a sequential manner.
- Container Adaptors : provide a different interface for sequential containers.
- Associative Containers : implement sorted data structures that can be quickly searched (O(log n) complexity).
- Unordered Associative Containers:  implement unordered data structures that can be quickly searched

```C++
vector<int> g1; //Sequence Containers vector
g1.push_back(1); 
for (auto i = g1.begin(); i != g1.end(); ++i) 
    cout << *i << " ";
list<string> mylist({ "3","2" });// list
```

```C++
stack <int> s; // Stack: LIFO; Queue: FIFO
s.push(10); 
s.push(30); 

cout << "\ns.size() : " << s.size(); 
cout << "\ns.top() : " << s.top(); 
cout << "\ns.pop() : "; 
s.pop(); //delete the top of

while (!s.empty()) 
{ 
    cout << '\t' << s.top(); 
    s.pop(); 
} 
```

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

```C++
#include<iostream> 
#include<iterator> // for iterators 
#include<vector> // for vectors 
using namespace std; 
int main() 
{ 
    vector<int> ar = { 1, 2, 3, 4, 5 }; 
    // Declaring iterator to a vector 
    vector<int>::iterator ptr = ar.begin(); 
    // Using advance() to increment iterator position 
    // points to 4 
    advance(ptr, 3); 
    // Displaying iterator position 
    cout << "The position of iterator after advancing is : "; 
    cout << *ptr << " "; 
    return 0; 
} 
```



