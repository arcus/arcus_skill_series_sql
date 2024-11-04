<!--
author: Rose Franzen
email: franzenr@chop.edu
version: 1.0.0
current_version_description: Updated for 2024 presentation by Rose Hartman
module_type: slides
docs_version: 3.0.0
language: en
narrator: US English Male
mode: Presentation
classroom: enable
@onload: window.LIA.settings.sound = false

title: SQL Basics
comment:  Structured Query Language, or SQL, is a relational database solution that has been around for decades.  Learn how to do basic SQL queries on single tables, by using code, hands-on.
long_description: Do you want to learn basic Structured Query Language (SQL) either to understand concepts or prepare for access to a relational database?  This module will give you hands on experience with simple queries using keywords including SELECT, WHERE, FROM, DISTINCT, and AS.  We'll also briefly cover working with empty (NULL) values using IS NULL and IS NOT NULL.  This module is appropriate for people who have little or no experience in SQL and are ready to practice with real queries.
estimated_time_in_minutes: 60

@pre_reqs
Experience working with rectangular data (data in rows and columns) is required, as is some exposure to the idea of SQL and its use of tables with rows and columns.  No experience writing SQL code is expected or required for this module.  If you would like a code-free overview to SQL we recommend our module [Demystifying SQL](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/education_modules/main/demystifying_sql/demystifying_sql.md).
@end

@learning_objectives  
After completion of this module, learners will be able to:

- Use SELECT, FROM, and WHERE to do a basic query on a SQL table
- Use IS NULL and IS NOT NULL operators to work with empty values
- Explain the use of DISTINCT and how it can be useful
- Use AS and ORDER BY to change how query results appear
- Explain why the LIMIT keyword can be useful
@end

good_first_module: false
data_domain: ehr
data_task: data_wrangling
collection: learn_to_code
coding_required: true
coding_level: basic
coding_language: sql
sequence_name: sql

@sets_you_up_for

@end

@depends_on_knowledge_available_in

@end

@version_history
No previous versions.
@end

