---
title: 1. Pet Lab
# draft: true
---

# Pet Lab

{{< devnote >}}
- move checkpoint qs to form
- change to VScode 
- add nap() and play()
- create a family of pets v. interface

{{< /devnote >}}

👀 **In this lab, you will learn about object oriented programming.** You will create the backend of a pet simulator game.

📖 **A few helpful resources:**
- Creating a Class: [12.5 Constructors](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_5)
- Inheritance: [12.6 Inheritance](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_6)

---

## [0] Setup
{{< code-action "Start by going into your" >}} `cs9/unit02_games` **folder.**
```shell
cd ~/desktop/cs9/unit_02
```

{{< code-action "Then, clone your starter code." >}} Be sure to change `YOUR-GITHUB-USERNAME` to your actual Github username.
```shell
git clone https://github.com/the-isf-academy/lab_pet_yourgithubusername
```

This lab includes the following files:
- `pet.py`
- `test_pet.py`
- `game_interface.py`
- `helpers.py`

---

## [1] Testing your Pet

{{< code-action  >}} **Open the folder in VSCode**
```shell
code .
```

{{< look-action >}} **First, we will focus on `pet.py` and `test_pet.py`**
- `pet.py` is the definition of a Python class for `Pet`
- `test_pet.py` is simple file just for testing our `Pet`


{{< code-action >}} **Let's start by running `test_pet.py`** 
```shell
python test_pet.py
```
```
Peanut
👋 Hi, I'm Peanut!
```

{{< code-action >}} **Create a `Pet` by storing it in the variable `my_pet`**
> *Do not copy the "> > >". This is to signify we are using the Python shell.*

```shell
>>> my_pet = Pet()
```

{{< code-action "Now that you've created a pet, let's give it a name." >}} I've named mine Ajax. You can name yours whatever you'd like.
```shell
>>> my_pet.set_name("Ajax")
```

{{< code-action >}} **Check the name was stored in `my_pet`.**
```shell
>>> my_pet.name
Ajax
```

{{< code-action "Have your pet introduce itself" >}}
```shell
>>> my_pet.introduce()
Hi, Im Ajax
```



{{< code-action "Try out these other methods in the terminal." >}}
```shell
>>> my_pet.play()
>>> my_pet.nap()
```



{{< checkpoint >}}
On the worksheet, answer the questions below before moving on.

0. What happens if you try to get your pet to take two naps in a row?
0. What happens if you play twice in a row without napping in between?
0. Can you change the name after it's already set?
0. Can you create 2 pets at the same time?

{{< /checkpoint >}}

{{< code-action "Exit the Python shell interface by typing" >}} `^D`.
Your pet and its name will not be saved.

---

## [2] What type of animal is your pet?

Now that you've used the `Pet` class, let's delve into the code and make our `Pet` more complex. People can have all different types of pets, so lets' add a `species` property to our `Pet`.

{{< code-action  >}} **Open `pet.py` in VSCode**
```shell
code pet.py
```

---

### [What's a class?]

In the Python interactive shell, **you just successfully created and used an instance of a class!**

{{< look-action >}} If you look in the Pet class, you can see on `line 1` - that we name the class `Pet`. **A class a simply a blueprint for group of data, or information, with specific functionalities.** In this class we are creating a blueprint for storing information about pets. Our pet will be able to talk, nap, and play.

```python {linenos=table, hl_lines=["1"],linenostart=1}
class Pet:
    def __init__(self):
        '''This initializes the pet with its properties.'''

        self.name = None        # holds the pet's name
        self.bored = True       # holds the pet's bored level
```

---

### [Adding a new property]

{{< look-action >}} The information associated with a `Pet` is defined on `lines 5-7`. **Information associated with a class is called `property` and is stored in a variable.** Our pet has three properties. Properties are variables that only belong to a specific class.

```python {linenos=table, hl_lines=["5-7"],linenostart=1}
class Pet:
    def __init__(self):
        '''This initializes the pet with its properties.'''

        self.name = None        # holds the pet's name
        self.bored = True       # holds the pet's bored level
```
>The `Pet` currently two properties, `name` and `bored`.


{{< code-action  >}} **Add a `species` property to the `Pet` class that is initially set to `None`.** It will work just like the `name` property.

---

### [Adding a new method]

Now that we've added the `species` property, we need to add a method to change the property.

{{< look-action >}} If you scroll down to lines 9-12, we see an example of a method. **A method is similar to a function. The only difference is that a method belongs to a certain class, like `Pet`.**


