# Live Project
## Project Introduction
From January 28th - March 3rd, 2021 I worked in a team setting on a full scale Python application to add to an existing library of apps at Prosper I.T. Consulting. Working on a standalone app to add to our library was at first nerve wracking but ended up being a great experience on how to reaserch and use efficient time management to complete the project. I also got experience using tKinter and django during this project which was a lot of fun when creating this app. I decided to create a budgeting app that would allow users to track montly expenses, income, and more on the application. This experience has shown me a lot about agile methodologies and has given me an appreciation for working on code collaboratively in a team setting. During this project we were given the opportunity to work on both [front end](#Front-End-Stories) and [back end](#Back-End-and-Mixed-Stories) stories so I took advantage of this and spent time on both types of stories, including some that were a mixture of the two. This was a very valuable experience for me and because of this I am confident working with both front and back end code and using them in conjunction to create applications. Along with practical coding knowledge, I also learned many useful [skills](#Other-Skills-Learned) that will help me in my career as a software developer.

Featured below are some stories I worked on over the live project with code snippets to demonstrate what was accomplished.

## Back End and Mixed Stories
- [Creating Budget model](#Budget-Model)
- [Creating Budget form](#Budget-Form)

### Budget Model
To start I needed to create a model to use for expeneses and cost and to keep track of the user and login information. Below is my model for doing this.
```Python
from django.db import models


class BudgetInfo(models.Model):

    expense_name = models.CharField(max_length=30, default='Expense Name')

    cost = models.FloatField()

    date_added = models.DateField()

    username = models.CharField(max_length=20, default='Your Name!')

    details = models.TextField(max_length=300, default='Details...')

    def __str__(self):
        return self.expense_name

    objects = models.Manager()
```
### Budget Form
I needed a form to be able to keep track of data entered in by the users. Below is my code to complete this.
```Python
class BudgetForm(ModelForm):
    class Meta:
        model = BudgetInfo
        fields = ['expense_name', 'cost', 'date_added', 'username', 'details']
        widgets = {
            'expense_name': forms.TextInput(attrs={'class': 'expense_name', 'placeholder': 'Name of expense'}),
            'cost': forms.NumberInput(attrs={'class': 'cost', 'placeholder': 'Cost'}),
            'date_added': forms.DateInput(attrs={'class': 'date_added', 'placeholder': 'Date Added', 'type': 'date'}),
            'username': forms.TextInput(attrs={'class': 'username', 'placeholder': 'Your Name!'}),
            'details': forms.TextInput(attrs={'class': 'details', 'placeholder': 'Enter Details Here..'}),
                   }


        def clean_budget_info(self):
            data = self.cleaned_data['expense_name', 'cost', 'date_added', 'username', 'details']

            return data
```
## Front End Stories
- [Base HTML page](#Base HTML)
- [Inheriting Base page to other HTML pages](#Inheritance)
- [Linking all pages to each other with django](#Links)
- [CSS for my pages](#CSS)
### Base HTML
I needed a base form that all my other pages could inherit from. Below is the code to complete that.
```HTML5
c{% load static %}
<!DOCTYPE html>
<html lang="en" class="background">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>{% block title %}{% endblock %}</title>
    <link rel="stylesheet"  href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <link rel="stylesheet" type="text/css" href="{% static 'css/BudgetingApp.css' %}">
</head>



<body>
      {% include "BudgetingApp/BudgetingApp_navbar.html" %}
    <div class="div_container">
        <header>
            <h2 class="header" >{% block header %}{% endblock %}</h2>
        </header>
        {% block content %}{% endblock %}
    </div>
</body>

<section id="footer-wrap">
    <footer class="footer">
        <p>Author: Samuel Lehner</p>
    </footer>
</section>

</html>
```
### Inheritance
One of the great things using django for this project was the ability to inherit your base page so you don't have to type redudant code. Below is one example of a page I made that inherited that base page while adding some unique code for that page. I will only show a few pages, one that uses my form from earlier and one for the user account.
```HTML
{% extends 'BudgetingApp/BudgetingApp_base.html' %}

{% block title %} Your Budget!{% endblock %}

{% block content %}
  <h2>Your Budget!</h2>
  <form action="" method="post">
    {% csrf_token %}
    {{ form.as_p }}


    <button type="submit">Submit</button>
  </form>
{% endblock %}
```
```HTML5
{% extends 'BudgetingApp/BudgetingApp_base.html' %}

{% block title %}Login{% endblock %}

{% block content %}
  <h2>Login</h2>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <label for="fname">First name:</label><br>
    <input type="text" id="fname" name="fname"><br>
    <label for="lname">Last name:</label><br>
    <input type="text" id="lname" name="lname">
    <button type="submit">Login</button>
  </form>
{% endblock %}
```
### CSS
I needed to have a style for my pages that was coherant with the other styles of apps in our library. Our project manager gave use the colors we needed to use and let the rest of it up to us. This is my styling for my application.
```CSS
.background {
    background-color: lightblue;
    background-image: url('/static/images/budget_background.jpg');
    -webkit-background-size: cover;
    -moz-background-size: cover;
    -o-background-size: cover;
    background-size: cover;
}

/* Added a background color */
.topnav {
    background--color: lightblue;
    overflow: hidden;
}

/* Style the links inside the nav bar */
.topnav a {
    float: left;
    display: block;
    color: black;
    text-align: center;
    padding: 14px 16px;
    text-decoration: none;
    font-size: 17px;
}

.topnav a:hover {
    background-color: #ddd;
    color: black;
}

.topnav a.active {
    background-color: #4CAF50;
    color: white;
}

body, html{
    margin: 0;
    font-family: Helvetica, Arial, sans-serif;
    width: 100%;
    height: 100%;
    padding: 0;
}

.div_container {
    padding: 10px;
    text-align: center;
}

.header {
    background-color: #4CAF50;
    text-align: center;
    display: inline;
}

.footer {
    position : absolute;
    bottom : 0;
    height : 40px;
    margin-top : 40px;
}
```
- Collaborated with other developers to find bugs in order to improve user experience.
  - Redirecting the user to the appropriate page.
  - Finding unhandled exceptions.
  - Fixing undesired outputs.
- Improved workflow efficiency by learning DevOps processes.
- Continuously learning new ideas and methologies from other developers to improve personally as a developer.
- Learned and enjoyed researching tKinter and dJango processes.