repo_link: [GitHub repository for these materials](https://github.com/arcus/arcus_skill_series_sql)
module_link: [SQL Basics](https://bit.ly/DART_sql_basics)

import: https://raw.githubusercontent.com/arcus/education_modules/main/_module_templates/macros.md
import: https://raw.githubusercontent.com/arcus/education_modules/main/_module_templates/macros_sql.md
import: https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/macros_slides.md

-->


# SQL Basics
@sql_series_slide

--{{0}}--
Welcome! 
I'm Rose Hartman, and I use she/her pronouns. 
I'm a data science educator with the Arcus project in DBHi. 
Today's talk is the third in our five-part series on SQL.  
Today's webinar will be recorded, so please leave your cameras and mics turned off until the question time at the end.
If you do have questions that come up during the talk, feel free to put them in the chat. 
So with that, let's get started!

## Today's talk

@todays_talk 

--{{0}}--
Today, we'll be learning how to do basic SQL queries on single tables. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting -- don't worry. I'll provide plenty of scaffolding, and we'll work through things together. 

--{{0}}--
You'll learn how to compose simple queries using keywords such as SELECT, WHERE, FROM, DISTINCT, AS, and ORDER BY. We'll also introduce you to the value of the LIMIT keyword, as well as cover working with null (or empty) values using IS NULL and IS NOT NULL. 


## Thank you!

<div class = "gratitude">
<b style="color: rgb(var(--color-highlight));">Thank you!</b><br>

Material for this talk is based closely on the DART module @module_link, written by Peter Camacho and Joy Payton.

</div>

--{{0}}--
Many thanks to Peter and Joy for their work developing this excellent content!
While our webinar today will cover all of the topics in their module, we won't be doing all of the exercises or quiz questions, so if you're interested in getting just a bit more practice, I suggest you check out the module after our session. 
I'll put the link to that online module in the chat now. 

## Learn by doing

@teams_polls

--{{0}}--
We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using a fake patient database. There will also be some short quizzes to help solidify your understanding as we go.

--{{0}}--
With that being said, lets hop in!

## SQL: A Brief Refresher

**SQL** (**S**tructured **Q**uery **L**anguage) is a programming language that for more than four decades has been used to interact with **relational databases**.

A relational database is a data storage solution that stores data in tables, which are comprised of columns (also called 'fields') and rows.

--{{0}}--
First, let's quickly review some key concepts from the earlier sessions in this series. 
"Sequel", or "S-Q-L" (either pronunciation is fine) stands for Structured Query Language. SQL is a programming language used to interact with **relational databases**. 

--{{0}}--
Relational databases consist of many different data tables. The model of storing data across multiple tables rather than one MEGA-table is useful because it is more efficient, reduces data duplication, and makes correcting or updating data simpler and less error prone. Today we will only be working with data from **one** table at a time that is stored in such a relational database. To learn more about combining data from more than one table, be sure to catch our final presentation in the series on SQL Joins (dates on the final slide).

{{1}}
*****
<h4> What SQL is for: </h4>
isolating and combining just the data you're interested in, such as:

 * extracting columns you're interested in
 * filtering to just the data that meets specific criteria
*****

--{{1}}--
SQL is great at working with rectangular data, data that is stored in tables with rows and columns / fields.  Its powerful SELECT - FROM - WHERE syntax makes SQL an ideal tool for isolating just the data you care about, whether that's specifying the columns you're interested in or limiting your data to just those rows that meet certain conditions. 

{{2}}
*****
<h4> What SQL is **NOT** good for: </h4>

* fine tuned statistical, linguistic, or data visualization needs
*****
--{{2}}--
However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other tools like R or Python, which are better suited for work like statistical analysis.

## SQL Implementations

Some popular "flavors" of SQL:

* [**MySQL**](https://www.mysql.com/) (open source)
* [**SQLite**](https://www.sqlite.org) (open source)
* [**PostgreSQL**](https://www.postgresql.org/) (open source)
* [**Oracle**](https://www.oracle.com/database/technologies/appdev/sql.html) (proprietary)
* [**BigQuery**](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) (proprietary) This is the SQL flavor in Arcus Labs

--{{0}}--
Although all SQL implementations have a similar structure, and the same basic syntax, each different SQL database product often has its own minor variations in dialect.

--{{0}}--
Knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. Whenever you search for documentation online or are troubleshooting, you'll want to be sure to include the name of the "flavor" you're working with in your search terms. 

{{1}}
*****
<h3>Flavor of the Day: [**AlaSQL**](https://alasql.org/) </h3> 
*****

--{{1}}-- 
In the hands-on portion of this webinar, we'll be using "AlaSQL", which is a form of SQL that runs in your web browser as you look at these pages. We pre-populated some tables for you to experiment with in this presentation. These tables are filled with fabricated data meant to look a little like an electronic health record (EHR).  Rest assured that this data was completely invented, although it might look realistic!

## SQL Queries

A SQL **query** is essentially a question or request for data, written in a specific structure. 

--{{0}}--
Let's take a closer look at how to compose a SQL query!

{{1}}
*****
At a high level, we generally provide three pieces of information when constructing SQL queries:

 1. The name of the **table(s)** where the data is stored.
 2. The **column name(s)** you want to look at from the table(s) you specified.
 3. Any **filtering condition(s)** you want to apply to your data pull.  This part is optional but is often used.
*****

{{2}}
*****
```sql
SELECT _2_ FROM _1_ WHERE _3_;
```
*****

--{{2}}--
You put these basic pieces of information together using the syntax show here to create a SQL query. 

{{3}}
*****

For example, here are three different sample queries, each of which take place on just a single table.  

--{{3}}--
What do you think the **name of the table** is in the first example query?

<!-- data-readOnly="true" -->
```sql
SELECT price FROM products WHERE product_type = "FRUIT";

SELECT mpg, transmission_type FROM cars;

SELECT * FROM patients WHERE age < 20;
```
*****

--{{3}}--
To be extra clear, we end each query with a semicolon. This tells SQL you're done with a query.  
If you're working interactively with SQL, one query at a time, you can sometimes get away with not ending your query with a semicolon.  
Still, one of the things we're interested in doing in this webinar is instilling good practices from the start, so we encourage you to always end your queries with proper punctuation.

--{{3}}--
Similarly, while we write these queries all on a single line to show you a few examples in just a little space, that's the last time you'll see that kind of SQL in this webinar. 
On the next slide, we're going to get into some suggestions we have for you about SQL style.

### An Aside About Style
--{{0}}--
Style is how we choose to write SQL or other languages, within the confines of syntax. Style can be used to help humans read and write code more easily, closer to how they they read and write their natural languages.

{{1}}
*****
<!-- data-readOnly="true" -->
```sql
select price, best_by_date, sale_pct, quantity from products where product_type = "FRUIT";
```

<!-- data-readOnly="true" -->
```sql
SELECT price, best_by_date, sale_pct,
quantity from products WHERE
product_type = "FRUIT";
```

<!-- data-readOnly="true" -->
```sql
SELECT
  products.price
  ,products.best_by_date
  ,products.sale_pct
  ,products.quantity
FROM products
WHERE product_type = "FRUIT";
```
*****

--{{1}}--
All of the queries are on screen valid and would work perfectly fine. 
They also all return exactly the same resulting data. 
What distinguishes them is __style__.  

--{{1}}--
You may be working with a group that has an established SQL style guide.  
If so, ignore the style suggestions we offer and do what they suggest.  
Since style is intended to help humans read and write code more easily, it's a good idea to go along with what is already understood within your team. 
Everyone agreeing on conventions like when to start a new line and how and where to comment means it's easier for other people to help you with your code or for you to copy / paste from existing examples your peers share with you.

--{{1}}--
It might seem silly to start talking about style now with very short queries, but this is all about developing good habits from the start. 
That way, when you do start writing more complex queries, it's one fewer thing to worry about. 
We are going to advocate for some style conventions that not everyone will share. 
If you depart from our suggestions, that's fine -- just be sure to eventually develop your own standards for style! 
We promise, this will help you immensely once your SQL queries get to be 5, 10, or 100 lines long. 
These suggestions might not all make sense right now, but once you see them in actual queries, we think you'll understand them more intuitively.

{{2}}
*****
1) **Put keywords in CAPITAL LETTERS so they stand out.**  
*****

--{{2}}--
Examples of keywords are SELECT, LIKE, AS, WHERE, JOIN, DISTINCT, MEAN, ORDER BY, and many more. 
Making sure keywords consistently stand out helps you figure out where each part of your query is.  

{{3}}
*****
2) **Put members of a list on separate lines.**  
*****

--{{3}}--
This usually means the list of fields or columns you're requesting. 
Putting each item on its own line is easier on the eyes and allows for much easier cut-and-paste to rearrange things. 
It also means you have space after each item of the list to add a comment if necessary. 
We'll talk more about adding comments a little later.

{{4}}
*****
3) **Use indentation to clarify the various sections of your query.**  
*****

--{{4}}--
Indenting the list of columns below a SELECT statement is a way of subordinating those lines to the SELECT, subtly indicating that those lines are a continuation of the SELECT statement. 
A new line that isn't indented (say, a FROM statement) shows that the SELECT part of the query is over.

{{5}}
*****
4) **Use "dot notation"**
*****

--{{5}}--
We'll talk more about dot notation in the next section, but for now: 
Dot notation means adding more information about your data, for example, by including the table name the column comes from. 
This practice will prepare you for using multiple data sources in your queries. 
In the example above, we do this by specifying that each column that we're requesting comes from the products table. 
This one may make more sense as we go along. 

{{6}}
*****
5) **Use a comma-first style.**  
*****

--{{6}}--
In a list of length n, when using a comma-first style, you put the comma **before** items 2 through n rather than instead of putting the comma **after** items 1 through n-1. 
The first time I saw someone doing this, it totally threw me for a loop! 
However, once I learned the reason, I became a quick convert, as I realized it solves some of my biggest annoyances when working with lists! 
There are two key reasons I prefer this approach over the more conventional style:

--{{6}}--
(1) the commas all line up -- this makes it much easier to identify at a quick glance if you've forgotten a comma -- a common source of errors when running code that involves lists!

--{{6}}--
(2) Relatedly, this it also makes it much easier to re-order a list or remove items entirely. 
In SQL we often try a short query with just a few fields, then add a few more, then maybe rearrange their order, and finally delete the fields we realize we don't need. 
Usually, the first item in a list of columns is something of central importance, like id_number, while the others in the list have a higher likelihood to be ones you may decide you don't need, or will change the order of. 
Because you rarely touch the first item in a list but more frequently change the last item, using a comma-first paradigm means it's less likely that you'll introduce a missing (or extra) commas as compared to the comma-last style. 
This also prevents you from accidentally winding up with a comma after the final item on your list -- another common issue or error!

--{{6}}--
Now that we've got you thinking about style, let's move on to the substance of SQL and work with SELECT and FROM.

### SELECT and FROM

**SELECT statement:** specifies which columns to return as output.

--{{0}}--
A **SELECT statement:** is used to specify which columns (or fields, we use both terms interchangeably here) you would like to have returned as output from your SQL query.

{{1}}
Keywords `SELECT` and `FROM`

--{{1}}--
The basic components of a select statement are the `SELECT` and `FROM` keywords. 
The `FROM` keyword is used to specify the table or tables that hold the data you're interested in, and the `SELECT` keyword is used to provide a list of columns within that table that you would like returned as output.  

*****
```sql
SELECT *
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable7a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable7a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients
@AlaSQL.buildTable_allergies

</div>

*****

--{{1}}--
The asterisk is the "wildcard" character in SQL. When used alone, it indicates that you want to match **everything**. So in this case, you're asking SQL to select **all** of the fields from the patients table. 

--{{2}}--
Taking a look at the `FROM` line of this query, you may notice that the table name is written as two words separated by a period. This is the "dot notation" that we alluded to earlier. Dot notation generally looks something like `dataset_name.table_name.column_name`

{{2}}
Dot notation: `dataset_name.table_name.column_name`

--{{2}}-- 
In our sample query here, the first word in dot notation after the FROM keyword is alasql, which is the name of the **schema**, **catalog**, or **dataset** that the data is stored in (terms vary according to which flavor of SQL you're using). 
The second word, "patients" is the name of the specific table within that dataset that we're hoping to query. 

--{{2}}--
Alright, lets run our first SQL query of the day! Hit the execute button, which is the right-facing triangle in the small circle below the SQL code.  

--{{2}}--
In our output, we have a variety of columns, such as id, birth date, death date, first and last name, and more. If we couldn't already tell before from just the name "patients", its clear now that this is a table that contains important demographic information for patients in this fake Electronic Health Record. 

--{{2}}--
Let's move on now to our first exercise!


### 💫 **Your Turn 1** 
--{{0}}--
Using the code template we've provided here, complete the code to get all the fields from the table `alasql.allergies`.  It might help to hide the query results from the query above, by clicking beside "Results of Query."  That way you can see the SQL query we used, and model your code on the query above! When you think you have it, try running the query to see if you get it right. 

{{0}}
*****
Select all of the fields from the `alasql.allergies` table

```sql
SELECT
FROM  ;
```
@AlaSQL.eval("#dataTable7b")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable7b" border="1"></table>

</details><br/><br/>
<div style = "display:none;">

@AlaSQL.buildTable_patients
@AlaSQL.buildTable_allergies

</div>
*****

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal answer once you're done!*</summary>

Try:

```sql
SELECT * 
FROM alasql.allergies;
```

</details>

--{{0}}--
To get this data, we're going to want to write out SELECT * FROM alasql.allergies; When you run the query, you should see a table with five columns: start, stop, patient, encounter, and description. Note that while you would also get these same results if you just wrote FROM allergies instead of alasql.allergies, for the reasons we discussed before, we suggest writing the table name out using dot notation, so as to also include the dataset/schema name. 

--{{0}}-- 
So we've practiced requesting all of the columns of a table, but what if we only want a few of them? 

#### Selecting Specific Columns

--{{0}}--
In order to return only a specific few of the columns, you need to write a comma-separated list of the columns you want after the `SELECT` keyword. 

```sql
SELECT
  patients.id
  ,patients.sex
  ,patients.race
  ,patients.ethnicity
  ,patients.state
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable7c")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable7c" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{0}}--
Note that this time, we're also using dot notation for our columns, in the form of `table_name.column_name`. We do this to be very explicit about which data we mean.  

--{{0}}--
Now, it might seem a bit redundant in this example to list our columns this way since we're only querying one table. This is another example of forming good habits early, because eventually (though not in today's webinar) you will need to do queries that involve multiple tables. Sometimes, these tables may have identical column names. SQL won't automatically know if you're asking for `date` in `encounters` table, or `date` in `medication_administration` table. In that case, you are **required** to specify which table you're referring to in order to disambiguate. 

