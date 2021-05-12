---
layout: post
title: "Useful Python packages"
description: Some useful Python packages and how they fit into my work.
published: true
future: true
mathjax: true
categories: [Python, Software engineering, Data science]
---

I use Python quite a lot as part of my job as an data engineer/scientist/backend magician. This page describes various packages that I've found useful and what I've used them for. I've divided these packages up into several categories:

- [Data wrangling](#data-wrangling) - for working with data.
- [Visualisation](#visualisation) - for visualising the data, both wrangled and unwrangled.
- [MVP development](#mvp-development) - for developing the first version of products, because that's what we're all about after all!
- [Service development](#service-development) - for developing the services which support products.
- [CI tools](#ci-tools) - for helping good quality code into production and attempting to keep bad code out.

## Data wrangling

- [Pandas](https://pandas.pydata.org/) is the ubiquitous Python data analysis package. Very useful, performant given the ease of implementation and has a welcoming community for first time committers. Good project to learn about managing a large Python codebase.
- [sqlalchemy](https://www.sqlalchemy.org/) is a package which allows us the power of SQL within Python. I'd use this to actually interact with a database and leave Pandas for the data analysis work.
- [SQL](https://en.wikipedia.org/wiki/SQL). SQL is a language you need to know to interact with most databases - probably not the noSQL databases, however. [Designing data intensive applications](https://dataintensive.net/) is a good book which has a chapter discussing the differences between noSQL and SQL databases.

## Visualisation

I use three different libraries for visualisation:

- [Matplotlib](https://matplotlib.org/) is a very customisable library for creating plots in Python. This does mean you have to write a bit of boilerplate code.
- [Seaborn](https://seaborn.pydata.org/) is based on matplotlib and is designed to remove the boilerplate code you have to write to plot nice statistical graphs.
- [Plotly](https://plotly.com/python/) makes nice interactive graphs which can be embedded in Jupyter Notebooks or apps online.

## MVP development

Developing applications to _do a thing_ that shows the interesting data science/modelling work is fun but can be difficult depending on how much customisation I want to be able to have on my webapp. Several packages exist that abstract some of the ~~boring~~ necessary tasks of creating and running a web application.

- I've used [Dash](https://dash.plotly.com/) a lot to develop MVPs of applications that expose quantitative models/data science models to users. I think it's got a good balance between customisation and off the shelf functionality and there is a solid user base. [This package](https://pypi.org/project/django-dash/) allows dash apps to be deployed using [Django](https://www.djangoproject.com/) that provides an excellent place to start for any new project.
- [Streamlit](https://streamlit.io/) lets you create an app from a single script and is targeted squarely at the data scientist turned software dev market. They've just recieved a lot of funding so I'm looking forwards to seeing what they come up with. Here's a [repo of mine](https://github.com/TAJD/workout_app) which tracks the reps from my workouts. The Streamlit app can be found [here](https://share.streamlit.io/tajd/workout_app/main/app.py).

## Service development

Here are some packages I've found useful for the purpose of developing backend services.

- [FastAPI](https://fastapi.tiangolo.com/) is an excellent framework for developing APIs in Python. It's got great documentation, is performant and usually you can find tutorials for deployment within the community. 100% recomment to all my friends.
- [Typer](https://typer.tiangolo.com/) is FastAPI's sibling and is used to write CLIs. I use it when I'm containerising some server script and I'm dressing it up with some form of simple API.
- [Jinja2](https://jinja.palletsprojects.com/en/3.0.x/) is mostly used within web development, but I use it a lot when I'm generating some form of configuration file or spitting out an html page with results. It's here because I had to include it somewhere.

## CI tools

Continuous integration is the attempt to make deploying performant code as smooth as possible. Part of this process involves running tools on code to spot errors that the humans missed. These tools don't write your code for you, but they help to reduce the frequency and magnitude of errors that occur.

- [Pylint](https://www.pylint.org/) helps with identifying style compliance, code refactoring and error detection. It returns a score after scanning your code and sometimes I get absorbed in cleaning code up! I then remember that I get paid for functionality rather than tidyiness.
- [MyPy](https://github.com/python/mypy) is used to check static types in Python code. [PEP 484](https://www.python.org/dev/peps/pep-0484/) added type hints to Python. Type hints are useful for thinking about how different functions fit together. MyPy helps to detect bugs when using type hints.
- [Black](https://github.com/psf/black) is a code formatter. It helps bring uniformity to rogue code bases and essentially helps everyone to read Python code the same way.
