<!--
author:   Rose Hartman
email:    hartmanr1@chop.edu
version: 1.2.0
current_version_description: Updated for FY25 session (dates, and added Arcus On-Ramp slide)
docs_version: 3.0.0
module_type: slides
language: en
narrator: US English Male
mode: Presentation
classroom: enable
@onload: window.LIA.settings.sound = false

title: Demystifying SQL
comment:  SQL is a relational database solution that has been around for decades.  Learn more about this technology at a high level, without having to write code.
long_description: Do you have colleagues who use SQL or refer to "databases" or "the data warehouse" and you're not sure what it all means?  This module will give you some very high level explanations to help you understand what SQL is and some basic concepts for working with it.  There is no code or hands-on application in this module, so it's appropriate for people who have zero experience and want an overview of SQL.
estimated_time_in_minutes: 40
@pre_reqs

Experience working with rectangular data (data in rows and columns) will be helpful.  For example, experience working in Excel, Google Sheets, or other software that helps organize data into rows and columns is sufficient expertise to take this module.

@end

@learning_objectives  
After completion of this module, learners will be able to:

- Define the acronym "SQL"
- Explain the basic organization of data in relational databases
- Explain what "relational" means in the phrase "relational database"
- Give an example of what kinds of tasks SQL is ideal for
@end

good_first_module: true
coding_required: false
@sets_you_up_for

- database_normalization
- sql_basics

@end
sequence_name: sql

@depends_on_knowledge_available_in

