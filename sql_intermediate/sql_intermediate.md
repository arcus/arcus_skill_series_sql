<!--
author: Joy Payton
email: paytonk@chop.edu
version: 2.0.0
current_version_description: Updated for 2024 presentation 
module_type: slides
docs_version: 3.0.0
language: en
narrator: US English Female
mode: Presentation
classroom: enable
@onload: window.LIA.settings.sound = false

title: SQL Intermediate Level

comment:  Learn how to do intermediate SQL queries on single tables, by using code, hands-on.

long_description: Do you want to learn intermediate Structured Query Language (SQL) for more precise and complex data querying on single tables?  This module will give you hands on experience with single-table queries using keywords including CASE, LIKE, GROUP BY, and HAVING, along with a number of aggregate functions like COUNT and AVG.  This module is appropriate for people who are comfortable writing basic SQL queries and are ready to practice more advanced skills.

estimated_time_in_minutes: 60

@pre_reqs
Some experience writing basic SQL code (SELECT, FROM, WHERE) is expected in this module.  If you would like a code-free overview to SQL we recommend our module [Demystifying SQL](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/education_modules/main/demystifying_sql/demystifying_sql.md).  If you need to develop basic SQL fluency we recommend our module [SQL Basics](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/education_modules/main/sql_basics/sql_basics.md).
@end

@learning_objectives  
After completion of this module, learners will be able to:

- Create new data classifications using `CASE` statements
- Find text that matches a given pattern using `LIKE` statements
- Use `GROUP BY` and `HAVING` statements along with aggregate functions to understand group characteristics
@end

good_first_module: false
data_domain: ehr
data_task: data_wrangling
collection: learn_to_code
coding_required: true
coding_level: intermediate
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
module_link: [SQL Intermediate Level](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/education_modules/main/sql_intermediate/sql_intermediate.md)

import: https://raw.githubusercontent.com/arcus/education_modules/main/_module_templates/macros.md
import: https://raw.githubusercontent.com/arcus/education_modules/main/_module_templates/macros_sql.md
import: https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/macros_slides.md

big: <b style="font-size: 1.25em;">@0</b>
center: <div style="text-align: center;">@0</div>
colorhighlight: <b style="font-size: 1.15em; color: rgba(var(--color-highlight));">@0</b>

@sql_series_slide

<div style = "text-align: center; font-weight: bold;font-size: 1.5em; color: white; background-color: rgba(var(--color-highlight));">Welcome to the Arcus Education Skill Series!</div>

<br>

<div style = "align-items: center; display: flex;">
<div style = "margin: 1rem; max-width: 30%; float:left; padding-right:4em;">![""](../media/SQL-Logo.png)
</div>
<div style = "margin: 1rem auto; max-width: 65%; float:left;">
<h3>Beyond the Spreadsheet: Understanding SQL and Relational Databases</h3> 

</div>
</div>
@end

@todays_talk
@big(@title)

After this session, learners will be able to:

@learning_objectives
@end

@about_these_slides

