---
layout: article
title: IPython notebook from Learn Python the Hard Way
---


# Exercise 37: Symbol Review

Most of the items here I am already quite familiar with. I will spend my time focusing on the ones I am not so familiar with. The entire exercise is given here: http://learnpythonthehardway.org/book/ex37.html.

Some of these keywords are bit hard to grasp before I get more familiar with other topics in python, like objects and classes. Many of the keywords are related to each other as well, like `try`, `finally`, `with` and `yield`, and it seems a bit hard to grasp `with` completely before getting acquinted with try and finally. The main point here is that these keywords should be **reviewed regularly**!

### Keywords

- `as`: Part of the with-as statement. **To be repeated** But, on the other hand, the with-as statement does not look very important. It's not an integral part of python: the with statement simplifies exception handling by encapsulating common preparation and cleanup tasks in so-called context managers.
    - The with statement is used to wrap the execution of a block with methods defined by a context manager (see section With Statement Context Managers). This allows common try...except...finally usage patterns to be encapsulated for convenient reuse.
- `assert`: Assert (ensure) that something is true. Used for debugging, not very important for the skill level I am currently at.
    - Python's assert statement helps you find bugs more quickly and with less pain. Assertions is a kind of internal self-check of the code, to make it easier to identify bugs and errors in the code. Assertions are a systematic way to check that the internal state of a program is as the programmer expected, with the goal of catching bugs.
    - Returns an error, with an optional message, if the asserted logical test fails. e.g. `assert False` returns an error. `assert True` returns nothing, and lets the script continue.
- `del`: Delete from dictionary
    - And also other items, like lists and entire variables.
    - Makes intent clearer than setting a value to `None`. E.g. `del foo` vs `foo = None`
- `except`: If an exception happens, do this. (Usually part of try-except block.)
    - In python, There are (at least) two distinguishable kinds of errors: syntax errors and exceptions. Syntax error: where the syntax is incorrect. Exceptions: Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. E.g. `1/0` would return an exception called `ZeroDivisionError`.
    - To avoid exceptions from terminating a script, a `try` statement can help you handle them. For more info: https://docs.python.org/2/tutorial/errors.html#handling-exceptions.
    - The except statement requires the type of exception to handle to be specified, e.g. `except (RuntimeError, TypeError, NameError):`
- `exec`: Run a string as Python.
    - Enables python to execute code from a string. **To be repeted**. Check out: http://stackoverflow.com/questions/2220699/whats-the-difference-between-eval-exec-and-compile-in-python
- `finally`: Exceptions or not, finally do this no matter what.
    - Can be included in `try` statements, like try-except-else-finally.
    - No matter what happened [before finally:], the final-block is executed once the code block is complete and any raised exceptions handled. Even if there's an error in an exception handler or the else-block and a new exception is raised, the code in the final-block is still run.
    - Example structure:
    
    
    try:
        block-1 ...
    except Exception1:
        handler-1 ...
    except Exception2:
        handler-2 ...
    else:
        else-block
    finally:
        final-block   
    
- `global`: Declare that you want a global variable.
    - Set the variable in the "top level" and call it using `global` inside a function etc. The keyword is needed beacause global variables are considered dangerous; "global variables are generally bad practice and should be avoided. In most cases where you are tempted to use a global variable, it is better to utilize a parameter for getting a value into a function or return value to get it out."
- `in`: Part of for-loops. Also a test of x in y.
    - (very?) similar to R's `%in%`. Returns a boolean (not a vector of booleans as for R's %in%).
