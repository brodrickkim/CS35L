# Learning by doing - python

* Spring 2019, CS35L - Lab 7
* TA: Rishab Ketan Doshi
* Week 3, Lecture 1, April 16

### Example 1 - Variables + Typing
Create a file `variables_types.py` with the below content.

```
#!/usr/bin/python
counter = 100    # An integer assignment 
miles = 1000.0   # A floating point 
name = "John"   # A string 
print counter 
print miles 
print name

score = 100
print(score)
print(type(score))
score = "great score"
print(score)
print(type(score))

```

Execute this file by typing

```
python variables.py
```

### Example 2 - Lists in Python
Open python in interactive mode by typing the word python in your command line.

``` 
python 
```
Type below commands into terminal.

```
t = [123, 3.0, ‘hello!’]
```

Play around with below commands:

```
t[0]
```

```
print(t)
```

### Example 3 - Merging Lists
Open python in interactive mode by typing the word python in your command line.

``` 
python 
```
Type below commands into terminal.

```
list1 = [1, 2, 3, 4]
```

```
list2 = [5, 6, 7, 8]
```

```
merged_list = list1 + list2
```

### Example 4 - Dictionary

* Create `dict.py`

```
hogwarts_dict = {}

hogwarts_dict['slytherin'] = 'salazar_slytherin'
hogwarts_dict['gryffindor'] = 'godric_gryffindor'
hogwarts_dict['ravenclaw'] = 'rowena_ravenclaw'
hogwarts_dict['hufflepuff'] = 'helga_hufflepuff'

print(hogwarts_dict)

print(hogwarts_dict.keys())

if 'slytherin' in hogwarts_dict.keys():
	print 'slytherin is one of the houses'
else
	print 'slytherin is not one of the houses'
	
del hogwarts_dict['slytherin']

if 'slytherin' in hogwarts_dict.keys():
	print 'slytherin is one of the houses'
else
	print 'slytherin is not one of the houses'

## Nested dictionaries

ron = {}

ron['name'] = 'Ronald Weasley'
ron['house'] = 'gryffindor'

hermionie = {}
hermionie['name'] = 'Hermionie Granger'
hermionie['house']= 'gryffindor'

harry = {}

harry['name'] = 'harry potter'
harry['house'] = 'gryffindor'
harry['aliases'] = ['the boy who lived', 'the chosen one']
harry['friends'] = [ron, hermionie]
```

* `python dict.py`

### Example 5 - for loops

* Create `for.py`

```
hogwarts_dict = {}

hogwarts_dict['slytherin'] = 'salazar_slytherin'
hogwarts_dict['gryffindor'] = 'godric_gryffindor'
hogwarts_dict['ravenclaw'] = 'rowena_ravenclaw'
hogwarts_dict['hufflepuff'] = 'helga_hufflepuff'

houses = list(hogwarts_dict.keys())

for h in houses:
	print(h)
	
for i in range(len(houses)):
	print(i)

```

* Run `python for.py`

### Example 6 - Slices
```
str = '0123456789'

print(str[:])
print(str[0:4])	
print(str[1:])

```

### Example 7 - Split

Open python in interactive mode and type in the below commands

* `x = "blue,red,green"`
* `x.split(",")`
* `a, b, c = x.split(",")`
* `a`
* `b`
* `c`

### Example 8 - Functions

* create `functions.py`

```
def fn():
	print("I am a function")
	
def fnWithParam(param):
	print("I am function with a param " + param)
	
def getDictKeysAsList(dict):
	return list(dict.keys())
	
fn()
fnWithParam("OK!!")

hogwarts_dict = {}

hogwarts_dict['slytherin'] = 'salazar_slytherin'
hogwarts_dict['gryffindor'] = 'godric_gryffindor'
hogwarts_dict['ravenclaw'] = 'rowena_ravenclaw'
hogwarts_dict['hufflepuff'] = 'helga_hufflepuff'

print(getDictKeysAsList(hogwarts_dict))

```

### Example 9 - Exception Handling

* create `newdict.py`

```
def getFounder(housename):
	hogwarts_dict = {}
	hogwarts_dict['slytherin'] = 'salazar_slytherin'
	hogwarts_dict['gryffindor'] = 'godric_gryffindor'
	hogwarts_dict['ravenclaw'] = 'rowena_ravenclaw'
	hogwarts_dict['hufflepuff'] = 'helga_hufflepuff'
	
	try:
		founder = hogwarts_dict[housename]
		return founder
	except KeyError:
		return "Invalid housename given"
	
print(getFounder("slytherin"))
print(getFounder("stark"))

```

### Example 10 - Raw Input

```
hogwarts_dict = {}

hogwarts_dict['slytherin'] = 'salazar_slytherin'
hogwarts_dict['gryffindor'] = 'godric_gryffindor'
hogwarts_dict['ravenclaw'] = 'rowena_ravenclaw'
hogwarts_dict['hufflepuff'] = 'helga_hufflepuff'

def addFounder(house, founder):
	hogwarts_dict[house]=founder
	return

def getFounder(housename):	
	try:
		founder = hogwarts_dict[housename]
		return founder
	except KeyError as ke:
		print(ke)
		return "Invalid housename given"

print("Enter the house name")
house = raw_input()
print("Enter the founders name")
founder = raw_input()

addFounder(house,founder)
print("Getting founder of input")
print(getFounder(house))
print(getFounder("invalidHouse"))

```

### Example 12 - name == main

* create a file `foo.py` with the below content. 
* Execute it to understand what is happening.


```
print("before import")
import math

print("before functionA")
def functionA():
    print("Function A")

print("before functionB")
def functionB():
    print("Function B {}".format(math.sqrt(100)))

print("before __name__ guard")
if __name__ == '__main__':
    functionA()
    functionB()
print("after __name__ guard")
```

* When you run `python foo.py` ; the interpreter will assign the hard-coded string "__main__" to the __name__ variable
* [srd](https://stackoverflow.com/questions/419163/what-does-if-name-main-do)


### Example 11 - Argparse Library

Head over to this [tutorial](https://www.pythonforbeginners.com/argparse/argparse-tutorial).
