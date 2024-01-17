# SQL Basics Speaker Notes

Welcome! 
I'm Rose Franzen, and I use she/her pronouns. 
I'm a data science educator with the Arcus project in DBHi. 
Today's talk is the third in our five-part series on sequel, or S-Q-L.  
Today's webinar will be recorded, so please leave your cameras and mics turned off until the question time at the end.
If you do have questions that come up during the talk, feel free to put them in the chat. 
So with that, let's get started!
<h2> **CLICK** </h2>

## Today's Talk
Today, we'll be learning how to do basic SQL queries on single tables. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting -- don't worry. I'll provide plenty of scaffolding, and we'll work through things together. 

You'll learn how to compose simple queries using keywords such as SELECT, WHERE, FROM, DISTINCT, AS, and ORDER BY. We'll also introduce you to the value of the LIMIT keyword, as well as cover working with null (or empty) values using IS NULL and IS NOT NULL. 

In order to code along with me, you'll need to open the following link in your browser: https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_basics/sql_basics.md 

<h2> **COPY INTO CHAT** </h2> https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/sql_basics/sql_basics.md  

<h2> **CLICK** </h2> 

## Thank you!

Many thanks to Peter and Joy for their work developing this excellent content!
And, of course, any errors or awkwardness in this version are mine. While our webinar today will cover all of the topics in their module, we won't be doing all of the exercises or quiz questions, so if you're interested in getting just a bit more practice, I suggest you check out the module after our session. 

<h2> **CLICK** </h2> 

## Learn by doing
We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using a fake patient dataset. There will also be some short quizzes to help solidify your understanding as we go.


With that being said, lets hop in

<h2> **CLICK** </h2> 

## SQL: A Brief Refresher

First, let's quickly review some key concepts from our November and December sessions. 
"Sequel", or S-Q-L (either pronunciation is fine) stands for Structured Query Language. SQL is a programming language used to interact with Relational Databases. 

Relational databases consist of many different data tables. The model of storing data across multiple tables rather than one MEGA-table is useful because it is more efficient, reduces data duplication, and makes correcting or updating data simpler and less error prone. When data has been fragmented to reduce inefficiency and repetition, it is considered to be **normalized**. Today we will only be working with data from **one** table at a time that is stored in such a relational database. To learn more about combining data from more than one table, be sure to catch our final presentation in the series on SQL Joins (dates on the final slide).

<h3> **CLICK** </h3> 

SQL is great at working with rectangular data, data that is stored in tables with rows and columns / fields.  Its powerful SELECT - FROM - WHERE syntax makes SQL an ideal tool for isolating just the data you care about, whether that's specifying the columns you're interested in or limiting your data to just those rows that meet certain conditions. 

<h3> **CLICK** </h3> 

However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other tools like R or Python, which are better suited for work like statistical analysis.

<h2> **CLICK** </h2> 

## SQL Implementations 

Believe it or not, SQL is technically not just one thing -- there are a variety of different implementations. Although all SQL implementations have a similar structure, and the same basic syntax, each different SQL database product often has its own minor variations in dialect.
 

Colloquially people often refer to the different SQL dialects as different "flavors" of SQL.

The most common difference between different SQL "flavors" are the availability of different functions that users can use for data manipulation, as well as the types of error messages that will be returned to the user when running code with syntax issues.

Knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. Whenever you search for documentation online or are troubleshooting, you'll want to be sure to include the name of the "flavor" you're working with in your search terms. 

<h3> **CLICK** </h3> 

In the hands-on portion of this webinar, we'll be using a form of SQL that actually runs in your web browser as you look at these pages.  This lightweight SQL engine is called "AlaSQL".  We pre-populated some tables for you to experiment with in this presentation.  These tables are filled with fabricated data meant to look a little like an electronic health record (EHR).  Rest assured that this data was completely invented, although it might look realistic!

<h2> **CLICK** </h2> 

## SQL Queries

In order to receive the data we want from the database, we must communicate our requests to it via special "queries". 
Let's take a closer look at how to compose a SQL query!

<h3> **CLICK** </h3> 