--{{0}}--
Rather than learn dot notation later, we want to introduce you to it now, even if it feels unnecessary. That way, when you do get to the point of querying multiple tables, it will already feel natural to you, and you can focus all your brain power on learning the other, trickier aspects of mastering queries of multiple tables at once.

--{{0}}--
Go ahead and run this code by clicking the execute button.  How are your results different from the `SELECT *` query you ran previously? 

--{{0}}--
Just as we would hope, this time we haven't received the entire patients table, like we saw on the page before, but instead can only see the five columns we requested. 

### DISTINCT
{{0}}
*****
`DISTINCT`: limits result set to only unique row values. 

  * is placed directly after the `SELECT` keyword
*****

--{{0}}--
The `DISTINCT` clause in **SQL** can be placed directly after the `SELECT` key word, and can be used to limit your result set to only the unique row values.  

--{{0}}--
This can be especially useful when exploring a table for the first time and trying to become familiar with the data in each column.  

--{{1}}--
For example, perhaps you want to see all the possible values for `sex` or `race` in the `patients` table, to understand a bit more about the data collection options.  If you were to use `SELECT` by itself to get just the `race` field from the `patients` table, you'd get the race of every patient, with lots of repeats.  Using `SELECT DISTINCT` instead, you get a much shorter list of every possible value for `race`, each listed just once.

