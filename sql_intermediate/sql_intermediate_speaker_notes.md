# SQL Intermediate Level Speaker Notes

<h3><strong><u>LINKS TO SHARE</u></strong></h3>
- The slides: https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_intermediate/sql_intermediate.md#1
- Your Turn 1: https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_intermediate/sql_intermediate.md#11
- Your Turn 2: https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_intermediate/sql_intermediate.md#16
- Your Turn 3: https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_intermediate/sql_intermediate.md#20

## Page 1: Welcome to the Arcus Education Skills Series

Hi everyone, my name is Joy Payton, and I use she/her pronouns. 

I'm a member of the Data Education team that forms part of the Arcus initiative of the CHOP Research Institute.

Today's talk is the fourth topic in our five topic series on sequel, or S-Q-L.  At the end of today's talk you will get a link to sign up for the final topic, SQL Joins, if you are so inclined.  

If you want to follow along in today's presentation, my colleague Rose will share in chat the link to this slide deck that I'm presenting, so that you can follow along.  I do recommend that you go ahead and click that link, because today's webinar is hands-on, and you'll want to have access to all the activities.

Today's webinar will be recorded, so please leave your cameras and mics turned off until the question time at the end.  That's when I'll turn the recording off so we can all feel comfortable asking questions without being recorded.

If you do have questions that come up during the talk, feel free to put them in the chat. 

Today, we'll be learning how to do some more advanced SQL queries on single tables. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting -- don't worry. I'll provide plenty of scaffolding, and we'll work through things together.

So with that, let's get started!

<h3><strong><u>CLICK</u></strong></h3>

## Page 2: Today's Talk

In the most recent webinar in this series, my colleague Rose Hartman showed how to compose simple queries using SELECT, WHERE, FROM, DISTINCT, AS, and ORDER BY.  That sets up up well for today's learning objectives.

Today, after a quick review of the commands we went over last time, we are going to learn how to write more complicated queries using CASE, LIKE, and GROUP BY. Along the way we will learn about some aggregate functions, as well as practice and refresh the skills you already know.

<h3><strong><u>CLICK</u></strong></h3>

## Page 3: Thank you!

Material for this talk is based closely on the DART module **SQL Intermediate Level,** written by Peter Camacho and by me.  It does feel a little weird to acknowledge myself, I admit, but I want to promote a culture of acknowledging the sources we use for education!

Our webinar today will **not** cover all of the topics in the module we wrote, because it's simply too long.  We won't have time to cover everything in the module Pete and I crafted, so I suggest you check out the module after our session. Rose will add the link to that module into the chat, in case you want to check it out on your own time afterwards!

<h3><strong><u>CLICK</u></strong></h3>

## Page 4: Learn by doing

We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using a fake patient database. There will also be some short quizzes to help solidify your understanding as we go.

<h3><strong><u>CLICK</u></strong></h3>

## Page 5: SQL: A Brief Refresher

First, let's quickly review some key concepts from our earlier topics. 

"Sequel", or S-Q-L (either pronunciation is fine) stands for Structured Query Language. SQL is a programming language used to interact with Relational Databases. 

Relational databases consist of many different data tables. Today we will be working with data from **one** table at a time, even though the three tables we will work with are stored in a single relational database. To learn more about combining data from more than one table, be sure to catch our final presentation in the series, which is called SQL Joins.

<h3><strong><u>CLICK</u></strong></h3>

SQL is great at selecting just the data you want from rectangular data, data that is stored in tables with rows and columns.  We sometimes also call columns "fields". 

<h3><strong><u>CLICK</u></strong></h3>

However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other languages like R, Python, or the Stata language, which are better suited for work like statistical analysis. We will, however, see some of the ways that SQL can generate simple summary statistics today.

<h3><strong><u>CLICK</u></strong></h3>

### Page 6: Flavors of SQL

SQL has various dialects or flavors, that have small differences in how they are implemented.

There will be a few times during this webinar when I will point out that the flavor of SQL we are using today is impacting the outputs we get. 

<h3><strong><u>CLICK</u></strong></h3>

Because different dialects of SQL can have different outputs, knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. 

In the hands-on portion of this webinar, we'll be using a form of SQL that actually runs in your web browser as you look at these slides.  This lightweight SQL engine is called "AlaSQL".  We pre-populated some tables for you to experiment with in this presentation.  These tables are filled with fabricated data meant to look a little like an electronic health record.  Rest assured that this data was completely invented, although it might look realistic!

