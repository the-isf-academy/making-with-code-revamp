---
title: 1. Request/Response Lifecycle
---

# The Request/Response Lifecycle

In this lab, you'll explore a Django app and make some changes to how it handles
the request/response lifecycle. 


{{< aside "Before we begin, a few reflections" >}}

{{< write-action "At the end of the lab, each student will turn in the answers to the questions in the lab." >}} 

{{< code-action >}} **Do the exploring parts, or you might not understand the questions**. (And we want you to be ready for the rest of the unit.)

 
{{< look-action  >}} **Make sure you actually read the content of this lesson.**

- You will be opening a lot of small files. It takes some practice learning your way around, but you'll get the hang of it.
- Most of the code you're looking at interacts with other code you're not
  seeing. For example, where's the code that actually calls `home_view` with a
  request? Where's the code that sends the response back to the client? It's all 
  there in the Django source--there's no magic--but you shouldn't bother reading it. 
- **As you start working
  with larger software packages, you'll need to get used to not
  understanding the whole system.** One of the main goals of computer science is
  to *reduce complexity*--making complicated problems easier to think about. One
  main way we reduce complexity is through *abstraction*, or hiding the parts we
  don't need to think about right now. 
{{</ aside >}}

--- 

{{< code-action >}} **Let's get started by making a `unit_02` folder and checking out the sample app.**
 
```shell
cd Desktop/cs10
mkdir unit_02
cd unit_02
git clone https://github.com/the-isf-academy/lab-colorama-YOUR-GITHUB-USERNAME.git
cd lab-colorama
pip install -r requirements.txt
```

{{< code-action >}} **Now have a look around using the `tree` command.** *If you don't have `tree` installed, you can skip this step.*
```shell
tree .
```

You'll meet some of these files today. For now, **the most important file to know
about is `manage.py`.** You'll always run this file when you want Django to do
anything. 

{{< code-action "To see a list of available commands, run:" >}} 
```shell
$ python3 manage.py help
```
---
## A. Hello

{{< code-action "Let's start up the app and test it out." >}}  The first command 
prepares the database (more on this later); the second command starts the server
running on port 8000 on your computer. 
```shell
python3 manage.py migrate
python3 manage.py runserver 8000
```

Now the server is waiting for requests. 

