---
title: "1. Database"
type: lab
slug: lab_riddle_database
repo_url: https://github.com/the-isf-academy/lab_riddle_database
init_action: create_from_template 
# draft: true
---

# Riddle Database

In this lab we are going to delve into databases and a new software, `banjo`.

---

## [0] Experience the ISF Riddle Server

The last time we saw riddles, they existed only within each of your computers. You had to manually add new ones and there was no way to keep track of how many people guessed them.

We are now going to look at Riddles that are hosted on the internet!

{{< code-action >}} **Visit [http://riddles.student.isf.edu.hk/riddles/all](http://riddles.student.isf.edu.hk/riddles/all) to view riddle server.**
> Not very easy to read, right? You can install the [JSON Formatter](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa?hl=en) Chrome extension to view better formatted JSON.*

{{< code-action >}} **Now try making `get` request to receive the same information in your terminal using `httpie`.**
```shell
http get http://riddles.student.isf.edu.hk/riddles/all
```

```shell
HTTP/1.1 200 OK
Connection: close
Content-Length: 94
Content-Type: application/json
Date: Thu, 15 Sep 2022 04:53:08 GMT
Server: gunicorn

{
    "riddles": [
        {
            "correct": 0,
            "guesses": 3,
            "id": 1,
            "question": "Where does dragon milk come from?"
        }
    ]
}
```

{{< code-action "Do you know the answer? Try posting a guess via the Terminal." >}}
```shell
http post http://riddles.student.isf.edu.hk/riddles/guess id=1 guess="scales"
```
> It is common for `POST` requests to send a *payload* with the request. In this case, the payload is a parameter called `id` specifying which riddle we are guessing, as well as `guess`.
>
> We are also sending this request to a different url `endpoint`: `/guess`


You should see something like this:
```shell
HTTP/1.1 200 OK
Connection: close
Content-Length: 94
Content-Type: application/json
Date: Thu, 15 Sep 2022 04:57:08 GMT
Server: gunicorn

{
    "correct": false,
    "guess": "scales",
    "riddle": {
        "correct": 0,
        "guesses": 4,
        "id": 1,
        "question": "Where does dragon milk come from?"
    }
}
```

---

### [Explore the Endpoints]
Server APIs often rely on different URL *endpoints* to determine what the API should do.

Here is a cheatsheet of the Riddle endpoints, what parameters they take in their payload, and what they do:

| Method | URL                                | Required Payload     | Action                                                                                   |
| ------ | ---------------------------------- | -------------------- | ---------------------------------------------------------------------------------------- |
| `GET`  | `/riddles/all`   |                      | Returns a list of all the riddles, without answers.                                      |
| `GET`  | `/riddles/one`   | `id`                 | Returns the riddle if it exists. (Otherwise, it returns an error with status code 404.)  |
| `POST` | `/riddles/new`   | `question`, `answer` | Creates a new riddle (with an automatically-assigned id). Returns the riddle.            |
| `POST` | `/riddles/guess` | `id`, `guess`        | Checks whether the guess is correct. In the response, `correct` is `True` or `False`.    |

{{< checkpoint >}}

{{< code-action "Explore each endpoint, and be sure to successfully:" >}}
- view all riddles without the answers
- view a single riddle
- add a new riddle
- guess a riddle
{{< /checkpoint >}}


---

## [1] Explore the Riddle Model

Now that you've experienced the riddle server, let's delve into how it's made.

The `Riddle` objects looks almost identical to how it looked in the Riddler lab. **The main difference, is we must define the datatype of each property.** This tells the database, what type of information each property will store.

```python
class Riddle(Model):
    question = StringField()
    answer = StringField()
    guesses = IntegerField()
    correct = IntegerField()

    MIN_FUZZ_RATIO = 80
```

---

### [Set Up]

For this lab, we need to download software to view the database in a nicely formatted chart.

{{< code-action "Download dbsqlite onto your computer:" >}} [https://sqlitebrowser.org/dl/](https://sqlitebrowser.org/dl/)

{{< figure src="https://sqlitebrowser.org/images/sqlitebrowser.svg" alt-text="database icon" >}}


{{< code-action "Get the lab and install any necessary packages." >}}
```shell
mwc update
```

{{< code-action "In the Terminal, open the lab folder." >}}
```shell
cd ~/desktop/making_with_code/cs10/unit00_networking/lab_riddle_database
```

{{< code-action "Enter the Poetry Shell." >}} As a reminder, we will run this command at the start of each lab, but only when we are inside a lab folder.
```shell
poetry shell
```
{{< aside "Exiting the poetry shell" >}}
When you want to exit the shell, you can type `exit` or `^D`
{{< /aside >}}


{{< code-action "Install Banjo." >}}
```shell
pip3 install django-banjo
```


---

### [Viewing the Database]

You have just downloaded a simple server that hosts `Riddles` onto your laptop. Let's start by looking at the its database.

{{< code-action "Open the database in the DB Browser:" >}}
```shell
open database.sqlite
```

{{< code-action "Select" >}} `Browse Data`

{{< figure src="images/courses/cs10/unit00/00_databases_00.png" alt-text="databases" >}}


{{< look-action "Here you will see all of the riddles that are in your locally hosted server." >}} This database file gets updated each time you guess or add a `Riddle`.

{{< figure src="images/courses/cs10/unit00/00_databases_01.png" alt-text="databases" >}}


---

### [Adding and Guessing Riddles]

Now, let's guess a `Riddle` and add a new `Riddle` and see how that affects the database.

In this unit, we will be using `Banjo` and wrapper over [Django](https://www.djangoproject.com/). Django is a popular web framework that is used to quickly create web apps. We will be using Django in the spring, so for now we will `Banjo` to introduce the software.

{{< code-action "Let's enter the Banjo shell to interact with the riddles." >}}
```shell
banjo --shell
```
```shell
No changes detected in apps 'app', 'banjo'
Operations to perform:
  Apply all migrations: admin, app, auth, contenttypes, sessions
Running migrations:
  No migrations to apply.
# Shell Plus Model Imports
from app.models import Riddle
Python 3.10.6 (v3.10.6:9c7b4bd164, Aug  1 2022, 17:13:48) [Clang 13.0.0 (clang-1300.0.29.30)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
(InteractiveConsole)
>>>
```

{{< code-action "Let's start by just viewing all the riddles in the shell:" >}}
```shell
Riddle.objects.all()
```
```shell
<QuerySet [<Riddle 1: I'm tall when I'm young, and I'm short when I'm old. What am I? (11/33)>, <Riddle 2: How many months of the year have 28 days? (5/10)>, <Riddle 3: I can fly but have no wings. I can cry but I have no eyes. Wherever I go, darkness follows me. What am I? (0/2)>, <Riddle 4: What has to be broken before you can use it? (3/7)>, <Riddle 5: The more you take, the more you leave behind. What are they? (3/10)>, <Riddle 6: What is so delicate that saying its name breaks it? (5/6)>, <Riddle 7: I am always in front and never behind. What am I? (2/2)>]>
```

{{< code-action "Now, let's add a new riddle:" >}}
```shell
new_riddle = Riddle(question='If you feed it, it lives; If you water it, it dies.', answer='Fire')
new_riddle.save()
```
> *Note how you must `save()` the riddle to ensure it gets saved in the database.*

{{< checkpoint >}}
Before moving on, make sure the Riddle was properly saved:
- view all the `Riddle` objects
- refresh the database in the DB Browser
{{< /checkpoint >}}

{{< code-action "Now, let's try to guess the riddle we just added:" >}}
```shell
>>> new_riddle.check_guess('fire')
True
```

{{< checkpoint >}}
Before moving on, make sure the Riddle properties, `guesses`, and `correct`, were properly updated:
- view all the `Riddle` objects
- refresh the database in the DB Browser
{{< /checkpoint >}}

---

### [Database Querying]

Now that you've experienced adding and updating the database, we're going to explore how to search, or query, the database.

{{< look-action "Open the Banjo documentation:" >}} [https://cs.fablearn.org/docs/banjo/index.html](https://cs.fablearn.org/docs/banjo/index.html)

{{< write-action "Using the Banjo documentation, fill out the worksheet and properly query the database using the Banjo shell." >}} 

---


## [3] Deliverables


{{< deliverables >}}  

**Once you've successfully completed the worksheet be sure to fill out [this Google form](https://docs.google.com/forms/d/e/1FAIpQLSfgWwxFI8SotkBsredlpQejYI2fHzJDQ-2oZgdYTq1ZQO_zjw/viewform?usp=sf_link).**

{{< /deliverables >}}

---

## [4] Extension

Next lab we will explore how to write the Riddle server.

{{< code-action "Feel free to open up the code and start to understand how it works!" >}}
```shell
atom .
```
