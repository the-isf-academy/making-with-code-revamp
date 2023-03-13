---
title: Act III
bookCollapseSection: true
draft: true
---

# Act III: Django Unchained

In the final section of the project, you will build out your web app using the skills learned in Act II. 

<iframe src="https://giphy.com/embed/L3bj6t3opdeNddYCyl" width="480" height="266" frameBorder="0" class="giphy-embed" allowFullScreen></iframe><p><a href="https://giphy.com/gifs/rickandmorty-season-4-episode-2-rick-and-morty-L3bj6t3opdeNddYCyl"></a></p>


## Set Up
Each team will have one project repository. This will require close communication with team members to ensure merging individuals' work is seamless. 

### [Cloning Repo]

{{< code-action >}} Clone your project repository: 

```shell
cd cs10/unit02
git clone https://github.com/the-isf-academy/project-webapp-TEAM-MEMBERS.git
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

## Timeline

Click below to see a detailed timeline for your class section.

#### cs10.1
{{< expand "cs10.1 Timeline" >}}

| Date        | Agenda                  |
|-------------|-------------------------|
| 25 April 2022  | Start Development |
| 26 April 2022  | Work Day |
| 29 April 2022  | Work Day|
| 03 May 2022  | Work Day|
| 05 May 2022 | Due: Milestone 1      |

{{< /expand >}}

#### cs10.2

{{< expand "cs10.2 Timeline" >}}

| Date        | Agenda                  |
|-------------|-------------------------|
| 27 April 2022  | Start Development |
| 29 April 2022  | Work Day|
| 04 May 2022 | Due: Milestone 1        |
{{< /expand >}}

## Assessment

For Act III of this project, your group will be assessed on your ability to develop the frontend and backend of your web app. 

- Both your backend and frontend development will receive a score from 0-3
    - 0 - little to no evidence of the concept
    - 1 - limited evidence of the concept
    - 2 - adequate evidence of the concept
    - 3 - substantial evidence of the concept

Due to scheduling, each section's deliverables are as follows: 
- CS10.1 must complete 2 pages of their web app 
- CS10.2 must complete 1 page of their web app

## Success Claims

Successful computer scientists should be able to make the following claims:

- We can develop the backend architecture
    - Model fields with appropriate properties and methods 
    - Appropriate use of form that update the database
    - Django views are used to link backend and frontend  
    - Any known bugs are documented in the README.md 
- We can design the frontend of a webapp
    - Demonstration of html and css knowledge 
    - Use of bootstrap elements to support your design
    - Routes are defined and appropriately named for each view
    - Any known issues are documented in the README.md 





<!-- ### [Heroku]

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

**We don't recommend pushing to Heroku after every edit.** Pushing live to the web should primarily be done after you are confident in update.  -->