At a high level, we generally provide three pieces of information when constructing SQL queries:

 1. The name of the **table(s)** where the data is stored.
 2. The **column name(s)** you want to look at from the table(s) you specified.
 3. Any **filtering condition(s)** you want to apply to your data pull.  This part is optional but is often used.

<h3> **CLICK** </h3>

 You put these basic pieces of information together using the syntax show here to create a SQL query. 

<h3> **CLICK** </h3> 

For example, here are some sample queries, each of which take place on a single table. 

In the chat, let me know what you think the name of the table is in the first example query. 

_Insert ad libs here as answers come in as appropriate_

 
To be extra clear, we end each query with a semicolon. This tells SQL you're done with a query.  If you're working interactively with SQL, one query at a time, you can sometimes get away with not ending your query with a semicolon.  Still, one of the things we're interested in doing in this webinar is instilling good practices from the start, so we encourage you to always end your queries with proper punctuation.

Similarly, while we write these queries all on a single line to show you a few examples in just a little space, that's the last time you'll see that kind of SQL in this webinar. On the next slide, we're going to get into some strong opinions about SQL style here that we'd like to share. 

<h2> **CLICK** </h2> 

## An Aside About Style
Style is how we choose to write SQL or other languages, within the confines of syntax. Style can be used to help humans read and write code more easily, closer to how they they read and write their natural languages.

<h3> **CLICK** </h3> 

All of the queries are on screen valid and would work perfectly fine.  What distinguishes them is __style__. 

Most of the style conventions we're going to advocate for are on display here in the third query.

There is no SQL-level enforcement of line breaks or indentation -- you could write a long query on a single line, even if its so long that it runs off the side of the screen.  You are free to write SQL as you see fit, but we encourage you to adopt specific conventions and hold yourself to them, as doing so may make it easier to understand and troubleshoot your own code. 

You may be working with a team that has an established SQL style guide, either in written form or as oral tradition.  If so, ignore the style suggestions we offer and do what they suggest.  Since style is intended to help humans read and write code more easily, it's a good idea to go along with what is already understood within your team.  Everyone agreeing on conventions like when to start a new line and how and where to comment means it's easier for other people to help you with your code or for you to copy / paste from existing examples your peers share with you.


It might seem silly to start talking about style now with very short queries, but this is all about developing good habits from the start. That way, when you do start writing more complex queries, it's one fewer thing to worry about. We are going to advocate for some style conventions that not everyone will share. If you depart from our suggestions, that's fine -- just be sure to eventually develop your own standards for style! We promise, this will help you immensely once your SQL queries get to be 5, 10, or 100 lines long.

Here are our (opinionated but not necessarily "right") style suggestions.  These might not make sense right now, but once you see them in actual queries, we think you'll understand them more intuitively.

<h3> **CLICK** </h3> 

Put keywords in CAPITAL LETTERS so they stand out. 

Examples of keywords are SELECT, LIKE, AS, WHERE, JOIN, DISTINCT, MEAN, ORDER BY, and many more.  While most code editors and SQL clients (software that lets you query a database) do a good job of color-coding these special words, you might end up seeing a SQL query in monochrome, and having keywords stand out helps  you figure out where each part of your query is.  

<h3> **CLICK** </h3> 

Put members of a list on separate lines
This usually means the list of fields you're requesting, or the tables that you're querying.  Putting each item on its own line is easier on the eyes and allows for much easier cut-and-paste to rearrange things.  It also means you have space after each item of the list to add a comment if necessary.

<h3> **CLICK** </h3> 
 
Use indentation to clarify the various sections of your query. 

Indenting the list of columns below a SELECT statement is a way of subordinating those lines to the SELECT, subtly indicating that those lines are a continuation of the SELECT statement.  A new line that isn't indented (say, a FROM statement) shows that the SELECT part of the query is over.

<h3> **CLICK** </h3> 
Use "dot notation"

We'll talk more  about dot notation in the next section, but for now --  Dot notation means adding more information about your data, for example, by including the table name the column comes from.  This practice will prepare you for using multiple data sources in your queries. In the example above, we do this by specifying that each column that we're requesting comes from the products table. This one may make more sense as we go along. 

