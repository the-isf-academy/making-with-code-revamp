---
Title: Project
# draft: true
---

# Unit 02 Games Story Project

In this project you will make a text-based game! It is totally up to you what type of story you make. For example you could make:
- choose your own adventure game 
- exploration game
- puzzle game 
- narrative story game

{{< figure src="https://steamuserimages-a.akamaihd.net/ugc/1791848543425884907/18A8A93A2B7215E654F50350F4C896FFE463B456/" width="70%" >}}
> [*Zork*](https://en.wikipedia.org/wiki/Zork) is often noted as one of the best video games of all time. 
>
>*"What Zork seemed to contribute more than anything was the idea that the computer could simulate a rich virtual environment" - [Matt Barton](https://web.archive.org/web/20220809014122/https://www.gamedeveloper.com/pc/the-history-of-zork)*

---


## [0] Explore Games


👾 **Start by exploring a couple of example choose your own adventure games.** As you play, consider the different genres and what's possible with this structure. 
- [Harry Potter - Sorting Hat](https://unfold.studio/stories/303/)
- [Oregon Trail 1971](https://unfold.studio/stories/10782/)
- [City Exploration](https://unfold.studio/stories/2649/)
- [Store front Example, variables](https://unfold.studio/stories/1065/)


---

## [0] Planning Document

This is a big project with a lot of room for customization. You will need to:
- outline your story in a graph diagram 
- plan the implementation of an additional feature 

It is important for you to plan the game prior to coding. 

{{< write-action "Plan your game prior to coding in your Google Doc:" >}} Unit 02: Games  - Story Project Planning Document


---


##  [1] Set Up

{{< code-action "Start by going into your" >}} `cs9/unit02_games` **folder.**
```shell
cd ~/desktop/making_with_code/cs9/unit02_games
```

{{< code-action "Clone your starter code." >}} Be sure to change `yourgithubusername` to your actual Github username.
```shell
git clone https://github.com/the-isf-academy/project_game_story_yourgithubusername
```

{{< code-action "Enter the Poetry shell and install the requirements:" >}}
```shell
poetry shell
poetry install
```

This repo includes the following files:
 - `game.py` when this program runs, it should launch your game
    - `view.py`
    - `story_setup.py`
    - `story.py`
    - `node.py`
    - `README.md` - a brief description of your game


---
## [2] Assessment


✅  **This project will be assessed on the following criteria:**
- **Planning [3]** 
    - I can consider the components of my game before coding
    - I can create a graph diagram to outline the branches of my story
    - game outline
    - graph diagram 
    - feature architecture 
- **Iterative Development [3]**
    - I can track the development of my project by successfully committing to Github a minimum of each class work day, preferably after each work session
    - I can write descriptive commit messages that accurately describe the changes made
    - I can systematically breakdown my project into smaller chunks  
- **Readability [3]**
    - I can write code as readable as possible for another CS student to understand
    - I can use descriptive names for modules, variables, classes, and methods
    - I can write descriptive comments to describe complex pieces of the code
    - I can design a `View` that is easily to read and understand 
- **Feature implementation [3]**
    - feature architecture here? 
    - abstraction 
- **Game implementation [3]**
    - I can write game with story that is fully functional 
    - I can properly implement my graph diagram




**For each criteria you will be assessed on a score from 0-3. With 9 criteria, there is a total of 9 potential points.** 
- 0 - no evidence of the practice
- 1 - limited evidence of the practice
- 2 - adequate evidence of the practice
- 3 - substantial evidence of the practice

{{< expand "Scoring Breakdown" >}}

The project is scored out of 7. 

*To calculate your score for the practices & concepts, look at the following bands:*

- 1 = 0
- 2 = 1
- 3 = 2
- 4 = 3-4
- 5 = 5-6
- 6 = 7-8
- 7 = 9
{{< /expand >}}


---

## [4] Deliverables

{{< deliverables  "Projects are due on Wednesday, 02 March." >}}

- A `Web Design Project | Design Specification Document` - a Google Doc
- A `yourgithubusername.github.io` repository 

- A `Unit 02 Games Project: Planning Document` 
- A `project-game-story` repository will include some if not all the following files:
    - `game.py` when this program runs, it should launch your game
    - `view.py`
    - `story_setup.py`
    - `story.py`
    - `node.py`
    - `README.md` - a brief description of your game


---

**🗓️ Timeline**

**You have 5 in class days to complete this project.**

- begins on Monday, 24 April 
- due on Monday, 08 May 

---

{{< code-action "Push your work to Github:" >}}
- `git status`
- `git add game.py`
    - you can add all of the changed files with: `git add -A`
- `git status`
- `git commit -m "your message goes here"`
    - be sure to customize this message, do not copy and paste this line
- `git push`
{{< /deliverables >}}

---



