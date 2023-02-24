---
title: 0. Pet Lab
draft: true
---

# Pet Lab

{{< devnote >}}
- move checkpoint qs to form
- change to VScode 
- add nap() and play()
- create a family of pets v. interface

{{< /devnote >}}

In this lab, you will learn about object oriented programming. You will create the backend of a pet simulator game.

{{< expand "To learn more, visit the resources below" >}}

- Creating a Class: [12.5 Constructors](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_5)
- Inheritance: [12.6 Inheritance](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_6)

{{< /expand >}}

## [0] Setup
{{< code-action "Start by making a new folder in your" >}} `cs9` **folder.**
```shell
cd Desktop/cs9
mkdir unit_02
cd unit_02
```

{{< code-action "Then, clone your starter code." >}} Be sure to change `YOUR-GITHUB-USERNAME` to your actual Github username.
```shell
git clone https://github.com/the-isf-academy/lab-pet-YOUR-GITHUB-USERNAME.git
```

This lab includes the following files:
- `pet.py`
- `interface.py`
> *`interface.py` is only required for the extension*

---

## [1] Creating your own pet

In `pet.py` is a Python class that defines a `Pet`.

{{< code-action >}} **First, let's run `pet.py` in the interactive Python shell.**
```shell
python3 -i pet.py
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
In your notebook, answer the questions below before moving on.

0. What happens if you try to get your pet to take two naps in a row?
0. What happens if you play twice in a row without napping in between?
0. Can you change the name after it's already set?

{{< /checkpoint >}}

{{< code-action "Exit the Python shell interface by typing" >}} `^D`.
Your pet and its name will not be saved.

---

## [2] What type of animal is your pet?

Now that you've used the `Pet` object, let's delve into the code and make our `Pet` more complex. People can have all different types of pets, so lets' add a `species` property to our `Pet`.

{{< code-action  >}} **Open `pet.py` in atom**
```shell
atom pet.py
```

### [Adding a new property]

If you look in the Pet class, you can see on lines 5-7 that we have three properties. Properties are variables that belong to a specific class.


```python {linenos=table, hl_lines=["5-7"],linenostart=1}
class Pet:
    def __init__(self):
        '''This initializes the pet with its properties.'''

        self.name = None #The pet's name
        self.tired = False #Tells us if the pet is tired
        self.bored = True #Tells us if the pet is bored
```
>The `Pet` currently 3 properties, `name`, `tired`, and `bored`.


{{< code-action  >}} **Add a `species` property to the `Pet` class.** It will work just like the `name` property.

---

### [Adding a new method]

Now that we've added the `species` property, we need to add a method to change the property.

If you scroll down to lines 9-12, we see an example of a method. **A method is similar to a function. The only difference is that a method belongs to a certain class, like `Pet`.**


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

If `tired` is `True`, then the pet needs a `nap()`. If `bored` is `True`, the pet wants to `play()`.

Let's add a new method that allows the `Pet` to communicate.

{{< code-action >}} **Add a new method called `status()`.** It should print out what the `Pet` currently needs.
> *Be sure consider the current state of the `tired` and `bored` property.*

> ```shell
> python3 -i pet.py
> >>> my_pet = Pet()
> >>> my_pet.set_name('Peanut')
> >>> my_pet.set_species('Dog')
> >>> my_pet.status()
> "I'm bored! Let's go for a walk!"

---

## [3] Deliverables

{{< deliverables "Push to Github." >}}

Push your `lab-pet` to Github.

In your notebook, answer the questions below before moving on to the extension.

0. How do you create a new `Pet` with the name "Peanut" that is a dog?
0. What is the difference between a `property` and `method`?

{{< /deliverables >}}

---

## [3] Extension

### [Upgrade the Interface]

At this point, you have a working pet with multiple features! Now, let's develop the interface to make the `Pet` more like a video game.

{{< code-action >}} **First, run the following command in your terminal.** It will install a package for creating your own terminal menus.

```shell
pip3 install simple-term-menu
```

{{< code-action >}} **Next, run `interface.py`.** The `Pet` now has a nice Terminal interface where you can interact with it like a video game.

However, currently all you can do it:
- Create a `Pet`
- Set its `name`ss
- `play()` with it


{{< code-action >}} **Edit `interface.py` to include all of the features the `Pet` has.**

{{< code-action >}} **Add any additional features to the `Pet` and the interface!**