<h3> **CLICK** </h3> 
Use a comma-first style
What this means is to that, in a list of length n, instead of putting the comma **after** items 1 through n-1.  Instead, you put the comma **before** items 2 through n.The first time I saw someone doing this, it totally threw me for a loop! However, once I learned the reason, I became a quick convert, as I realized it solves some of my biggest annoyances when working with lists! There are two key reasons I prefer this approach over the more conventional style:


(1) the commas all line up -- this makes it much easier to identify at a quick glance if you've forgotten a comma -- a common source of errors when running code that involves lists!

(2) Relatedly, this it also makes it much easier to re-order a list or remove items entirely. Typically, the first item in your list is something of central importance, and will stay in first place. In SQL we often try a short query with just a few fields, then add a few more, then maybe rearrange their order, and finally delete the columns we don't need.  Usually, the first item in a list of columns is something of central importance, while the others in the list have a higher likelihood to be ones you may decide you don't need, or will change the order of. Because you rarely touch the first item in a list but more frequently change the last item, it's less likely that you'll introduce a missing (or extra) comma using a comma-first paradigm as compared to the comma-last style. This also prevents you from accidentally winding up with a comma after the final item on your list -- another common issue or error! 


Now that we've got you thinking about style, let's move on to the substance of SQL and work with SELECT and FROM.

<h2> **CLICK** </h2> 

## SELECT AND FROM 

A **SELECT statement:** is used to specify which columns (or fields, we use both terms interchangeably here) you would like to have returned as output from your SQL query.

<h3> **CLICK** </h3> 

The basic components of a select statement are the `SELECT` and `FROM` keywords. The `FROM` keyword is used to specify the table or tables that hold the data you're interested in, and the `SELECT` keyword is used to provide a list of columns within those table(s) that you would like returned as output.  

<h3> **CLICK** </h3> 


The asterisk is the "wildcard" character in SQL. When used alone, it indicates that you want to match **everything**. So in this case, you're asking SQL to select **all** of the fields from the patients table. 


Taking a look at the `FROM` line of this query, you may notice that the table name is written as two words separated by a period. This is the "dot notation" that we alluded to on the previous slide. Dot notation generally looks something like 

<h3> **CLICK** </h3> 

`dataset_name.table_name.column_name`


In our sample query here, the first word in dot notation after the FROM keyword is alasql, which is the name of the **schema**, **catalog**, or **dataset** that the data is stored in. (terms vary according to which flavor of SQL you're using). The second word, "patients" is the name of the specific table within that dataset that we're hoping to query. 


Alright, lets run our first SQL query of the day! I'm going to hit the execute button, which is the right-facing triangle in the small circle below the SQL code.

<h3> **CLICK RUN ON THE CODE** </h3> 


So let's take a look at our output. We have a variety of columns, such as id, birthdate, deathdate, first and last name, and more. If we couldn't already tell before from just the name "patients", its clear now that this is a table that contains important demographic information for patients in this fake Electronic Health Record. 

Let's move on now to our first exercise!

<h2> **CLICK** </h2> 

## Your Turn 1

Using the code template we've provided here, complete the code to get all the fields from the table `alasql.allergies`.  It might help to hide the query results from the query above, by clicking beside "Results of Query."  That way you can see the SQL query we used, and model your code on the query above! When you think you have it, try running the query to see if you get it right. 


Once you've had a chance to try this exercise, like my message in the chat, so I can have a good sense for  when we should regroup to move on. (remove from slides)


<h3> Copy the following into chat:</h3> 

"Like this message when you're done with "Your Turn 1"."


Okay, it seems like a fair number of people have had a chance to work through this, so lets start to regroup.....



To get this data, we're going to want to write out SELECT * FROM alasql.allergies; 

When you run the query, you should see a table with five columns: start, stop, patient, encounter, and description. Note that while you would also get these same results if you just wrote FROM allergies instead of alasql.allergies, for the reasons we discussed before, we suggest writing the table name out using dot notation, so as to also include the dataset/schema name. 


I'll pause here briefly to see if there are any questions...

_Answer the questions if they exist_


So we've practiced requesting all of the columns of a table, but what if we only want a few of them? 


<h2> **CLICK** <h2>

## Selecting Specific Columns


In order to return only a specific few of the columns, you need to write a comma-separated list of the columns you want after the `SELECT` keyword.

<h3> CLICK </h3>


Note that this time, we're also using dot notation for our columns, in the form of `table_name.column_name`. We do this to be very explicit about which data we mean.  

Now, it might seem a bit redundant in this example to list our columns this way. After all, we already list that the data is coming from the `patients` table in the `FROM` statement, and we're only querying one table.


This is another example of forming good habits early. While right now, we're only querying from one table, eventually (though not in today's workshop) you will need to do queries that involve multiple tables. Sometimes, these tables may have identical column names. In that case, you are **required** to specify which table you're referring to in order to disambiguate. 


