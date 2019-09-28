# Python Notes

## Python Basics

**Changing types in Python:**

Change from `int` to `string`

```py
str(15)
```

Change from `str` to `int`

```py
int("15")
```

**Named Arguments:**

One of the interesting feature that I found about Python functions are the "Named Arguments" or the "Keyword Arguments". When you have multiple parameters defined in a function, you can pass the argument in whatever order if you use Named Argument. 

Example: 

```python
def add(a, b, c):
  print(a + b - c)
  
add(c = 20, b = 10, a = 5) #Named arguments
```

Like seen above, we can assign value to parameters in any order we want and they will still get the proper value. It's the name that matters, not the position. 

Note: This does not work in JavaScript. 

**\*args and \**kwargs:**

\*args and \**kwargs are the wild parameters in python. They represent more than one parameters.

Example: 

```python
def args_function(name,*args):
  print("This is the normal text: ", name)
  for value in args: 
    print("This is the value from *args wildcard: ", value)

args_function('Yankee', 'Hello', 5, 'Can', 'Put', 'Anything')
```

Similarly, kwargs stands from Keyword Arguments. Whatever the number maybe, we should pass it as Keyword argument. There are few things to consider while using kwargs:

- They return a dictionary (object). So to get the data out of it, we use the `.items` method. The `.items` method returns a key value pair or Keyword Arguments.
- If we just want the value, then we can use `.values` method.
- To iterate through each items of kwarr, we need to pass key and value representation to the `for..in` loop. 

```python
def kwargs_function(name, **kwargs):
  print("Came from the normal parameter: ", name)
  for kwar, kwarr in kwargs.items(): 
    print("Came from the kwargs: ", kwarr)
    
kwargs_function(name = "Yankee", age = 22, Location = "Kathmandu")

# With .values() method

def kwargs_function(name, **kwargs):
  print("Came from the normal parameter: ", name)
  for kwar in kwargs.values(): 
    print("Came from the kwargs: ", kwar)
    
kwargs_function(name = "Yankee", age = 22, Location = "Kathmandu")
```

In the example above, `kwar` represents the key and `kwarr` represents the value. 

**Generator Functions: Yield**

Function usually returns something when it is called. For the most part, they just take new variables and work on them to return their value. But if  we use `yield` keyword inside our function it will make the function a generator function. ~~It means, the generator will resume the execution where it was left off.~~

**Range**

Range is used to generate numbers in  a range. For example,  if i want all the numbers between  0 and 10, then it can be simply generated using `range(10)`. Range returns an immutable sequence type in python 3 but for easy understanding just think that it returns a list i.e. in python 2.

Range takes 3 arguments: namely, start value, end value and step size. 

For example: let's print all the numbers between 1 and 10 with the difference of 2. 

```python
for i in range (1, 10, 2):
  print (i) 
```



**Lambda Functions**

Lambda in python is an anonymous function like in JS. Meaning a function without a name. The function is assigned with a variable. 

Lambda function is denoted using the `lambda` keyword.

Example : 
Normal Function

```python
def double(x):
  return x * 2
```

Lambda Function 

```python
double  = lambda x: x * 2
```

## Object Oriented Python 

**Pass keyword**

Whenever we are creating methods inside of classes and we are not sure of what the method is going to do, we just return `pass` from that method. Meaning it tells the Python interpreter to do nothing.  It's useful for placeholder classes and functions.

Example: 

```python
class Name: 
  def speak(language):
    pass

 # Or we can do it like this, if there are no methods

class Name: 
  pass
```

**Constructor**

Constructor in python is defined using the `__init__` keyword. Which means initializing the class. Constructor can be useful to omit methods, meaning instead of calling methods to pass some value we can pass value directly using the constructor. 

Example: 

Class with method

```python
students = []

class Student: 
  def add_student(name,id = 332): 
    student = {"name": name, "student_id": id}
    students.append(student)
    
new_student = Student()
new_student.add_student("Yankee", 36)

print(students)
    
```

Class with constructor 

```python
students = []

class Student: 
  def __init__(name, id = 332):
    self.name = name
    self.id = id
    students.append(self)
    
new_student = Student("Yankee", 36)
print(new_student)
```

**Class and Instance Attributes**

Class attributes are the variables defined inside of the class, it can be accessed by the methods inside of the class. It acts as a global variable. To access class attributes, we don't need to create an instance of the class.

Example: 

```python
class Student: 
  # class attribute
  school_name = "Panga Secondary Boarding School" 
  
  def add_student: 
    pass
```

Instance attribute are the variables or attributes defined inside of the method of the class. Since methods get initialized only when we create an instance of the class, the instance attributes can be accessed only after we create an instance of the class. Also the instance attribute can be accessed inside of that method. 

Example: 

```python
class Student: 
    def add_student(self, name):
    # instance attribute
    self.name = name
```

**Inheritance**

To inherit the methods of parent class we just need to pass the name of the parent class as parameter to our child class.  Then we can access all the methods of our parent class from the child class. 

Example: 

We already have a student class from above, we will inherit the methods from that class to our new child class. 

```python
# Parent Class

students = []
class Student:
    school_name = "Panga Secondary Boarding School"

    def __init__(self, name, student_id=332):
        self.name = name
        self.student_id = student_id
        students.append(self)

    def get_name_capitalized(self):
        return self.name.capitalize()

    def get_schoolname(self):
        return self.school_name
      
# Child Class

class HighSchoolStudents(Student):
  school_name = "DAV College"
  # Method Overriding 
  def get_schoolname(self):
    return f"The name High School is {self.school_name}"

yankee  = HighSchoolStudents("Yankee")
print(yankee.get_name_capitalized())
```

In the HighSchoolStudents class we have override the `get_schoolname` method, that means the inherited method from parent class will not work.  If we still want to access the method from parent after overriding it then we can use the `super` keyword. 

Example: 

We now want to override `get_name_capitalized` method but still want to access the functionality of the parent class method so that we can add the HS tag to represent a High school student.

```python
class HighSchoolStudents(Student):
  school_name = "DAV College"
  # Method Overriding 
  def get_schoolname(self):
    return f"The name High School is {self.school_name}"
  
  def get_name_capitalized(self):
    original_name = super().get_name_capitalized() # super
    return f"{original_name} - HS"
```







 

