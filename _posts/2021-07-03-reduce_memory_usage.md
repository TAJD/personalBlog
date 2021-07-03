---
layout: post
title: "Reducing the memory usage of dataframes"
description: A script illustrating how the memory usage of a pandas DataFrame can be reduced through altering data types.
published: true
mathjax: true
categories: [Python, Software engineering, Data science]
---

This post describes a useful script for reducing the memory usage of a pandas DataFrame. There have been a few blog posts and Stack Overflow questions in this area such as [here](https://stackoverflow.com/questions/57531388/how-can-i-reduce-the-memory-of-a-pandas-dataframe) and [here](https://www.mikulskibartosz.name/how-to-reduce-memory-usage-in-pandas/).

You might want the memory of a dataframe to be reduced if you want to work with more data or you want to speed up what you are doing. A related problem is about getting the most amount of data you can out of your database (or data warehouse) - [this article](https://pythonspeed.com/articles/pandas-sql-chunking/) covers a few different ways you can use pandas to load lots of data..

I wanted to include this snippet here as it's a working version of the functionality that I'm happy with. This function loads a dataframe and iterates over each column to identify whether a data type with a reduced memory requirement can describe the existing data. It returns a modified version of the dataframe.

<script src="https://gist.github.com/TAJD/9b30c92d12b0908781d2a39aba47237b.js"></script>