SQL won't automatically know if you're asking for `date` in `encounters` table, or `date` in `medication_administration` table?  Rather than learn dot notation later, we want to introduce you to it now, even if it feels unnecessary. That way, when you do get to the point of querying multiple tables, it will already feel natural to you, and you can focus all your brain power on learning the other, trickier aspects of mastering queries of multiple tables at once.


It's also a good idea to get into the habit of doing it now so that it's easier to change your code down the line. You may write an initial query on just one table from a dataset you're not super familiar with, only to discover that in order to answer your question, you actually need to get data from more than one table. Rather than having to go back through and update all of your code to ensure it references the table so you can add references to the other table, you will already be set up for successfully querying more than one table. 


--{{0}}--
Let's go ahead and run this code by clicking the execute button.  

_click the button and run the code_

_pause and count to 5 before continuing so folks have a moment to process the results_ 

--{{0}}--
Just as we would hope, this time we haven't received the entire patients table, like we saw on the page before, but instead can only see the five columns we requested. 

<h2> CLICK </h2>

## DISTINCT

(The next keyword we're going to discuss is `DISTINCT`.) The `DISTINCT` clause in **SQL** can be placed directly after the `SELECT` key word, and can be used to limit your result set to only the unique row values.  


This can be especially useful when exploring a dataset for the first time and trying to become familiar with the data in each column of a given table.  

<h3> CLICK </h3>

For example, perhaps you want to see all the possible values for `sex` or `race` in the `patients` table, to understand a bit more about the data collection options.  If you were to use `SELECT` by itself to get just the `race` field from the `patients` table, you'd get the race of every patient, with lots of repeats.  Using `SELECT DISTINCT` instead, you get a much shorter list of every possible value for `race`, each listed just once.


As you can see in this example, `SELECT DISTINCT` can also be used on more than one field.  The code block below provides an example of using this syntax to investigate the unique combinations of values from the `sex` and `ethnicity` columns from the `patient` table. Let's go ahead and execute this code to see the results.  


_click the button and run the code_

_pause and count to 5 to give folks a chance to process the results_ 


We can see here that there are four different combinations of sex and ethnicity. Note, though, that `SELECT DISTINCT ` only shows you the combinations that actually exist in the table, rather than all of the combinations that could possibly exist. So, for example, if there were no female nonhispanic patients in this table, our result would have only been three rows long. 

<h2> CLICK </h2>

## Your Turn 2 

Now, let's use what we've just learned to write a query that returns all of the unique combinations of `county` and `state` from the `patients` table. How many different combinations do you find? 

Don't forget to like my message in the chat when you're done! 

<h3> Copy the following into chat: </h3>

Like this message when you're done with "Your Turn 2".

_wait for a while as folks complete_

Ok, it looks like a decent number have had a chance to complete, so let's start to regroup.... 

_pause for a few moments to give people a moment to switch gears_ 

We accomplish this by running

```sql
SELECT DISTINCT
	patients.county
	,patients.state
FROM alasql.patients;
```

When we run this code, we should get a result that shows 9 different rows -- 9 counties, all of which are in Massachusetts. 

Before we move on any further, I'm going to pause for a few moments to see if there's any new questions that have risen in the chat..... 

_answer any of them if they exist, also just have a sip of water and breathe_ 

<h2> CLICK </h2>

## Adding Comments

**Comments** are explanatory or helpful bits of text that you can add to your code as documentation for yourself or other reviewers of your code.  Similarly to style choices, comments don't actually affect the execution of the SQL code in any way and are simply there for humans.


In **SQL** there are 2 different techniques that can be used for adding comments. First, there's single line comments. 


Single-line comments are created by typing 2 minus signs in a row. Then, anything that appears to the right that delimiter will be treated as comment text.


And there's also multi-line comments. These are started by adding the `/*` characters at the beginning of your comment, and `*/` characters at the very end of your comment.

<h3> CLICK </h3>

Here's an example that uses both! By having the code commented, it's much easier for Future You to remember exactly what this query does without having to do any extra work, or for someone who _isn't you_ to figure out what's going on! 

<h2> CLICK </h2>

## WHERE 

The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.


As an example, here's how you'd filter the output to only include records for a specific county: 


<h3> CLICK </h3>


_read through the example on the screen, provide interpretation_

Although this example shows only one constraint for the dataset, the WHERE clause can contain any number of filtering arguments needed.

<h3> CLICK </h3>

This example includes multiple constraints, and makes use of both **comparison** operators like equals `=` and `<=` less than or equal to, and **logical** operators including `AND` and `OR`.  


Helpfully, this query has some comments added in! Since the queries are getting a bit more complex, it's worth trying to describe this query to yourself in plain English (or another natural language). Take a moment and work through this query in your head, and see if you can figure out what it's saying. 


_Give everyone a moment to look at it, maybe 20-30 secs before you regroup and tell them what it is_


So, you may have figured out that this query is limiting the data to only patients in Suffolk or Barnstable counties who are either hispanic or race other than white. Let's run it just to be sure

_RUN QUERY -- review results._
 As you can see, we receive just four rows back -- each of which are from either Barnstable or Suffolk county, and are for patients that are either hispanic or non-white.



You may have also noticed that there are some parentheses in this query. There are parentheses surrounding the county-related bits of logic and the race and ethnicity bits of logic. This is because it's easy to make a logical order-of-operations mistake when you mix both `AND` and `OR`. That's why it's crucial to include parentheses to show the scope of your `AND` and `OR` logical operators.

To see this in action, let's remove the second set of parentheses, around the `race` and `ethnicity` comparisons, and re-run the query.  What happens?  Why?  

_remove just the SECOND set of parentheses, and run the query again_ 

_pause for a moment while results process. Read the following as you show what's going on in the table_ 

Now, our resulting table is much longer, and includes rows where the patient is from a county other than Barnstable or Suffolk, as long as they are not white, which satisfies the final "OR" condition. 


Ready to try your luck at a complex WHERE statement? Let's move on to our third exercise!

<h2> CLICK </h2>

## Your Turn 3

Get every field from `patients` for all male patients who were born on or after January 1, 2001. Remember, you can write the query iteratively. So if you're not  sure about the field name that holds sex, or whether male is coded "Male" (with a capital M), "male" (with a lowercase m), "M", or some other way?  Look at the results of other queries to get this information! 


Whenever you've had a chance to finish working through the example, be sure to like my message in the chat! 

<h3> Copy the following into chat:</h3> 
Like this message when you're done with "Your Turn 3".


It seems like many of us have had a chance to try it/ so lets regroup....

_wait a moment while brains do their task switching_ 

We're able to accomplish this by running:

```sql
SELECT *
FROM alasql.patients
WHERE 
	patients.birthdate >= "2001-01-01" AND
	patients.sex = "M";
```

Let's move on to our next topic: null values

<h2> CLICK <h2>

## Null values

Like many programming languages, **SQL** deals with "blank" values in a very specific way.
**SQL** uses the concept of **null** to represent "blank" row values.

<h3> CLICK </h3>

When you need to filter on null values you'll use the `IS NULL` or `IS NOT NULL` operators.

Let's imagine we want to see rows from the `allergies` table where the `stop` value (the date at which the presumed allergy was considered no longer applicable, resolved, a mistake, or not an allergy) isn't missing.  In other words, the allergy has a date at which it was ruled to not exist.

<h3> CLICK </h3>

As you can see in our example, you achieve this by using the keywords `IS NOT NULL`. Take careful note that we are _not_ filtering null values by using the inequality operator. In fact, you _can't_ filter null values using equality or inequality operators. That's why the `IS` and `IS NOT` key words exist. That's because, in a more esoteric sense, null values are inherently unknowable, and therefore we can't assess whether it is equal to anything. Similarly, you can't do math with a null value. 

Let's think about this in the context of the `stop` column in the `allergies` table. 

<h3> CLICK </h3>

Here, we're asking SQL to give us all of the columns in the allergies table where the stop date is less than March 1, 2020. 

--{{3}}--
When this code is run, each row's `stop` value will be assessed against our `where` statement. Let's think through all of the possible categories that these values could fall into. 

The `stop` value could be a date less than (or earlier to) March 1, 2020. 
It could be a date that is equal to March 1, 2020. 
It could be a date greater than (or after) March 1, 2020. 
Or, the value could be blank, with no date listed at all -- in other words, it could be `null`. 


Given what you've learned so far about WHERE statements, filtering, and `NULL` values, which category or categories do you think the returned data will fall into? Take a moment and respond in the Teams poll.  


_as necessary, make sure the teams poll is highly visible_

_wait for a bit as responses come in_

--{{4}}--

Riff here as responses come in looks like a lot of people think its x, and others think its also y.... etc


Let's run the code now and see what the results are! 

_run the code_ 


(It seems like we were mostly on the right mark / riff here based upon what the most popular answer was). The only rows returned are those with a date earlier than March 1, 2020. Dates equal to or later than that date are not included, of course, because they are in obvious violation of the WHERE clause filter. Rows that do not have a date (ie, NULL values) are not returned, because they cannot be evaluated with the comparison operator. 

 
The fact that nulls aren't included in comparisons is a very subtle distinction that can drastically alter the output of your SQL statements.  This can be very important when writing inclusion and exclusion logic and thinking about what cases belong in your data set.  Always keep in mind that you might have missing values, and consider what that might mean for your selection of rows.  

Now, perhaps we're interested in running an analysis only on allergies that are current, that is, they do not have a `stop` date. And perhaps we're aware that allergies with a date prior to March 1, 2020 have some possible data quality issues, and should be manually checked to see if they are actually current allergies that had a stop date entered by mistake. 


In that case, we would want to return a mix of both null and non-null values. In order to achieve this, we'd need to combine what we already know about comparison operators and null values, along with our previously learned lessons about **logical** operators. 

<h3> CLICK </h3>

By combining a date comparison along with the `IS NULL` operator using the `OR` keyword, we create a WHERE statement that returns any rows that either have no stop date, or have a stop date prior to March 1, 2020. 

<h2> CLICK </h2>

## ORDER BY Statement

Another useful piece of SQL syntax for exploring datasets is the `ORDER BY` statement, which (as its name suggests) is used to order your result set by a given set of one or more columns.

When listing columns in the `ORDER BY` statement you can specify that they be sorted in either ascending (`ASC`) or descending (`DESC`) order. By default, all items in the `ORDER BY` clause will be sorted in `ASC` (ascending) order if no explicit ordering direction is provided.

If you list more than one column in `ORDER BY`, items will be sorted first by the first column you provide, and then, within "ties", by the second, then third, etc., column.  

<h3> CLICK </h3>

For instance, this code sorts first by `county`, and then within each possible value of `county` sorts by `ethnicity`. Let's run it and take a look at the output. ((ad libs here about the result. at first it might look like its not sorting w/in ethnicity, but actualy quite a few counties don't seem to have any hispanic patients in the dataset, remember from before that DISTINCT only shows the combinations that actually exist in the data, not all theoretically possible combinations ..... ))