```python {linenos=table, linenostart=9}
def set_name(self, name):
    '''This method sets the name property'''

    self.name = name
```
> The `set_name()` method changes the `name` property to whatever the user put as the parameter.
>
> *e.g. `my_pet.set_name('Bob')`*

Just like the `name` property, we need to be able to set the `species` of our pet.

{{< code-action "Add a new method called " >}} **`set_species()`.** This method should change the `species` property of the `Pet` class.

---

### [Testing your changes]

Let's see if the `species` property and `set_species()` method is working by jumping back into the Python shell.

```shell
python3 -i pet.py
```

{{< code-action "Test your changes by typing these in the terminal one at a time." >}} You can set your species to whatever kind of pet you want!
> *Do not copy the "> > >". This is to signify we are using the Python shell.*

```shell
>>> my_pet = Pet()
>>> my_pet.set_species("fox")
>>> my_pet.species
fox
```
*Remember, when you're finished using the shell, you can exit by typing `^D`.
Your pet and its species will not be saved.*

---

### [Using the species property]

Right now, the `introduce()` method just has the pet say their name. Let's make it more detailed by including their `species` in the introduction.

```python {linenos=table, linenostart=14}
def introduce(self):
    '''This method introduces the pet with its name.'''

    print("Hi, I'm", self.name)
```
<br>

{{< code-action  >}} **Edit the `introduce()` method so that your pet will also tell you its species.**

{{< code-action  >}} **Test the updated `introduce() `method using the shell.** If you need a reminder of how to do this, check the earlier examples at the beginning of the lab.

---


## [2] What's wrong with my pet?

Wouldn't it be nice if your pet could tell you whether it wanted to play or take a nap? Right now, the only way to know for sure is to print out the properties.
Let's add a new method that allows the `Pet` to communicate.

{{< code-action >}} **Add a new method called `status()`.** It should print out what the `Pet` currently needs.

- If `tired` is `True`,
    - then the pet needs a `nap()`
- If `bored` is `True`
    - then, the pet wants to `play()`

> *Be sure consider the current state of the `tired` and `bored` property.*

> ```shell
> python3 -i pet.py
> >>> my_pet = Pet()
> >>> my_pet.set_name('Peanut')
> >>> my_pet.set_species('Dog')
> >>> my_pet.status()
> "I'm bored! Let's go for a walk!"

---

## [3] Pet Simulator


👾 **Now that you have experienced the backend of the `Pet`, let's play the game!** The `Pet` now has a nice Terminal interface where you can interact with it through a menu system, just like a lo-fi video game.
```shell
python game_interface.py
```

```shell
-----------------------------------
---- Welcome to Pet Simulator ----
----------------------------------- 

What would you like to name your pet?
 > Peanut
-------------------------
Your pet is ready!
-------------------------
> Introduce                                                                                                                
  Quit         
```

---

### [play]

{{< code-action >}} **Edit `game_interface.py` so you can `play()` with your `Pet`!**

{{< code-action >}} **Play test it:** `python game_interface.py`

---

## [3] Deliverables


{{< deliverables  >}}

**Once you've successfully completed the game be sure to fill out [this Google form](https://docs.google.com/forms/d/e/1FAIpQLScz0x6-s3GRD9P7oZlcqq24XifGDTw9BQ_j8t8TIqqRYw0naw/viewform?usp=sf_link)**.


{{< code-action "Push your work to Github:" >}}
- git status
- git add file_name.py file_name2.py
- git status
- git commit -m "describe your drawing and your process here"
  > be sure to customize this message, do not copy and paste this line
- git push

{{< /deliverables >}}

---

## [3] Extension

### [Add a hunger level]

At this point, you have a working `Pet`, but it's pretty basic. Most pets, get hungry and need to eat. 

**This will require you to add a `hunger` property and `eat()` method.**

**Your `hunger` property should:**
- be an numerical data type
- decreased when it plays 
- increase when it uses `eat()`

{{< code-action >}} **Test your edits with the `python shell`.**  


{{< code-action >}} **Edit `interface.py` to include all of the features the `Pet` has.**

{{< code-action >}} **Play test it:** `python game_interface.py`

---

### [Tamagotchi Features]

This lab was inspired by the Tamagotchi!

{{< figure src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/Tamagotchi_0124_ubt.jpeg/330px-Tamagotchi_0124_ubt.jpeg" width="40%" >}}

{{< code-action >}} **Include as many of the original Tamagotchi features as you can!**
- [Tamagotchi wiki](https://en.wikipedia.org/wiki/Tamagotchi)