--{{1}}--
As you can see in this example, `SELECT DISTINCT` can also be used on more than one field.  The code block below provides an example of using this syntax to investigate the unique combinations of values from the `sex` and `ethnicity` columns from the `patient` table. Go ahead and execute this code to see the results.  

--{{1}}--
We can see here that there are four different combinations of sex and ethnicity. Note, though, that `SELECT DISTINCT ` only shows you the combinations that actually exist in the table, rather than all of the combinations that could possibly exist. So, for example, if there were no female nonhispanic patients in this table, our result would have only been three rows long.

{{1}}
*****
```sql
SELECT DISTINCT
  patients.sex
  ,patients.ethnicity
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable8a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable8a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****

### 💫 **Your Turn 2** 

In the code block below, write a query that will return the unique combinations of `county` and `state` from the `patients` table. How many unique combinations do you get?

```sql
SELECT ... 
```
@AlaSQL.eval("#dataTable9a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable9a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{0}}--
Use what we've just learned to write a query that returns all of the unique combinations of `county` and `state` from the `patients` table. How many different combinations do you find? 

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal answer once you're done!*</summary>

```sql
SELECT DISTINCT
	patients.county
	,patients.state
FROM alasql.patients;
```

</details>

### Adding Comments

**Comments**: helpful bits of text or documentation added to your code for the benefit of future you or other people who look at your code

__ Can be **single-line**__: using `--` as a delimiter

or **multi-line** : using `/*` and `*/`

--{{0}}--
**Comments** are explanatory or helpful bits of text that you can add to your code as documentation for yourself or other reviewers of your code.  Similarly to style choices, comments don't actually affect the execution of the SQL code in any way and are simply there for humans.

--{{0}}-- 
In **SQL** there are 2 different techniques that can be used for adding comments. First, there's single line comments. 

--{{0}}--
Single-line comments are created by typing 2 minus signs in a row. Then, anything that appears to the right that delimiter will be treated as comment text.

--{{0}}--
And there's also multi-line comments. These are started by adding the `/*` characters at the beginning of your comment, and `*/` characters at the very end of your comment.

{{1}}
*****
```sql
/* This is a simple demographics query*/
SELECT
  patients.id         --unique patient identifier.
  ,patients.sex       --patient sex {'M', 'F'}
  ,patients.race      --patient race
  ,patients.ethnicity --patient ethnicity {'hispanic', 'nonhispanic'}
  ,patients.state     --full name of patients state of residence.