<h2> CLICK </h2>

## LIMIT

The `LIMIT` clause can be used to limit the result set of your select statement to a maximum number of rows.

<h3> CLICK </h3>


This is achieved by adding the word `LIMIT` as the last line of your query, followed by the number of rows you would like your result set truncated at. This really useful when initially exploring tables you are unfamiliar with.  Showing just the first three or five or ten rows of a table can give you a quick intuitive grasp of the contents of the whole table and will come back very quickly.  Without a `LIMIT`, large tables can take a long time to return all their results.

_run it to show_

This example returns all columns from the `patients` table, and limits the result set to only 3 rows.

<h2> CLICK </h2>

## Aliasing with AS

In SQL, it is possible to assign a custom name (usually a kind of shortened name) to a table or column in your query using a technique called **aliasing**.

<h3> CLICK </h3>

Aliasing **tables** can be helpful for long or complex queries involving multiple tables because it allows you to avoid typing out the full name of a table each time you refer to it. 

<h3> CLICK </h3>

For example, in a long query involving the `patients` table, the `encounters` table, and the `diagnosis` table, you might prefer to use the shorthand terms `pt`, `enc`, and `dx` or even `p`, `e`, and `d`.

<h3> CLICK </h3>

Aliasing **columns** can be helpful by assigning clearer, more comprehensible names for a given column than the name that might be assigned to it in the database.  

