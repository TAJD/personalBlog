---
layout: post
title: "Useful SQL techniques"
description: Some notes on useful SQL commands and when they might be useful.
published: true
future: true
mathjax: true
categories: [Postgres, SQL]
---

The purpose of this note is to describe some key SQL commands and when they might be useful to use. The note concludes with key resources and guides I've found helpful. The perspective is more towards commands which might be useful for running analytical queries rather than traditional relational database use cases. Joins, for example, have been covered to death elsewhere.

For a wide ranging and in-depth review for using SQL in data analysis see [this article here](https://hakibenita.com/sql-for-data-analysis). I'm using this page to consolidate my notes and some useful links.

## EXPLAIN and ANALYZE

`EXPLAIN` and `ANALYZE` are used to quantify how a given query might perform. `EXPLAIN` is used to describe the plan that Postgres is going to use to execute a query with an estimated cost of execution and `ANALYZE` executes the query and returns the actual cost and time to execute.

I use these commands to check:

1. Is the query using the indexes I intended it to use?
2. The cost of the query whilst I am trying to optimise it for production purposes.


## Common table expression to hold settings

[Common table expressions](https://www.postgresql.org/docs/current/queries-with.html) (CTE)s can be thought of as temporary tables which last for the duration of the query. You can also think of them as _import_ statements for data to use within your main query.

The step change in the use of CTEs here is to use them as a location to set variables which are used within CTES in the rest of the query. For example:

```SQL
WITH settings AS (
	SELECT
		(SELECT 1256 AS id_object),
		(SELECT '2021-02-02'::timestamp AS lower_date),
		(SELECT '2021-02-12 23:59:59'::timestamp AS upper_date)
)
SELECT *
FROM settings
```

This CTE can be included in your original query using a clause such as:

```SQL
WITH timestamp BETWEEN (SELECT lower_date FROM settings)
AND (SELECT upper_date FROM settings)
```

## NULLIF

```NULLIF``` is a [conditional function](https://www.postgresql.org/docs/current/functions-conditional.html). It's handy for handling divide by zero errors. Remember this.

## LAG

```LAG``` allows you to calculate the difference between rows based on how the table from the previous query is `PARTITIONED` and `ORDERED`. [Obligatory documentation reference](https://www.postgresql.org/docs/current/tutorial-window.html).

```PARTITIONED``` defines how the data is partitioned prior to the lag calculation.

```ORDERED``` defines how the data is ordered for the ```LAG``` calculation to be applied.

## CROSSTAB (Pivot tables)

```CROSSTAB``` is how pivot tables are implemented in Postgres. It's handy for returning data which can be plotted straight away, although some SQL juggling is required for a dynamic number of variables to create columns for. See [this](https://stackoverflow.com/questions/12879672/dynamically-generate-columns-for-crosstab-in-postgresql) stackoverflow answer - it's a bit grim isn't it. [Here's](https://stackoverflow.com/questions/39779734/dynamically-generate-columns-in-postgresql) another SO answer which has some useful links on using ```CROSSTAB```.

My current preferred solution is to export the data at this stage to Pandas for further manipulation.

## dbt and macros

[dbt](https://github.com/fishtown-analytics/dbt) is a useful tool for running complex SQL analytics. It applies software engineering principles to data analysis using SQL. Key advantages lie in it's version control, documentation (the lineage map is a killer feature). It has solved a lot of problems for me.

I have been bitten however with using it to produce tables that are queried directly by a production web app. When a dbt model is being rebuilt the table is dropped and queries using it hang. This is obviously not good and I was not the flavour of the month. Lesson learnt there.

Hopefully this edge case will be fixed in the future, but for now I created a hacky macro (another dbt killer feature) to generate a _static_ table which is queries by the web app. This macro generates a table but removes the last 4 characters of the dbt model to avoid name conflicts. Not pleasant but it works for now.

The macro looks something like, where the argument is the name of the dbt model that you don't want dropped.

<script src="https://gist.github.com/TAJD/38cf35819f98831af98de60b9927befe.js"></script>

A macro for importing CTEs directly into models can be seen [here](https://gitlab.com/gitlab-data/analytics/-/merge_requests/4322/diffs?commit_id=e951aec2ae04d888e28f9951e6296a09f998962b#3677f7ec9a0cda5e3249444ea6f0fb5cbba1ff34).

## `GENERATE_SERIES`

`GENERATE_SERIES` can be used to generate a range of equally spaced values. It can be used to:

1. Generate sample data.
2. Accurate reporting on time series data.

My experience has primarily been with performing analysis with time series data. `GENERATE_SERIES` can be used to return zeros for dates where no data has been found. In other words, `GENERATE_SERIES` can be used to generate a timestamp/date range which can be `LEFT OUTER JOINED` on a given dataset to return zero values for dates with no data.

Here are some useful articles:

1. [Fake data and better weekly reporting](https://www.citusdata.com/blog/2018/03/14/fun-with-sql-generate-sql/).
2. [Use generate series to get continous results](https://www.sisense.com/en-gb/blog/use-generate-series-to-get-continuous-results/).

## Useful resources


1. [This page](https://hakibenita.com/sql-for-data-analysis) has to be the best page I've ever seen for summarising all the main useful SQL commands for data analysis.
1. The Gitlab SQL guide is the first port of call for writing production quality SQL code - found [here](https://about.gitlab.com/handbook/business-ops/data-team/platform/sql-style-guide/).
2. The official Postgres documentation is zen like and instructive. Find it [here](https://www.postgresql.org/docs/).
3. An excellent tutorial on SQL can be found [here](https://mode.com/sql-tutorial/).