FROM alasql.patients;


/*
    Aren't Comments Great!
*/
```
@AlaSQL.eval("#dataTable10a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable10a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>
*****
--{{1}}--
Here's an example that uses both! By having the code commented, it's much easier for Future You to remember exactly what this query does without having to do any extra work, or for someone who _isn't you_ to figure out what's going on!  

### WHERE

`WHERE`: Optional keyword for filtering your output. 

--{{0}}--

The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.

--{{0}}-- 
As an example, here's how you'd filter the output to only include records for a specific county

{{1}}
*****
```sql
SELECT *
FROM alasql.patients
WHERE
	patients.county = "Suffolk County";
```
@AlaSQL.eval("#dataTable11a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable11a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>
*****

--{{1}}--
Although this example shows only one constraint, the WHERE clause can contain any number of filtering arguments needed.

{{2}}
*****
```sql
SELECT *
FROM alasql.patients
WHERE 
	( -- looking just in Suffolk or Barnstable counties
		patients.county = "Suffolk County"
		OR patients.county = "Barnstable County"
	)
	AND
	( -- patients who are hispanic or non-white
	  patients.ethnicity = "hispanic"
	  OR patients.race != "white"
	);
```
@AlaSQL.eval("#dataTable11b")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable11b" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>
*****

--{{2}}--
This example includes multiple constraints, and makes use of both **comparison** operators like equals `=` and `<=` less than or equal to, and **logical** operators including `AND` and `OR`.  

--{{2}}-- 
Helpfully, this query has some comments added in! Since the queries are getting a bit more complex, it's worth trying to describe this query to yourself in plain English (or another natural language). Take a moment and work through this query in your head, and see if you can figure out what it's saying. 

--{{2}}--
So, you may have figured out that this query is limiting the data to only patients in Suffolk or Barnstable counties who are either hispanic or race other than white. Let's run it just to be sure.

--{{2}}--
As you can see, we receive just four rows back -- each of which are from either Barnstable or Suffolk county, and are for patients that are either hispanic or non-white.  

--{{2}}--
You may have also noticed that there are some parentheses in this query. There are parentheses surrounding the county-related bits of logic and the race and ethnicity bits of logic. This is because it's easy to make a logical order-of-operations mistake when you mix both `AND` and `OR`. That's why it's crucial to include parentheses to show the scope of your `AND` and `OR` logical operators.

--{{2}}--
To see this in action, let's remove the second set of parentheses, around the `race` and `ethnicity` comparisons, and re-run the query.  What happens?  Why?  

--{{2}}--
Now, our resulting table is much longer, and includes rows where the patient is from a county other than Barnstable or Suffolk, as long as they are not white, which satisfies the final "OR" condition. 

--{{2}}--
Ready to try your luck at a complex WHERE statement? Let's move on to our third exercise!
 
### 💫 **Your Turn 3** 

--{{0}}--
Get every field from `patients` for all male patients who were born on or after January 1, 2001. Remember, you can write the query iteratively. So if you're not  sure about the field name that holds sex, or whether male is coded "Male" (with a capital M), "male" (with a lowercase m), "M", or some other way?  Look at the results of other queries to get this information! 

Return every field from `patients` for all male patients who were born on or after January 1, 2001. 

```sql
SELECT
FROM
WHERE