<h3> CLICK </h3>

For example, you might want to see the results from the `stop` column in the `allergies` table returned to you not as `stop`, but rather as `ruled_out_date`.

<h3> CLICK </h3>

Aliases are assigned by placing the `AS` key word directly after the item (table/column) you would like to alias, followed by the name you would like to assign as its **alias**.


In this example, we can see aliasing being used to rename the `patient` table to `p`, and renaming the `id` column to `unique_patient_id` (because there are other id fields you're working with elsewhere) and the `state` coluumn to `state_name` (because you want to point out that this isn't the state abbreviation).
_run code, show that results are true_ 

<h2> CLICK </h2>

## Your Turn 4

For one final exercise, let's combine several of the skills that we've learned so far write a query that accomplishes the following:

* Retrieves the patient identifier, sex, ethnicity, state, and zip
* Aliases the `patients` table as `pt`
* Aliases the `sex` field as `sex_assigned_at_birth`
* Aliases `zip` as `postal_code`
* Orders the result by zip/postal code


If you're feeling unsure of where to start, consider starting with a simple query (something like a `SELECT * ...`) and gradually changing it so that you knock out one bullet point at a time! 


Take a few moments to try this out on your own. When you're done, don't forget to let me know by liking the message in the chat. 

<h3> Copy the following into chat:</h3> 
Like this message when you're done with "Your Turn 4".

