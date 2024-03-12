<h3><strong><u>LINKS TO SHARE</u></strong></h3>

- The slides:  
- Your Turn 3:
- Your Turn 4: 
- Your Turn 5: 
- Your Turn 6: 

Welcome! 
I'm Meredith Lee, and I use she/her pronouns. 
I'm a data instructor on the Arcus Education team in DBHi, which is a part of CHOP's Data Education Collaborative. 
Today's talk is the final piece of our five-part series on sequel, or S-Q-L.  
This webinar will be recorded, so please leave your cameras and mics turned off until the end, when we'll turn off the recording and give you time to ask any questions. 
If you do have questions that come up during the talk, feel free to put them in the chat. 
So with that, let's get started!

<h3><strong><u>CLICK</u></strong></h3>

## Today's talk

Today, we'll be learning how to combine data from two or more interrelated tables into one dataset using the JOIN command. This is a hands-on webinar -- we'll be writing some real SQL code! If that sounds daunting, don't worry; I'll provide plenty of scaffolding, and we'll work through things together. 

In previous webinars in this series my colleagues Rose Franzen and Elizabeth Drellich taught you how to write basic SQL queries using SELECT, FROM, and WHERE, and then to craft more complicated queries using CASE, LIKE, GROUP BY, and some aggregate functions.  Today, we'll first quickly review some of these commands, and then we'll learn how to combine data from multiple tables using the JOIN command. 

<h3><strong><u>CLICK</u></strong></h3>

Material for this talk is based closely on the DART module **SQL Joins**, written by Joy Payton.

Many thanks to Joy for her work developing this excellent content!

Our webinar today many not cover all of the topics in the module, as we simply many not have time, so I suggest you check it out after our session. 

<h3><strong><u>CLICK</u></strong></h3>

We're firm believers that the best way to learn is to practice! As I mentioned before, we will have opportunities to practice writing our own SQL code today using tables containing fake medical records. There will also be some short quizzes to help solidify your understanding as we go.

With that being said, lets get started!

<h3><strong><u>CLICK</u></strong></h3>

## SQL: A Quick Review

First, let's quickly review some key concepts from our previous four sessions. 

As a reminder, "Sequel", or S-Q-L, stands for **Structured Query Language**, and is a specialized programming language that is used to interact with Relational Databases. 

Relational databases consist of many different data tables. Today we will be working with multiple tables that are stored in a single relational database. 

<h3><strong><u>CLICK</u></strong></h3>

SQL is great at working with rectangular data, data that is stored in tables with rows and columns / fields. 

<h3><strong><u>CLICK</u></strong></h3>

However, it's not great for fine-tuned statistical, linguistic, or data visualization purposes.  SQL is therefore a tool that is often partnered with other tools like R or Python, which are better suited for work like statistical analysis.

<h3><strong><u>CLICK</u></strong></h3>

### Flavors of SQL

Recall that SQL has a variety of different implementations, and while they all have a similar structure, and the same basic syntax, each different SQL database product often has its own minor variations in dialect. People often refer to these SQL dialects as different "flavors" of SQL. 

The most common difference between different SQL "flavors" are the availability of certain functions, as well as the types of error messages you might see. There will be times later in this webinar when I will point out that the flavor of SQL we are using today is impacting how we need to write a query. 

<h3><strong><u>CLICK</u></strong></h3>

Knowing the specific flavor or dialect of SQL your database uses is especially useful when first getting started writing queries and troubleshooting errors. Whenever you search for documentation online or are troubleshooting, you'll want to be sure to include the name of the "flavor" you're working with in your search terms. 

<h3><strong><u>CLICK</u></strong></h3>

In the hands-on portion of this webinar, we'll be using a form of SQL that actually runs in your web browser as you look at these pages, called "AlaSQL".  We pre-populated some tables for you to experiment with in this presentation. Some of these tables are filled with fabricated data meant to look a little like an electronic health record (EHR).  Rest assured that this data was completely invented, although it might look realistic!

<h3><strong><u>CLICK</u></strong></h3>

### SELECT, FROM, WHERE

Before we learn any new SQL commands, let's do a quick review of the commands SELECT, FROM, and WHERE that we learned about a couple of months ago.

