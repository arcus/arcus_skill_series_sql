# SQL Intermediate Level Speaker Notes

Welcome! 
I'm Elizabeth Drellich, and I use she/her pronouns. 
I'm a member of CHOP's Data Education Collaborative and I sit on the Arcus Education team in DBHi. 
Today's talk is the fourth in our five-part series on sequel, or S-Q-L.  
Today's webinar will be recorded, so please leave your cameras and mics turned off until the question time at the end.
If you do have questions that come up during the talk, feel free to put them in the chat. 
So with that, let's get started!

<h3><strong><u>CLICK</u></strong></h3>

## Today's talk
Today, we'll be learning how to do some more advanced SQL queries on single tables. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting -- don't worry. I'll provide plenty of scaffolding, and we'll work through things together. 

In the last webinar in this series my colleague Rose Franzen taught you how to compose simple queries with SELECT, WHERE, FROM, DISTINCT, AS, and ORDER BY. Today, after a quick review of those commands, we are going to learn how to write more complicated queries using CASE, LIKE, and GROUP BY. Along the way we will learn about some aggregate functions, as well as practice and refresh the skills you already know.

<h3><strong><u>CLICK</u></strong></h3>

## Thank you!
Material for this talk is based closely on the DART module **SQL Intermediate Level,** written by Peter Camacho and Joy Payton.

Many thanks to Peter and Joy for their work developing this excellent content!

Our webinar today will **not** cover all of the topics in their module, as we simply won't have time, so I suggest you check out the module after our session. 

<h3><strong><u>CLICK</u></strong></h3>

## Learn by doing
We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using a fake patient database. There will also be some short quizzes to help solidify your understanding as we go.

With that being said, lets jump in!

## SQL: A Brief Refresher

**SQL** (**S**tructured **Q**uery **L**anguage) is a query language that for more than four decades has been used to interact with **relational databases**.

A relational database is a data storage solution that stores data tables, which are comprised of columns (also called 'fields') and rows.

First, let's quickly review some key concepts from our November, December, and January sessions. 
"Sequel", or S-Q-L (either pronunciation is fine) stands for Structured Query Language. SQL is a programming language used to interact with Relational Databases. 

Relational databases consist of many different data tables. Today we will only be working with data from **one** table at a time, even though the three tables we will work with are stored in a single relational database. To learn more about combining data from more than one table, be sure to catch our final presentation in the series on SQL Joins (dates on the final slide).

<h3><strong><u>CLICK</u></strong></h3>

SQL is great at working with rectangular data, data that is stored in tables with rows and columns / fields. 

<h3><strong><u>CLICK</u></strong></h3>

However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other tools like R or Python, which are better suited for work like statistical analysis. We will, however, see some of the ways that SQL can generate simple summary statistics today.

<h3><strong><u>CLICK</u></strong></h3>

### Flavors of SQL
SQL is technically not just one thing -- there are a variety of different implementations. Although all SQL implementations have a similar structure, and the same basic syntax, each different SQL database product often has its own minor variations in dialect.

Colloquially people often refer to the different SQL dialects as different "flavors" of SQL. We've listed some popular "flavors" of SQL on this slide.

The most common difference between different SQL "flavors" are the availability of different functions that users can use for data manipulation, as well as the types of error messages that will be returned to the user when running code with syntax issues. There will be a few times during this webinar when I will point out that the flavor of SQL we are using today is impacting the outputs we get. 

<h3><strong><u>CLICK</u></strong></h3>

Because different flavors can have different outputs, knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. Whenever you search for documentation online or are troubleshooting, you'll want to be sure to include the name of the "flavor" you're working with in your search terms. 

In the hands-on portion of this webinar, we'll be using a form of SQL that actually runs in your web browser as you look at these pages.  This lightweight SQL engine is called "AlaSQL".  We pre-populated some tables for you to experiment with in this presentation.  These tables are filled with fabricated data meant to look a little like an electronic health record (EHR).  Rest assured that this data was completely invented, although it might look realistic!

