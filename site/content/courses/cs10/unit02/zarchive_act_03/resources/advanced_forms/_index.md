---
title: Advanced Forms
---

# Advanced Forms

Forms are an incredibly powerful tool that allow the user to change the database. Up until now, the forms you've interacted with have primarily been text input field. But, what if you want to specify what the user can choose? 

Below are a few examples of how to implement advanced form fields. Some are just a simple change to the `forms.py` file and some will require you to alter your `model`. 


## Calendar Picker 

In Act II, the to-do app required the user to input the date in a specific format. With the addition of a calendar picker, the user can much more easily select a due date. 

{{< figure src="images/courses/cs10/unit02/resources_advanced_forms_01.png" width="60%"  >}}

{{< code-action >}} To add this functionality, reference this code snippet in the `forms.py` file. 

```python {linenos=table,hl_lines=["1-2","17-19"]}
class DateInput(forms.DateInput):
    input_type = 'date'


# Form to create a task 
class TaskForm(forms.ModelForm): 
    class Meta: 
        model = Task 
        fields = (
            'title',
            'label',
            'notes',
            'due_date',
            'task_assigned_to',
            )

        widgets = {
            'due_date':DateInput()
        }
```

To learn more about how this woks watch this video!

{{< youtube "I2-JYxnSiB0" >}}


## Drop-down Menu with Pre-filled Choices 

We see examples of drop-down menus all the time. For example, when filling out an address, there is often a drop down field for country as opposed to the user writing in "Hong Kong". 

Let's consider the to-do app example. What if we wanted to add a priority field that allowed to user to select if a task is "low", "medium", or "high" priority. 

{{< figure src="images/courses/cs10/unit02/resources_advanced_forms_02.png" width="60%"  >}}

{{< code-action >}} To add this functionality, we must alter the model in `model.py` file. 


```python {linenos=table,hl_lines=["20-28"]}
import datetime
from django.db import models
from django.utils import timezone
from django.utils.timezone import now
from django.contrib.auth.models import User 

class Task(models.Model):
    task_user = models.ForeignKey(User, on_delete=models.CASCADE, default=1) 
    task_assigned_to = models.CharField(max_length=30,default="",blank=True)
    task_assigned_by = models.CharField(max_length=30,default="", editable=False)

    title =  models.CharField(max_length=30)
    label =  models.CharField(max_length=8)
    notes = models.TextField(editable=True, max_length=200)

    due_date = models.DateField('Date Due', editable=True)    
    pub_date = models.DateTimeField('Date Created',default=now, editable=False)    
    archive = models.BooleanField(default=False)

    class Priority(models.IntegerChoices):
        LOW = 1, "Low"
        MEDIUM = 2, "Medium"
        HIGH = 3, "High"

    priority = models.PositiveSmallIntegerField(
        choices=Priority.choices,
        default=Priority.LOW
    )

    def __str__(self):
        return self.title

    def date_created(self):
        return self.pub_date >= timezone.now() - datetime.timedelta(days=1)
```
 - `lines 20-23` - define a `Choices` object. 
    - `IntegerChoices` - allows you to assign a numerical value to the choices which allows you easily compare choices against each other. For example, if you want to rank the tasks from low priority to high priority, you can now use the number values to do so. 
    - `LOW` - defines a variable with the values `1` and `"Low"`
        - `1` - represents what the database value will be for the `priority` field
        - `"Low"` - represents the human readable name of what will appear in the form
- `lines 25-28` - defines a field, or property, of the `Task` model. 
    - `PositiveSmallIntegerField` - defines the data type for the field 
    - `choices=Priority.choices` - defines the optional `choices` argument to be the choices from the `Priority` class
    - `default-Priority.LOW` - defines the default value of the field as `1`

{{< code-action >}} Now, we must update the `forms.py` file to include the new field. 


```python {linenos=table,hl_lines=["15"]}
class DateInput(forms.DateInput):
    input_type = 'date'


# Form to create a task 
class TaskForm(forms.ModelForm): 
    class Meta: 
        model = Task 
        fields = (
            'title',
            'label',
            'notes',
            'due_date',
            'task_assigned_to',
            'priority',
            )

        widgets = {
            'due_date':DateInput()
``` 

And with that, we have a working drop-down menu with pre-defined choices! 

To learn more about what's possible with Django's `choices` field, visit their [official documentation](https://docs.djangoproject.com/en/3.0/ref/models/fields/#enumeration-types).