To select only the columns (or fields) you want, you can use a `SELECT` statement. `SELECT` specifies the columns you're interested in, and `FROM` specifies the table (or tables) those columns are from.

As a reminder, we recommend using dot notation and comma-first style to list the specific fields you want to see.

<h3><strong><u>CLICK</u></strong></h3>

The **WHERE clause**, using the `WHERE` keyword, is the section of your query used to specify any "filtering logic" that should be applied to your query before returning any output.  It's optional but very useful.

As an example, here's how you'd filter the output to only include records for a specific county.

In the previous webinar in this series, we learned other keywords such as `DISTINCT`, `CASE`, `LIKE`, `GROUP BY`, and `HAVING`. We won't need to use those today, and so we're not going to review them here. If you need a review of those keywords, or any other topic we've previously covered, please see our previous webinar recordings. 

<h3><strong><u>CLICK</u></strong></h3>

## Overview of Joins

Up to now, we have be working with data from only one table at a time, but SQL databases are made up of many tables, and often the questions you want to answer will require referencing more than one table-- this is where SQL "join" functionality and the `JOIN` keyword come into play. 

This is what a SQL join looks like. We will be discussing the various parts that make up a SQL join throughout this webinar. 

<h3><strong><u>CLICK</u></strong></h3>

### Joins: Why?

Let's consider the case where you have data about a multi-site study's research subjects. One table holds depression scores for subjects and a different table holds subject addresses.  Your hypothesis is that people who live in certain zip codes have higher rates of depression.  

To see if your hypothesis has evidence to back it, you need to combine data, taking the subject ID and depression score from one table, and the subject ID and zip code from another table, and combining them, so that you get matching information in the same row of the same table.

Maybe your source tables look something like the tables below:

The result should be a single table that might only have three columns: "subj_id", "dep_total", and "zip".  That way you can more easily look at the relationship between depression inventory scale and zip code.

<h3><strong><u>CLICK</u></strong></h3>

### Joins: How? 

There are two basic pieces of information you need to know to write successful joins:

<h3><strong><u>CLICK</u></strong></h3>

The first is the **type of join**. The type of join shows up in SQL in a `FROM` statement. Let's say you have some students with math grades and some students with language grades.  Some students are in only the math table, some are only in the language table, and some are in both.  What part of the overlapping data do you want?  Only the data on students with both kinds of grades?  Or some other, larger set of student data? The answer to this question will determine what type of join you choose. 

<h3><strong><u>CLICK</u></strong></h3>

The second is **join criteria**. The join criteria shows up in SQL in an `ON` or `USING` statement. When thinking about join criteria, we want to know what constitutes a "match" of data from one table to data from another. If you're joining tables that hold student grades, for example, you probably want to only join data together where the student ID matches.

It can be surprisingly tricky to figure out what makes data "match" or "go together" in your join criteria. If we take a look at the tables on the previous slide, what data should be considered "matching" between the "depression_scale" table and the "subject_address" table? Write your answer in the chat.

Was the answer as simple as just matching on the subject id ("subj_id")?

<h3><strong><u>CLICK</u></strong></h3>

### Combining Join type and criteria

This is the basic structure of a SQL join, including the type of join and the criteria we're using to match data across table 1 and table 2.  For the rest of this webinar, we'll first talk about join types, then join criteria, and then we'll finish up with more examples to help you understand how these two elements of a join work together to give you the results you care about. 

Your SQL query might include lines that look something like this:

<h3><strong><u>TALK THROUGH SQL</u></strong></h3>

<h3><strong><u>CLICK</u></strong></h3>

## Join Types

Let's consider the gradebook example we mentioned earlier. We might have two tables, one called "math_grades" and one called "language_grades".  Some students appear in "math_grades", some in "language_grades", and some students have rows in both tables. 

<h3><strong><u>CLICK</u></strong></h3>

This can be represented by a Venn diagram where the left circle represents a group of students who appear in the math_grades table and the right circle represents the group of students who appear in the language_grades table. There's some overlap of these two circles, representing the subset of students who appear in both tables. There are 4 basic join types we'll talk about now. The data you would want to capture with each type of join is represented in blue. 