These slides were created with [LiaScript](https://liascript.github.io/), an open source markdown parser for writing educational content.

All of the speaker notes from today's talk are saved in the slides themselves -- try changing the view to Textbook and it will integrate the text from the notes into the slides themselves, or turn on the sound at the bottom to hear the notes read out loud as you go through. 

<div style = "align-items: center; display: flex;">
<div style = "margin-left: 10%; max-width: 25%; float:left; border-style: solid; border-color: rgba(var(--color-highlight));">
![Screenshot showing the upper right menus on a liascript page with the mode menu open and Textbook highlighted.](../media/liascript_mode.png)
</div>
<div style = "margin-right: 10%; max-width: 25%; float:right; border-style: solid; border-color: rgba(var(--color-highlight));">
![Screenshot showing the sound buttons at the bottom of a liascript page with the speaker button highlighted.](../media/liascript_sound.png)
</div>
</div>

The content from this talk is also available as an online self-paced tutorial: @module_link 

For all of the files and information from this talk, go to our @repo_link 

@end

@teams_polls 

@big(Today's presentation will include interactive content!)

The best way to learn is to practice!

When we reach 💫 **Your Turn** sections, you'll have a chance to write or edit some SQL code of your own. There will also be opportunities to ask questions, and there will be some polls and other prompts in the chat to respond to.

@end

link:  https://cdn.jsdelivr.net/gh/arcus/arcus_skill_series_sql@main/assets/styles.css
-->


# SQL Intermediate Level
@sql_series_slide

--{{0}}--
Hi everyone, my name is Joy Payton, and I use she/her pronouns. 
I'm a member of the Data Education team that forms part of the Arcus initiative of the CHOP Research Institute.
Today's talk is the fourth topic in our five topic series on sequel, or S-Q-L.  At the end of today's talk you will get a link to sign up for the final topic, SQL Joins, if you are so inclined.  
If you want to follow along in today's presentation, my colleague Rose will share in chat the link to this slide deck that I'm presenting, so that you can follow along.  I do recommend that you go ahead and click that link, because today's webinar is hands-on, and you'll want to have access to all the activities.
Today's webinar will be recorded, so please leave your cameras and mics turned off until the question time at the end.  That's when I'll turn the recording off so we can all feel comfortable asking questions without being recorded.
If you do have questions that come up during the talk, feel free to put them in the chat. 
Today, we'll be learning how to do some more advanced SQL queries on single tables. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting -- don't worry. I'll provide plenty of scaffolding, and we'll work through things together.
So with that, let's get started!

## Today's talk

@todays_talk 

--{{0}}--
In the most recent webinar in this series, my colleague Rose Hartman showed how to compose simple queries using SELECT, WHERE, FROM, DISTINCT, AS, and ORDER BY.  That sets up up well for today's learning objectives.
Today, after a quick review of the commands we went over last time, we are going to learn how to write more complicated queries using CASE, LIKE, and GROUP BY. Along the way we will learn about some aggregate functions, as well as practice and refresh the skills you already know.

## Thank you!

<div class = "gratitude">
<b style="color: rgb(var(--color-highlight));">Thank you!</b><br>

Material for this talk is based closely on the DART module @module_link, written by Peter Camacho and Joy Payton.

</div>

--{{0}}--
Material for this talk is based closely on the DART module **SQL Intermediate Level,** written by Peter Camacho and by me.  It does feel a little weird to acknowledge myself, I admit, but I want to promote a culture of acknowledging the sources we use for education!
Our webinar today will **not** cover all of the topics in the module we wrote, because it's simply too long.  We won't have time to cover everything in the module Pete and I crafted, so I suggest you check out the module after our session. Rose will add the link to that module into the chat, in case you want to check it out on your own time afterwards!

## Learn by doing

@teams_polls

--{{0}}--
We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using a fake patient database. There will also be some short quizzes to help solidify your understanding as we go.

## SQL: A Brief Refresher

**SQL** (**S**tructured **Q**uery **L**anguage) has, for more than four decades, been used to interact with **relational databases**.

A relational database is a data storage solution that stores data tables, which are comprised of columns (also called 'fields') and rows.

--{{0}}--
First, let's quickly review some key concepts from our earlier topics. 
"Sequel", or S-Q-L (either pronunciation is fine) stands for Structured Query Language. SQL is a programming language used to interact with Relational Databases. 
Relational databases consist of many different data tables. Today we will be working with data from **one** table at a time, even though the three tables we will work with are stored in a single relational database. To learn more about combining data from more than one table, be sure to catch our final presentation in the series, which is called SQL Joins.

{{1}}
*****
<h4> What SQL is for: </h4>
isolating and combining just the data you're interested in, such as:

 * extracting columns you're interested in
 * filtering to just the data that meets specific criteria
*****
--{{1}}--
SQL is great at selecting just the data you want from rectangular data, data that is stored in tables with rows and columns.  We sometimes also call columns "fields". 

{{2}}
*****
<h4> What SQL is **NOT** good for: </h4>

* fine tuned statistical, linguistic, or data visualization needs
*****
--{{2}}--
However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other languages like R, Python, or the Stata language, which are better suited for work like statistical analysis. We will, however, see some of the ways that SQL can generate simple summary statistics today.

### Flavors of SQL

--{{0}}--
SQL has various dialects or flavors, that have small differences in how they are implemented.
There will be a few times during this webinar when I will point out that the flavor of SQL we are using today is impacting the outputs we get. 

Some popular "flavors" of SQL:

* [**MySQL**](https://www.mysql.com/) (open source)
* [**SQLite**](https://www.sqlite.org) (open source)
* [**PostgreSQL**](https://www.postgresql.org/) (open source)
* [**Oracle**](https://www.oracle.com/database/technologies/appdev/sql.html) (proprietary)
* [**BigQuery**](https://cloud.google.com/bigquery/docs/reference/standard-sql/query-syntax) (proprietary)


{{1}}
*****
<h3>Flavor of the Day: [**AlaSQL**](https://alasql.org/) </h3> 
*****

--{{1}}-- 
Because different dialects of SQL can have different outputs, knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. 
In the hands-on portion of this webinar, we'll be using a form of SQL that actually runs in your web browser as you look at these slides.  This lightweight SQL engine is called "AlaSQL".  We pre-populated some tables for you to experiment with in this presentation.  These tables are filled with fabricated data meant to look a little like an electronic health record.  Rest assured that this data was completely invented, although it might look realistic!

### SELECT, FROM, WHERE

--{{0}}--
Before we learn any new SQL commands, let's do a quick review of the commands SELECT, FROM, and WHERE that we learned about earlier.
The basic structure of a SQL query is
SELECT, followed by some field or column names, then 
FROM, followed by one or more table names, then, possibly
WHERE, followed by a filtering condition.

The basic structure of a SQL query is

```sql
SELECT
  fields
FROM dataset_name.table_name
WHERE conditional_statement
```

--{{1}}--
To start exploring the `patients` table from the `alasql` database, let's first take a look at all of the fields in the table. Use the asterisk as a wildcard to select all fields.
For these in-browser code cells, the "play" button below the code box will run your code.
I'll go ahead and click this button.
When you run your query, the results of the query will be stored in a collapsable section below. I'll expand that section by clicking on this triangle!
This black bar between the code cell and the results is where any error messages will appear.

{{1}}
*****
Use the asterisk as a wildcard to select all fields:

```sql
SELECT *
FROM alasql.patients
```
@AlaSQL.eval("#dataTable_select_wildcard")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_select_wildcard" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****

--{{2}}--
Once you know what the column names are, you should usually select only the columns (or fields) you actually need.
We recommend using dot notation and comma-first style, shown here, to list the specific fields you want to see. 
I'll run this code to see the output.

{{2}}
*****
We recommend using dot notation and comma-first style to list the specific fields you want to see.

```sql
SELECT 
  patients.id
  ,patients.address
  ,patients.city
  ,patients.county
  ,patients.state
FROM alasql.patients
```
@AlaSQL.eval("#dataTable_select_list_fields")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_select_list_fields" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****
--{{3}}--
The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.
As an example, here's how you'd filter the output to include only the records for a specific county, in our case, Suffolk County.

{{3}}
*****
Use WHERE to return only rows for which a conditional statement is true:

```sql
SELECT 
  patients.id
  ,patients.address
  ,patients.city
  ,patients.county
  ,patients.state
FROM alasql.patients
WHERE
	patients.county = "Suffolk County";
```
@AlaSQL.eval("#dataTable_where")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_where" border="1"></table>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****

--{{3}}--
We will also be seeing the `DISTINCT` and `ORDER BY` functions again today, and we will review them when we get there.

## `CASE`

--{{0}}--
Now that we've reviewed the basic SQL we learned last time, we are ready to learn some new SQL keywords and explore our database further. Our example database has three tables, `patients`, `allergies`, and `observations`. 
Let's look at the observations of "Peanut Immunoglobulin E Antibody in Serum" in the `alasql.observations` table.

```sql
SELECT
	observations.*
FROM alasql.observations
WHERE
	observations.description = 'Peanut IgE Ab in Serum';
```
@AlaSQL.eval("#dataTable_observations")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_observations" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_observations

</div>

--{{0}}--
Taking a closer look at the `observation_value` field, those numbers would be a lot more useful if we knew what those numeric values indicate.
Often when working with data, you will come across the need to define your own custom categories or groupings given some raw row data as input. For example, you might have lipid levels that you want to categorize as _normal_, _borderline_, or _abnormal_. This is where the `CASE` statement can come in handy!

### Structure

--{{0}}--
The `CASE` statement is used to produce conditional row-level output.  It's like an "if" statement, but with multiple possibilities, or "cases," that are considered. Let's take a look at a generic example, then we'll practice with our dataset.
One way to think of a case statement is by its components. We will look at these components one by one, starting in the middle of the statement and working our way out.


The `CASE` statement has 4 main components (shown below).


```sql
CASE                --COMPONENT 1: start tag of the case statement.
  WHEN (…) THEN (…) --COMPONENT 2: conditional when "some input" then "some output" logic.
  …                 --             additional "when / then" possibilities continue,
                    --             as many as you need.
  ELSE (…)          --COMPONENT 3: declaration of default value to be returned if
                    --             none of the when/then conditions are met.
END                 --COMPONENT 4: end tag of case statement with optional
                    --             field name (for instance, `AS patient_category`)
```

{{1}}
*****
Conditional statements:

```sql
  WHEN conditional_statement THEN some_output  
```
*****

--{{1}}--
Conditional statements in SQL use this `WHEN`/`THEN` form. `WHEN` the conditional statement is true, `THEN` the designated output will be returned to you.
You can have as many conditional statements as you want. Be aware, however, that for each row, SQL will only return one output, corresponding to the first time a condition is found to be true.

{{2}}
*****
You include have multiple conditional statements.

```sql
  WHEN patients.age < 1 THEN 'infant'
  WHEN patients.age <= 12 THEN 'child'
  WHEN patients.age <= 17 THEN 'teen'
```
*****

--{{2}}--
Let's consider what these statements would do in a row where `patients.age` (by the way, that's not actually a field that exists in our `patients` table, but let's just pretend) is, say, age 10. 
That row would not be categorized as an infant because it's not true that 10 is less than 1.  So the first WHEN/THEN doesn't trigger.
Let's look at the next WHEN/THEN.  Well, age 10 would be categorized as a child because 10 is indeed less than or equal to 12. That means this is the first WHEN/THEN to be triggered.
That means we're done checking.  We won't keep going and looking at the final WHEN/THEN statement.  So, even though 10 is less than or equal to 17, the age of 10 will not be categorized as "teen" because we already triggered an earlier WHEN/THEN statement, the one for "child".


{{3}}
*****
`ELSE` comes after all of the `WHEN`/`THEN` statements and tells SQL what to return if none of the cases are true. 

```sql
  WHEN patients.age < 1 THEN 'infant'
  WHEN patients.age <= 12 THEN 'child'
  WHEN patients.age <= 17 THEN 'teen'
  ELSE 'adult'
```
*****

--{{3}}--

`ELSE` comes after all of the `WHEN`/`THEN` statements and tells SQL what to return if none of the cases, none of the WHEN/THEN statements, evaluate to true. 
If you leave out the `ELSE` clause, SQL imposes a condition of `ELSE NULL` by default. 
We strongly encourage you to always include an `ELSE` clause even if you like the default value of `ELSE NULL`, to make your code more explicit.  After all, you can always say `ELSE NULL` explicitly!

{{4}}
*****
Open the statement with `CASE` and close it with `END`.

```sql
CASE
  WHEN patients.age < 1 THEN 'infant'
  WHEN patients.age <= 12 THEN 'child'
  WHEN patients.age <= 17 THEN 'teen'
  ELSE 'adult'
END
```
*****
--{{4}}--
Lastly, you need to open the statement with `CASE` and close it with `END`.
The indentation before each of the `WHEN` statements and the `ELSE` statement are for us as human readers of this code. SQL doesn't need those lines to be indented, but it makes it a lot clearer to us where this block of code starts and ends.
We have started with a lot of theory because `CASE` statements are complicated, so let's return to that `observations` table that we were looking at earlier, and see how using a `CASE` statement can help us categorize the data.

### Example


A `CASE` statement goes between the `SELECT` statement and the `FROM` statement in a SQL query.

```sql
SELECT
	observations.*
	,CASE
        WHEN observations.observation_value >= 17.5 THEN 'Strongly Positive'
        WHEN observations.observation_value >= .7 THEN 'Positive'
        WHEN observations.observation_value >= 0.35 THEN 'Equivocal'
        WHEN observations.observation_value >= 0.10 THEN 'Borderline'
        WHEN observations.observation_value < 0.10 THEN 'Negative'
        ELSE NULL
	END
FROM alasql.observations
WHERE
	observations.description = 'Peanut IgE Ab in Serum';
```
@AlaSQL.eval("#dataTable_observations_cases")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_observations_cases" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_observations

</div>


--{{0}}--
A `CASE` statement goes between the `SELECT` statement and the `FROM` statement in a SQL query. We might know that if that observed value of IgE Antibody is greater than or equal to 17.5, that is a strongly positive result, and also have known cutoff values corresponding to Positive, Equivocal, Borderline, and Negative results.  This might be helpful in writing reports to help families understand what these values mean.  Let's run this code, which gives us everything from the observations table, and then some category, which we derive using this case statement.

--{{1}}--
When we run this code, we get a new column with the outcomes of our conditional `WHEN`/`THEN` statements in it. The data here looks great, we can read immediately that all three Peanut IgE antibody results were positive, two of them strongly positive. But we have this ugly column name, with the entire `CASE` statement as the name.  
We can make that column name much nicer by using an alias. At the end of the `CASE` statement, immediately after the word `END`....
[scroll up here] 
I'm going to add `AS interpretation` and run the code again. Using `AS` to give this new column an alias will make it much easier for us to read and understand.
Here we just give an abstraction of what we just did.  It is usually a good idea to follow a closing `END` with `AS` to give your new column a useful alias.
I want to pause here for questions before giving you your first opportunity to practice coding in SQL on your own.

{{1}}
******
Follow a closing `END` with `AS` to give your new column a useful name.

```sql
CASE
  WHEN (…) THEN (…)
  ELSE (…)
END AS new_column_name
```
******

### 💫 **Your Turn 1** 

--{{0}}--
You're studying attitudes about smoking and will issue a survey in phases.  Phase 1 will go out to residents of Plymouth County, Phase 2 will go out to residents of Essex County and Phase 3 will go out to Barnstable County.  Finish the following query such that you get the patient name, county, and a new column called `phase`. 
I'm going to give you a few minutes to try this on your own.  Don't forget that you can use the forward and back pagination to look back at what we covered earlier today, in case you need to copy and paste some example code.
You can see that there is a comment in the chat for you to thumbs-up when you are done, and when we have a sufficient number of people having finished, we will complete the query together. 

You're studying attitudes about smoking and will issue a survey in phases.  Phase 1 will go out to residents of Plymouth County, Phase 2 will go out to residents of Essex County and Phase 3 will go out to Barnstable County.  Finish the following query such that you get the patient name, county, and a new column called `phase`. 

```sql
SELECT
  patients.first
  ,patients.last
  ,patients.county
  ,CASE
    WHEN      THEN "Phase 1"
    WHEN      THEN "Phase 2"
    WHEN      THEN "Phase 3"
    ELSE NULL
  END
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable_case_your_turn")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_case_your_turn" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal an answer once you're done!*</summary>

Try:

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

</details>


## `LIKE`
--{{0}}--
So far, we've run queries that assume we know a lot about our database.  But sometimes we don't know exactly what's in our data. We can use SELECT DISTINCT to learn more. Let's take a closer look at the `allergies` table.
Use `SELECT DISTINCT` to discover which distinct allergy descriptions appear in the `allergies` table.


Use `SELECT DISTINCT` to discover which distinct allergy descriptions appear in the `allergies` table.

```sql
SELECT DISTINCT allergies.description
FROM alasql.allergies;
```
@AlaSQL.eval("#dataTable_allergies")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_allergies" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_allergies

</div>
--{{0}}--
Say you are interested in all types of pollen allergies, but not other allergies. With the tools we already have, you could get that information using a `WHERE` statement.

{{1}}
*****
To get all pollen allergies from the `allergies` table with a `WHERE` statement, you can spell out each possible match in its entirety.

```sql
SELECT *
FROM alasql.allergies
WHERE
  allergies.description = "Allergy to tree pollen"
  OR
  allergies.description = "Allergy to grass pollen";
```
*****

--{{1}}--
To get all pollen allergies from the `allergies` table with a `WHERE` statement, you can list out every possibility and use "OR" between them.
In the very small table we are working with here, this method works fine. But if we were looking at a real patient data, there might be hundreds of types of pollen allergies. And the same allergy might show up as "Allergy to grass pollen" and "grass pollen allergy" with different wording and different capitalization, because different people chart differently! Or maybe a new patient comes in who has a new, different pollen allergy. In that case you would need to update the query or you'd run the risk of missing someone with a novel allergy.  You can imagine that this level of specificity is error-prone.
How can we get all the pollen allergies without having to specify them all, perfectly? We need the `LIKE` operator to help us out.


### Structure

--{{0}}--
`LIKE` operators let you compare text data to a pattern rather than checking if two strings of characters match perfectly.
This action is known as **pattern matching**, and can let you filter on row values that are similar, but not exact matches.


`LIKE` operators let you compare textual data to a pattern rather than checking if two strings of characters are exactly equal with `=`.

```sql
SELECT *
FROM alasql.allergies
WHERE
    allergies.description LIKE a_particular_pattern;
```

This action is known as **pattern matching**, and can let you filter on row values that are similar, but not exact matches.

### Patterns

The `LIKE` operator uses 2 distinct **wildcard characters** that let you make patterns where some characters are unknown.

| Wildcard Characters | Description |
| --- | --- |
| `%` | "Wildcard" for 0 or more characters. |
| `_` | "Wildcard" for exactly 1 character. |

--{{0}}--
The `LIKE` operator uses 2 distinct **wildcard characters** that let you make patterns where some characters are unknown.
The percent symbol is the "Wildcard" for 0 or more characters.
The underscore is the "Wildcard" for exactly 1 character.
Wildcard characters let us build patterns to compare with a string of text data. Let's take a closer look at some examples using the percent wildcard.

--{{1}}--
Putting a percent symbol just at the beginning means anything can come before the characters in pollen, but the data must _end_ with "pollen". 
`%pollen` matches "Allergy to tree pollen" 

{{1}}
*****
`%pollen` matches "Allergy to tree pollen" 
*****

--{{1}}--
If instead the percent symbol is only after the string `pollen`, a phrase would have to start with the letters "pollen" to be a match.
Capitalization matters to the `LIKE` operator.  If the P were capitalized in "Pollen allergy - trees" that would not be a match. We will return to the problem of capitalization in a moment.

{{2}}
*****

`pollen%` matches "pollen allergy - trees" (but not "Pollen allergy - trees")

*****

--{{3}}--
To match both of these constructions, as well as data like "Tree pollen allergy," we can put percent symbols both before and after.

{{3}}
*****

`%pollen%` matches both, and also "Tree pollen allergy"

****

--{{4}}--
In the same way we needed quotes around the data we wanted to match exactly, the entire string of characters, wildcards included, must be enclosed in quotes.

{{4}}
*****

Surround the pattern in quotes:

`allergies.description LIKE '%pollen%'` 

or 

`allergies.description LIKE "%pollen%"`

*****

### Example

--{{0}}--
Let's apply this structure to finding the pollen allergies from our `alasql.allergies` table.  I'll run my query that looks for all allergies that contain the lower case word pollen somewhere in the description field.

```sql
SELECT *
FROM alasql.allergies
WHERE
    allergies.description LIKE '%pollen%';
```
@AlaSQL.eval("#dataTable_like_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_like_example" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_allergies

</div>

--{{0}}--
If we had a larger collection of possible allergies, this query would return all of the rows in which the character string "pollen" appears in the `allergies.description` field. 
But what if there was an entry where the word "Pollen" was capitalized? The `LIKE` operator cares about capitalization, a lower case `p` and an upper case `P` are not the same characters.

--{{1}}--
The `LOWER()` (or `UPPER()`) operator can help us out by taking the data in a field and making all of the characters lowercase (or uppercase).
Wrap the database data that we want to search in `LOWER()` so that we're flattening out any capitalization differences in our comparison.  This allows us to make sure the query returns both capital and lowercase versions of our pattern. 
So, I'll change allergies.description here to LOWER(allergies.description), so that no matter whether people typed in the allergy in upper or lower case, we'll convert it to lower case before we compare it to the lower case word pollen here on the right.

{{1}}
Wrap left side of the `LIKE` statement in `LOWER()` to make sure the query returns both capital and lowercase versions of our pattern. 


### 💫 **Your Turn 2** 

--{{0}}--
You'd like to research patients born in the 1970s (so any year starting with 197 would work).  Use a `LIKE` statement to enrich the query below and limit the patient set to just the patients you care about.
I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will complete the query together. 

You'd like to research patients born in the 1970s (so any year starting 197\_ would work).  Use a `LIKE` statement to enrich the query below and find the patient set you care about.

```sql
SELECT
  patients.id
  ,patients.birthdate
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable_like_your_turn")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_like_your_turn" border="1"></table><br>

</details><br/><br/>

<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>


<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal an answer once you're done!*</summary>

Try:

```sql
SELECT
  patients.id
  ,patients.birthdate
FROM alasql.patients
WHERE patients.birthdate LIKE '197%';
```

</details>


## Aggregate Functions

**Aggregate functions** can be used to get a single value related the values for multiple rows of data in some meaningful way.  

--{{0}}--
**Aggregate functions** can be used to get a single value related the values for multiple rows of data in some meaningful way.  And it's really important to remember that it returns ONE value and one value only.
This aggregation could be a numerical statistic, like the sum or standard deviation of a number of rows, or it could pull out a special value, like the minimum or maximum value (this works as well for strings, in which case it would be the first or last value in alphabetical order). There are many other possibilities as well, like giving a count of rows or pulling a value at random from the rows.
Here are some commonly used aggregate functions:
`COUNT()`- Returns the count of the number of non-null values among the column(s)/rows provided as input.
`SUM()`- Returns the summation of all values from a column provided as input.
`MIN()`- Returns the minimum value from a column provided as input.
`MAX()`- Returns the maximum value from a column provided as input.
`AVG()`- Returns the numerical mean of all values from a column provided as input.
To count the rows in a table, use `COUNT(*)`.
COUNT will ignore null values, which can help you figure out how many values are in various columns, as we see here.

Commonly used aggregate functions:

|Function|Description|
|:---|:---|
|`COUNT()`|Returns the count of the number of non-null values among the column(s)/rows provided as input.|
|`SUM()`|Returns the summation of all values from a column provided as input.|
|`MIN()`|Returns the minimum value from a column provided as input.|
|`MAX()`|Returns the maximum value from a column provided as input.|
|`AVG()`|Returns the numerical mean of all values from a column provided as input.|

To count the rows in a table, use `COUNT(*)`.

These aggregate functions will ignore null values if you apply them to a specific column:

```sql
SELECT 
  COUNT(*) AS total_rows
  ,COUNT(patients.birthdate) AS births
  ,COUNT(patients.deathdate) AS deaths
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable_count_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_count_example" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{1}}--
The count function shows us that the `patients` table has 25 rows, and all of those 25 rows contains a `birthdate`. But most rows have a `NULL` value for the `deathdate`.
SQL will do its best to use the aggregate functions regardless of what type of data is in the column, but the outputs will make the most sense if the data type is what the function expects. For example `SUM` works best, as you might suspect, with numbers.  It might return some kind of value for a column that isn't numeric, but it probably won't be useful information. The `MAX` and `MIN` functions, on the other hand, are also typically used with numbers, but they might be useful even when used on text data: they will give the first or last, the min or max, value, of the text once it's ordered alphabetically.

{{1}}
*****

```sql
SELECT 
  SUM(patients.expenses)
  ,MAX(patients.last)
  ,MIN(patients.first)
  ,AVG(patients.coverage)
FROM alasql.patients;
```
@AlaSQL.eval("#dataTable_aggregate_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_aggregate_example" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

*****

--{{1}}--
We can see how SQL tries to adapt by changing which columns we try to sum or average. Let's see how all four functions work on the column `patients.sex`. Summing the `patients.sex` column just concatenates all of the entries, while averaging `patient.sex` returns a null value. These outputs might differ depending on what flavor of SQL you are using.  Our flavor, AlaSQL, returns a null value when it can't parse an aggregate statement, but other flavors of SQL may give you error messages.

### `GROUP BY`

--{{0}}--
Often, you are interested in statistics by group, such as the average BMI for men and that for women, or the standard deviation of reading test scores in teens with ADHD, depression, neither condition, or both conditions.
The `GROUP BY` clause is used to group column results into only the unique/distinct values among them. 
It is used in combination with aggregate functions to generate summary statistics about the larger dataset that was "grouped" (i.e. "collapsed") by `GROUP BY`. These can be tricky, so let's see a `GROUP BY` function in action before we examine how it works in more depth.

The `GROUP BY` clause is used to group column results into only the unique/distinct values among them. 

```sql
SELECT 
  patients.sex
  ,COUNT(patients.birthdate) AS births
  ,COUNT(patients.deathdate) AS deaths
FROM alasql.patients
GROUP BY
    patients.sex;
```
@AlaSQL.eval("#dataTable_group_by_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_group_by_example" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

{{1}}
*****
`GROUP BY` aggregations like the one above can be confusing and frustrating for new SQL users, because you have to remember that an aggregation returns **one and only one** value for the entire group of rows. This means you **cannot** ask for something in your `SELECT` clause that could give more than one value for the group.
*****

--{{1}}--
`GROUP BY` aggregations like this one can be confusing and frustrating for new SQL users, because you have to remember that an aggregation returns **one and only one** value for the entire group of rows. This means you **cannot** ask for something in your `SELECT` clause that could give more than one value for the group.
I find it helps to start with the `GROUP BY` clause. In this first example, we are grouping by one thing, `patient.sex`. That means each group will have one value for `patient.sex`. We couldn't ask for `race` when we have only grouped by `sex` because not every member of the `M` group is guaranteed to have the same `race` value. If we try to add `race` to our `SELECT` statement, AlaSQL just returns a null value. Other flavors of SQL may give you an error message in these cases.


{{2}}
*****
You can `GROUP BY` more than one column. 

```sql
SELECT 
  patients.sex
  ,patients.race
  ,COUNT(patients.birthdate) AS births
  ,COUNT(patients.deathdate) AS deaths
FROM alasql.patients
GROUP BY
    patients.sex
    ,patients.race;
```
@AlaSQL.eval("#dataTable_group_by_2_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_group_by_2_example" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>
*****

--{{2}}--
There are two types of fields in this `SELECT` statement. We are only selecting fields that 1. we are grouping by in the `GROUP BY` statement, or 2. are aggregate functions. 

--{{2}}--
Notice, also, that the rows being output by the `GROUP BY` statement correspond to the same rows we would have gotten using a `DISTINCT` statement -- only combinations that actually correspond to rows of the `patients` table appear. The aggregate function `COUNT` gives a single value for each of those distinct combinations. 

### `HAVING`

--{{0}}--
And this is our last topic, and it's one you might not use that often.  I've left it for last because I know this is a dense session.
So far when we have grouped data using `GROUP BY` we have gotten relatively few rows. When you are working with real data, this may not be the case. Maybe you are grouping patients by zip code. Pennsylvania has over 1500 active 5-digit zip codes, perhaps it only makes sense to look at zip codes which have a minimum patient population.


The `HAVING` clause can be used to filter your result set on the value of an aggregate function.  It works similarly to a `WHERE` clause, but the two are not interchangeable.  

--{{0}}--
This is a common error people who are new to SQL often encounter -- mixing up `WHERE` and `HAVING`. `WHERE` is for filtering rows, `HAVING` is for filtering groups.

The `HAVING` clause is placed directly after your `GROUP BY` statement. Let's take a look at this query into the population of subjects in each county.
 

```sql
SELECT 
  patients.county
  ,COUNT(*) AS subject_pop
FROM alasql.patients
GROUP BY
    patients.county
--HAVING COUNT(*) > 1;
```
@AlaSQL.eval("#dataTable_having_example")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_having_example" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{0}}--
Let's run the code as it is, and then see how the results change when we un-comment the `HAVING` statement. 

{{1}}
You can use an `ORDER BY` statement **after** a `HAVING` statement. Let's add `ORDER BY patients.county` to the end of our query.

### 💫 **Your Turn 3** 

**Challenge:** create a query below that queries `alasql.patients` and gives the patient population of each city (`patients.city`) which has more than one patient living there.  Give the results in an alphabetized list. 

**Hint:** You don't need to write the entire query at once, try first writing a query that returns the COUNT of patients in each city, and then modify that query to get the list you want.

```sql





```
@AlaSQL.eval("#dataTable_blank_quiz")

<details open>

<summary>**Results of Query (click to collapse or expand this section)**</summary>

<table id="dataTable_blank_quiz" border="1"></table><br>

</details><br/><br/>


<div style = "display:none;">

@AlaSQL.buildTable_patients

</div>

--{{0}}--
I'm going to give you a few minutes to try this on your own. There will be a comment in the chat for you to "like" when you are done, and when we have a quorum, we will construct the query together.

<details>
<summary style = "margin-bottom: 1rem;">*Going through these slides on your own? Click here to reveal an answer once you're done!*</summary>

Try:

```sql
SELECT
	patients.city
	,count(patients.city)
FROM alasql.patients
GROUP BY patients.city
HAVING count(patients.city)>1
ORDER BY patients.city;
```

</details>

## Recap

--{{0}}--
Today, you continued learning about the language "sequel" or S-Q-L, which is an acronym for "Structured Query Language." 

--{{0}}--
We covered several important functions, represented in SQL by **keywords** that let us build more complicated queries. In particular, we covered: 

{{1}}
*****
**`CASE`**: used to return different values based on a conditional statement. A full `CASE` statement uses 5 keywords:

* `CASE`: opens the statement
* `WHEN`: give a conditional statement that could be true or false
* `THEN`: what value should be returned when that conditional statement is true
* `ELSE`: what value should be returned when none of the `WHEN` statements are true
* `END`: closes the statement

*****

{{2}}
*****
------

**`LIKE`**: used to compare patterns of characters in ways more complicated than an exact match. We saw several helper functions to use with `LIKE`:

* `%`: represents any number of unknown characters
* `_`: represents exactly one unknown character
* `LOWER()`: makes all the characters inside the parentheses lowercase
* `UPPER()`: makes all the characters inside the parentheses uppercase

*****


{{3}}
*****
------

**Aggregate functions** return one value for multiple rows of data. We saw the most frequently used aggregate functions:

* `COUNT()`: returns the number of non-null values
* `SUM()`: sums all non-null values (numeric data)
* `MIN()`: returns the first (alphabetically) or smallest (numerically) value
* `MAX()`: returns the last (alphabetically) or largest (numerically) value
* `AVG()`: returns the average of all non-null values (numeric data)

*****

{{4}}
*****
------

**`GROUP BY`**: used to collect rows into groups with matching entries in a particular column or columns. 

*****

{{5}}
*****
------

**`HAVING`**: used filter for only groups that meet a condition. 

*****


--{{5}}--
You also got to practice hands on, which probably meant you got to see some error messages, too, which is helpful experience.

## Additional Resources

* Khan Academy's [Introduction to SQL](https://www.khanacademy.org/computing/computer-programming/sql) is high quality and easy to learn from.

* Tutorials Point has some helpful documentation you may want to check out to read more [about the basic types of **operators** available for use in a SQL query](https://www.tutorialspoint.com/sql/sql-operators.htm).

* Give the [SQL Murder Mystery](https://mystery.knightlab.com/) a try. Note that some of the content is more advanced than what we cover here, but there is a walkthrough, and you can always stop once you've reached the limits of what we've learned so far. 

* Select Star SQL is a [free interactive book that teaches SQL](https://selectstarsql.com/) by exploring Texas state execution data. The second and third chapters mostly cover topics we learned about today, while the remaining chapters dig deeper.

## Upcoming sessions

Want to see the materials from an earlier session? 
Everything is available on the [Arcus SQL Skill Series website](https://arcus.github.io/arcus_skill_series_sql/). 

@colorhighlight(SQL Intermediate Level)

Learn about intermediate SQL queries with keywords like CASE, LIKE, and GROUP BY. We'll work on single tables, using code, hands-on.

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