- `is`: "Like == to test equality." BUT IS IT? No, they ar not similar.
    - `is` is identity (the object's memory address) testing (or 'point to the same object'), `==` is equality testing. In other words: is is the id(a) == id(b)
    - See: http://stackoverflow.com/questions/1504717/why-does-comparing-strings-in-python-using-either-or-is-sometimes-produce and http://stackoverflow.com/questions/2988017/string-comparison-in-python-is-vs
- `lambda`: Create a short anonymous function. **Anonymous functions need to be learned better. And then repeat it."**
- `pass`: "This block is empty." `pass` is a null statement, it results in no operation (NOP). Generally used as a placeholder.
- `raise`: Raise an exception when things go wrong. Raise your own error/exception, in e.g. an if statement.
- `try`: Try this block, and if exception, got `except`. See `except` and `finally`.
- `with`: With an expression as a variable do. See `as`.
- `yield`: Pause here and return to caller. It returns a generator!
    - A generator is like an iterable, except that the values in the generator are not stored but only generated on the fly and "forgotten" afterwards.
    - `yield` is a keyword that is used like `return`, except the function will return a generator. handy when you know your function will return a huge set of values that you will only need to read once. 
    - See: http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python

### Data Types

- `None`: Represents "nothing" or "no value". SAME AS R 'NONE'? Yes, similar to R None (I think).

### Operators

- `//`: Floor division. I understand what this is, just don't forget that this possibility is there.
- `@`: At (decorators). Decorators are related to classes and objects, **repeat after being more familiar with those**.
    - http://stackoverflow.com/questions/6392739/what-does-the-at-symbol-do-in-python

# Exercise 38: Doing things to lists

Programming exercise:





```python
ten_things = "Apples Oranges Crows Telephone Light Sugar"

print "Wait there are not 10 thins in that list. Let's fix that."

stuff = ten_things.split(' ')
more_stuff = ["Day", "Night", "Song", "Frisbee", "Corn", "Banana", "Girl", "Boy"]

while len(stuff) != 10:
    next_one = more_stuff.pop()
    print "Adding: ", next_one
    stuff.append(next_one)
    print "Therer are %d items now." % len(stuff)

print "There we go: ", stuff

print "Let's do some things with stuff."

print stuff[1]
print stuff[-1] # whoa! fancy
print stuff.pop()
print ' '.join(stuff) # what? cool!
print '#'.join(stuff[3:5]) # super stellar!
```

    Wait there are not 10 thins in that list. Let's fix that.
    Adding:  Boy
    Therer are 7 items now.
    Adding:  Girl
    Therer are 8 items now.
    Adding:  Banana
    Therer are 9 items now.
    Adding:  Corn
    Therer are 10 items now.
    There we go:  ['Apples', 'Oranges', 'Crows', 'Telephone', 'Light', 'Sugar', 'Boy', 'Girl', 'Banana', 'Corn']
    Let's do some things with stuff.
    Oranges
    Corn
    Corn
    Apples Oranges Crows Telephone Light Sugar Boy Girl Banana
    Telephone#Light
    

# Exercise 39: Dictionaries, Oh Lovely Dictionaries
## A dictionary example
Notes:

- must use dict.items() to loop over a dicts key value pairs


```python
# create a mapping of state to abbreviation 
states = {
    'Oregon': 'OR',
    'Florida': 'FL',
    'California': 'CA',
    'New York': 'NY',
    'Michigan': 'MI'  
}

# create a basic set of states and some cities in them
cities = {
    'CA': 'San Francisco',
    'MI': 'Detroit',
    'FL': 'Jacksonville'
}

# add some more cities
cities['NY'] = 'New York'
cities['OR'] = 'Portlant'

# print out some cities
print '-' * 10
print "NY State has: ", cities['NY']
print "OR State has: ", cities['OR']

# print some states
print '-' * 10
print "Michigan's abbreviation is: ", states['Michigan']
print "Florida's abbreviation is: ", states['Florida']

# do it by using the state then cities dict
print '-' * 10
print "Michigan has: ", cities[states['Michigan']]
print "Florida has: ", cities[states['Florida']]

# print every state abbreviation
print '-' * 10
for state, abbrev in states.items(): # NB: must use dict.items() to loop over a dicts key value pairs
    print "%s is abbreviated %s" % (state, abbrev)
    
# print every city in state
print '-' * 10
for abbrev, city in cities.items():
    print "%s is abbreviated %s" % (abbrev, city)
    
# now do both at the same time
print '-' * 10
for state, abbrev in states.items():
    print "%s state is abbreviated %s and has city %s" % (state, abbrev, cities[abbrev])
    
print '-' * 10
# safely get a abbreviation by state that might not be there
state = states.get('Texas') # NB: if key not found the returned value is None (unless specified); 
                            #    states['Texas'] would return
                            # an error. If key is found, both returns the value pair.
                            # D.get(k[,d]) -> D[k] if k in D, else d. d defaults to None.

if not state:
    print "Sorry, no Texas."
    
# get a city with a default value
city = cities.get('TX', 'Does Not Exist') # Here the value if key not found is specified.
print "The city for the state 'TX' is: %s" % city
```

    ----------
    NY State has:  New York
    OR State has:  Portlant
    ----------
    Michigan's abbreviation is:  MI
    Florida's abbreviation is:  FL
    ----------
    Michigan has:  Detroit
    Florida has:  Jacksonville
    ----------
    California is abbreviated CA
    Michigan is abbreviated MI
    New York is abbreviated NY
    Florida is abbreviated FL
    Oregon is abbreviated OR
    ----------
    FL is abbreviated Jacksonville
    CA is abbreviated San Francisco
    MI is abbreviated Detroit
    OR is abbreviated Portlant
    NY is abbreviated New York
    ----------
    California state is abbreviated CA and has city San Francisco
    Michigan state is abbreviated MI and has city Detroit
    New York state is abbreviated NY and has city New York
    Florida state is abbreviated FL and has city Jacksonville
    Oregon state is abbreviated OR and has city Portlant
    ----------
    Sorry, no Texas.
    The city for the state 'TX' is: Does Not Exist
    

## Making Your Own Dictionary Module

A bit difficult code here, and an interesting exercise to go through. It is not included here though, because of the function names in the code overwrites built-in python function (`set` and `list`). See http://learnpythonthehardway.org/book/ex39.html for exercise. 

# Exercise 40: Modules, Classes and Objects

#### Classes are like modules
You can think about a module as a specialized dictionary that can store Python code access it with the . operator. Python also has another construct that serves a similar purpose called a class. A class is a way to take a grouping of functions and data and place them inside a container so you can access them with the . (dot) operator.

**Unclear**:
Here's why classes are used instead of modules: You can take this MyStuff class and use it to craft many of them, millions at a time if you want, and each one won't interfere with each other. When you import a module there is only one for the entire program unless you do some monster hacks.

If a class is like a "mini-module," then there has to be a similar concept to import but for classes. That concept is called "instantiate", which is just a fancy, obnoxious, overly smart way to say "create." When you instantiate a class what you get is called an object.

You instantiate (create) a class by calling the class like it's a function, like this:

    thing = MyStuff()
    
Remember that this is not giving you the class, but instead is using the class as a blueprint for building a copy of that type of thing.

Keep in mind that I'm giving you a slightly inaccurate idea for how these work so that you can start to build up an understanding of classes based on what you know about modules. The truth is, classes and objects suddenly diverge from modules at this point. If I were being totally honest, I'd say something more like this:

- Classes are like blueprints or definitions for creating new mini-modules.
- Instantiation is how you make one of these mini-modules *and* imåprt it at the same time. "Instatiate" just means to create an object from the class.
- The resulting created mini-module is called an object and you then assign it to a varieable to work with it.
    
## A First Class Example 


```python
class Song(object):
    
    def __init__(self, lyrics):
        self.lyrics = lyrics
        
    def sing_me_a_song(self):
        for line in self.lyrics:
            print line

happy_bday_lyrics = ["Happy birthday to you",
                  "I don't want to get sued",
                  "So I'll stop right there"]            
            
happy_bday = Song(happy_bday_lyrics)

bulls_on_parade = Song(["They rally around that family",
                       "With pockets full of shells"])

hurra_for_deg = Song(["Hurra for deg som fyller ditt år",
                     "ja deg vil vi gratulere"])

happy_bday.sing_me_a_song()

bulls_on_parade.sing_me_a_song()

hurra_for_deg.sing_me_a_song()
```

    Happy birthday to you
    I don't want to get sued
    So I'll stop right there
    They rally around that family
    With pockets full of shells
    Hurra for deg som fyller ditt år
    ja deg vil vi gratulere
    

# Exercise 41: Learning To Speak Object Oriented

Terms to remember:

- `class`: Tell python to make a new type of thing (or object)
- `object`: Two meanings: the most basic type of thing, and any instance of some thing
- `instance`: What you get when you tell Python to create a class.
- `def`: How you define a function inside a class
- `self`: Inside the functions in a class, self is a variable ofr the instance/object being accessed.
- `inheritance`: The concept that one class can inherit traits from another class, much like you and your parents.
- `composition`: The concept that a class can be composed of other classes as parts, much like how a car has wheels.
- `attribute`: A property classes have that are from composition and are usually variables.
- `is-a`: A phrase to say that something inhertis form another, as in a "salmon" is-a "fish." 
- `has-a`: A phrase to say that something is composed of other things, or has a trait, as in "a salmon has a mouth".

- class X(Y): "Make a class named X that is-a Y."
- class X(object): def __init__(self, J) - "class X has-a __init__ that takes self and J parameters."
- class X(object): def M(self, J) - "class X has-a function named M that takes self and J parameters."
- foo = X() - "Set foo to an instance of class X."
- foo.M(J) - "From foo get the M function, and call it with parameters self, J."
- foo.K = Q - "From foo get the K attribute and set it to Q."

Flash cards for practicing the above is available here: http://www.cram.com/flashcards/learning-to-speak-object-oriented-6273469

A little Python hack script that will drill you on these words you know in an infinite manner:


```python
import random
from urllib import urlopen
import sys

WORD_URL = "http://learncodethehardway.org/words.txt"
WORDS = []

PHRASES = {
    "class %%%(%%%):":
      "Make a class named %%% that is-a %%%.",
    "class %%%(object):\n\tdef __init__(self, ***)" :
      "class %%% has-a __init__ that takes self and *** parameters.",
    "class %%%(object):\n\tdef ***(self, @@@)":
      "class %%% has-a function named *** that takes self and @@@ parameters.",
    "*** = %%%()":
      "Set *** to an instance of class %%%.",
    "***.***(@@@)":
      "From *** get the *** function, and call it with parameters self, @@@.",
    "***.*** = '***'":
      "From *** get the *** attribute and set it to '***'."
}

# do they want to drill phrases first
#if len(sys.argv) == 2 and sys.argv[1] == "english":
#    PHRASE_FIRST = True
#else:
#    PHRASE_FIRST = False
PHRASE_FIRST = True

# load up the words from the website
for word in urlopen(WORD_URL).readlines():
    WORDS.append(word.strip())


def convert(snippet, phrase):
    class_names = [w.capitalize() for w in
                   random.sample(WORDS, snippet.count("%%%"))]
    other_names = random.sample(WORDS, snippet.count("***"))
    results = []
    param_names = []

    for i in range(0, snippet.count("@@@")):
        param_count = random.randint(1,3)
        param_names.append(', '.join(random.sample(WORDS, param_count)))

    for sentence in snippet, phrase:
        result = sentence[:]

        # fake class names
        for word in class_names:
            result = result.replace("%%%", word, 1)

        # fake other names
        for word in other_names:
            result = result.replace("***", word, 1)

        # fake parameter lists
        for word in param_names:
            result = result.replace("@@@", word, 1)

        results.append(result)

    return results


# keep going until they hit CTRL-D
try:
    while True:
        snippets = PHRASES.keys()
        random.shuffle(snippets)

        for snippet in snippets:
            phrase = PHRASES[snippet]
            question, answer = convert(snippet, phrase)
            if PHRASE_FIRST:
                question, answer = answer, question

            print question

            raw_input("> ")
            print "ANSWER:  %s\n\n" % answer
except EOFError:
    print "\nBye"
```

    class Blow has-a function named crow that takes self and blow, chicken, bulb parameters.
    > class Blow(object): def crwo(self, blow, chicken, bulb)
    ANSWER:  class Blow(object):
    	def crow(self, blow, chicken, bulb)
    
    
    From approval get the can function, and call it with parameters self, band, body, attempt.
    > approval.can(band, body, attempt)
    ANSWER:  approval.can(band, body, attempt)
    
    
    Make a class named Cloth that is-a Brake.
    > class Cloth(Brake)
    ANSWER:  class Cloth(Brake):
    
    
    class Basketball has-a __init__ that takes self and disgust parameters.
    > class Basketball(object): def __init__(self, disgust)
    ANSWER:  class Basketball(object):
    	def __init__(self, disgust)
    
    
    Set condition to an instance of class Chain.
    > condition = Chain()
    ANSWER:  condition = Chain()
    
    
    From change get the attention attribute and set it to 'calendar'.
    > change.attention = calendar
    ANSWER:  change.attention = 'calendar'
    
    
    Make a class named Cow that is-a Bath.
    > class Cow(Bath):
    ANSWER:  class Cow(Bath):
    
    
    From balance get the cellar function, and call it with parameters self, chicken, disease, arithmetic.
    > balance.cellar(chicken, disease, arithmetic)
    ANSWER:  balance.cellar(chicken, disease, arithmetic)
    
    
    class Belief has-a function named board that takes self and crush, bun, carriage parameters.
    > class Belief(object): def board(self, crush, bun, carriage):
    ANSWER:  class Belief(object):
    	def board(self, crush, bun, carriage)
    
    
    From coal get the beam attribute and set it to 'cream'.
    > coal.beam = 'cream'
    ANSWER:  coal.beam = 'cream'
    
    
    Set bean to an instance of class Crate.
    > exit()
    ANSWER:  bean = Crate()
    
    
    class Creature has-a __init__ that takes self and border parameters.
    

#Exercise 42: Is-A, Has-A, Objects, and Classes

Go through this piece of code and replace each ##?? comment with a comment that says ehether the next line represents an is-a or a has-a relationship and what that relationship is.


```python
## Animal is-a object (yes, sort of confusing) look at the extra credit
class Animal(object):
    pass

## Dog is-a Animal
class Dog(Animal):

    def __init__(self, name):
        ## Dog has-a name
        self.name = name
        
    def bark(self, n):
        for i in range(n):
            print "wof!",

## Cat is-a Animal
class Cat(Animal):

    def __init__(self, name):
        ## Cat has-a name
        self.name = name

## Person is-a object
class Person(object):

    def __init__(self, name):
        ## Person has-a name
        self.name = name

        ## Person has-a pet of some kind
        self.pet = None

## Employee is-a Person
class Employee(Person):

    def __init__(self, name, salary):
        ## Employee has-a name (superclass makes you able to run the __init__ in the parent class reliably)
        super(Employee, self).__init__(name)
        ## Employee has-a salary
        self.salary = salary

## Fish is-a object
class Fish(object):
    pass

## Salmon is-a Fish
class Salmon(Fish):
    pass

## Halibut is-a Fish
class Halibut(Fish):
    pass


## rover is-a Dog
rover = Dog("Rover")

## satan is-a cat
satan = Cat("Satan")

## mary is-a person
mary = Person("Mary")

## mary has-a cat
mary.pet = satan

## frank is-a Employee
frank = Employee("Frank", 120000)

## frank has-a Dog
frank.pet = rover

## flipper is-a fish
flipper = Fish()

## crouse is-a Salmon
crouse = Salmon()

## harry is-a Hallibut
harry = Halibut()

## Run code
frank.pet.bark(3)
```

    wof! wof! wof!
    

# Exercise 43: Basic Object-Oriented Analysis and Design

Recommended (newbie) process for solving problems with OOP (Top down process):

1. Write or draw about the problem.
2. Extract key concepts from 1 and research them.
3. Create a class hierarchy and object map for the concepts.
4. Code the classes and a test to run them.
5. Repeat and refine.

Bottom up (generally: "I find this process is better once you're more solid at programming and, are naturally thinking in code about prolems):

1. Take a small piece of the problem; hack on some code and get it to run barely.
2. Refine the code into something more formal with classes and automated tests.
3. Extract the key concepts you're using and try to find research for them.
4. Write a description of what's really going on.
5. Go back and refine the code, possibly throwing it out and starting over.
6. Repeat, moving on to some other piece of the problem.

This process is very good when you know small pieces of the overall puzzle, but maybe don't have enough information yet about the overall concept. 

See exercise for long text and code: http://learnpythonthehardway.org/book/ex43.html

#Exercise 44: Inheritance Versus Composition


