<h3><strong><u>CLICK</u></strong></h3>

### SELECT, FROM, WHERE

Before we learn any new SQL commands, let's do a quick review of the commands SELECT, FROM, and WHERE that we learned about last month.


The basic structure of a SQL query is

```sql
SELECT
  fields
FROM dataset_name.table_name
WHERE conditional_statement
```
<h3><strong><u>CLICK</u></strong></h3>

To start exploring the `patients` table from the `alasql` database, let's first take a look at all the whole table. Use the asterisk as a wildcard to select all fields.

<h3><strong><u>RUN CODE</u></strong></h3>

For these in-browser code cells, the "play" button will run your code, and the results will appear below. You can collapse the results if you want by clicking this text. The black bar between the code cell and the results is where any error messages will appear.

<h3><strong><u>CLICK</u></strong></h3>

Once you know what the column names are, you can select only the columns (or fields) you want.

We recommend using dot notation and comma-first style to list the specific fields you want to see.
<h3><strong><u>RUN CODE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.

As an example, here's how you'd filter the output to only include records for a specific county.

<h3><strong><u>RUN CODE</u></strong></h3>


We will also be seeing the `DISTINCT` and `ORDER BY` functions again today, and will review them when we get there.

<h3><strong><u>CLICK</u></strong></h3>

## `CASE`

Now we are ready to learn some new SQL keywords and explore our database further. Our miniature database has three tables, `patients`, `allergies`, and `observations`. 

Let's look at the observations of "Peanut IgE Ab in Serum" in the `alasql.observations` table.

<h3><strong><u>RUN CODE</u></strong></h3>

We have already filtered this data using a `WHERE` statement to only look at the observations of Peanut IgE Ab in Serum. If we wanted to see what other types of observations are in the table, we could comment out the last two lines of the query to get the whole table.

Taking a closer look at the `observation_value` field, those numbers would be a lot more useful if we knew what those numeric values indicate.

Often when working with data, you will come across the need to define your own custom categories or groupings given some raw row data as input. For example, you might have hemocrit levels that you want to categorize as _normal_, _borderline_, or _abnormal_. This is where the `CASE` statement can come in handy!

<h3><strong><u>CLICK</u></strong></h3>

### Structure


The `CASE` statement is used to produce conditional row-level output based on columns/rows provided as input.  It's like an "if" statement in other languages, but with multiple possibilities, or "cases," that are considered. Let's take a look at a generic example, then we will practice with our dataset.

One way to think of a case statement is by its components. We will look at these components one by one, starting in the middle of the statement and working our way out.

<h3><strong><u>CLICK</u></strong></h3>

Conditional statements in SQL use this `WHEN`/`THEN` form. If you are used to other programming languages, you might be used to "if/then" statements, and this is very similar. `WHEN` the conditional statement is true, `THEN` the designated output will be returned to you.

You can have as many conditional statements as you want. Be aware, however, that for each row, SQL will only return one output, corresponding to the first time a condition is true.

<h3><strong><u>CLICK</u></strong></h3>

Let's consider what these statements would do in a row where `patients.age` (a field that isn't actually in our `patients` table) is 10. That row would not be categorized as an infant because 10 is greater than 1, but it would be categorized as a child because 10 is less than or equal to 12. However, even though 10 is less than 17, row will not be categorized as "teen" because it has _already_ been put in the "child" category. 

<h3><strong><u>CLICK</u></strong></h3>

`ELSE` comes after all of the `WHEN`/`THEN` statements and tells SQL what to return if none of the cases are true. 

If no `ELSE` clause is explicitly specified SQL imposes a condition of `ELSE NULL` by default.  We strongly encourage you to always include an `ELSE` clause even if you like the default value of `ELSE NULL`, to make your code more explicit.

<h3><strong><u>CLICK</u></strong></h3>

Lastly, you need to open the statement with `CASE` and close it with `END`.

