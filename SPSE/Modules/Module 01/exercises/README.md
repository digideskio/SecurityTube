## Module 1: Video 1 Exercises

#### Q1\. Install Python 3.x in Ubuntu 11.10

```
Installed Python 3.x in Kali. Close enough.
```



#### Q2\. How can you switch between different versions of Python?

```
Console: You can specify the version of python on the command line.
         (Examples: python2, python2.6, python2.7, python3)

Script: For each command in the Console section, simply add that to
        to hashbang in the script (#!/usr/bin/$PYTHON_CMD)
```



#### Q3\. Explore Virtualenv in Python.

```
From "http://docs.python-guide.org/en/latest/dev/virtualenvs/":

    A Virtual Environment is a tool to keep the dependencies required by
    different projects in separate places, by creating virtual Python 
    environments for them. It solves the “Project X depends on version 1.x 
    but, Project Y needs 4.x” dilemma, and keeps your global site-packages
    directory clean and manageable.

    For example, you can work on a project which requires Django 1.3 while 
    also maintaining a project which requires Django 1.0.
```

---

## Module 1: Video 4 Exercises

#### Q1\. While loops can also have a "else" in Python. Explore this functionality and write a simple program to illustrate it.

```
#!/usr/bin/python

myNumber = 5
while myNumber <= 100:
  print "myNumber =  {0}".format(myNumber)
  if myNumber == 10:
    break
  myNumber += 1
else:
  print "This won't execute."

while myNumber >= 500:
  print "myNumber =  {0}".format(myNumber)
  myNumber -= 1
else:
  print "This is going to execute."
```


#### Q2\. For loops can have a "else" statement as well. Write a simple program to illustrate this functionality.

```
#!/usr/bin/python

for number in range(1,6):
  print "Step {0} of 5.".format(number)
  if number == 5:
    break
else:
  print "This won't execute."


for number in range(0,0):
  print "Step {0} of 0.".format(number)
  if number == 100:
    break
else:
  print "This is going to execute."
```

---

## Module 1: Video 6 Exercises

#### Q1\. What are global, class, and instance variables?

```
Global variables can be referenced anywhere within the program.
Class variables can be referenced anywhere within the class they are defined.
Instance variables can be reference in the instance of the object they live in.

An excellent illustration of the scopes of these can be found at:
    http://www.saltycrane.com/blog/2008/01/python-variable-scope-notes/
```

```
#!/usr/bin/python

globalVar = "This is a global variable."

class SampleClass:

  classVar = "This is a class variable."

  def __init__(self):
    self.instanceVar = "This is an instance variable."

  def usageDemo(self):
    global globalVar;
    print "Global variable: {0}".format(globalVar)
    print "Class variable: {0}".format(SampleClass.classVar)
    print "Instance variable: {0}".format(self.instanceVar)
```

#### Q2\. How can we override a method in a parent class?

```
To override a method found in a parent class, simply redefine the function in the child class.
```
---

## Module 1: Video 9 Exercises

#### Q1\. Python allows for user-defined exceptions. Code up a demo which has a user-defined exception and an example use case.

```
#!/usr/bin/python

class OutOfStockException(Exception):
  pass


class Order:  
  colorsInStock = ["RED", "GREEN", "BLACK"]
  
  def __init__(self, colorRequest):
    if colorRequest not in Order.colorsInStock:
      raise OutOfStockException("Color '{0}' not in stock. Choose from {1}".format(colorRequest, Order.colorsInStock))
    else:
      self.color = colorRequest


colorChoices = ["WHITE", "YELLOW", "GREEN", "BROWN", "RED"]
for color in colorChoices:
  try:
    newOrder = Order(color)
    print "We successfully ordered color '{0}'".format(color)
  except OutOfStockException as ex:
    print "Color '{0}' is out of stock.".format(color)
  except Exception as ex:
    print "Order failed for unknown reason: {0}".format(ex)
```

---

## Module 1: Video 10 Exercises

#### Skipping these due to requirements outside just a laptop.