<h3><strong><u>CLICK</u></strong></h3>
Inner joins
<h3><strong><u>CLICK</u></strong></h3>
Left joins
<h3><strong><u>CLICK</u></strong></h3>
Right joins
<h3><strong><u>CLICK</u></strong></h3>
Full joins

We'll start with inner joins. 
<h3><strong><u>CLICK</u></strong></h3>

### `INNER JOIN`

Here, an `INNER JOIN` (and this is the default behavior of `JOIN` without any modifying words) finds matching grade data falling in the "Both Math and Language Grades" overlap section. This is often the data you want to capture, and if you're conducting research on the correlation between math and language grades, this is the join you want. If a student lacks one or the other grade, their data isn't useful to you, so you don't want it.

<h3><strong><u>CLICK</u></strong></h3>

The result of an inner join will be a table that only has rows of data for students who appear in both tables.  If a student is missing in one or the other table of grades, that student won't appear in your result set.

<h3><strong><u>CLICK</u></strong></h3>

An `INNER JOIN` shows up in code like this. Note that the word `JOIN` by itself means `INNER JOIN`-- you can use either in your code. 

<h3><strong><u>CLICK</u></strong></h3>

In fact it is important to remember that an inner join is the **default** behavior if you just use `JOIN`. Be certain that this is the type of join that you really want!

<h3><strong><u>CLICK</u></strong></h3>

### `LEFT JOIN`

