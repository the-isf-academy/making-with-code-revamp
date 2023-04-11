---
title: 2. Uno Lab
resources:
- name: Uno
  src: images/courses/cs9/unit02/02_01_uno.jpg
# draft: true
---

# Uno Lab

In this lab, you are going to go behind the scenes of the classic card game, Uno.

{{< figure src="images/courses/cs9/unit02/02_01_uno.jpg" width="400px" >}}

## [0] Let's Play Uno

🃏 **Let's start by playing the classic card game, Uno.** As your playing, consider the different components and mechanics of the game. 

---

## [1] Setup

Now that you've been reminded of how to play Uno,  let's delve into a Python implementation of it.

{{< code-action >}} **In your `making_with_code/cs9/unit02_games` directory, clone the `lab-uno` repository inside it.**

## [0] Setup

{{< code-action "Start by going into your" >}} `cs9/unit02_games` **folder.**
```shell
cd ~/desktop/making_with_code/cs9/unit_02
```

{{< code-action "Clone your starter code." >}} Be sure to change `yourgithubusername` to your actual Github username.
```shell
git clone https://github.com/the-isf-academy/lab_uno_yourgithubusername
```


{{< code-action "Enter the Poetry shell and install the requirements:" >}}
```shell
poetry shell
poetry install
```

This lab includes the following files to play the Spelling Bee game:
- `spellingbee.py`
- `game.py`
- `view.py`

---

## [2] Play Test


{{< code-action >}} **Play through Uno in your Terminal.** 

```shell
python game.py
```

> If you're interested, you can find the [full rules of Uno here](http://play-k.kaserver5.org/Uno.html). Our implementation varies slightly. Can you identify the differences?

🤔 Was the gameplay different than you expected? 


---

### [Documentation]

Uno is a pretty significant software project - there are more classes than you've seen before.
 
It's up to you, to finish the documentation of Uno.

---

{{< checkpoint >}}
In your group, complete the worksheet. 
{{< /checkpoint >}}
s

---

## [3] Advanced Player the player 

As you've experienced, you are playing against a computer. The `ComputerPlayer` has 3 main methods.
- `get_playable_cards()`
- `play_card()`
- `choose_color()` 

However, the current computer is not very intelligent. It doesn't always play a valid card on a wild and it always chooses 'red' if it plays a wild.
  
**Let's make a slightly more competitive computer by considering the best strategy for uno.** 

It's up to you to extend the [`ComputerPlayer`](https://cs.fablearn.org/docs/uno/player.html#player.ComputerPlayer) class and complete the `StrategicComputerPlayer` class:

**You will need to override the following methods of `StrategicComputerPlayer` with the correct functionality:**
- `choose_color()`
- `choose_card()`

**🤔 Your goal: write a strategic computer that consistently wins more than 30% of games against 2 other computer players who are using a random valid choice strategy.** Consider the rules and mechanics of Uno. Given a hand of cards, what would make playing one card better than playing another card? 



{{< code-action >}} **Finish `StrategicComputerPlayer` to implement a strategic strategy.**
> You may want to read more about [inheritance](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_6).

{{< code-action >}} **Test your strategy by running:**
```shell
python test_lab.py -k strategy
```

---

## [5] Deliverables

{{< deliverables "Push to Github." >}}

For this lab, you should push your `lab-uno` repository containing updates to the following files:
  - `game.py`
  - `player.py`

{{< /deliverables >}}

---


## [6] Extension:

Now that you've got a fully functional Uno game, let's expand its functionality. 


### [Saying Uno]

Currently, there is no way to system in place for saying 'Uno'. It's up to you to add in that feature!

{{< code-action >}} **Add a 'saying Uno' feature into the game.** Be sure to consider:
- how will you allow the player to say 'Uno'?
- how will you keep track if the player said 'Uno' at the correct time? 
- how will you allow the player to say 'Uno' and play a card? 
- how will you penalize the player if they forget to say 'Uno? 

👾 **Play test your feature to ensure it works as intended!** 
> 🤔 *How would you add in this feature to the `ComputerPlayer`?*
---

### [Advanced Deck Building]

Cards are read into the deck as entries in a csv file. Look at the `deck.py` module and you'll note that we're using pandas to read the cards, looks like those data science skills will come in handy after all!

{{< look-action >}} **Take a look at the current cards in `uno_cards.csv`.** As you can see, each card is on a new line and commas separate their properties. 

{{< code-action >}} **Create your own deck and add a new special card by writing new a csv file.** Just create a new csv file with the name of your special card in the special column.

{{< code-action >}} **Implement your special card in the `UnoGame` class.**

👾 **Play test your new deck to ensure it works as intended!** 




 <!-- Fortunately, [Uno's functionality is well documented](https://cs.fablearn.org/docs/uno/index.html).

- [Game](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame)
- [View](https://cs.fablearn.org/docs/uno/view.html#view.TerminalView)
- [Card](https://cs.fablearn.org/docs/uno/card.html#card.Card)
- [Deck](https://cs.fablearn.org/docs/uno/deck.html#deck.Deck)
- [Player](https://cs.fablearn.org/docs/uno/player.html#player.Player)
    - [HumanPlayer](https://cs.fablearn.org/docs/uno/player.html#player.HumanPlayer)
    - [ComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.ComputerPlayer)
        - [RandomComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.RandomComputerPlayer)
        - [StudentComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.StudentComputerPlayer) -->


