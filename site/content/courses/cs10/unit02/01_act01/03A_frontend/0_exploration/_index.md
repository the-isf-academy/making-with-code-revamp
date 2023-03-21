---
title: "[Exploring Templates]"
# draft: true
---

# Exploring Templates

During the track lessons you will be creating the web app for the ISF Riddler. You should remember the Riddle database from the Networking Unit! 

🔍 **You will be primarily focused on learning the [Django template language](https://docs.djangoproject.com/en/4.1/ref/templates/language/) uses and [Bootstrap](https://getbootstrap.com/docs/5.0/layout/containers/).**

---


## [0] Model

{{< look-action >}} **You can find the `Riddle` model in `riddle_app/models.py`.** It can be helpful to know the architecture of the model so you know what are you are able to display in the frontend.

{{< expand "riddle_app/models.py" >}}

```python
from django.db import models
from fuzzywuzzy import fuzz


class Riddle(models.Model):
    question = models.CharField(max_length=500)
    answer = models.CharField(max_length=500)
    likes = models.IntegerField(default=0)
    date_added = models.DateTimeField(auto_now_add = True)

    DIFFICULTY_CHOICES = [
        ('E', 'Easy'),
        ('M','Medium'),
        ('H', 'Hard'),
    ]

    difficulty = models.CharField(
        max_length=1,
        choices=DIFFICULTY_CHOICES,
        default=None,
    )

    def __str__(self):
        return f"{self.question}"
    
    def check_guess(self,guess):
        MIN_FUZZ_RATIO = 70
        similarity = fuzz.ratio(guess.lower(), self.answer.lower())
        
        if similarity >= MIN_FUZZ_RATIO:
            return True
        else:
            return False
        
    def increase_likes(self):
        self.likes += 1
        self.save()
```

{{< /expand >}}

{{< code-action >}} **Firstly, let's `migrate` our `Riddle` model into the database. Then, run the server.**
```shell
python manage.py migrate
python manage.py runserver   `
```

{{< code-action >}} **Visit [127.0.0.1:8000/](http://127.0.0.1:8000/) to view the app!** As you are in the backend track, the website looks pretty boring...

---


## [1] Explore Templates

{{< code-action >}} **Open up the files with:** `code .`

{{< look-action >}} **Explore the `templates`  the**: `riddle_app/templates` directory 

{{< code-action >}} **Open the different `html` files and follow the instructions in the comments.** The comments are denoted with a `<!-- 💻 -->`
```html
<!-- 💻 Add the Difficulty for the specific riddle -->
```

--- 

## [2] Add Bootstrap

Bootstrap is a *massive* `CSS` framework library. It's easy to get lost in it. 

It's up to you whether you'd like to incorporate it. 

{{< look-action >}} **Start by taking a look at what's available:** 
- [bootstrap documentation](https://getbootstrap.com/docs/5.0/layout/containers/)
- [bootstrap cheat sheet](https://getbootstrap.com/docs/5.0/examples/cheatsheet/)
