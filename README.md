# Advanced_Python
some advanced skills for Python

## Multi-Processing and threading

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



## Class and Static method

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

regular instant method: pass the instant as the 1st argument

class method: pass the class

static method: don't operate to instance or class any where within function

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