@end
@version_history
[1.0.0](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/fb522e46ad7ca27304c730966c33eed7fe8e0a6a/demystifying_sql/demystifying_sql.md#1): Version given Nov 2023.
@end

repo_link: [GitHub repository for these materials](https://github.com/arcus/arcus_skill_series_sql)
module_link: [an online self-paced tutorial](https://bit.ly/DART_demystifying_sql)

import: https://raw.githubusercontent.com/arcus/education_modules/main/_module_templates/macros.md
import: https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/macros_slides.md
-->

# Demystifying SQL

@sql_series_slide

--{{0}}--
Welcome! 
I'm Rose Hartman, and I use she/her pronouns. 
I'm a data science educator with the Arcus project in DBHi. 
Today's talk is the first in a series of talks about SQL we'll be offering this year. 
We'll be recording today, so please leave your cameras and mics turned off until the question time at the end.
If you have questions that come up during the talk, feel free to put them in the chat. 
Okay, let's get started!

## Today's talk 

@todays_talk

--{{0}}--
Today will be about providing a high level overview of SQL -- what it is, what it's good for, why you might want to learn it. 
We won't be doing any hands-on coding with SQL today, although we will during some of the future sessions in this series.

--{{0}}--
And I just want to mention that although we have an hour booked for today's workshop, we probably won't need all of that time. 
The later workshops in this series will take the whole hour, but today's is a little lighter. 
So we can use the extra time at the end for questions, or of course you can feel free to drop off and take a little time back.

## Thank you!

<div class = "gratitude">
<b style="color: rgb(var(--color-highlight));">Thank you!</b><br>

Material for this talk is based closely on the DART module [Demystifying SQL](https://bit.ly/DART_demystifying_sql), written by Peter Camacho and Joy Payton.

</div>

--{{0}}--
Many thanks to Peter and Joy for their work developing this excellent content!
And, of course, any errors or awkwardness in this version are mine.

## Learn by doing

@teams_polls

--{{0}}--
We're firm believers that the best way to learn is to practice!
We won't have any hands-on coding practice today, but we will have short quizzes that come up to help you check your understanding and consolidate learning. 
Okay, let's dive in.

## What is SQL?

**S**tructured **Q**uery **L**anguage

--{{0}}--
You can pronounce it as "sequel" or just say the letters S-Q-L.

{{1}}
**SQL** is a programming language used to interact with "**Relational Databases**".  

{{2}}
So, what is a **relational database**?

--{{2}}--
Let's start with the word "**database**".  A database is a data storage solution that stores data in objects called tables.  Tables are objects comprised of columns (sometimes called 'fields') and rows (similar to data in an Excel spreadsheet or .csv file).
When we add the word "**relational**" as a modifier, we mean that tables within the database are **related** to one another by columns they have in common (like a patient id column that appears in several different tables). 
Usually, with a relational database, you will use several tables to answer a single question, and use information from one table to look up information in the next, like a series of clues.
Let's dig into this idea a little further by looking at an example.

### Relational Database Example

--{{0}}--
Consider, for example, this small relational database with three tables: `demographics`, `encounters`, and `medication_order`.  
The tables are rectangular (or tabular) in shape and organize data in rows and columns.  
Take a look at these tables now and see if you can identify the column they have in common.  
In this case, `patient_id` is the column that links these three tables together.

--{{0}}--
Let's consider an example, and walk through how we might use this small relational database.
Let's say you wanted to figure out how many times Prairie Dawn had an encounter in the Emergency Department.
How would you go about that?

--{{0}}-- 
Well, information about whether or not each encounter was in the Emergency Department is stored in the `encounters` table (`ed_ind` equal to 1).
But when you look in that table, you won't see the patient name "Prairie Dawn" anywhere.

--{{0}}-- 
First, we need to find the patient Prairie Dawn in our `demographics` table, and note that this patient has a patient_id of SMLE321.  
We can then use this patient ID to find **related** data in other tables.  
Now, when we look in the `encounters` table, even though we don't see her name, we **do** find her ID, SMLE321.  
So now we can see that she's had three encounters, and two of them were in the Emergency Department. 

<h4>A `demographics` table</h4>

<!-- data-type="none" -->
| patient\_id | date\_of\_birth | sex | last\_name | first\_name |
| -------    | -----------   | -   | ------    | ----- |
| ABC123     | 1970-03-15    | M   | Bird      | Big |
| TRSH789    | 1985-08-20    | M   | the Grouch | Oscar |
| SMLE321    | 1990-12-12    | F   | Dawn      | Prairie |

<h4>An `encounters` table</h4>

<!-- data-type="none" -->
| patient\_id | encounter\_id | encounter\_date | ed\_ind |
| ---------- | ------------ | -------------- | ------ |
| SMLE321    | 8827371048   |  2020-03-10    | 1      |
| SMLE321    | 8829502289   |  2020-09-05    | 0      |
| TRSH789    | 8837498101   |  2020-11-29    | 0      |
| TRSH789    | 8871386401   |  2021-04-01    | 0      |
| SMLE321    | 8901861569   |  2021-11-22    | 1      |
| ABC123     | 8927551899   |  2021-12-30    | 0      |
| ABC123     | 8954998113   |  2022-03-19    | 1      |


<h4>A `medication_order` table</h4>

<!-- data-type="none" -->
| patient\_id | provider\_id | med\_id | order\_date |
| -------    | -----------   | --- | ------    | ----- |
| ABC123     | 491272    | 8000412   | 2021-05-15 |  
| ABC123     | 491272  | 7960004   | 2022-02-01 |
| SMLE321    | 223618    | 8000412 | 2020-08-19 |

### Relational Databases

<div class = "important">
<b style="color: rgb(var(--color-highlight));">Key Idea</b><br>

Relational databases work by using data fields like IDs to allow us to find out data about a patient, or encounter, or purchase order, or other thing we're interested in, by following the matching ID into other, **related** tables.

</div>

--{{0}}--
The primary benefit of the **relational database** model is the ability to use columns containing the same data (things like patient IDs) to create complex reports combining information from multiple tables.  
This enables users of the data to derive specific information from the data in highly customizable ways.

--{{0}}--
Now that you have that background, you can think of SQL as the computer code (the "Language" in Structured Query Language) that you can use to ask explicit questions (called "queries") about the information in your relational database.

### A Little Background

<div class = "history">
<b style="color: rgb(var(--color-highlight));">Historical context</b><br>

Where did SQL come from?  SQL was created in the early 1970's by IBM as a method for more easily accessing information from their internal database system.

By 1979, Relational Software Inc. (now Oracle Corporation) released the first commercially available implementation of SQL as a part of their Oracle V2 database application.

Today SQL is the most common programming language for extracting and organizing data in relational database systems.

</div>

--{{0}}--
So SQL is not only very commonly used, it's also very well-established. SQL has been around much longer than other programming languages you may have worked with. 

### 💫 Your turn! SQL

What does "SQL" stand for?

[[Structured Query Language]]
<script>
  let input = "@input".trim().toLowerCase();
  input == "structured query language";
</script>

--{{0}}--
SQL, which can be pronounced "sequel" or S-Q-L, stands for Structured Query Language!

### 💫 Your turn! Relational Databases

Which of these correctly describe relational databases?  Choose all the correct options.

[[ ]] **A.** Relational databases are an alternative to SQL
[[X]] **B.** Relational databases organize data into tables
[[ ]] **C.** Tables in relational databases are organized into ranks and files
[[X]] **D.** Relational databases permit the extraction of highly specific data
[[X]] **E.** The "relational" in "relational database" refers to data that occurs in multiple places and allows for linking, or "relating" data
*********

<div class = "answer">

Relational databases are a data storage solution and they store data in tables, which are in turn organized into rows and columns.  
Relational databases use SQL as a way to access data, search for data meeting particular conditions, and connect related data, using columns that tables have in common.  
This allows for extracting data in very specific and customized ways.

</div>

***********

### When to Use SQL

SQL should be used any time you need to access data stored within a relational database and select data that meets your requirements.

--{{0}}--
Usually, SQL is used for getting custom datasets for export and downstream analysis.  
For example, you might use SQL to export data for doing statistical analysis and visualization in other languages like R, Python, or Stata.

--{{0}}--
If your source data comes from a relational database (like a data warehouse), your major data transformations (like selecting just the columns you care about or selecting only certain rows) should be done using SQL. 
This ensures that the dataset you export from the relational database is pretty close to the final data you will analyze or visualize.

--{{1}}--
This is because, especially for large datasets, SQL is a much more efficient tool for large-scale data transformations than your traditional scripting or analytic packages.

{{1}}
*****
<div class = "important">
<b style="color: rgb(var(--color-highlight));">Key Idea</b><br>

SQL is a much more efficient tool for large-scale data transformations than your traditional scripting or analytic packages. 

Use SQL to get close to the final data you'll want to analyze, then export it. 

</div>
*****

--{{1}}--
If you think about carving a sculpture out of stone or wood, you can imagine that the rough work of getting rid of big slabs of material that aren't needed can be done with powerful instruments like chainsaws or jackhammers.  
Then, when an artist gets close to the shape of the final product, they might switch to smaller tools to give the sculpture its final form.  
In this analogy, SQL is the heavy duty tool that gets your data close to its final form.

### Save your queries

<div class = "important">
<b style="color: rgb(var(--color-highlight));">Key Idea</b><br>

It's a good idea to document your SQL queries and save them, because this allows you to show your steps and give data provenance.  

This helps with reproducibility and standardization of your work, and might help provide a place to start for future projects.

</div>

### When SQL Isn't the Right Tool

--{{0}}--
Although SQL is a great tool for organizing your data into meaningful datasets for extraction, it is usually not a great tool to use for your actual analysis work.

SQL is the wrong choice for:

- any text analysis beyond very basic parsing
- statistical analysis
- data visualization

--{{0}}--
Despite having many functions for simple text parsing, SQL is not the tool/language you want to use for advanced NLP (Natural Language Processing) work.  
Similarly, SQL has some basic statistical functions, but isn't intended to provide statistical analysis at the level of a statistical programming language like R.
SQL also doesn't have any capabilities to directly support data visualization work.

--{{0}}--
For all of these "downstream analytics" use cases, you will want to use an actual analytical programming language or tool like R or Python.

{{1}}
*****
<div class = "important">
<b style="color: rgb(var(--color-highlight));">Key Idea</b><br>

Don't use SQL for actual analysis work. 
Switch to a tool like R, Python, or Stata.

</div>
*****

### SQL Implementations

--{{0}}--
Although all SQL implementations have a similar structure, and the same basic syntax, each different SQL database product often has its own minor variations in dialect.

--{{0}}--
Colloquially people often refer to the different SQL dialects as different "flavors" of SQL.

{{1}}
*****
Some popular "flavors" of SQL:

* [**MySQL**](https://www.mysql.com/) (open source)
* [**SQLite**](https://www.sqlite.org) (open source)
* [**PostgreSQL**](https://www.postgresql.org/) (open source)
* [**Oracle**](https://www.oracle.com/database/technologies/appdev/sql.html) (proprietary)
* [**BigQuery**](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) (proprietary)
*****

--{{1}}--
A given database will be set up for one particular "flavor" of SQL, so you generally don't get to choose what SQL implementation to work in (unless you're the one designing the database). Instead, you'll use whatever the SQL "flavor" is for the database you want to access. 

--{{1}}--
The most common difference between different SQL "flavors" are the availability of different functions that users can use for data manipulation, as well as the types of error messages that will be returned to the user when running code with syntax issues.

--{{1}}--
That said, knowing the specific "flavor" of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors.
When you're trying to troubleshoot a SQL query, being able to add the name of the implementation to your search terms will help you get more relevant results.

## SQL Queries

A SQL **query** is essentially a question or request for data, written in a specific structure.  

--{{0}}--
Let's take a closer look at how to compose a SQL query!
But first, a word of encouragement. 
If you are one of the many people who feel anxious when they see code, you have a great opportunity today.

{{1}}
*****
<div class = "care">
<b style="color: rgb(var(--color-highlight));">A little encouragement...</b><br>

We're going to give some simple examples of SQL code to help build your intuition about SQL.  
You **won't** have to write or run any code, and we're only going to barely scratch the surface of SQL **syntax** (supported commands and how to write them -- the grammar and vocabulary of SQL).  

The goal is to help **build your intuition about what SQL is good at** (picking out just the right data).

</div>
*****

--{{1}}--
So this is a no-pressure situation. 
With that frame in mind, let's take a look at what SQL queries actually look like!

### What does a SQL query look like?

At a high level, we generally provide three pieces of information when constructing SQL "**queries**":

 1. The name of the **table(s)** where the data is stored.
 2. The **column name(s)** you want to look at from the table(s) you specified.
 3. Any **filtering condition(s)** you want to apply. 

{{1}}
*****
You put these basic pieces of information together using the syntax shown below to create a SQL query:

```sql
SELECT _2_ FROM _1_ WHERE _3_;
```
*****

{{2}}
*****
For example, here are some sample queries, each of which take place on just a single table.

```sql
SELECT price FROM products WHERE product_type = "FRUIT";

SELECT med_id, order_date FROM medication_order;

SELECT * FROM patients WHERE age < 20;
```
*****

### SELECT and FROM

A **select statement** is used to specify which columns you would like to have returned as output from your SQL query.

--{{0}}--
The basic components of a select statement are the `SELECT` and `FROM` keywords. 
The `FROM` keyword is used to specify the table or tables that hold the data you're interested in, and the `SELECT` keyword is used to provide a list of columns within those table(s) that you would like returned as output.

{{1}}
*****
- `FROM`: specify the table or tables
- `SELECT`: provide a list of columns
*****

--{{1}}--
Note that many people choose to write SQL keywords in all capital letters, but that's so that they stand out clearly in SQL code, not because it's a language requirement.

### Select All Columns

--{{0}}--
If you would like to return **all** of the columns from the table(s) specified in your SQL query, you can use the `*` wild card character as shown in the example below.  
You'll notice that we put a line break between the asterisk and the `FROM` keyword.  Spaces and line breaks, or **whitespace**, don't really matter for SQL.  
You can run your code together on a single line, or (preferably) add indentation and spaces that help human readers understand your code more easily.

```sql
SELECT *
FROM patient;
```

### Select Specific Columns

--{{0}}--
If you would only like to return a specific set of columns in your select statement you will need to explicitly list out each of those columns after the `SELECT` keyword, with each column name separated by a comma:

```sql
SELECT last_name, first_name, date_of_birth, sex
FROM patient;
```

### WHERE

--{{0}}--
The **where clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.

{{1}}
*****
<div class = "important">
<b style="color: rgb(var(--color-highlight));">Key Idea</b><br>

Use `SELECT` to specify the columns you want, and `WHERE` to specify the rows you want.

</div>
*****

### Filtering with WHERE

--{{0}}--
This example uses the where clause to filter output on only those records that represent female patients.

```sql
SELECT *
FROM patient
WHERE sex = "F";
```

### More complex filtering

--{{0}}--
Although the previous example lists only one constraint for the dataset, the **where clause** can contain any number of filtering arguments needed.
Here's a more complex example:

```sql
SELECT *
FROM patient
WHERE sex = "F" AND date_of_birth >= '2019-01-01';
```

## 💫 Your turn! SQL Tasks

Which of these correctly describe the strengths of SQL? Choose all the correct options.

[[X]] **A.** SQL is the most common tool for exporting data from relational databases
[[ ]] **B.** SQL is often used for data visualization purposes
[[X]] **C.** SQL can pick just the columns you want as well as only the rows that meet some conditions
[[ ]] **D.** SQL is a good solution for complex language processing
[[X]] **E.** SQL is a good choice for accessing data that can be organized in tables with rows and columns
*********

<div class = "answer">

SQL is great at working with rectangular data, data that is stored in tables with rows and columns.
If the data you want to use are stored in a relational database, then you'll likely need to use SQL to access the data you need. 
Its powerful SELECT / FROM / WHERE syntax makes SQL an ideal tool for isolating just the data you care about, whether that's specifying the columns you're interested in or limiting your data to just those rows that meet certain conditions.  
However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  

</div>

*********

## Recap

--{{0}}--
Today, you learned about the language SQL, which is an acronym for "Structured Query Language". 

SQL is a powerful tool for requesting specific subsets of data from a relational database.

--{{0}}--
It has been around since the 1970's because of its efficiency and utility.  

We also introduced you to two important elements of the language:

* The "select" statement, which uses `SELECT` and `FROM`
* The "where" statement, which uses `WHERE`

We also discussed what SQL doesn't provide, like robust language and statistical processing and data visualization.  

--{{0}}--
SQL is a tool that ordinarily is used in concert with other tools, each one used in its area of greater strength.

Finally, you learned about the structure of relational databases: data stored in tables, which are comprised of rows and columns.  Columns may contain identifiers that allow data from different tables to be related to one another, and that's why the word "relational" appears.

## Additional Resources

* Khan Academy's [Introduction to SQL](https://www.khanacademy.org/computing/computer-programming/sql) is high quality and easy to learn from.

* [What is SQL?](https://education.arcus.chop.edu/sql-intro/) is a brief introduction to SQL similar to the material in this module.

* If you are interested in the history of technology, [Early History of SQL](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6359709) is a comprehensive look into how SQL has evolved.  It's very jargon-dense!

## Upcoming sessions

@colorhighlight(Database Normalization)

Learn about the concept of normalization and why it's important for organizing complicated data in relational databases.

- [**October 21, 2024 at 12 pm** sign up link](https://events.teams.microsoft.com/event/5fe93c3c-c3c7-4dc0-b17a-edab5b92b62f@a6112416-07b0-41a5-9bb1-d146b575c975)
- [**October 29, 2024 at 4 pm** sign up link](https://events.teams.microsoft.com/event/d1866e4a-c318-4b02-bafe-380f403c5428@a6112416-07b0-41a5-9bb1-d146b575c975)

@colorhighlight(SQL Basics)

Learn basic SQL queries (with the SELECT, FROM, WHERE, DISTINCT keywords). We'll work single tables, using code, hands-on.

- [**November 4, 2024 at 12 pm** sign up link](https://events.teams.microsoft.com/event/5f6fd2ab-9e1b-43e6-ab39-21671d3140d1@a6112416-07b0-41a5-9bb1-d146b575c975)
- [**November 12, 2024 at 4 pm** sign up link](https://events.teams.microsoft.com/event/5007b4f0-06bc-4a5a-b629-92b448d1d382@a6112416-07b0-41a5-9bb1-d146b575c975)

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
