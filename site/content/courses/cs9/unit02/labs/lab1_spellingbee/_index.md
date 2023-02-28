---
title: 1. Spelling Bee
draft: true
---

# Spelling Bee

In this lab, you will learn about the different layers that make up a game.

## [0] Play the Game

Let's start by playing Spelling Bee!

Play the game at [https://www.nytimes.com/puzzles/spelling-bee](https://www.nytimes.com/puzzles/spelling-bee).

{{< checkpoint >}}

✏️ Complete the worksheet with your partner. 

{{< /checkpoint >}}

---

## [0] Setup

{{< code-action "Clone your starter code." >}} Be sure to change `YOUR-GITHUB-USERNAME` to your actual Github username.
```shell
cd desktop/cs9/unit_02
git clone https://github.com/the-isf-academy/lab-spellingbee-YOUR-GITHUB-USERNAME.git
```

This lab includes the following files to play the Spelling Bee game:
- `spellingbee.py`
- `game.py`
- `view.py`

---

## [1] Fixing the View 

In this version of Spelling Bee, the game is separated into 3 distinct layers:
- game structure (`spellingbee.py`)
- game logic (`game.py`)
- game communication to the user (`view.py`)

The game strucutre and the game logic work as is and replicates the web version. It's up to you to finish the communication to the user. 

### [Play the Game]

{{< code-action "Let's start by playing the game." >}} 

```shell
python3 game.py
```

It runs like so:
```shell 
---Welcome to Spelling Bee---

[RULES]
You can use any of these letters: ['T', 'C', 'O', 'L', 'I', 'N', 'M']
You must you use the letter M

---Mystery Method 2---
 > 

---Mystery Method 6---

---Mystery Method 2---
 > 
```

**It works perfectly, but the messages are a mystery!**

---

### [Solving the Mysteries]

The `View` class is purely responsible for the communication of what is happening in the game with the user. It does not affect the game flow or logic. 

The `View` is unique in that it only has methods and has no properties. It's methods are only responsible for printing information and getting user input. 

**It's up to you to solve the mystery methods and fix the `View`!** This will require you to undersatnd the logic of the game in `game.py`. 

{{< code-action >}} **Edit each `mystery_method` in the `View` class so the messages accurately communicate to the user what is happening the game.** 

{{< code-action >}} **Make the code more readable by renaming all of the `mystery_methods` in the `View`.** 
> *Once you change the name of a method in the `View`, you will also need to change it in `game.py`*

{{< code-action >}} **Play test your and make sure it works bug free!** 

{{< code-action >}} **Play test your partner's game and see how they implented their `View`!** 


## [3] Deliverables

{{< deliverables "Push to Github." >}}

Push your `lab-spellingbee` to Github.


{{< /deliverables >}}

---

## [3] Extension: Menu


Currently, this game does not have a menu system. **It's up to you to implement one!**


{{< code-action >}} **First, if you have not done so, install the simple-terminal-menu:** 

```shell
pip3 install simple-term-menu
```

{{< code-action >}} **Next, implement a menu system. The user should be able to:**

- make a guess
- view the rules 
- view their previous successful guesses
- quit the game

> *Hint: take a look at the `interface.py` file from the Pet lab*














