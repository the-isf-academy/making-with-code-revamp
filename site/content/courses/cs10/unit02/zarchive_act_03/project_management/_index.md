---
title: Set Up
draft: true
---

## Project Management 

For this project, we will use Github’s project planning and development tools: `issues` and `project boards`.  
<br>

{{< code-action >}} **Start by going to your team's Github page.** You'll be using this page a lot during the development of your web app. We suggest bookmarking it for quick access. <br>`https://github.com/the-isf-academy/project_webapp_YOUR_PROJECT_TEAM_NAME`

### [Issues]


{{< code-action >}} **Open your team's `Issues`.** Each issue will represent a task that needs to be completed to build out a feature of your web app. Add each task from your User Stories doc as an individual `issue`. Feel free to add additional tasks you can think of. 

{{< figure src="images/courses/cs10/unit02/project_management_01.png" width="100%"  >}}

- ✔️For each task create a unique issue 
    - For each issue, under `Projects` select `Project Tracking`
    - For each issue, under `Milestone` select `1`, `2`, or `3` according to level of difficult (1 being easiest, 3 being most difficult) 
    - For each issue, we recommend adding notes in the "Write" section. 

### [Project Boards]

{{< code-action >}} **Open your team's `Projects` and select `Project Tracking`.** Github automatically pulls each new issue and categorizes it under the `To do` column.

{{< figure src="images/courses/cs10/unit02/project_management_02.png" width="100%"  >}}

✔️ Updating issues and your project board, allows you and the teaching team to easily see the development status of your web app. 

0. Every time you start on a new task, move it to the `In progress` column
0. Every time you complete a task, select the issue and click `Close issue`. This will automatically move it to the `Done` column and progress your milestone. 




We suggest you reference this board often to keep on track with your application. 


## Repo Management 
Each team will have one project repository. This will require close communication with team members to ensure merging individuals' work is seamless. 

### [Cloning Repo]

{{< code-action >}} Clone your project repository: 

```shell
$ cd cs10/unit02
$ git clone https://github.com/the-isf-academy/project_webapp_YOUR_PROJECT_TEAM_NAME.git
```

### [Advanced Git]

When using Git as an individual, the primary action is to `push` your work to the server. However, when multiple people are working on a single project you must remember to `pull` before beginning to code. 

Be sure to follow these steps: 

0. `git pull`
0. resolve merge conflicts
0. update files 
0. `git status`
0. `git add`
0. `git commit`
0. `git push`

### [Heroku]

Up until this point, although we've been building web app we've only been interacting with them on your local machine. For this project, you will be able to push your work live to the web! 

{{< code-action >}} To set up this functionality, copy and past the following into the terminal:
```shell
$ cd project_webapp_YOUR_PROJECT_TEAM_NAME
$ brew tap heroku/brew && brew install heroku
$ heroku git:remote -a cs10-team-name
```

To push to the web follow these steps:

0. add all updated files
0. commit files
0. push to github: `git push`
0. push to heroku remote: `git push heroku main`
0. check deployment: `heroku open`

We don't recommend pushing to Heroku after every edit. Pushing live to the web should primarily be done after you are confident in update. 