<h3><strong><u>CLICK</u></strong></h3>

### Page 7: SELECT, FROM, WHERE

Before we learn any new SQL commands, let's do a quick review of the commands SELECT, FROM, and WHERE that we learned about earlier.

The basic structure of a SQL query is

SELECT, followed by some field or column names, then 
FROM, followed by one or more table names, then, possibly
WHERE, followed by a filtering condition.

<h3><strong><u>CLICK</u></strong></h3>

To start exploring the `patients` table from the `alasql` database, let's first take a look at all of the fields in the table. Use the asterisk as a wildcard to select all fields.

<h3><strong><u>RUN CODE</u></strong></h3>

For these in-browser code cells, the "play" button below the code box will run your code.

I'll go ahead and click this button.

When you run your query, the results of the query will be stored in a collapsable section below. I'll expand that section by clicking on this triangle!

This black bar between the code cell and the results is where any error messages will appear.

<h3><strong><u>CLICK</u></strong></h3>

Once you know what the column names are, you should usually select only the columns (or fields) you actually need.

We recommend using dot notation and comma-first style, shown here, to list the specific fields you want to see. 

I'll run this code to see the output.

<h3><strong><u>RUN CODE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.

As an example, here's how you'd filter the output to include only the records for a specific county, in our case, Suffolk County.

<h3><strong><u>RUN CODE</u></strong></h3>

We will also be seeing the `DISTINCT` and `ORDER BY` functions again today, and we will review them when we get there.

<h3><strong><u>CLICK</u></strong></h3>

## Page 8: `CASE`

Now that we've reviewed the basic SQL we learned last time, we are ready to learn some new SQL keywords and explore our database further. Our example database has three tables, `patients`, `allergies`, and `observations`. 

Let's look at the observations of "Peanut Immunoglobulin E Antibody in Serum" in the `alasql.observations` table.

<h3><strong><u>RUN CODE</u></strong></h3>

Taking a closer look at the `observation_value` field, those numbers would be a lot more useful if we knew what those numeric values indicate.

Often when working with data, you will come across the need to define your own custom categories or groupings given some raw row data as input. For example, you might have lipid levels that you want to categorize as _normal_, _borderline_, or _abnormal_. This is where the `CASE` statement can come in handy!

<h3><strong><u>CLICK</u></strong></h3>

### Page 9: Structure

The `CASE` statement is used to produce conditional row-level output.  It's like an "if" statement, but with multiple possibilities, or "cases," that are considered. Let's take a look at a generic example, then we'll practice with our dataset.

One way to think of a case statement is by its components. We will look at these components one by one, starting in the middle of the statement and working our way out.

<h3><strong><u>CLICK</u></strong></h3>

Conditional statements in SQL use this `WHEN`/`THEN` form. `WHEN` the conditional statement is true, `THEN` the designated output will be returned to you.

You can have as many conditional statements as you want. Be aware, however, that for each row, SQL will only return one output, corresponding to the first time a condition is found to be true.

<h3><strong><u>CLICK</u></strong></h3>

Let's consider what these statements would do in a row where `patients.age` (by the way, that's not actually a field that exists in our `patients` table, but let's just pretend) is, say, age 10. 

That row would not be categorized as an infant because it's not true that 10 is less than 1.  So the first WHEN/THEN doesn't trigger.
Let's look at the next WHEN/THEN.  Well, age 10 would be categorized as a child because 10 is indeed less than or equal to 12. That means this is the first WHEN/THEN to be triggered.
That means we're done checking.  We won't keep going and looking at the final WHEN/THEN statement.  So, even though 10 is less than or equal to 17, the age of 10 will not be categorized as "teen" because we already triggered an earlier WHEN/THEN statement, the one for "child".

<h3><strong><u>CLICK</u></strong></h3>

`ELSE` comes after all of the `WHEN`/`THEN` statements and tells SQL what to return if none of the cases, none of the WHEN/THEN statements, evaluate to true. 

If you leave out the `ELSE` clause, SQL imposes a condition of `ELSE NULL` by default. 

We strongly encourage you to always include an `ELSE` clause even if you like the default value of `ELSE NULL`, to make your code more explicit.  After all, you can always say `ELSE NULL` explicitly!

<h3><strong><u>CLICK</u></strong></h3>