_once its time to regroup_ 

Alright, don't worry if you didn't have a chance to finish, let's regroup now and go over the result together!


_type out the result as you go over the answer_

```sql
SELECT 
	pt.id
	,pt.sex as sex_assigned_at_birth
	,pt.ethnicity
	,pt.state
	,pt.zip as postal_code
FROM alasql.patients as pt
ORDER BY postal_code;
```

We start off with a SELECT statement, followed by our list of columns, each of which is on a new line. Although the FROM line doesn't come until after this, it's okay to use the table alias when we list our columns, even though it looks like we haven't told SQL about the table name yet! 
As we go, we alias the sex and zip columns.

Then, we have our FROM statement, where we specify the table that we're querying, and the alias that we want to use for it. 
Finally, we order our results by the (aliased) postal code field!

<h2>CLICK </h2>

So, to recap, today, you learned about the language "sequel" or S-Q-L, which is an acronym for "Structured Query Language", a powerful tool for retrieving data from relational databases. 

We covered a variety of important functions, represented in SQL by **keywords**. In particular, we covered: 

 <h3> CLICK AND READ x9 <h3>

We also learned about comparison operators, comments, and style -- how to write code in a specific way that promotes reusability and readability.

You also got to practice hands on, which probably meant you got to see some error messages, too, which is helpful experience.

<h2> CLICK </h2>

On this slide, we have some suggestions of additional resources for learning more about SQL. As I mentioned earlier, we also didn't exhaust 100% of the exercises and quiz questions in the module that this presentation is based upon, so you can also use that as another resource. We'll drop the link into the chat again. 

<h2> CLICK </h2>

Finally, for even more learning, we suggest coming to the final sessions in our series on SQL!

In February, we will practice more with single tables, learning keywords like CASE, LIKE, and GROUP BY.

Then, in March, we'll cover working with multiple tables, and how to join data from different tables into one dataset to work with!