```
@AlaSQL.eval("#dataTable11c")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable11c" border="1"></table>

</details><br/><br/>
<div style = "display:none;">
@AlaSQL.buildTable_patients
</div>

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal answer once you're done!*</summary>

```sql
SELECT *
FROM alasql.patients
WHERE 
	patients.birthdate >= "2001-01-01" AND
	patients.sex = "M";
```
</details>

### Null Values

**Null:** concept used to represent "blank" values

--{{0}}--
Like many programming languages, **SQL** deals with "blank" values in a very specific way.
**SQL** uses the concept of **null** to represent "blank" row values.

{{1}}
`IS NULL` and `IS NOT NULL`: operators used to filter based on null values

--{{1}}--
When you need to filter on null values you'll use the `IS NULL` or `IS NOT NULL` operators.

--{{1}}--
Let's imagine we want to see rows from the `allergies` table where the `stop` value (the date at which the presumed allergy was considered no longer applicable, resolved, a mistake, or not an allergy) isn't missing.  In other words, the allergy has a date at which it was ruled to not exist.

{{2}}
*****
```sql
SELECT *
FROM alasql.allergies
WHERE
    allergies.stop IS NOT NULL; -- there is some value here, it's not empty
```
@AlaSQL.eval("#dataTable12a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable12a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_allergies

</div>
*****

--{{2}}--
As you can see in our example, you achieve this by using the keywords `IS NOT NULL`. Take careful note that we are _not_ filtering null values by using the inequality operator. 

--{{2}}--
In fact, you _can't_ filter null values using equality or inequality operators. That's why the `IS` and `IS NOT` key words exist. That's because, in a more esoteric sense, null values are inherently unknowable, and therefore we can't assess whether it is equal to anything. Similarly, you can't do math with a null value. 

### NULL and Comparisons
--{{0}}--
Let's think about this in the context of the `stop` column in the `allergies` table. 

{{0}}
*****
```sql
SELECT *
FROM alasql.allergies
WHERE
    allergies.stop < '2020-03-01';
```
@AlaSQL.eval("#dataTable12b")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable12b" border="1"></table>

</details>

<br/>
<br/>

<div style = "display:none;">

@AlaSQL.buildTable_allergies

</div>
*****

--{{0}}--
Here, we're asking SQL to give us all of the columns in the allergies table where the stop date is less than March 1, 2020. 

--{{0}}--
When this code is run, each row's `stop` value will be assessed against our `where` statement. Let's think through all of the possible categories that these values could fall into. 

{{1}}
1. A date less than (before) March 1, 2020,
2. A date equal to March 1, 2020,
3. A date greater than (after) March 1, 2020,
4. No date at all (null)

--{{1}}--
The `stop` value could be a date less than (or earlier to) March 1, 2020. 
It could be a date that is equal to March 1, 2020. 
It could be a date greater than (or after) March 1, 2020. 
Or, the value could be blank, with no date listed at all -- in other words, it could be `null`. 

--{{1}}--
Given what you've learned so far about WHERE statements, filtering, and `NULL` values, which category or categories do you think the returned data will fall into? 

--{{1}}--
Let's run the code now and see what the results are! The only rows returned are those with a date earlier than March 1, 2020. Dates equal to or later than that date are not included, of course, because they are in obvious violation of the WHERE clause filter. Rows that do not have a date (ie, NULL values) are not returned, because they cannot be evaluated with the comparison operator. 

--{{1}}-- 
The fact that nulls aren't included in comparisons is a very subtle distinction that can drastically alter the output of your SQL statements.  This can be very important when writing inclusion and exclusion logic and thinking about what cases belong in your data set.  Always keep in mind that you might have missing values, and consider what that might mean for your selection of rows.  

--{{1}}--
Now, perhaps we're interested in running an analysis only on allergies that are current, that is, they do not have a `stop` date. And perhaps we're aware that allergies with a date prior to March 1, 2020 have some possible data quality issues, and should be manually checked to see if they are actually current allergies that had a stop date entered by mistake. 

--{{1}}--
In that case, we would want to return a mix of both null and non-null values. In order to achieve this, we'd need to combine what we already know about comparison operators and null values, along with our previously learned lessons about **logical** operators. 

{{2}}
*****
```sql
SELECT *
FROM alasql.allergies
WHERE
    (
        allergies.stop < '2020-03-01'
        OR allergies.stop IS NULL
    );