Lastly, you need to open the statement with `CASE` and close it with `END`.

The indentation before each of the `WHEN` statements and the `ELSE` statement are for us as human readers of this code. SQL doesn't need those lines to be indented, but it makes it a lot clearer to us where this block of code starts and ends.

We have started with a lot of theory because `CASE` statements are complicated, so let's return to that `observations` table that we were looking at earlier, and see how using a `CASE` statement can help us categorize the data.

<h3><strong><u>CLICK</u></strong></h3>

### Page 10: Example

A `CASE` statement goes between the `SELECT` statement and the `FROM` statement in a SQL query. We might know that if that observed value of IgE Antibody is greater than or equal to 17.5, that is a strongly positive result, and also have known cutoff values corresponding to Positive, Equivocal, Borderline, and Negative results.  This might be helpful in writing reports to help families understand what these values mean.  Let's run this code, which gives us everything from the observations table, and then some category, which we derive using this case statement.

<h3><strong><u>RUN CODE</u></strong></h3>

When we run this code, we get a new column with the outcomes of our conditional `WHEN`/`THEN` statements in it. The data here looks great, we can read immediately that all three Peanut IgE antibody results were positive, two of them strongly positive. But we have this ugly column name, with the entire `CASE` statement as the name.  

We can make that column name much nicer by using an alias. At the end of the `CASE` statement, immediately after the word `END`....

[scroll up here] 

I'm going to add `AS interpretation` and run the code again. Using `AS` to give this new column an alias will make it much easier for us to read and understand.

<h3><strong><u>CLICK</u></strong></h3>

Here we just give an abstraction of what we just did.  It is usually a good idea to follow a closing `END` with `AS` to give your new column a useful alias.

I want to pause here for questions before giving you your first opportunity to practice coding in SQL on your own.

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### Page 11: 💫 **Your Turn 1** 

Rose has shared the link in chat, thank you Rose.  So you can click on that link to be taken directly to this page. 

You're studying attitudes about smoking and will issue a survey in phases.  Phase 1 will go out to residents of Plymouth County, Phase 2 will go out to residents of Essex County and Phase 3 will go out to Barnstable County.  Finish the following query such that you get the patient name, county, and a new column called `phase`. 

I'm going to give you a few minutes to try this on your own.  Don't forget that you can use the forward and back pagination to look back at what we covered earlier today, in case you need to copy and paste some example code.

You can see that there is a comment in the chat for you to thumbs-up when you are done, and when we have a sufficient number of people having finished, we will complete the query together. 

<h3><strong><u>MODIFY CODE WITH CODE BELOW</u></strong></h3>

OK, great, so it looks like we have a number of people who are ready to move on, and I apologize to those of you who aren't finished yet, but I am going to go ahead and show how to solve this.  First, we want to complete the WHEN/THEN statements, by adding patients.county to each statement and then setting them equal to "Plymouth County", then "Essex County", and finally "Barnstable County".  And I'm not quite done, because I want to give this value that gets returned, whether it's Phase 1, Phase 2, Phase 3, or NULL, a useful column name, so I'll alias that by typing AS phase here after the END statement.

Let's run that.

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

Any questions about that?


<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## Page 12: `LIKE`

So far, we've run queries that assume we know a lot about our database.  But sometimes we don't know exactly what's in our data. We can use SELECT DISTINCT to learn more. Let's take a closer look at the `allergies` table.

Use `SELECT DISTINCT` to discover which distinct allergy descriptions appear in the `allergies` table.

<h3><strong><u>RUN CODE</u></strong></h3>

Say you are interested in all types of pollen allergies, but not other allergies. With the tools we already have, you could get that information using a `WHERE` statement.

<h3><strong><u>CLICK</u></strong></h3>

To get all pollen allergies from the `allergies` table with a `WHERE` statement, you can list out every possibility and use "OR" between them.

In the very small table we are working with here, this method works fine. But if we were looking at a real patient data, there might be hundreds of types of pollen allergies. And the same allergy might show up as "Allergy to grass pollen" and "grass pollen allergy" with different wording and different capitalization, because different people chart differently! Or maybe a new patient comes in who has a new, different pollen allergy. In that case you would need to update the query or you'd run the risk of missing someone with a novel allergy.  You can imagine that this level of specificity is error-prone.

How can we get all the pollen allergies without having to specify them all, perfectly? We need the `LIKE` operator to help us out.

