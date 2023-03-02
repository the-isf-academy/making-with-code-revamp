---
title: 2. Uno Lab
resources:
- name: Uno
  src: images/courses/cs9/unit02/02_01_uno.jpg
draft: true
---

# Uno Lab

In this lab, you are going to go behind the scenes of the classic card game, Uno.


{{< figure src="images/courses/cs9/unit02/02_01_uno.jpg" width="400px" >}}

Your tasks:

0. Learn about how class inheritance works in Python
0. Add special cards to make the game more interesting
0. Write a random strategy for a computer player

## [0] Let's Play Uno

🃏 **Let's start by playing the classic card game, Uno.** As your playing, consider the different components and mechanics of the game. 

{{< checkpoint >}}
In your group, complete the worksheet. 
{{< /checkpoint >}}

---

## [1] Setup

Now that you've got a model for how the Uno software should work, let's delve into the code.

{{< code-action >}} **In your `cs9/unit_02` directory, clone the `lab-uno` repository inside it.**

```shell
cd cs9/unit_02
git clone https://github.com/the-isf-academy/lab-uno-YOUR-GITHUB-USERNAME.git
```

{{< code-action >}} **Install the packages you need to run this lab:**
```shell
cd lab-uno-YOUR-GITHUB-USERNAME
pip3 install --upgrade -r requirements.txt
```

---


### [Documentation]