```
@AlaSQL.eval("#dataTable12c")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable12c" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_allergies

</div>
*****

--{{2}}--
By combining a date comparison along with the `IS NULL` operator using the `OR` keyword, we create a WHERE statement that returns any rows that either have no stop date, or have a stop date prior to March 1, 2020. 

### ORDER BY Statement

`ORDER BY`: orders the result set by one or more columns. 

--{{0}}--
Another useful piece of SQL syntax for exploring data is the `ORDER BY` statement, which (as its name suggests) is used to order your result set by a given set of one or more columns.

--{{0}}--
When listing columns in the `ORDER BY` statement you can specify that they be sorted in either ascending (`ASC`) or descending (`DESC`) order. By default, all items in the `ORDER BY` clause will be sorted in `ASC` (ascending) order if no explicit ordering direction is provided.

--{{0}}--
If you list more than one column in `ORDER BY`, items will be sorted first by the first column you provide, and then, within "ties", by the second, then third, etc., column.  

{{1}}
*****
```sql
SELECT DISTINCT
  patients.county
  ,patients.ethnicity
FROM alasql.patients
ORDER BY
  patients.county ASC
  ,patients.ethnicity DESC;
```
@AlaSQL.eval("#dataTable14a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable14a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****

--{{1}}--
For instance, this code sorts first by `county`, and then within each possible value of `county` sorts by `ethnicity`. Let's run it and take a look at the output. 

### LIMIT

`LIMIT`: sets a maximum number of rows to be returned. 

--{{0}}--
The `LIMIT` clause can be used to limit the result set of your select statement to a maximum number of rows.

{{1}}
```sql
SELECT *
FROM alasql.patients
LIMIT 3;
```
@AlaSQL.eval("#dataTable15a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable15a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{1}}--
This is achieved by adding the word `LIMIT` as the last line of your query, followed by the number of rows you would like your result set truncated at. This really useful when initially exploring tables you are unfamiliar with.  Showing just the first three or five or ten rows of a table can give you a quick intuitive grasp of the contents of the whole table and will come back very quickly.  Without a `LIMIT`, large tables can take a long time to return all their results.

--{{1}}--
This example returns all columns from the `patients` table, and limits the result set to only 3 rows.

### Aliasing with AS

`AS`: used to alias (rename) tables or columns

--{{0}}--
In SQL, it is possible to assign a custom name (usually a kind of shortened name) to a table or column in your query using a technique called **aliasing**.

{{1}}
* Aliasing **tables** is especially helpful for long or complex queries involving many tables

--{{1}}--
Aliasing **tables** can be helpful for long or complex queries involving multiple tables because it allows you to avoid typing out the full name of a table each time you refer to it.  

{{2}}
*****
* EX: 

  * shortening `patients` table to `pt`

  * `encounters` table to `enc`

  * `diagnosis` to `dx`
*****

--{{2}}--
For example, in a long query involving the `patients` table, the `encounters` table, and the `diagnosis` table, you might prefer to use the shorthand terms `pt`, `enc`, and `dx` or even `p`, `e`, and `d`.

{{3}}
* Aliasing **columns** is especially helpful for querying data with confusingly named columns, or for columns that exist in multiple tables.

--{{3}}--
Aliasing **columns** can be helpful by assigning clearer, more comprehensible names for a given column than the name that might be assigned to it in the database.  

{{4}}
* EX: `allergies.stop` as `ruled_out_date`

--{{4}}--
For example, you might want to see the results from the `stop` column in the `allergies` table returned to you not as `stop`, but rather as `ruled_out_date`.

{{5}}
*****
```sql
SELECT
  p.id AS unique_patient_id
  ,p.sex
  ,p.race
  ,p.ethnicity
  ,p.state AS state_name
FROM alasql.patients AS p;
```
@AlaSQL.eval("#dataTable16a")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable16a" border="1"></table>

</details><br/><br/>

<div style = "display:none;">
@AlaSQL.buildTable_patients
</div>
*****

--{{5}}--
Aliases are assigned by placing the `AS` key word directly after the item (table/column) you would like to alias, followed by the name you would like to assign as its **alias**.

--{{5}}--
In this example, we can see aliasing being used to rename the `patient` table to `p`, and renaming the `id` column to `unique_patient_id` (because there are other id fields you're working with elsewhere) and the `state` coluumn to `state_name` (because you want to point out that this isn't the state abbreviation).

### 💫 **Your Turn 4 ** 

Write a query that accomplishes the following: 

* Retrieves the patient identifier, sex, ethnicity, state, and zip
* Aliases the `patients` table as `pt`
* Aliases the `sex` field as `sex_assigned_at_birth`
* Aliases `zip` as `postal_code`
* Orders the result by zip/postal code

```sql