The indentation before each of the `WHEN` statements and the `ELSE` statement are for us as human readers of this code. SQL doesn't need those lines to be indented, but it makes it a lot clearer to us where this block of code starts and ends.

We have started with a lot of theory because `CASE` statements are complicated, so let's return to that observations table and see how using a `CASE` statement helps us understand the data.

<h3><strong><u>CLICK</u></strong></h3>

### Example

A `CASE` statement goes between the `SELECT` statement and the `FROM` statement in a SQL query. We might know that if that observed value of IgE Ab is greater than or equal to 17.5, that is a strongly positive result, and also have known cutoff values corresponding to Positive, Equivocal, Borderline, and Negative results.

<h3><strong><u>RUN CODE</u></strong></h3>

When we run this code, we get a new column with the outcomes of our conditional `WHEN`/`THEN` statements in it. The data here looks great, we can read immediately that all three Peanut IgE Ab results were positive, two of them strongly positive. But we have this ugly column name, with the entire `CASE` statement.

We can make that column heading much nicer by telling SQL what we want it to be called. At the end of the `CASE` statement, immediately after the word `END`, add `AS interpretation` and run the code again. Using `AS` to give this new column an alias will make it much easier for us to read and understand.

<h3><strong><u>MODIFY CODE</u></strong></h3>

That looks a lot more readable.

<h3><strong><u>CLICK</u></strong></h3>

It is usually a good idea to follow a closing `END` with `AS` to give your new column a useful alias.

I want to pause here for questions before giving you your first opportunity to practice coding in SQL.

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 1** 

You're studying attitudes about smoking and will issue a survey in phases.  Phase 1 will go out to residents of Plymouth County, Phase 2 will go out to residents of Essex County and Phase 3 will go out to Barnstable County.  Finish the following query such that you get the patient name, county, and a new column called `phase`. 

I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will complete the query together. 

<h3><strong><u>COPY INTO CHAT</u></strong></h3>
Like this comment when you have completed "Your Turn 1"

<h3><strong><u>MODIFY CODE</u></strong></h3>

ANSWER:
```sql
SELECT
  patients.first
  ,patients.last
  ,patients.county
  ,CASE
    WHEN patients.county = "Plymouth County" THEN "Phase 1"
    WHEN patients.county = "Essex County" THEN "Phase 2"
    WHEN patients.county = "Barnstable County" THEN "Phase 3"
    ELSE NULL
  END AS phase
FROM alasql.patients;
```
<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## `LIKE`
So far every time we have created a query, we have needed to know the exact form the data in our table takes. To see what I mean, let's take a closer look at the allergies table.

Use `SELECT DISTINCT` to discover which distinct allergy descriptions appear in the `allergies` table.

<h3><strong><u>RUN CODE</u></strong></h3>

Say you are interested in all types of pollen allergies, but not other allergies. With the tools we already have, you could get that information using a `WHERE` statement.

<h3><strong><u>CLICK</u></strong></h3>

To get all pollen allergies from the `allergies` table with just a `WHERE` statement, you need to have each possible entry spelled out in its entirety.

In the very small table we are working with here, this method works fine. But if we were looking at a real patient data, there might be hundreds of types of pollen allergies specified. Moreover, if these data were entered by hand, the same allergy might show up as both "Allergy to grass pollen" and "grass pollen allergy" with different wording and different capitalization. Or maybe a new patient comes in who has a new, different pollen allergy. In that case you would need to update the query to get that data that you want, and that interferes with one of the main reasons we write scripted queries like this. For reproducibility purposes, you should be able to rerun the same query every time new data is gathered.

How can we get all the pollen allergies without having perfectly type them out in a very long `WHERE` statement? We need the `LIKE` operator to help us out.

<h3><strong><u>CLICK</u></strong></h3>

### Structure

`LIKE` operators let you compare textual data to a pattern rather than checking if two strings of characters are exactly equal with `=`.

This action is known as **pattern matching**, and can let you filter on row values that are similar, but not exact matches.

### Patterns