Uno is a pretty significant software project - there are more classes than you've seen before. Fortunately, [Uno's functionality is well documented](https://cs.fablearn.org/docs/uno/index.html).

- [Game](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame)
- [View](https://cs.fablearn.org/docs/uno/view.html#view.TerminalView)
- [Card](https://cs.fablearn.org/docs/uno/card.html#card.Card)
- [Deck](https://cs.fablearn.org/docs/uno/deck.html#deck.Deck)
- [Player](https://cs.fablearn.org/docs/uno/player.html#player.Player)
    - [HumanPlayer](https://cs.fablearn.org/docs/uno/player.html#player.HumanPlayer)
    - [ComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.ComputerPlayer)
        - [RandomComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.RandomComputerPlayer)
        - [StudentComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.StudentComputerPlayer)

---

## [2] Play Test


{{< code-action >}} **Play through Uno in your Terminal.** Start with the "basic deck".

```shell
python3 game.py
```
> If you're interested, you can find the [full rules of Uno here](http://play-k.kaserver5.org/Uno.html). Our implementation varies slightly. Can you identify the differences?

🤔 Was the gameplay different than you expected? 

---


### [Special Cards]

Uno would be pretty boring if you just went around in a circle matching colors and numbers. Fortunately, **Uno has special cards that make the game more interesting:**

- **reverse:** changes the direction of play from clockwise to counterclockwise or vice versa
- **skip:** skips the next player's turn
- **wild:** can be played on any card and lets the player call the color to be played next
- **draw-two:** forces the next player to draw two cards (they still get a turn)
- **wild-draw-four:** the current player calls the color *and* the next player has to draw 4 cards

Other than the wild cards, all of the special cards have colors and must be played following the color/value matching rule of the game.

{{< code-action >}} **Try playing again, but this time use the select the "special no draw deck".**
> This deck includes the reverse, skip, and wild cards. 


---

## [3] Implement Draw Cards

Your version of Uno is almost complete. **All you need to do is finish the special cards by writing the code for:**

- [draw_two()](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame.draw_two)
- [wild_draw_four()](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame.wild_draw_four)

> This deck can be played by selecting "special with draw deck" from the game menu.

### [Draw Two]

{{< code-action >}} **Implement the `draw_two()` method  near the bottom of the `game.py` file in the [UnoGame](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame) class.**

{{< code-action >}} **Add the function calls to the [special_card_action()](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame.special_card_action) method.**

{{< code-action >}} **Test your method by running the test script:`python3 test_lab.py -k draw_two`.**
> If successful, you will see a message like so: 
> ```shell
> Ran 1 test in 0.009s
>
>OK
>```
---

### [Wild Draw Four]

{{< code-action >}} **Implement the `wild_draw_four()` method in the [UnoGame](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame) class.**

{{< code-action >}} **Add the function calls to the [special_card_action()](https://cs.fablearn.org/docs/uno/game.html#game.UnoGame.special_card_action) method.**

{{< code-action >}} **Test your method by running the test script: `python3 test_lab.py -k wild`.**
> If successful, you will see a message like so: 
> ```shell
> Ran 1 test in 0.009s
>
>OK
>```

---

## [4] AI: Random Strategy

Currently the computer strategy is quite simple: 
- when it chooses a card, it picks the last card in its hand (regardless if it's valid)
- when its asked to choose a color, it always chooses red
  
**Let's make a slightly more competitive computer by introducing randomness.** 

It's up to you to extend the [`ComputerPlayer`](https://cs.fablearn.org/docs/uno/player.html#player.ComputerPlayer) class and complete the `RandomComputerPlayer` class:

**You will need to override the following methods of `RandomComputerPlayer` with the correct functionality:**
- `choose_color()` - random chooses red, green, blue, or yellow
- `choose_card()` - randomly selects a valid card from its hand if a valid card exists


{{< code-action >}} **Finish `RandomComputerPlayer` to implement a random strategy.**
> You may want to read more about [inheritance](http://programarcadegames.com/index.php?chapter=introduction_to_classes&lang=en#section_12_6).

{{< code-action >}} **Test your implementation by playing Uno without any human players and selecting "random" strategy.** 


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

### [A Wining Strategy]

🤔 **Start thinking about the best strategy to win games.**  Consider the rules and mechanics of Uno. Given a hand of cards, what would make playing one card better than playing another card? 

**Your goal: write a strategic computer that consistently wins more than 30% of games against 2 other computer players who are using a random valid choice strategy.**

{{< code-action >}} **Implement the [StrategicComputerPlayer](https://cs.fablearn.org/docs/uno/player.html#player.StudentComputerPlayer) class in the `player.py` module.**

{{< code-action >}} **Test your strategy by running `python test_lab.py -k strategy`**

---

### [Advanced Deck Building]

For this implementation of the game, cards are read into the deck as entries in a csv file. Look at the `deck.py` module and you'll note that we're using pandas to read the cards  looks like those data science skills will come in handy after all!

{{< code-action >}} **Create your own deck and add a new special card by writing new a csv file.** Just create a new csv file with the name of your special card in the special column.

{{< code-action >}} **Implement your special card in the `UnoGame` class.**


--

## [7] File Updates

{{< code-action "Copy and paste the following updates into your files." >}} 

{{< expand "game.py: bottom of file" >}}

```python
if __name__ == "__main__":
    view = TerminalView()

    view.welcome()

    rounds = int(view.get_input("How many rounds do you want to play for?"))

    deck_file = view.menu("Choose a deck",["basic deck","special no draw deck","special with draw deck"])

    if deck_file == "basic deck":
        deck_file = "uno_cards_basic.csv"
    elif deck_file == "special no draw deck":
        deck_file = "uno_cards_special_no_draw.csv"
    elif deck_file == "special with draw deck":
        deck_file = "uno_cards_special_with_draw.csv"
    
    human_players = view.menu("Do you want a human player?",["yes","no"])

    if human_players == "yes":
        name = view.get_input("What is your name?")
        num_computers = 2

    else:
        name = None
        num_computers = 3

    computer_strategies = []
    
    for i in range(num_computers):
        computer_strategies.append(view.menu("What strategy should the Computers use? ",["basic","random","strategic"]))
    

    game = UnoGame(view, name, computer_strategies, deck_file, rounds*3)

    game.play()

    view.end_game()
```

{{< /expand >}}

{{< expand "game.py: __init__" >}}
```python
def __init__(self, game_view, human_names, computer_strategies, deck_file=None, total_turns=10):
        self.view = game_view
        self.turns_remaining = total_turns
        self.deck = Deck(deck_file)
        self.discard = Deck()
        self.direction = self.CLOCKWISE
        self.current_player_index = 0
        self.top_card = self.deal_one_card()

        if "wild" in self.top_card.special:
            self.top_card.color = choice(self.COLORS)
        self.players = []

        if human_names != None:
            self.players.append(HumanPlayer(name))

        for i in range(0,len(computer_strategies)):
            if computer_strategies[i] == "random":
                self.players.append(RandomComputerPlayer("Computer {} ({})".format(i, computer_strategies[i])))

            elif computer_strategies[i] == "strategic":
                self.players.append(StrategicComputerPlayer("Computer {} ({})".format(i, computer_strategies[i])))

            else:
                self.players.append(ComputerPlayer("Computer {} ({})".format(i, computer_strategies[i])))
```
{{< /expand >}}

{{< expand "game.py: play-turn()" >}}
```python
def play_turn(self):
        """ Plays one round of uno

        Returns:
            (bool) whether the game has been won by the current player
        """
        player = self.current_player()
        self.view.show_beginning_turn(player, self.top_card)

        if type(player) == HumanPlayer:
            card = player.choose_card(self.view,self.top_card)
        else:
            card = player.choose_card(self.top_card)




        if card:
            self.view.show_played_card(player, card)
            if self.valid_card_choice(card):
                if self.top_card.special == 'wild' or self.top_card.special == 'wild-draw-four':
                    self.top_card.color = None   #reseting the color of the wild card before it goes into the discard pile
                self.discard.add_card(self.top_card)
                self.top_card = card

                if len(player.hand) == 0:
                    return True
                if card.special:
                    self.special_card_action(card)

            else:
                self.view.show_invalid_card(player, card, self.top_card)
                player.add_to_hand(card)
                self.deal_n_cards(2, player)
        else:
            self.deal_n_cards(1, player)

        self.increment_player_num()
        return False
```
{{< /expand >}}

{{< expand "test_lab.py" >}}

```python
# Testing file for bank lab
# By: Chris Proctor and Jacob Wolf and Emma Brown

# =============================================================================
# ☕️ More-Than-You-Need-To-Know Lounge ☕️
# =============================================================================
# Welcome to the More-Than-You-Need-To-Know Lounge, a chill place for code that
# you don't need to understand.

# Thanks for stopping by, we hope you find something that catches your eye.
# But don't worry if this stuff doesn't make sense yet -- as long as we know
# how to use code, we don't have to understand everything about it.

# Of course, if you really like this place, stay a while. You can ask a
# teacher about it if you're interested.
#
# =============================================================================

import unittest
import sys, io
from tqdm import tqdm
from collections import defaultdict


from game import UnoGame
from card import Card
from view import TerminalView

class TestUnoLab(unittest.TestCase):

    def test_draw_two(self):
        """
        Test checking the implementation of the draw_two() function.
        """
        game = UnoGame(TerminalView(), None,['basic','basic','basic'], "uno_cards_special_with_draw.csv", 10)
        draw_two = Card("red", None, "draw-two")
        game.top_card = draw_two
        game.special_card_action(draw_two)
        next_player = game.next_player()
        self.assertTrue(len(next_player.hand) == 2)
        game.special_card_action(draw_two)
        self.assertTrue(len(next_player.hand) == 4)
        game.increment_player_num()
        game.special_card_action(draw_two)
        next_player = game.next_player()
        self.assertTrue(len(next_player.hand) == 2)
        reverse = Card("red", None, "reverse")
        game.top_card = reverse
        game.special_card_action(reverse)
        game.top_card = draw_two
        game.special_card_action(draw_two)
        next_player = game.next_player()

        self.assertTrue(len(next_player.hand) == 2)


    def test_wild_draw_four(self):
        """
        Test checking the implementation of the wild_draw_four() function.
        """
        game = UnoGame(TerminalView(), None,['basic','basic','basic'], "uno_cards_special_with_draw.csv", 10)
        wild_draw_four = Card(None, None, "wild-draw-four")
        game.top_card = wild_draw_four
        game.special_card_action(wild_draw_four)
        next_player = game.next_player()
        self.assertTrue(len(next_player.hand) == 4)
        self.assertTrue(game.top_card.color == "red")
        game.special_card_action(wild_draw_four)
        self.assertTrue(len(next_player.hand) == 8)
        self.assertTrue(game.top_card.color == "red")
        game.increment_player_num()
        game.special_card_action(wild_draw_four)
        next_player = game.next_player()
        self.assertTrue(len(next_player.hand) == 4)
        reverse = Card("red", None, "reverse")
        game.top_card = reverse
        game.special_card_action(reverse)
        game.top_card = wild_draw_four
        game.special_card_action(wild_draw_four)
        next_player = game.next_player()
        self.assertTrue(len(next_player.hand) == 4)


    def test_strategy(self):
        """
        Test to see if student strategy can beat the random strategy
        """
        print("\n\nTESTING STUDENT'S COMPUTER STRATEGY.")
        print("STUDENT'S COMPUTER STRATEGY SHOULD WIN A HIGHER PERCENTAGE OF GAMES THAN THE RANDOM STRATEGY.")
        print("PLAYING 1000 Strategy (Computer O) vs RANDOM (Computer 1) GAMES :")

        game_stats = defaultdict(lambda : 0)
        for i in tqdm(range(1000)):
            stdout = sys.stdout
            sys.stdout = io.StringIO()

            game = UnoGame(TerminalView(), None, ['strategic','random'],  "uno_cards_special_with_draw.csv", 500)
  
            winner = game.play()
            game_stats[winner] += 1
            sys.stdout = stdout

        print("\nTEST COMPLETE. GAME STATS:")
        print("_______________________________")
        print("| Player.................Win % |")
        for player, wins in game_stats.items():
            print("| {}...{}% |".format(player, round(wins/1000*100,2)))
        print("|______________________________|")
        self.assertTrue(game_stats["Computer 0 (strategic)"]/1000 > 0.3)


unittest.main()
```

{{< /expand >}}