```
@AlaSQL.eval("#dataTable16b")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable16b" border="1"></table>

</details><br/><br/>

<div style = "display:none;">
@AlaSQL.buildTable_patients
</div>

--{{0}}--
If you're feeling unsure of where to start, consider starting with a simple query (something like a `SELECT * ...`) and gradually changing it so that you knock out one bullet point at a time! 

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal answer once you're done!*</summary>

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

--{{0}}--
We start off with a SELECT statement, followed by our list of columns, each of which is on a new line. Although the FROM line doesn't come until after this, it's okay to use the table alias when we list our columns, even though it looks like we haven't told SQL about the table name yet! 
As we go, we alias the sex and zip columns.

--{{0}}--
Then, we have our FROM statement, where we specify the table that we're querying, and the alias that we want to use for it. 
Finally, we order our results by the (aliased) postal code field!

</details>

## Recap

--{{0}}--
Today, you learned about the language "sequel" or S-Q-L, which is an acronym for "Structured Query Language", a powerful tool for retrieving data from relational databases. 

We covered a variety of important functions, represented in SQL by **keywords**. 
In particular, we covered: 

* `SELECT`: used to indicate which fields (columns) you want to retrieve
* `FROM`: used to indicate which table you want to retrieve data from
* `DISTINCT`: used to ask for only a single example of each possible unique value
* `WHERE`: used to give a condition which filters the data retrieved
* `IS NULL`: used to compare a value to *NULL* (an empty/missing value)
* `IS NOT NULL`: used to compare a value to not *NULL* (a value that is not missing and not empty)
* `ORDER BY`: used to display results organized by the values in one or more columns
* `LIMIT`: used to truncate (cut off) the number of result rows retrieved at a given number
* `AS`: used to alias (rename) columns or tables

--{{0}}--
We also learned about comparison operators, comments, and style -- how to write code in a specific way that promotes reusability and readability.

--{{0}}--
You also got to practice hands on, which probably meant you got to see some error messages, too, which is helpful experience.

## Additional Resources

* Khan Academy's [Introduction to SQL](https://www.khanacademy.org/computing/computer-programming/sql) is high quality and easy to learn from.

* Tutorials Point has some helpful documentation you may want to check out to read more [about the basic types of **operators** available for use in a SQL query](https://www.tutorialspoint.com/sql/sql-operators.htm).

* Give the [SQL Murder Mystery](https://mystery.knightlab.com/) a try. Note that some of the content is more advanced than what we cover here, but there is a walkthrough, and you can always stop once you've reached the limits of what we've learned so far. 

* Select Star SQL is a [free interactive book that teaches SQL](https://selectstarsql.com/) by exploring Texas state execution data. The first chapter mostly covers topics we learned about today, while the remaining chapters begin to dig deeper.

## Upcoming sessions

Want to see the materials from an earlier session? 
Everything is available on the [Arcus SQL Skill Series website](https://arcus.github.io/arcus_skill_series_sql/). 

@colorhighlight(SQL Intermediate Level)

Learn about intermediate SQL queries with keywords like CASE, LIKE, and GROUP BY. We'll work on single tables, using code, hands-on.

- [**November 18, 2024 at 12 pm** sign up link](https://events.teams.microsoft.com/event/3846b911-ba5b-42d4-be4b-5ba6a85c181a@a6112416-07b0-41a5-9bb1-d146b575c975)
- [**December 3, 2024 at 4 pm** sign up link](https://events.teams.microsoft.com/event/a017dd51-d1c9-4378-9b2a-42e437673f25@a6112416-07b0-41a5-9bb1-d146b575c975) 

@colorhighlight(SQL Joins)

Work with multiple tables and learn about SQL joins: learn what they accomplish and how to write them.

- [**December 9, 2024 at 12 pm** sign up link](https://events.teams.microsoft.com/event/2ab870fa-cb27-49d0-a903-a7d42932caa2@a6112416-07b0-41a5-9bb1-d146b575c975)
- [**December 17, 2024 at 4 pm** sign up link](https://events.teams.microsoft.com/event/c4d671df-292b-4562-af1d-bcbc49381081@a6112416-07b0-41a5-9bb1-d146b575c975)

## Arcus On-Ramp

@onramp_slide

--{{0}}--
We offer three different Arcus On-Ramp workshops, each focused on a different aspect of doing research in Arcus. 
We offer these on a regular, rotating basis all year.

--{{0}}--
The Arcus On-Ramp workshops are different from these skill series workshops in two big ways: First, although the Arcus On-Ramp workshops use tools like SQL, R, and Python, the focus is on how to work in an Arcus Lab, not learning those languages per se. 
And secondly, because the On-Ramp workshops use real patient data, unlike today's workshop, you need to have completed CITI training and attested the Arcus terms of use before you can sign up.

--{{0}}--
If you're feeling like you'd like a realistic, worked example of how SQL might be used in an Arcus Lab to answer a research question, then the Arcus On-Ramp is for you!

## 💫 One last poll!

--{{0}}--
I have one final poll for you.
Note that this poll has two questions, so after you answer the first one you'll need to click the little arrow at the bottom right to go to the second question.
Your time is a non-renewable resource, and it's very important to us that we use your time wisely. 
Data we collect like this are really important in shaping what kinds of education we offer, so thank you so much for taking a moment to provide feedback!

--{{0}}--
I'll also turn off the recording now and answer any questions you may have.

## About these slides

@about_these_slides
