---
title: Pagination
---

# Pagination

Pagination is the ability to divide content amongst multiple pages. 


For example when using Google, the results are organized in pages as opposed to an infinitely scrolling webpage. 

{{< figure src="images/courses/cs10/unit02/resources_pagination_01.png" width="60%"  >}}


Enabling pagination in your web app will require a few small additions to your framework. With just a few additions to the `view` and `template` files, you'll have pagination up and running!


[Django has a built in pagination feature](https://docs.djangoproject.com/en/3.2/topics/pagination/) 
 that makes implementing it into your web app super simple.

## View.py 

Let's take a look at this code snippet from a built out version of the to-do app. 

```python {hl_lines=["4","7"]}  
class AllTasks(ListView):
    template_name = 'task/all_tasks.html' 
    model = Task
    paginate_by = 3
    context_object_name = 'tasks'

    def get_queryset(self):
        #Filters out archived tasks for logged in user
        data = self.model.objects.all().filter(archive=False).filter(task_user=self.request.user)

        return data.order_by('-due_date') 
```
- `paginate_by` - defines how many instances of the model should be displayed on each page
- `get_queryset()` - defines the data that will be sent to th model 




## Templates
As a reminder, Django uses templates and `block` content to build web pages. This allows you to easily repeat elements throughout your site. 

We can employ the same idea behind teh `navbar.html` template from Act II.


### [pagination.html]

Start by creating a `pagination.html` file in your `template` directory. Copy and paste this code. 

```python 
<div style="margin: auto">
    <nav aria-label="Page navigation example">
        <ul class="pagination">
            {% if page_obj.has_previous %}
                <li class="page-item">
                    <a class="page-link" href="?page={{ page_obj.previous_page_number }}" aria-label="Previous">
                        Previous
                    </a>
                </li>
            {% else %}
                <li class="page-item disabled">
                    <a class="page-link" href="#!" aria-label="Previous">
                        Previous
                    </a>
                </li>
            {% endif %}

            {% if page_obj.has_next %}
                <li class="page-item">

                    <a class="page-link" href="?page={{ page_obj.next_page_number }}" aria-label="Next">
                    Next
                    </a>
                </li>
            {% else %}
                <li class="page-item disabled">
                    <a class="page-link" href="#!" aria-label="Next">
                        Next
                    </a>
                </li>
            {% endif %}
        </ul>
  </nav>
</div>
```

Although this may look complicated, it is simply the [Bootstrap pagination html](https://getbootstrap.com/docs/4.0/components/pagination/) in combination with the Django templating language. 
- `{% if page_obj.has_previous %}` - if the current page has a previous page, it displays a blue clickable back arrow 
    - `{% else %}` - if the current page does not have a previous page, it displays a grey unclickable back arrow
- `{% if page_obj.has_next %}` - if the current page has a next page, it displays a blue clickable right arrow
    - `{% else %}` - if the current page does not have a next page, it displays a grey unclickable back arrow

### [all_tasks.html]

Now that we've set up the pagination template, we can add it into our template for displaying all the tasks. 

```python {hl_lines=[13]}
{% extends "base.html" %}

{% block content %}

<div class="container">
    <ul class="list-group">
        {% for task in tasks %}
        {% include 'task/tasklist-for-user.html' %}
        {% endfor %} 
  
    </ul>

    {% include 'task/pagination.html' %}
</div>

{% endblock %}
```

All we have to do is add `{% include 'task/pagination.html' %}` at the end of the file(s) we'd like to have pagination. 



## Working Pagination 
Once your `view` and `template` files have been updated accordingly, Django will take care of the rest! 

{{< figure src="images/courses/cs10/unit02/resources_pagination_02.png" width="100%"  >}}

