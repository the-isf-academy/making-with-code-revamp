---
title: Advanced Filtering
---

# Advanced Filtering

In Django, the `view` is used to handle the logic for the request and response. In Act II, we learned how to send all of the data from the model to the view and then how to display that information in the template. But, what if we only want to send some of the data? 

We see real world implementations of this all time. Take OpenRice for example. 

{{< figure src="images/courses/cs10/unit02/resources_advanced_views.png" width="40%"  >}}

When searching for restaurants in Tsim Sha Tsui, the platform will initially give you all the available options. But what you only want to view Thai restaurants, or only restaurants with a noodle dish, or only restaurants with wi-fi. Open Rice gives you the ability to filter the data. 

Django has made filtering quite easy via [class based views](https://docs.djangoproject.com/en/3.2/ref/class-based-views/). 

## List View

List view is one of Django's class based views. It returns a list of objects (instances of your model). 

{{< code-action >}} Let's take a look at a view from our To-Do app in the `views.py` file. 

```python
from django.views.generic import ListView

class ArchivedTasks(ListView):
    template_name = 'task/archived_tasks.html'
    model = Task
```

- `from django.views.generic import ListView` - imports the class based view from Django
- `template_name = 'task/dashboard.html'` - defines which template should be called when this view is requested
- `model = Task` - defines which object should be returned

### [get_queryset()]

The `get_queryset()` function can be overridden to specify exactly which instances of the model should be returned. 

{{< code-action >}} For the `ArchivedTask` view, we only want to view tasks that have been archived. 

```python
from django.views.generic import ListView

class ArchivedTasks(ListView):
    template_name = 'task/archived_tasks.html'
    model = Task

     def get_queryset(self):
        #Filters archived tasks out of main list 
        return self.model.objects.all().filter(archive=True) 
```

- `self.model.objects.all().filter(archive=False)` - returns all of the objects with the `archive` property set as `True` 

{{< code-action >}}  Let's take a took at what this allows us to do on the template side in `archived_tasks.html`.

```python {hl_lines=["6-8"]}
{% extends "base.html" %}
{% block content %}

<div class="container" style="width:50%">
    <ul class="list-group">
        {% for task in tasks %}
            <li class="list-group-item"> {{ task }} | {{ task.label }} </li>
        {% endfor %}
    </ul>
</div>

{% endblock %}
```
- `{% for task in tasks %}` - loop through each instance of the model that was returned via the `get_queryset()` function
- `{{ task }}` - prints what is defined in the `__str__` function of the model 
- `{{ task.label }}` - prints the `label` property of the model 

### [get_context_data()]

The `get_context_data` function can be overridden to return a dictionary of instances of your model. 

{{< code-action >}} Let's imagine a task dashboard that displays current tasks in one section and archived tasks in another section. 

```python {hl_lines=[12,15]}
from django.views.generic import ListView

class TaskDashboard(ListView):
    template_name = 'task/task_dashboard.html'
    model = Task

    def get_context_data(self, **kwargs):
        context = super().get_context_data(**kwargs)
        data = self.model.objects.all()

        # filter active tasks 
        context['active_tasks'] = data.filter(archive=False) 

        # filter archived tasks
        context['archived_tasks'] = data.filter(archive=True) 

        return context
```
- `context['active_tasks']` - just like a dictionary, we are defining a key and value pair. The key being `active_tasks` and the value being all instances of the Task model with `archive=False`

{{< code-action >}} Let's take a took at what this allows us to do on the template side in `task_dashboard.html`.

```python {hl_lines=[7,17]}
{% extends "base.html" %}
{% block content %}

<div class="container" style="width:75%">
    <h4>Active Tasks</h4>
    <ul class="list-group">
        {% for task in active_tasks %}
            {{ task }}
        {% endfor %} 
    </ul>
</div>
  

<div class="container" style="width:75%">
    <h4>Archived Tasks</h4>
    <ul class="list-group">
        {% for task in archived_tasks %}
            {{ task }}
        {% endfor %} 
    </ul>
</div>
  
{% endblock %}
```
- `{% for task in active_tasks %}` - we can now loop through the individual keys in the `context` dictionary we defined in the `get_context_data()` function. 

## Chaining Filters

As of yet, we've only been filtering our data on one property. But to return to the OpenRice example, what if a user only wants to see restaurants that are in Sai Ying Pun, serve Indian Cuisine, with a 5 star rating. [Django allows filters to be chained together](https://docs.djangoproject.com/en/3.2/topics/db/queries/#chaining-filters) to achieve this level of specificity. 

{{< code-action >}} Let's imagine a simplified version of the `model.py` file for OpenRice. 

```python
class Restaurant(models.Model):
    name = models.CharField()
    cuisine = models.CharField()
    location = models.CharField()
    rating = models.SmallIntegerField()
```

{{< code-action >}} Now let's create a query_set in our `view.py` for Indian restaurants in Sai Yin Pun with a 5 star rating. 

```python
class FilteredRestaurants(ListView):
    template_name = 'task/filtered_restaurants.html'
    model = Restaurant

     def get_queryset(self):
        #Filters archived tasks out of main list 
        all_restaurants = self.model.objects.all()
        filtered_restaurants = all_restaurants.filter(location="Sai YinPun").filter(cuisine="Indian").filter(rating=5)
        return filtered_restaurants
```
Pretty simple! As the developers, you just need to know the model and what information you'd like to display. Django makes the rest relatively easy. 

## Even more filtering! 

Depending on the complexity of your database, you may need to filter data and then combine it before defining the query_set for the context. For that, [Django has a extensive documentation on how to query and filter](https://docs.djangoproject.com/en/3.2/topics/db/queries/#contains). 

We're not going to go over all of the functionalities, but please let a member of the teaching team know if you'd like us to post a specific tutorial. 