The `LIKE` operator uses 2 distinct **wildcard characters** that let you make patterns where some characters are unknown.

`%` is the "Wildcard" for 0 or more characters.
`_` is the "Wildcard" for exactly 1 character.

Wildcard characters let us build patterns to compare with a string of text data. Let's take a closer look at some examples using the `%` wildcard.

<h3><strong><u>CLICK</u></strong></h3>

Putting a `%` symbol just at the beginning means anything can come before the characters in pollen, but the data must _end_ with "pollen". 
`%pollen` matches "Allergy to tree pollen" 

<h3><strong><u>CLICK</u></strong></h3>

If instead the `%` symbol is only after the string `pollen`, a phrase would have to start with the letters "pollen" to be a match.

Capitalization matters to the `LIKE` operator, if the P were capitalized in "Pollen allergy - trees" that would not be a match. We will return to the problem of capitalization in a moment.

<h3><strong><u>CLICK</u></strong></h3>

To match both of these constructions, as well as data like "Tree pollen allergy," we can put `%` symbols both before and after.

<h3><strong><u>CLICK</u></strong></h3>

In the same way we needed quotes around the data we wanted to match exactly, the entire string of characters, wildcards included, must be enclosed in quotes.

<h3><strong><u>CLICK</u></strong></h3>

### Example

Let's apply this structure to finding the pollen allergies from our `alasql.allergies` table.

<h3><strong><u>RUN CODE</u></strong></h3>

If we had a larger collection of possible allergies, this query would return all of the rows in which the character string "pollen" appears in the `allergies.description` field. 

But what if there was an entry where the word "Pollen" was capitalized? The `LIKE` operator cares about capitalization, a lower case `p` and an upper case `P` are not the same characters.

<h3><strong><u>CLICK</u></strong></h3>

The `LOWER()` (or `UPPER()`) operator can help us out by taking the data in a field and making all of the characters lowercase (or uppercase).

<h3><strong><u>MODIFY CODE</u></strong></h3>

Wrap both sides of the `LIKE` statement in `LOWER()` to make sure the query returns both capital and lowercase versions of our pattern. 

I want to pause here for questions before giving you your next opportunity to practice coding in SQL.

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 2** 

You'd like to research patients born in the 1970s (so any year starting 197\_ would work).  Use a `LIKE` statement to enrich the query below and find the patient set you care about.

I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will complete the query together. 

<h3><strong><u>COPY INTO CHAT</u></strong></h3>
Like this comment when you have completed "Your Turn 2"

<h3><strong><u>MODIFY CODE</u></strong></h3>

ANSWER:

```sql
SELECT
  patients.id
  ,patients.birthdate
FROM alasql.patients
WHERE patients.birthdate LIKE '197%';
```

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## Aggregate Functions

**Aggregate functions** can be used to get a single value related the values for multiple rows of data in some meaningful way.  

This aggregation could be a numerical statistic, like the sum or standard deviation of a number of rows, or it could pull out a special value, like the minimum or maximum value (this works as well for strings, in which case it would be the first or last value in alphabetical order). There are many other possibilities as well, like giving a count of rows or pulling a value at random from the rows.

Here are some commonly used aggregate functions:

`COUNT()`- Returns the count of the number of non-null values among the column(s)/rows provided as input.
`SUM()`- Returns the summation of all values from a column provided as input.
`MIN()`- Returns the minimum value from a column provided as input.
`MAX()`- Returns the maximum value from a column provided as input.
`AVG()`- Returns the numerical mean of all values from a column provided as input.

To count the rows in a table, use `COUNT(*)`.

These aggregate functions will ignore null values if you apply them to a specific column:

<h3><strong><u>RUN CODE</u></strong></h3>

The count function shows us that the `patients` table has 25 rows, and all of those 25 rows contains a `birthdate`. But most rows have a `NULL` vaule for the `deathdate`.

<h3><strong><u>CLICK</u></strong></h3>
<h3><strong><u>RUN CODE</u></strong></h3>