<h3><strong><u>CLICK</u></strong></h3>

### Page 13: Structure

`LIKE` operators let you compare text data to a pattern rather than checking if two strings of characters match perfectly.

This action is known as **pattern matching**, and can let you filter on row values that are similar, but not exact matches.

### Page 14: Patterns

The `LIKE` operator uses 2 distinct **wildcard characters** that let you make patterns where some characters are unknown.

The percent symbol is the "Wildcard" for 0 or more characters.
The underscore is the "Wildcard" for exactly 1 character.

Wildcard characters let us build patterns to compare with a string of text data. Let's take a closer look at some examples using the percent wildcard.

<h3><strong><u>CLICK</u></strong></h3>

Putting a percent symbol just at the beginning means anything can come before the characters in pollen, but the data must _end_ with "pollen". 
`%pollen` matches "Allergy to tree pollen" 

<h3><strong><u>CLICK</u></strong></h3>

If instead the percent symbol is only after the string `pollen`, a phrase would have to start with the letters "pollen" to be a match.

Capitalization matters to the `LIKE` operator.  If the P were capitalized in "Pollen allergy - trees" that would not be a match. We will return to the problem of capitalization in a moment.

<h3><strong><u>CLICK</u></strong></h3>

To match both of these constructions, as well as data like "Tree pollen allergy," we can put percent symbols both before and after.

<h3><strong><u>CLICK</u></strong></h3>

In the same way we needed quotes around the data we wanted to match exactly, the entire string of characters, wildcards included, must be enclosed in quotes.

<h3><strong><u>CLICK</u></strong></h3>

### Page 15: Example

Before we do our example, I'd like to do a quick poll to check our understanding of LIKE.  Rose, can you launch that first poll question?  Thank you!

Great, so a lot of people are correctly answering that LIKE can help us find patterns that are relevant to us, such as pollen allergies that will emerge in the future, or pollen allergies that people might list in different ways, using different phrasing but always with the word "pollen."  And you're right, the capitalization was a bit of a trick to see if you were listening.  LIKE does NOT automatically handle capitalization differences, but I'll show you how to handle that on this slide!

Let's apply this structure to finding the pollen allergies from our `alasql.allergies` table.  I'll run my query that looks for all allergies that contain the lower case word pollen somewhere in the description field.

<h3><strong><u>RUN CODE</u></strong></h3>

If we had a larger collection of possible allergies, this query would return all of the rows in which the character string "pollen" appears in the `allergies.description` field. 

But what if there was an entry where the word "Pollen" was capitalized? The `LIKE` operator cares about capitalization, a lower case `p` and an upper case `P` are not the same characters.

<h3><strong><u>CLICK</u></strong></h3>

The `LOWER()` (or `UPPER()`) operator can help us out by taking the data in a field and making all of the characters lowercase (or uppercase).

<h3><strong><u>MODIFY CODE</u></strong></h3>

Wrap the database data that we want to search in `LOWER()` so that we're flattening out any capitalization differences in our comparison.  This allows us to make sure the query returns both capital and lowercase versions of our pattern. 

So, I'll change allergies.description here to LOWER(allergies.description), so that no matter whether people typed in the allergy in upper or lower case, we'll convert it to lower case before we compare it to the lower case word pollen here on the right.

I want to pause here for questions before giving you your next opportunity to practice coding in SQL.  Rose, will you add the next link to chat?  Thanks!

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### Page 16: 💫 **Your Turn 2** 

<h3><strong><u>SHARE LINK</u></strong></h3>

You'd like to research patients born in the 1970s (so any year starting with 197 would work).  Use a `LIKE` statement to enrich the query below and limit the patient set to just the patients you care about.

I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will complete the query together. 

ANSWER:

Okay, so let's add a WHERE statement here.  We'll say where patients.birthdate is LIKE '197%'.

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## Page 17: Aggregate Functions

**Aggregate functions** can be used to get a single value related the values for multiple rows of data in some meaningful way.  And it's really important to remember that it returns ONE value and one value only.

This aggregation could be a numerical statistic, like the sum or standard deviation of a number of rows, or it could pull out a special value, like the minimum or maximum value (this works as well for strings, in which case it would be the first or last value in alphabetical order). There are many other possibilities as well, like giving a count of rows or pulling a value at random from the rows.

Here are some commonly used aggregate functions:

