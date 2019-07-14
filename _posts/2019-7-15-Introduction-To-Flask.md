---
layout: post
title: Hello
---

# What is Flask
Flask is micro web framework for Python based on Werkzeug and Jinja2 which very simple but still powerful.

# Why Flask?

There are many reasons I like Flask.
Firstly, Flask is a micro web framework, this means it is not 'batteries included' like frameworks such as Django and therefore does not include other features, such as an ORM, authentication or application structure.
Many people would consider this a disadvantage but I think it makes it really easy to learn for people not familiar with web frameworks.
Flask also makes it really easy to add on functionality.
For example, I like to use Peewee as my ORM and Flask-Login to handle user authentication.


However, it does include enough for you to easily get started. For example, Flask does include Jinja2 which is a powerful templating language and a simple but flexible routing system (which does not make use of regular expressions which makes it much easier for beginners).

# Setup Flask

For this example, I am going to use Python 3 although the tutorial should be able to easily adjusted to work with Python 2. I am going to assume you have Python 3 and pip installed as it is now bundled with Python 3.

For this project we are going to use virtualenv which is a tool that allows you to create a python installation for individual projects as to avoid issues with dependices, for example needing different versions of a package in seperate projects. To install virtualenv, run in your terminal:

`pip install virtualenv`

Now run:

 `mkdir FlaskTutorial && cd FlaskTutorial`

 which will create an new directory for our project and move us into it.

Next, you are going to need to know the path to your Python installation. To do this open the Python 3 interpreter (run `python3` in your shell):

```
import sys
sys.executable
```

Now, you are going to need to exit the interpreter (Ctrl/Cmd + C) as we are actually going to create the virtualenv, so run (please substitute in your path from the above step):

`virtualenv venv -p {{your path goes here}}`

For example, I might run:

`virtualenv venv -p /usr/bin/python3`

Next, we need to start using the virtualenv so run:

`source venv/bin/activate`

The final step will be to actually install Flask, so run:

`pip install flask`

And we are done.

# Hello, World

Now we have actually installed flask we are going to our customary hello world application. So inside the FlaskTutorial directory we created earlier, create a file called `app.py`, open it in your favourite text editor and type:

```
from flask import Flask
app = Flask(__name__)
@app.route('/')
def index():
    return 'Hello, World'

app.run(debug=True, port=8000)
```

Now if you run this script with `python app.py` and visit `localhost:8000` in your browser you should see the text: Hello, World

So, here is an overview of the code we just wrote.

On line 1 we import the Flask class from flask module. Next, we create a new instance of the Flask class in a variable called app. If this does not make sense to you then don't worry, just know this basically sets up flask.

On line 5 we have a decorator. If you haven't encountered decorators before we will cover them at a future as they are quite hard to get your head around. For now just know it sets which url will call the function on line 6, which in our case is the root/base url.

Line 6 just defines a function called index.

Line 7 simply returns the string `'Hello, World'`.

Finally, line 9 starts our flask web application in debug mode and on the port 8000. We are running the application in debug mode so if we encounter errors we get as much infomation about them as possible which makes them easier to debug.

To stop your application press `Ctrl + C` and exit your virtualenv to use your standard python setup type: `deactivate`.