SQL will do its best to use the aggregate functions regardless of what type of data is in the column, but the outputs will make the most sense if the data type is what the function expects. For example `SUM` might return a value for a column that isn't numeric, but it isn't particularly useful information. The `MAX` and `MIN` functions, on the other hand, can be useful when used on text data: they will order the text alphabetically.

<h3><strong><u>MODIFY CODE</u></strong></h3>

We can see how SQL tries to adapt by changing which columns we try to sum or average. Let's see how all four functions work on the column `patients.sex`. Summing the `patients.sex` column just concatenates all of the entries, while averaging `patient.sex` returns a null value. These outputs might differ depending on what flavor of SQL you are using.  Our flavor, AlaSQL, returns a null value when it can't parse an aggregate statement, but other flavors of SQL may give you error messages.

<h3><strong><u>CLICK</u></strong></h3>

### `GROUP BY`
Often, you are interested in statistics by group, such as the average BMI for men and for women, or the standard deviation of reading test scores in teens with ADHD, depression, neither condition, or both conditions.

The `GROUP BY` clause is used to group column results into only the unique/distinct values among them. 

It is used in combination with aggregate functions to generate summary statistics about the larger dataset that was "grouped" (i.e. "collapsed") by `GROUP BY`. These can be tricky, so let's see a `GROUP BY` function in action before we examine how it works in more depth.

<h3><strong><u>RUN CODE</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>


`GROUP BY` aggregations like this one can be confusing and frustrating for new SQL users, because you have to remember that an aggregation returns **one and only one** value for the entire group of rows. This means you **cannot** ask for something in your `SELECT` clause that could give more than one value for the group.

I find it helps to start with the `GROUP BY` clause. In this first example, we are grouping by one thing, `patient.sex`. That means each group will have one value for `patient.sex`. We couldn't ask for `race` when we have only grouped by `sex` because not every member of the `M` group is guaranteed to have the same `race` value. If we try to add `race` to our `SELECT` statement, AlaSQL just returns a null value. Other flavors of SQL may give you an error message in these cases.

<h3><strong><u>CLICK</u></strong></h3>

You can `GROUP BY` more than one column. 

<h3><strong><u>RUN CODE</u></strong></h3>

There are two types of fields in this `SELECT` statement. We are only selecting fields that 
1. we are grouping by in the `GROUP BY` statement, or 
2. are aggregate functions. 

<h3><strong><u>RUN CODE</u></strong></h3>

Notice, also, that the rows being output by the `GROUP BY` statement correspond to the same rows we would have gotten using a `DISTINCT` statement -- only combinations that actually correspond to rows of the `patients` table appear. The aggregate function `COUNT` gives a single value for each of those distinct combinations. 

### `HAVING`

So far when we have grouped data using `GROUP BY` we have gotten relatively few rows. When you are working with real data, this may not be the case. Maybe you are grouping patients by zip code. Pennsylvania has over 1500 active 5-digit zip codes, perhaps it only makes sense to look at zip codes which have a minimum patient population.


The `HAVING` clause can be used to filter your result set on the value of an aggregate function.  It works similarly to a `WHERE` clause, but the two are not interchangeable.  

This is a common error people who are new to SQL often encounter -- mixing up `WHERE` and `HAVING`. `WHERE` is for filtering rows, `HAVING` is for filtering groups.

The `HAVING` clause is placed directly after your `GROUP BY` statement. Let's take a look at this query into the population of subjects in each county.
 
Let's run the code as it is, and then see how the results change when we un-comment the `HAVING` statement. 

<h3><strong><u>RUN CODE</u></strong></h3>
<h3><strong><u>MODIFY CODE</u></strong></h3>
<h3><strong><u>RUN CODE</u></strong></h3>

You can use an `ORDER BY` statement **after** a `HAVING` statement. Let's add `ORDER BY patients.county` to the end of our query.

<h3><strong><u>MODIFY CODE</u></strong></h3>
<h3><strong><u>RUN CODE</u></strong></h3>