Again, let's consider the left table to be **math\_grades** and the right table to be **language\_grades**.
A `LEFT JOIN` (or a `LEFT OUTER JOIN` as you'll sometimes see it) finds unmatched data in "Only Math Grades" -- that's the "outer" part on the left -- and also finds matching data in "Both Math and Language Grades" -- the overlap section.  It would exclude student data in the "Only Language Grades" section (which is on the right). Maybe you want this data because as the chair of the mathematics department, you want to see what students are strongest in math, and also in language if known, in order to select who to award a math prize to.  Perhaps you'll use language grades as a tie-breaker, for example?

<h3><strong><u>CLICK</u></strong></h3>

The result of a left join is a table which contains rows of data for students who only have math grades (and therefore appear in the left table) as well as rows of data for students who have math and language grades (and therefore appear in both tables), but no rows of data for students who only have language grades. When there is no matching data from the language table to join to the data from the math table, because the students don't have language grades, these cells in the table are empty, or `NULL`. 

<h3><strong><u>CLICK</u></strong></h3>

A `LEFT JOIN` shows up in code like this.  Note that one table is listed first, and is therefore on the left, and the other table is listed second, and is therefore on the right (because English is written left to right). Note that unlike an inner join, you'll always need to specify that you are using a left join (though depending on your preference, the "outer" is not necessary).

<h3><strong><u>CLICK</u></strong></h3>

### `RIGHT JOIN`

A `RIGHT JOIN` (or a `RIGHT OUTER JOIN`) finds unmatched data in "Only Language Grades" -- that's the "outer" part on the right of the Venn diagram -- and also finds matching data in "Both Math and Language Grades" -- the overlap section.  It would exclude student data in the "Only Math Grades" section (which is on the left). Maybe you want this data to create a graph of language grade distribution, and want to enrich it with some statistics about math grades where available, but it doesn't matter if some students lack math grades. 

<h3><strong><u>CLICK</u></strong></h3>

The result of a right join is a table which contains rows of data for students who only have language grades (and therefore appear in the right table) as well as rows of data for students who have language and math grades (and therefore appear in both tables), but no rows of data for students who only have math grades. When there is no matching data from the math table to join to the data from the language table, because the students don't have math grades, these cells in the table are empty, or `NULL`. 

<h3><strong><u>CLICK</u></strong></h3>

A `RIGHT JOIN` shows up in code like this.  Recall that "left" and "right" refer to the order in which the table names are typed in the `FROM` statement, and "math grades" is our left table and "language grades" is our right table.

<h3><strong><u>CLICK</u></strong></h3>

You might not see a lot of right joins "in the wild", and that's because many people who write SQL code simply prefer to use all left joins! It's simple preference, it's not correct or incorrect practice. Because "right" and "left" simply refer to the order in which the tables are written in the FROM statement, you can re-write a right join into a left join by switching the order of the tables in the FROM statement. That way, you choose whether you use a right or left join (and this is often a left join by convention.)

<h3><strong><u>CLICK</u></strong></h3>

### `FULL JOIN`

A `FULL JOIN` (or sometimes you'll see `FULL OUTER JOIN`) will consider all the data -- all of the outer, unmatched data on the right (language_grades) and left (math_grades) tables, as well as the inner overlapping data which has matching data from both tables. This kind of join is important if you want to create a grade book that shows student grades for each student, including their math grades and/or their language grades.  

<h3><strong><u>CLICK</u></strong></h3>

The result of a full join will be a table that has rows of data for students that have only math grades (and therefore appear only in the left table), students that have only language grades (and therefore appear only in the right table), and student that have both grades (and therefore appear in both tables). When there's no matching data from the one of the tables to join to the data you included from the other table, `NULL` values (empty cells) are added. When there is no matching data from one table to join to the data from the other table, because the student doesn't have grades for both subjects, these cells in the table are empty, or `NULL`. 

<h3><strong><u>CLICK</u></strong></h3>

A `FULL JOIN` shows up in code like this. You can specify `FULL OUTER JOIN`, but just `FULL JOIN` means the same thing; which you choose will come down to preference. 

<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 1: Join Types**

<h3><strong><u>TEAMS POLL</u></strong></h3>

Consider the scenario of a table of math grades for 9th grade students and a table of language grades for 9th grade students.  Some 9th graders appear in both tables, but some appear only in one of them.  Fatima appears in the math_grades table, but not in the language_grades table.  When you perform a full outer join on these two tables, what will happen to Fatima's data in the resulting joined table?

I'm going to give you a few minutes to answer this on your own, then we will talk about the answer together. 


ANSWER: 

In this case, Fatima's data will appear in the results, because regardless of whether the math_grades table was written on the left or the right, a full outer join includes both the left and right tables' data. Her math grade appears in the math_grades table, so that will appear, but since Fatima has no language grade in the language_grades table, she'll have empty cells with `NULL` values for any columns that come from the language_grades table.

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## Join Criteria

The second component of a SQL Join, which you will need regardless of the join type, is the set of conditions  by which rows from two different tables are said to "match", called join criteria. Join criteria will be some sort of relationship statement referencing data that occurs in both tables you want to join. This relationship statement will be valuated to TRUE or FALSE when your join is executed. 

<h3><strong><u>CLICK</u></strong></h3>

As a reminder, SQL is a **relational database**, so it's not surprising that we talk about data relationships here. If for example you had the two tables, "depression scale" and "subject address", you might want to match on the common field "subject ID". 

<h3><strong><u>CLICK</u></strong></h3>

Similarly, if you had the two tables "items" and "orders", you might want a subset of data from these two tables, but ony where the item ID is the same. 

<h3><strong><u>CLICK</u></strong></h3>

When the conditions in your join criteria evaluate as TRUE for a row then a join will be performed for those rows, and when the join criteria are evaluated as FALSE, no join for those rows will take place. Often, the relationship is equality, such as in the examples above -- you're looking for a perfect match between your two tables (though this is not always the case, as we'll see later).

<h3><strong><u>CLICK</u></strong></h3>

### Examples of Equality

Equality is the most frequently used condition for joins, when you are looking for "matches" between two tables. We've already seen a few general examples, but now let's look at some tables and how we might express our criteria in SQL. 

<h3><strong><u>CLICK</u></strong></h3>

Do you have subject identifiers or student ID numbers in two different tables?  This shared information can be used to join data from these tables, based on the identifier being equal.  

For example, if the subject ID matches, a row from table A and a row from table B will be joined.  If the subject ID doesn't match, these rows won't be joined.  Maybe we're trying to match lung cancer occurrence and smoking exposure in the same row. In the code, we usually use an `ON` statement to do this (though we can instead use a `USING`).

In this case, we're comparing the equality of two fields that **have the same name**, so we could also use **USING**.  This special word only applies when you're looking for a perfect match between fields that have matching names, too.  It's okay if you never use `USING` and prefer to always stick with `ON`, which is more multi-purpose. 

With either of the above code snippets (`ON` or `USING`): subject 3 from disease **matches** with subject 3 from smoking, subject 5 from disease **doesn't match** with anyone in smoking, subject 8 from disease **doesn't match** with anyone from smoking, subject 2 from smoking **doesn't match** with anyone from disease, and subject 4 from smoking **doesn't match** with anyone from disease 

<h3><strong><u>CLICK</u></strong></h3>

Sometimes the data that appears in the two tables has the same field name, as we just saw, but sometimes the data might be stored under different names. Here is an example in which the "same" data, "semester" in "math grades" and "term" in "language grades", is labeled differently between the two tables. Luckily, SQL can handle this. 

In this example, the A grade for Jan-May 2023 from math_grades **matches** with the B grade for Jan-May 2023 in language_grades (even though the student_id doesn't match!), and the C grade for Sep-Dec 2022 in language_grades **does not match** with any row in math_grades. 

This also highlights the importance of documenting your data so you can tell which fields hold which data in order to use them properly for joins!  If `semester` and `term` are  different things, not just the same thing with two different names, the result of your join will be disappointing. This also shows that figuring out your join criteria requires close attention: we probably don't mean to match student 11's math grades with student 14's language grades!

<h3><strong><u>CLICK</u></strong></h3>

### Non-Equality and More

Sometimes you don't need equality as your condition. Let's look again at our example from our multi-site mental health research, and let's say we want to associate a particular depression score with a particular address **only if the depression inventory was given between the start and end dates of residency at that address**.

<h3><strong><u>CLICK</u></strong></h3>

### Multiple conditions

Of course, in the example of the depression inventory, we'd also want to make sure that there was a match on subject identifier (you don't want to match Lakshmi's depression score with Larry's address, just because the dates worked!).  You can combine conditions too.  Here, we want to look for an exact match on subject ID **and** a date match that's between the correct dates.

<h3><strong><u>CLICK</u></strong></h3>

### Getting More Complicated

Let's keep thinking about our depression inventories and our goal of matching depression scores to addresses in our study. What if some addresses don't have end dates?  This could be because the subject is currently still living there. We can see in our data that there are some addresses with `NULL` end dates, so this is something we should account for.

You can create arbitrarily complex **boolean logic** (or **boolean algebra**), using AND, OR, NOT, and parentheses as needed.  Much as in math, there's an order of operations in this kind of logic, and you might need several sets of parentheses to make sure you're applying the conditions correctly.  For example, see below.  We've added comments to help illustrate the logic.

With this most recent join criteria: the depression score (dep\_total) for subject 11234, measured on 2021-05-15, **matches** with the address 123 Oak Lane for the same subject and time period, the depression score (dep\_total) for subject 11234, measured on 2021-05-15, will **not match** with the address 123 Main Street for the same subject, because the time period doesn't match, the other rows in the depression\_scale **don't match** with any rows in the subject\_address table, and the first and third rows of the subject\_address table **don't match** with any rows in the depression\_scale table. 

<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 2: Join Criteria**

True or False: a matching ID (like student\_id or patient\_id) is always sufficient as a join criterion.


<h3><strong><u>TEAMS POLL</u></strong></h3>


Answer: 

Often, a matching identifier is part of what makes up good join criteria, but it may not be sufficient on its own.  For example, consider trying to link patient diagnoses with medication orders.  Patients can appear dozens or hundreds of times across decades, so to correctly link diagnoses with medications, it's not sufficient to rely just on patient id.  You might need to use an "encounter id", a date range, or another join criteria to make sure you're matching data that really belongs together (instead of joining Mary's diagnosis of diaper rash when she was 3 months old to her prescription of Ritalin at age 9).

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

## Combining It All

Now, we'll get the chance to combine the two parts of SQL joins to craft some queries. We'll use `FROM` statements to describe the type of join and an `ON` statement to describe the join criteria. Don't worry, we'll add plenty of scaffolding in the beginning, and slowly work up to crafting an entire SQL query. 

Importantly, we will only present a few examples.  There are many combinations we could consider, at all levels of complexity, and we won't have time to cover all of the possibilities. Instead of being exhaustive, we've concentrated on the most frequent use case you'll encounter over and over: equality.  We'll go over each join type (inner, left, right, and full) on a simple equality matching a single field from each table.

<h3><strong><u>CLICK</u></strong></h3>


### 💫 **Your Turn 3: `INNER JOIN` and Equality Condition**

<h3><strong><u>SHARE LINK</u></strong></h3>

Your Turn 3: 


To understand what an `INNER JOIN` with equality looks and acts like practically, let's perform an inner join on these two tables.  To do this, we have to combine join criteria (subject\_id matching) with join type (inner). 

You are studying the link between lung cancer and smoking behavior. Let's perform an **inner join** on these two tables, matching on `subject_id`. (Remember, with an inner join, we only want subjects for which data are present in **both** tables). 

The join criteria is already written, but we need to add the join type. You'll need two table names separated by some kind of `JOIN` command.  For now, leave the `ON` statement unchanged. Think about what rows you expect to see in your result set before you run any code. When you want to see the results of your code, click on the "play" button below the code block. Return here when you're done and we'll do through the answer together. 


<h3><strong><u>COPY INTO CHAT</u></strong></h3>
Like this comment when you have completed "Your Turn 3: `INNER JOIN` and Equality Condition"

<h3><strong><u>MODIFY CODE</u></strong></h3>

Answer: 

```sql
SELECT *
FROM disease JOIN smoking
ON disease.subject_id = smoking.subject_id;
```

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>


### 💫 **Your Turn 4: `LEFT JOIN` and Equality Condition**

<h3><strong><u>SHARE LINK</u></strong></h3>

Your Turn 4:

Now's let's practice a left join. This time, you'll need to add both the `FROM` and the `ON` code sections to the SQL code. For now, use `ON`, and don't try `USING` just yet.

Now let's try a `LEFT JOIN`. We'll make **disease** the left table and **smoking** the right table, still matching on `subject_id`.

<h3><strong><u>COPY INTO CHAT</u></strong></h3>
Like this comment when you have completed "Your Turn 4: `LEFT JOIN` and Equality Condition"

<h3><strong><u>MODIFY CODE</u></strong></h3>

Answer: 

```sql
SELECT *
FROM disease LEFT JOIN smoking
ON disease.subject_id = smoking.subject_id;
```

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 5: `RIGHT JOIN` and Equality Condition**

<h3><strong><u>SHARE LINK</u></strong></h3>

Your Turn 5:

Let's try a right join next. This time, if you would like, you can try `USING` rather than `ON`, but note that in AlaSQL, you have to write `USING` without parentheses. 

<h3><strong><u>COPY INTO CHAT</u></strong></h3>

Like this comment when you have completed "Your Turn 5: `RIGHT JOIN` and Equality Condition"

<h3><strong><u>MODIFY CODE</u></strong></h3>

ANSWER: 

```sql
SELECT *
FROM disease RIGHT JOIN smoking
ON disease.subject_id = smoking.subject_id;
```

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

### 💫 **Your Turn 6: `FULL JOIN` and Equality Condition**

<h3><strong><u>SHARE LINK</u></strong></h3>

Your Turn 6:

Finally, let's try a full join. 

It is important to note that different SQL dialects have different quirks, and one of these is that AlaSQL **requires that you use `FULL OUTER JOIN` instead of just `FULL JOIN`.** That's not the case for every dialect of SQL, but here, please use `FULL OUTER JOIN`.

<h3><strong><u>COPY INTO CHAT</u></strong></h3>

Like this comment when you have completed "Your Turn 6: `FULL JOIN` and Equality Condition"

<h3><strong><u>MODIFY CODE</u></strong></h3>

ANSWER: 

```sql
SELECT *
FROM disease FULL OUTER JOIN smoking
ON disease.subject_id = smoking.subject_id;
```

<h3><strong><u>QUESTIONS?</u></strong></h3>
<h3><strong><u>CLICK</u></strong></h3>

