# Module 01 Notes

## Python Language Essentials

#### Raw Strings

- Does not interperet escape sequences
- Example: ```r'this is a test\nNo new lines!\n"```


#### Unicode Strings

- Sometimes known as wide characters
- Example ```u'This is a wide character string"```


#### String Conversions

- Unicode to regular string: ```str(unicode_string)```
- Regular to unicode stiring: ```unicode(regular_string)```


#### String Properties and Methods

- Strings are immutable
- Replication:  ```"A" * 5``` = 'AAAAA'
- Slicing:  ```my_string[start : end : steps]```
- Parse integer: ```str(42)``` = '42'


#### Methods for Classes / Help

- To find all methods you can run on a class: ```dir(className)```
- To get help on a method: ```help(className.method)```

#### Tuples

- Immutable list
- Can convert from list to tuple and back
  - ```newTuple = tuple(myList)```
  - ```newList = list(myTuple)```


#### Sequence Unpacking

```
>>> sampleTuple = tuple(["Item 1", "Item 2", "Item 3"])
>>> itemOne, itemTwo, itemThree = sampleTuple
>>> itemOne
'Item 1'
>>> itemTwo
'Item 2'
>>> itemThree
'Item 3'
```

#### Functions

- Sample function definitions:
  - ```def functionWithNoArgs()```
  - ```def functionWithArgs(argOne, argTwo)```
  - ```def functionWithDefaultArgs(argOne = 1, argTwo = 2)```
  - ```def functionInObjectWithNoArgs(self)```
  - ```def functionInObjectWithArgs(self, argOne, argTwo)```


#### Classes

```
# Sample class that contains two fields, a constructor, and a function.
class SampleClass:

  def __init__(self, inputOne, inputTwo):
    self.fieldOne = inputOne
    self.fieldTwo = inputTwo
    print "SampleClass created with {0} and {1}.".format(self.fieldOne, self.fieldTwo)

  def sampleClassMethod(self):
    print "Running sampleClassMethod."
    print " Field One: {0}".format(self.fieldOne)
    print " Field Two: {0}".format(self.fieldTwo)


# Contains all functions from SampleClass plus one more bonus function.
class SuperSampleClass(SampleClass):
  
  def swapFields(self):
    temp = self.fieldOne
    self.fieldOne = self.fieldTwo
    self.fieldTwo = temp
```


#### Modules

  - Used for code organization.
  - Ways to import modules:
    - ```import MODULE_NAME```
    - ```from MODULE_NAME import SAMPLE_CLASS```


#### Packages

  - Hierarchical directories to organize code
  - Consists of modules and sub-packages
  - Directories contain ``__init__.py`` file
  - Import name of directory as package name.


#### Exception Handling

```
def failingMethod():
  print "Going to divide by zero!"
  try: 
    quotient = 100 / 0
    print "Division Succeded!"
  except ZeroDivisionError:
    print "Cannot Divide by zero!"
  except Exception as ex:
    print "Unknown exception: {0}".format(ex)
  else:
    print "No exception happened."
  finally:
    "Cleanup code goes here!"
```