Phew, that was a lot! I want to pause here for questions before giving you your next opportunity to practice coding in SQL.

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 3** 

This is a bit of a challenge because I'm not giving you and code to start with.

Create a query below that queries `alasql.patients` and gives the patient population of each city (`patients.city`) which has more than one patient living there.  Give the results in an alphabetized list. 

**Here is a hint:** You don't need to write the entire query at once, try first writing a query that returns the COUNT of patients in each city, and then modify that query to get the list you want.

I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will complete the query together. 

<h3><strong><u>COPY INTO CHAT</u></strong></h3>
Like this comment when you have completed "Your Turn 3"

<h3><strong><u>MODIFY CODE</u></strong></h3>

ANSWER:

```sql
SELECT
	patients.city
	,count(patients.city)
FROM alasql.patients
GROUP BY patients.city
HAVING count(patients.city)>1
ORDER BY patients.city;
```

## Recap

Today, you continued learning about the language "sequel" or S-Q-L, which is an acronym for "Structured Query Language." 

We covered several important functions, represented in SQL by **keywords** that let us build more complicated queries. In particular, we covered: 

**`CASE`**: used to return different values based on a conditional statement. A full `CASE` statement uses 5 keywords:

* `CASE`: opens the statement
* `WHEN`: give a conditional statement that could be true or false
* `THEN`: what value should be returned when that conditional statement is true
* `ELSE`: what value should be returned when none of the `WHEN` statements are true
* `END`: closes the statement

------

**`LIKE`**: used to compare patterns of characters in ways more complicated than an exact match. We saw several helper functions to use with `LIKE`:

* `%`: represents any number of unknown characters
* `_`: represents exactly one unknown character
* `LOWER()`: makes all the characters inside the parentheses lowercase
* `UPPER()`: makes all the characters inside the parentheses uppercase

------

**Aggregate functions** return one value for multiple rows of data. We saw the most frequently used aggregate functions:

* `COUNT()`: returns the number of non-null values
* `SUM()`: sums all non-null values (numeric data)
* `MIN()`: returns the first (alphabetically) or smallest (numerically) value
* `MAX()`: returns the last (alphabetically) or largest (numerically) value
* `AVG()`: returns the average of all non-null values (numeric data)

------

**`GROUP BY`**: used to collect rows into groups with matching entries in a particular column or columns. 

------

**`HAVING`**: used filter for only groups that meet a condition. 

You also got to practice hands on, which probably meant you got to see some error messages, too, which is helpful experience.

## Additional Resources

* Khan Academy's [Introduction to SQL](https://www.khanacademy.org/computing/computer-programming/sql) is high quality and easy to learn from.

* Tutorials Point has some helpful documentation you may want to check out to read more [about the basic types of **operators** available for use in a SQL query](https://www.tutorialspoint.com/sql/sql-operators.htm).

* Give the [SQL Murder Mystery](https://mystery.knightlab.com/) a try. Note that some of the content is more advanced than what we cover here, but there is a walkthrough, and you can always stop once you've reached the limits of what we've learned so far. 

* Select Star SQL is a [free interactive book that teaches SQL](https://selectstarsql.com/) by exploring Texas state execution data. The second and third chapters mostly cover topics we learned about today, while the remaining chapters dig deeper.

## Upcoming sessions

(all sessions are held 12:00pm – 1:00pm) 

@colorhighlight(March 2024 - SQL Joins)

Work with multiple tables and learn about SQL joins: learn what they accomplish and how to write them.

[Tuesday March 12, 2024](https://events.teams.microsoft.com/event/3b0842a5-d7ba-4292-a5e5-7bb47c9e6f13@a6112416-07b0-41a5-9bb1-d146b575c975) and [Wednesday March 20, 2024](https://events.teams.microsoft.com/event/5323d936-a3b7-4e70-81ed-ae428c93df09@a6112416-07b0-41a5-9bb1-d146b575c975)

## About these slides
