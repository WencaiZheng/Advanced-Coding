# Python Primer

## Multi-Processing and threading

**GIL**: CPython has a global interpreter lock () is a mechanism used in computer-language interpreters to synchronize the execution of threads so that only one native thread can execute at a time. An interpreter that uses **GIL** always allows exactly one thread to execute at a time, even if run on a multi-core processor.

A particular feature of CPython is that it makes use of a [global interpreter lock](https://en.wikipedia.org/wiki/Global_interpreter_lock) (GIL) on each CPython interpreter process, which means that within a single process only one thread may be processing Python bytecode at any one time. This does not mean that there is no point in multithreading; the most common multi-threading scenario is where threads are mostly waiting on external processes to complete.

For example, imagine when three threads are servicing separate clients. One thread may be waiting for a client to reply, another may be waiting for a database query to execute, while the third thread is actually processing Python code.

However the GIL does mean that CPython is not suitable for processes that implement CPU intensive algorithms in Python code that could potentially be distributed across multiple cores.

**I/O bound** refers to a condition in which the time it takes to complete a computation is determined principally by the period spent waiting for **input/output** operations to be completed.

**CPU bound** refers to more computation time.

```python
import multiprocessing
def func(x):
    return x
for i in range(10):
	p1=multiprocessing.Process(func,args=[x])
	p1.start()
	p1.join()
```

```python
import concurrent
with concurrent.futures.ProcessPoolExecutor() as executor:
    # concurrent.futures.ThreadPoolExecutor()
    x = [5,4,3,2,1]
    results = executor.map(func,x)
finish=time.perf_counter
```

## Special Variable

```python
class Test:
	def __init__(self):
        self.foo=1
        self._bar=2
        self.__baz =3
```

`Test().__baz` does not exist. The compiler changed the attributes to `_Test__baz`. The other two are good despite that `_bar` by convention is a private member.

## Generator

```python
#Fibonacci
def fib(num):
    a,b=0,1
    for i in range(num):
        yield i+1,a
        a,b=b,a+b

for item in fib(10):
    print(item)
```

## Class variable

```python
class Student:
    #class variable
    _num_stu = 0 # private variable
    grade_grow = 1 #same for all instant
    def __init__(self,first,last,grade):
        self.grade = grade # instant variables
        self.first = first
    	Student.num_stu += 1 # each time instance created, number increase one
    def apply_grow(self):
        self.grade = self.grade + self.grade_grow# yes,need self. or Student.
stu_1 = Student("Jessi","Li",20)
stu_1.grade_grow = 2 # jump two grade,stu1 can override the constant
# Correct way to change the value of class variable 
Student.grade_grow = 2 # for all students
```

## Class method and Static method

```python
class Student:
    #class variable
    student_grade = 8
    def __init__(self,first,last,age):
        self.age = age
        self.first = first
        self.last = last
    # regular instant pass the instant as the 1st arg*
    def fullname(self):
        return self.first+self.last
    # classmethod:pass the class, alter class inside variable
    @classmethod
    def grow_grade(cls,by):
        cls.studen_grade+=by
    # use classmethod as alternative constructure
    @classmethod
    def from_string(cls,stu_str):
        f,l,a = stu_str.split(" ")
        return cls(f,l,a)
    # staticmethod: dont operate to instance or class any where within func
    @staticmethod
    def is_heavy(int:hw):
        if hw>10:return True
        return False
stu_1 = Student("Jessi","Li",20)
Student.grow_grade(1)
# run from instance also change whole class(not good)
stu_1.grow_grade(1)
stu_str_1 = "a b 12"
stu_2 = Student.from_string(stu_str_1)
Student.is_heavy(20)
```

1. regular instant method: pass the instant as the 1st argument

2. class method: pass the class, class method decorated function can be used in derived classes

3. static method: don't operate to instance or class any where within function


## Inheritance

```python
class CleverStudent(Student):
    grade_grow = 2
    def __init__(self,first,last,age,college):
        super().__init__(first,last,age)
        self.college = college
jessi = CleverStudent("Jessi","Li",20,"NYU")
isinstance(jessi,CleverStudent): # True
isinstance(jessi,Student): # True
issubclass(CleverStudent,Student)# True
```

## GUI

```python
from tkinter import *
root = Tk()
mylabel = Label(root,text="Hello")
mylabel.pack()

root.mainloop()
```

## Property

```python
# Using @property decorator
class Celsius:
    def __init__(self, temperature=0):
        self._temperature = temperature
        #if use setter we assign
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    @property
    def temperature(self):
        print("Getting value...")
        return self._temperature,
	
    # if use self.temperature = y, it calls this funciton first to assign 
    # the variable in this way
    # if use self._temperature in init function then we don't need to use setter
    @temperature.setter
    def temperature(self, value):
        print("Setting value...")
        if value < -273.15:
            raise ValueError("Temperature below -273 is not possible")
        self._temperature = value

x=Celsius(37)
x.temperature
# it avoid people modify the temperature by simple asign x.temperature = y
```

## iterator and generator

A python generator is an iterator. Generator in python is a subclass of Iterator.

```python
def even(x):
	while(x!=0):
    	if x%2==0:
        	yield x
        x-=1
for i in even(8):
	print(i)
```

Python iterator is an iterable. Iterator in python is a subclass of Iterable.

```
iter_obj=iter([3,4,5])
next(iter_obj)
```

Difference between Iterators and Generators in python.

1. In creating a python generator, we use a function. But in creating an iterator in python, we use the _iter()_ and _next()_ functions.
2. A generator in python makes use of the ‘yield’ keyword. A python iterator doesn’t.
3. Python generator saves the states of the local variables every time **yield** pauses the loop in python. An iterator does not make use of local variables, all it needs is iterable to iterate on.
4. A generator may have any number of **yield** statements.
5. You can implement your own iterator using a python class; a generator does not need a class in python.
6. To write a python generator, you can either use a Python function or a comprehension. But for an iterator, you must use the iter() and next() functions.

## Callable instances

can be called using

```python
function()
```