{{< code-action "Head over to your web browser and navigate to:" >}} [http://localhost:8000](http://localhost:8000). 

{{< checkpoint >}}
Each student should individually answer this question, and the questions later
in this lab. 

{{< write-action >}} **A.0:** What is the name of the color shown on the web page?

{{</ checkpoint >}}

## B. How the parts fit together

Let's see how the parts of the app worked together to show this page. When a
request first arrives, its URL is separated into a host name and a path. In
this case, the host name is `localhost:8000` and the path is `/`. 

{{< code-action >}} **Open `colorama/urls.py`.** The file `colorama/urls.py` declares the app's routing, matching paths
to views which should handle them. 

```python
urlpatterns = [
    path('/', include('colors_app.urls')),
    path('starter_app/', include('starter_app.urls')),
    path('admin/', admin.site.urls),
]
```
>This code is actually just importing URLs from other modules--`colors_app.urls`,
`starter_app.urls`, and `admin.site.urls`.

{{< code-action >}} **We're going to be working with `colors_app` today, so let's open `colors_app/urls.py`:**

```python {linenos=table, linenostart=4}
from django.urls import path
from colors_app import views

app_name = "colors_app"
urlpatterns = [
    path('', views.home_view, name="index"),
    path('colors/random', views.random_color_view, name="random_color"),
]
```
> Two views are defined. If you go to [the home page](http://localhost:8000) (empty path), 
the request will be handled by `views.home_view`. And if you go to 
[`/colors/random`](http://localhost:8000/colors/random), the request will be handled by
`views.random_color_view`.

{{< code-action >}} **Let's look at these views. You can see that they are imported from `colors_app.views`, so we'll open `colors_app/views.py`.**

```python {linenos=table, linenostart=8}
def home_view(request):
    "A view function which renders the homepage"
    log.info("In colors_app.views.home. Rendering the homepage.")
    skyblue = Color(name="skyblue", red=135, green=206, blue=250)
    params = {
        "name": "stranger",
        "color": skyblue,
    }
    response = render(request, 'colors_app/index.html', params)
    return response
```
> The homepage view is just a simple function! It receives a `request`, builds a
`response`, and returns it. However, the view relies on a few helpers to get the job done. 

### [Templates]

**Many views use
*templates*, or pieces of HTML code that can be used to build a webpage.** The
call to `render` on line 16 requests the template `colors_app/index.html`.
(Every app in the project has a folder called `templates`; when you ask for a
template, Django searches these folders for a match). 

{{< code-action "Find this template and open it." >}} 

```html {linenos=table}
{% extends "base.html" %}

{% block content %}
  <div class="row">
    <div class="col text-center">
      <h1> Hello {{name}}</h1>
      {% include "colors_app/swatch.html" %}
      <p>
        <a href="{% url 'colors_app:random_color' %}">
          How about a random color?
        </a>
      </p>
    </div>
  </div>
{% endblock %}
```
There's a lot here, so we'll just take a quick tour. This template is made up of
HTML tags like `<h1>...</h1>` and template commands like `{% ... %}` and `{{ ...
}}`. The HTML tags will be read by the client's browser as it presents the webpage; the template
commands tell Django what to do. 
- `extends` (line 1) means this template extends another template (in this
  case, `base.html`, which you can find in `colorama/templates/base.html`.
  Extending another template works by overriding particular *blocks*. Here, we
  are overriding the block called `content` (lines 3-15).
- `{{name}}` (line 6) is a placeholder which will be replaced with the parameter called `name` given to the
  template by the view (`colors_app/views.py`, lines 12-16). 
- `include` (line 7) means include another template. Colorama needs to show
  color swatches all over the place, so we have a special template just for the
  color swatch circle. 
- `url` (line 9) means look up a url by name (`colors_app/urls.py`, line 10). Why not
  just type in the url? If you change it later, you might forget to fix it here,
  especially after you have a few dozen templates. And you might want to deploy
  this site to multiple hosts, like `localhost:8000` while you're developing it
  and `colorama.com` when you're ready to go public. 

### [Models]
In addition to a template, `home_view` also uses a *model* called `Color` (`colors_app/views.py`, line 11). 
**Think of views as connecters, and think of models as objects that do most of the work.**

{{< code-action >}} **The `Color` model has some neat abilities; let's check them out by opening
`colors_app/models.py`.**

```python {linenos=table}
from django.db import models
from colors_app.validators import color_channel_validator

class Color(models.Model):
    name = models.CharField(max_length=50)
    red = models.IntegerField(validators=[color_channel_validator])
    green = models.IntegerField(validators=[color_channel_validator])
    blue = models.IntegerField(validators=[color_channel_validator])
    ...
```
> A `Color` has four attributes: `name`, `red`, `green`, and `blue`. (Every pixel
on a computer display has a tiny red, green, and blue light. So every color can
be made by describing how bright each should be.) The `color_channel_validator`
attached to each color field checks to make sure the color value is between 0
and 255. 
>
> If you look a little further
down, the `Color` class also has some helpful methods, such as the ability to
represent its value in hexidecimal, the way CSS styles expect it. This lets us
define a `Color` and then use it to style our web pages. 

**Models are just regular Python classes, but they have a special relationship
with a database which can store objects across requests to the server.** (This is
why the `Color` attributes are defined as `models.IntegerField`: they define how
the data should get stored in the database.  Storing
objects in a database and then later retrieving them makes it possible for web
apps to have state: if you create an object, other users will also see it and it
will still be there if you come back later. We'll come back to this idea
shortly. 

{{< figure src="images/courses/cs10/unit02/02_request_response.jpg" width="100%" title="Request/response lifecycle diagram" >}}



{{< checkpoint >}}

{{< write-action >}} **B.0:** When you go to the [home page](http://localhost:8000), it says "Hello
  stranger" at the top. However, if you look at the template 
  `colors_app/templates/colors_app/index.html`, the word "stranger" does not
  appear. **Explain how the word "stranger" ends up on the page.**
  
  > {{< code-action >}} **Then, without
  changing the template, change the home page so that it says hello to you instead.**

{{< write-action >}} **B.1:** Figure out how to change the color swatch on the home page to a different
  color. **Explain how to do it.** 

{{< write-action >}} **B.2:** If you didn't already check it out, go to the [random color page](http://localhost:8000/colors/random).
  You'll notice that the color swatch changes every time you load the page, and 
  the background changes to an opposite color. **Explain how this works.** *(Hint:
  We previously noticed that `/colors/random` is served by `colors_app.views.random_color_view`,
  so start there. Figure out which template is being used. Look in the
  template to figure out how the background color gets set. Make sure you
  explain how the `Color` model is involved too.)*

{{</ checkpoint >}}

--- 
## C. Saving stuff

**Now we're going to extend the app to let users create their own colors.** And
whereas our views were previously functions, now our views are going to be classes. 
Some class-based views are provided for you in
`colors_app/class_based_views.py`. We need to do a little work to wire these in
to the app. 

{{< code-action >}} **Open `colors_app/urls.py` and add the highlighted lines:**

```python {linenos=table, hl_lines=[3, 9, 10]}
from django.urls import path
from colors_app import views
from colors_app.class_based_views import ColorListView, NewColorView

app_name = "colors_app"
urlpatterns = [
    path('', views.home_view, name="index"),
    path('colors/random', views.random_color_view, name="random_color"),
    path('colors', ColorListView.as_view(), name="color_list"),
    path('colors/new', NewColorView.as_view(), name="new_color"),
]
```

> When you save the file, the server will notice the change and automatically
restart itself. If you accidentally make a mistake, the server might crash and
you'll need to restart it (just run `python manage.py runserver` again).

{{< code-action >}} **Now go to [`/colors`](http://localhost:8000/colors), and play around.** You can now add new colors and see a list of all the colors. If your app were live online, many users could all contribute colors. 

Once again, let's have a look at the code that made this possible. We added two
new URL routes, `colors` and `colors/new`, and routed them to `ColorListView`
and `NewColorView`, respectively. 

{{< code-action >}} **Let's look in `colors_app/class_based_views.py`:**
```python
from django.views.generic import DetailView, ListView, CreateView                                                      
from django.urls import reverse_lazy                                                                                   
from colors_app.models import Color                                                                                    
from colors_app.forms import ColorForm                                                                                 
                                                                                                                       
class ColorListView(ListView):                                                                                         
    model = Color                                                                                                      
    template_name = "colors_app/color_list.html"                                                                       
    queryset = Color.objects.order_by("name")                                                                          
                                                                                                                       
class NewColorView(CreateView):                                                                                        
    model = Color                                                                                                      
    form_class = ColorForm                                                                                             
    template_name = "colors_app/color_form.html"                                                                       
    success_url = reverse_lazy("colors_app:color_list")    
```
*That's it???* 

> **Here's the idea: by breaking up the work of a view into methods of a class, we can use a *generic view class* which just needs a little information and then will work the way most web apps need it to work.**
>
> If you need the behavior to be a little bit different from standard, you can write a custom method for just that part, and leave the rest alone. It takes more work to learn how these work,
but then using class-based views can save you TONS of time. 

- For `ColorListView`, you can imagine what needs to be done: Get all the colors
from the database, sort them somehow, and then give them to the template for
rendering. The three properties listed here are enough; the generic view can
handle the rest. 

- `NewColorView` actually does quite a bit more: It creates an empty `ColorForm` (e.g.
the name isn't filled in and the colors aren't set) and gives it to the
template, which renders a response. The user sees a page with sliders and a
text field to name the color. 
  > When the user submits the form (this is a `POST`
request because it's making a change; all the previous requests have been `GET`
requests), `NewColorView` again receives the request. This time, since it's a
`POST` with form data (name, color values), it creates a `ColorForm`, checks to
make sure the data is valid, and if so, creates a `Color`, saves it to the
databaase, and then sends a redirect response telling the user to go to
`/colors`. 

All this logic is *generic*; when the class is given a few necessary parameters,
it can do the rest because it's following the same old pattern. (Even though
it's actually a pretty complicated pattern and it's completely new to you!)

{{< figure src="images/courses/cs10/unit02/02_post_request_response.jpg" width="100%" title="POST Request/response lifecycle diagram" >}}

{{< checkpoint >}}

{{< write-action >}} **C.0:** There is currently no link from the homepage to the color list, or the
  form to add new colors. You have to enter the URL directly to get to these
  pages, and 99% of users (you no longer included) even know how to enter URLs
  directly. 
  > {{< code-action >}} **Add a link to the home page taking the user to the color list page.**
  *(Hint: There's already a link from the home page to the random color page. Use the same pattern.)*
  >
  > **Explain what you did.** 

{{< write-action >}} **C.1:** There's also no link away from the random color page; you're 
  stuck looping through random colors forever. 
  > {{< code-action >}} **Decide where the random color page should link to add add an appropriate link.** 
  >
  > **Where did you decide to link to?**

{{< write-action >}} **C.2:** Make five or six new colors, if you haven't already. Then look at the color list page. 
  The colors are currently sorted alphabetically (with all the upper-case names first
  and then the lower-case names). 
  > {{< code-action >}} **Figure out how to change this page so that
  colors are instead sorted by how much red they contain.**
  >
  > **Explain what you had to do.**
{{</ checkpoint >}}

## D. Wrapping up

{{< code-action >}} **Press `Control + C` to kill your server.** 

**In this lesson, you learned the basic structure of a Django app**, by looking at the files and tracing their execution as they handled a basic request and response lifecycle. 

This lesson guided you through the first steps of the official 
[Django tutorial](https://docs.djangoproject.com/en/3.1/intro/tutorial01/#creating-a-project); 
have a look. We didn't do everything, but you should recognize some of the steps
over there. The sooner you get familiar with the style of Django's
documentation the better. When you get stuck and Google for answers, you'll find
that Stack Overflow often has a quick fix, but you'll want the Django
documentation if you want to really understand what's going on. 