* `COUNT()`- Returns the count of the number of non-null values among the column(s)/rows provided as input.
* `SUM()`- Returns the summation of all values from a column provided as input.
* `MIN()`- Returns the minimum value from a column provided as input.
* `MAX()`- Returns the maximum value from a column provided as input.
* `AVG()`- Returns the numerical mean of all values from a column provided as input.

To count the rows in a table, use `COUNT(*)`.

COUNT will ignore null values, which can help you figure out how many values are in various columns, as we see here.

<h3><strong><u>RUN CODE</u></strong></h3>

The count function shows us that the `patients` table has 25 rows, and all of those 25 rows contains a `birthdate`. But most rows have a `NULL` value for the `deathdate`.

<h3><strong><u>CLICK</u></strong></h3>
<h3><strong><u>RUN CODE</u></strong></h3>

SQL will do its best to use the aggregate functions regardless of what type of data is in the column, but the outputs will make the most sense if the data type is what the function expects. For example `SUM` works best, as you might suspect, with numbers.  It might return some kind of value for a column that isn't numeric, but it probably won't be useful information. The `MAX` and `MIN` functions, on the other hand, are also typically used with numbers, but they might be useful even when used on text data: they will give the first or last, the min or max, value, of the text once it's ordered alphabetically.

<h3><strong><u>CLICK</u></strong></h3>

### Page 18: `GROUP BY`

Often, you are interested in statistics by group, such as the average BMI for men and that for women, or the standard deviation of reading test scores in teens with ADHD, depression, neither condition, or both conditions.

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

### Page 19: `HAVING`

And this is our last topic, and it's one you might not use that often.  I've left it for last because I know this is a dense session.

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

Phew, that was a lot! I want to pause here for questions before giving you your final opportunity to practice coding in SQL in this session.

<h3><strong><u>PAUSE</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

### Page 20: 💫 **Your Turn 3** 

<h3><strong><u>SHARE LINK</u></strong></h3>

This is a bit of a challenge because I'm not giving you any code to start with.

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

## Page 21: Recap

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

## Page 22: Additional Resources

* Khan Academy's [Introduction to SQL](https://www.khanacademy.org/computing/computer-programming/sql) is high quality and easy to learn from.

* Tutorials Point has some helpful documentation you may want to check out to read more [about the basic types of **operators** available for use in a SQL query](https://www.tutorialspoint.com/sql/sql-operators.htm).

* Give the [SQL Murder Mystery](https://mystery.knightlab.com/) a try. Note that some of the content is more advanced than what we cover here, but there is a walkthrough, and you can always stop once you've reached the limits of what we've learned so far. 

* Select Star SQL is a [free interactive book that teaches SQL](https://selectstarsql.com/) by exploring Texas state execution data. The second and third chapters mostly cover topics we learned about today, while the remaining chapters dig deeper.

## Page 23: Upcoming sessions

Want to see the materials from an earlier session? 
Everything is available on the [Arcus SQL Skill Series website](https://arcus.github.io/arcus_skill_series_sql/). There's another session of today's topic, SQL intermediate, on December 3.  And later on in December, we have SQL Joins, which you'll want to take because you'll learn how to gather data from multiple tables into one dataset, which is what we almost always have to do in medicine.

## Page 24: Arcus On-Ramp

We offer three different Arcus On-Ramp workshops, each focused on a different aspect of doing research in Arcus.  We offer these on a regular, rotating basis all year.

The Arcus On-Ramp workshops are different from these skill series workshops in two big ways: First, although the Arcus On-Ramp workshops use tools like SQL, R, and Python, the focus is on how to work in an Arcus Lab, not learning those languages per se. 

And secondly, because the On-Ramp workshops use real patient data, unlike today's workshop, you need to have completed CITI training and attested the Arcus terms of use before you can sign up.

If you're feeling like you'd like a realistic, worked example of how SQL might be used in an Arcus Lab to answer a research question, then the Arcus On-Ramp is for you!

## Page 25: 💫 One last poll!

I have one final poll for you.

Note that this poll has two questions, so after you answer the first one you'll need to click the little arrow at the bottom right to go to the second question.

Your time is a non-renewable resource, and it's very important to us that we use your time wisely. 
Data we collect like this are really important in shaping what kinds of education we offer, so thank you so much for taking a moment to provide feedback!

I'll also turn off the recording now and answer any questions you may have.
