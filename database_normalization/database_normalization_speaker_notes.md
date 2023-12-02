## Slide 1: Database Normalization

Welcome everyone! 

I’m Joy Payton and I use she/her pronouns. 

I’m a data science educator with the Arcus project in DBHI, the Department of Biomedical and Health Informatics. 

Today’s talk is the second in a series of talks about “sequel”, S-Q-L, that we’ll be offering over the next several months.
We’re going to be recording today’s webinar, so please leave your cameras and mics turned off until the question time at the end.

We’ll give some time with the recording turned off, so that you can ask questions and not worry about being recorded. If you do have questions that come up during the talk, please feel free to put them in the chat, and I’ll keep an eye on the chat to see what comes up.

With that let’s get started!

## Slide 2: Today's talk

Today in our webinar, we will be talking about why SQL data is structured in interrelated tables, and why that is both useful and can be a bit challenging for newcomers to SQL. 

We will not be doing any hands-on coding with SQL today. However, in future sessions in this series, that **will** be available to you.

After this session, we believe that you will be able to do the following three things:

You will be able to explain the significance of one-to-many data relationships, and how these relationships affect data organization.

You will be able to describe how a normalized database is typically organized (and don’t worry if the phrase “normalized database” is foreign to you, we will talk about that!)

And finally we believe you will be able to explain how data can be linked between tables, and in so doing, be able to define “primary keys” and “foreign keys”.

## Slide 3: Thank you!

Now, it feels weird to thank myself as the author of the module that this talk is based on, but I do think it’s important to acknowledge authors.  

And of course we also want to express gratitude to NIH for funding our data education efforts in our R25 grant, which is the project that gave rise to the source materials we will be using throughout these series for the next few months.

## Slide 4: Learn by doing

Today’s presentation will include interactive content. We are firm believers that the best way to learn is to **practice**, so I’m going to ask you to be active learners today. 

We will not have any hands-on coding practice today, but we will have short quizzes that come up to help you check your understanding.

And I’ll also ask you to contribute your thinking about some questions I’m going to pose by typing into chat.  I will warn you ahead of time that I’m about to ask for your participation, and I really encourage you to make the best use of your time and jump in and participate.

## Slide 5: Quick Review

Let’s do a little short review of last month’s topic. Last month's topic was “Demystifying SQL”, which was a brief introduction to what SQL is for people who have never heard of it or who have heard of it but know very little about it. 

I’m not going to go in depth in reviewing last month's session. 

[If available: I will include a link to the recording of last month’s session so you can watch this on your own if you choose.]

In terms of review, I want to hit on three main takeaways from our first topic from November, and they are as follows:

First, S-Q-L or “sequel”, and you can say it either way, SQL stands for “structured query language” and it is a language used to request data –  to make queries –  from a relational database. What is a relational database?

The next bullet point speaks to that!  Relational databases are ways that we organize data in tables that are interrelated.  There might be, for example, a subject ID that appears in several different tables, and that shows the relationship between those tables, and that’s what makes a database a **relational** database.

And finally, tables have columns –  and sometimes we call those fields –  and tables also have rows.

That’s what we went over last month. Again, in this session today, we’re going to talk about how data is organized in these relational databases and why it is that you have to use multiple tables – not just one table, but multiple tables –  for just about everything interesting you want to do with data from a database.

Often you have to combine data from two or more tables to get the information you need for your work, and this can be frustrating if you are accustomed to getting a CSV for analysis.  If one spreadsheet, one table, is what you’re accustomed to working with, having more than one table to deal with can be annoying!  Therefore, I want to start by giving a use case that illustrates why getting data from multiple tables is important, and then we'll talk about why it's not practical to store medical data in a single table.

## Slide 6: Multiple Tables

Let’s start with a use case that explains this situation.  In the example on your screen, consider the case where you have data about depression. You are studying depression in research subjects who live in different areas, and you have lots of tables of data, but we’re just showing a sample.  

One of these tables holds depression scores for subjects. This looks like it is a four question psychometric scale, with a total depression score, in a table that is called “depression scale”. 

Then we have a different table that holds subject addresses.

I’m going to ask for your participation now.

Let’s posit that your hypothesis is that people who live in certain ZIP Codes – maybe ZIP Codes that experience more socioeconomic challenges – those folks have higher rates of depression.   

If you had this hypothesis, that ZIP Code was linked to depression, which columns would you need to look at in each of these tables?  When you have an idea of what you think you would want to look at in each table, share that in chat.

[Respond appropriately, e.g., OK great I see some good answers here, some thoughtful answers about what data you would need.]

I would argue that to see if your hypothesis has evidence to back it, you need to combine data from two tables.  From the depression scale, table, you would need the subject ID and the depression total score. And then from the addresses table, you would need the subject ID and the ZIP Code.  That’s the data that you would need to analyze to see if your hypothesis about ZIP Codes affecting depression is supported by the evidence.

## Slide 7: Multiple Tables

What you might want to eventually end up with would be a single table of results that might just have three columns, the subject ID the depression total score might be a second column, and the third column could be ZIP Code And that way you have all your data in one place and you can look at the relationship between depression, score and ZIP Code.

You may be asking yourself, and you may have asked yourself in the past when you’ve requested data, “why don’t the people who are collecting this data or the people designing the database just put all of the information about each patient (or each research subject, or each sample or each animal model) –  why don’t they put all of that information together in one table to start with?”

After all, getting one row per subject is how we usually prepare for applying statistical tests, so it would be great if we could just **start** with one row per patient or one row per research subject with everything we need across the columns.  If we started with that, we would be ready to jump into the science, and we would not have to do so much data preparation work. 

So why isn’t it that way when you work with databases?

The reason why this usually doesn’t happen in a database and instead see lots of different tables that you have to pull data from and join together is because of a concept known as **normalization**, and to explain normalization, we will first need to talk about **one-to-many data relationships**.

## Slide 8: One-to-Many

Medicine often has one-to-many data relationships.

What does one-to-many mean?  I think the best way may be to consider a couple of use cases.

Consider a hospital and a retail website.  Each organization has one-to-many data relationships.

In a hospital, for example, one patient has multiple encounters on different dates.  One encounter may include multiple orders for different procedures or medications. One medication order can give rise to multiple medication administrations…. and you can probably think of a lot more examples of one-to-many data relationships in medicine.

Or in a retail website, one customer may have several associated addresses – for shipping, or billing, or both. One customer will probably have multiple orders, and each order can have one or many associated items in that order.

A one-to-many data relationship is one in which one X is related to more than one Y, and these can be very hard to accommodate in a single table with all of the data included.

Let’s exercise our imagination a little bit.

Imagine that for an online store, you tried to construct a table of order information in which a single row represented an order.  Each order is one row, and in that row you want to include every single item included in that order.  

Maybe you start with five columns:  item one, item two, item three, item four, item five.  But there will be people that have more than five items in their order! 

So maybe you have 100 columns for the first item in the order, the second, the third, etc., all the way to the 99th and the 100th. But then maybe somebody orders 110 items!  What do we do with that?  It’s hard to know how many columns to provision to begin with.  

Also, many times, orders are much smaller. Many orders will just be one or two items, so they’re not taking advantage of all of those empty cells for those hundred columns that you created.  That’s not an efficient way to store data!

## Slide 9: Quiz: One-to-Many

Let’s pause here. I am going to ask for your participation and bring up a poll in teams, and I’d like to ask you which of the following relationships are likely to be one to many relationships.  There is more than one correct answer.   Please give that a read, and tell me what you think!

[Respond appropriately, e.g.:  All right, thank you so much for your participation. A lot of you are exactly right, I see a good pattern of responses here.]

So, we hope that any gym member will have more than one recorded work out. That’s the goal anyway!  Therefore, that relationship is one-to-many.

However, a particular street address will only be related to a single latitude and longitude, so that is not a one-to-many relationship. That is a one-to-one relationship.

A patient can have multiple providers, so that’s one-to-many, and providers certainly have many patients so that’s also one-to-many.  In fact, you could really call the relationship between patient and provider many-to-many.

And finally, this is a little silly, but we would argue that a baseball team should have at most one mascot, not multiple, so that is a one-to-one relationship, not a one one-to-many relationship.

## Slide 10: One-to-Many Data in Medicine

Let’s again consider the data from our fictional multisite research study on mental health, and I’m going to ask for your participation here.  Take a moment and notice where are there one-to-many relationships in this data.  Type what you see in terms of these one-to-many relationships into the chat.

[Respond appropriately, e.g.:  Great you guys got it!]

We see that the subject with the identifier 86234 has two different administrations of the depression inventory on two different dates, and the subject with the identifier 11234 has two different addresses for two different date ranges.

This kind of repetition is not unrealistic in research and in medicine. Our patients and our research subjects might retake psychometric surveys, and they certainly move to new addresses.
Now let’s take a moment to consider how the one to many relationships make it really hard to try to smush data together in a single table.  We can start with combining the data in two tables.  

## Slide 11: Row Repetition Woes

If you were to try to combine, let’s say, demographic data and depression scale data into one table, you’d start to run into some issues related to the efficient storage of data and data repetition.  Take a few moments, and maybe even grab a pencil and paper, to draw up what you think the combined table might look like. 

How many columns would it have?  How many rows?  

Please think about if any of the one-to-many data relationships here might mean that we end up repeating ourselves when we combine these two tables into one!  I'll pause here to allow you to think about that!

OK, now let's go to what I think the combined data might look like.

## Slide 12: Row Repetition Woes

One of the things that you’re going to encounter is that the demographic data for a given subject is **the same** for each time they take the depression inventory.  That is, their date of birth doesn’t change, their sex doesn’t change, and their race doesn’t change from the first to the second to the third to the fourth Instance that they take the depression inventory.
Is there duplicated data in this table?  Yes!

Here it doesn’t look that bad, it’s just subject 86234 who has repeated demographic data, but in a more realistic table, you might have many more rows of repeated data.  

For a given subject, you might have have four or five or 10 rows in which the demographic data is repeated. That’s a lot of data repetition.  That takes up space, and it can be tricky because if we realize that there’s an error in the date of birth then we have to find **all of the rows** that that date of birth appears on and correct it, and it could be easy to accidentally miss one.

We also have rows with partial data.  We have a subject here, 93452, for whom we have demographic information, but who lacks a depression screening, and that means some empty cells.  That’s not a huge deal, but it is a bit inefficient.

## Slide 13: A Column Conundrum

Often, however, people would like *all* the data on a given patient or a given research subject all in a single row.  That’s even more complicated!  Let’s say that there are three tables that you asked to combine: demographics, depression scale, and subject addresses. 

I’m going to ask for your participation, so take a moment and try to imagine how you would respond if you were working with a colleague or a supervisor who asked you to combine *all* the data you see here such that each research subject has one and only one row in the final table.

Type into chat some of the problems you foresee, or some of the questions you might ask.  I'll pause to let you try to sketch out or imagine how you might combine all of this data into a table that had one row per subject, with all of the information we know about that subject enclosed in that row.

[Respond appropriately, like: Yes, these are some good points you’re all making!]

In this case, we know that our subjects can have more than one address.  So how do we accommodate our subjects with more than one address, if we want to put everything about that subject in one row? We’re going to need more columns to account for multiple addresses.  Maybe we could have two sets of columns for addresses, like street address one and city one, street address two and city two, and so on.

But this is a longitudinal study, so people might move three times, or even 10 times! Who knows? Do we need to add 10 sets of address columns to make sure that we get all possible addresses included?

It’s hard to know ahead of time how many columns we would need.
And the same problem emerges when we have multiple administrations of the depression inventory. What if some people take the depression inventory five times? 

Keep in mind the depression inventory is four questions and a total, so that’s five columns for each instance of the depression inventory.  Are we going to repeat those five columns 5 or 10 times so that we have enough columns to allow for multiple retakes?  This is a huge issue!

If we try to combine data that can repeat into a one row per subject model, we do not know how many columns to create.

## Slide 14: One Table? Not a Good Idea!

In short, I hope I’ve managed to convince you here that if we take all the data that we know about someone and we try and force all of that data into a single table, we have a lot of problems. 

We have a problem of potential data repetition where we have the same information repeating row after row after row, and, depending on how we organize our data, we may also have the problem of an unpredictable number of columns.

These problems makes it tricky to maintain data and correct any errors, and it can make analysis very hard.  We’re much better off collecting various groups of facts about our patients, or our research subjects, or our animal models into distinct, separate tables.   

You may have seen in the past things like a demographics table, an address table, a procedures table, a diagnosis table, and so on.  In each of these tables we’ll have an ID column, such as a subject, ID or patient ID that would allow us to link the rows from different tables to one another and understand who we’re talking about.

This is the core of normalization – dividing data into tables that each represent a specific concept.  The concept of demographics, the concept of address, the concept of procedure…  when data is normalized, we organize the data into tables in such a way that we reduce needless data duplication, we reduce unpredictability of not knowing how many columns we’re going to need, and we reduce the number of empty cells and waste in our data.

## Slide 15: Normalization

On your screen now you’re going to see a little bit of behind the scenes that gives more information, but only if you’re extra interested in this topic.  For most of us, we do not need this level of detail, but I wanted to add some context here for people who want to do some deeper learning on their own.

In short, normalization is a complex information science topic, and there are various levels of normalization that can be performed.  Here we will not go into details about these various forms of normalization. We’re just going to talk about what normalization **looks like** more than what it **is** in information science terms. You do not need to remember that there are different kinds of normalization. This is just extra information for those of you who want to go deeper.

In a normalized database, we separate data into tables, and these tables represent different logical **concepts** or **entities** like address, procedure, medication, patient, device, etc.

We tend to only include in these tables the data elements that have a single value that is relatively stable.  

For instance, for a particular medication, the generic name is not likely to change very often if at all.  In the case of a device, a device probably has just one barcode sticker on it and it’s not going to change very often.  A patient date of birth should be singular and unchanging.  A medical procedure will have one billing code associated with it, and again, that will change very frequently. 

Those singular, stable elements are usually the kind of things that go in these entity tables.  

We may exclude things from entity tables that can have multiple values or change frequently.  So for example, we probably would not have the the name of the insurance company providing coverage for a patient in the patient table right because patients will change their insurance or have multiple carriers.  That concept, of insurance carrier, doesn’t adhere to patients strongly – it can change a lot.  

Therefore, in the patient table we’re really going to only include things that are really closely adhering to the patient themselves, not accidental things that can change.

In these entity tables, whether it’s a device table or a patient table or a procedure table, we give each of the instances, each device, or patient, or procedure, a unique identifier.  It would be something like device ID or medication ID or patient ID or provider ID.

## Slide 16: Primary Keys and IDS

So far, we know we have tables that describe entities like “medication” or “patient”, and each of these tables has an ID associated that uniquely identifies each example of this entity – each medication, or each patient.  A unique ID like this that can only occur once in a table is a primary key.

And that’s a vocabulary alert!

A primary key is an identifier that is linked to one and only one row in an entity table.  For example, the patient ID.  A given patient ID links to one and only one patient.

A medication ID adheres to one and only one medication.

For those of you who are already using SQL it’s helpful to know that if you define an identifier as a primary key, SQL will enforce this. It will not allow you to add a new row with the same ID.  For example, if you’ve said hey, the field called patient_id is a primary key, SQL will not let you accidentally give the same ID to a new patient once that ID has already been assigned to someone.  If it’s a primary key, that ID should only occur once in the patient table, and can’t be added a second time.

In the table you see on your screen, you can see that this is a medication table, and there is a primary key, which is indicated with the letters PK. Lot of SQL systems will indicate that an identifier is a primary key with either a special symbol like a little icon of a key, or the letters PK for primary key. 

Because med_id is a primary key, we know that medication 123 can only occur one time in the whole table and in this case it’s Motrin. No other medication can be added with that same medication ID. 

## Slide 17: Interactions: How do Entities Interact?

Once we have tables representing our various entities, we then make tables that represent the interactions between entities. 

For example, interactions between patients, providers, and medications might be stored in a table called medication_orders. This table will record this interaction between a patient, provider, and medication, including the ID numbers of the entities involved along with other data like the date of the interaction and other details. 

For example, medication_orders might include a field that holds the patient ID who is to receive the order, a field for the medication ID being ordered, a field for the provider ID who placed the order, the date and time of the medication order, and other important details.

Whether these tables of interactions have primary keys and their own identifiers depends, but they often will.  For example, our "medication\_order" table has a primary key called "med\_order\_id", which uniquely identifies this particular interaction with this patient, this provider, and this medication, on this day. 

I'm now going to invite your participation.  In chat, tell me what you think: is the pat\_id in this table a primary key?  Why or why not?  

[Respond appropriately here, e.g.: Yes, that's right, there is repetition...]

The same patient might get have more than one medication order, and we need to allow for the patient id to repeat, so the pat\_id is **not** a primary key in this table.  Now, in the patient table, where each patient appears once and only once, the pat\_id **will** be a primary key.  Again, I'm going to ask you to tell me in chat. Is med\_id a primary key?

[Respond appropriately, e.g.: Oh, we have some difference of opinion on this one!]

While in this case, in the rows we see, there's no duplication, the fact is that ibuprofen gets ordered many times a day, and so does klonopin, and prozac, and cipro, and any number of medications.  Medications need to be able to repeat in the medication order table, so med\_id won't be a primary key in this table.  Now, back in the medication table, where each medication is listed once and only once, med\_id **will** in fact be a primary key.

Similarly, if we consider a provider, Dr. Smith, she'll be prescribing multiple medications in any given day during her work as a hospitalist. The provider id needs to repeat, so it's also not a primary keys. Instead, these IDs are references to other tables, and they are called foreign keys.  

Foreign here means "originating in a different place than here."  

The pat\_id is a foreign key in the medication\_order table, and it originated in the patient table.  The med\_id is a foreign key in the medication\_order table, and it originated in the medications table.

## Slide 18: Entity Relationships

We can depict the relationships between tables, and indicate primary and foreign keys, using an entity relationship diagram.  

If this kind of diagram helps you, great!  If this is more confusing than it is helpful, you can just ignore this slide. 

What we see here is the depiction of four tables.  At the top you see patient, medication, and provider.  Each of these entities is linked to, or has a relationship with, the table called medication\_order, which is an interaction between these three entities.  

You can see that the pat\_id is a primary key in the patient table, but appears as well as a reference in the medication\_order table, where it's a foreign key.  Similarly, the med\_id and provider\_id are primary keys in their originating tables, and they are foreign keys in the table that uses them as references.  

## Slide 19: Why Bother With Normalization?

All of this may seem very complicated, so I want to go back to another example to show why organizing data in a normalized way is helpful. Consider the following example of a typographical error in a database.  

When they set up the point of sale system at the supermarket, someone misspelled “orange juice”, and now we want to correct that error.  On this slide, we have a single table representation of orders at a supermarket. This is the non-normalized way of organizing the data, trying to get everything on a single row. That’s why we have 50 columns, only a few of which are shown, to allow for many items in any given order.  

In this non-normalized database table, consider what you would have to do here to fix the misspelling of orange juice.  How many places might the misspelled phrase appear?  Which columns could the typo exist in?  How many rows might the typo appear in?

## Slide 20: Why Bother With Normalization?

And here we have an alternate way of organizing the data. This is a normalized approach. We have an items table, which is an entity table, and it lists all the different items for sale at our supermarket.  Then we have an interaction table that shows the interaction between orders and items.

Consider what you would have to do in this normalized data organization style to fix the spelling of orange juice. 

Is it easier to correct the misspelling with the data stored in one single table or with the data in two tables in a normalized fashion?

[Respond appropriately to anything in chat]

Well, in the one-table option, we have to look for the typo anywhere in 50 columns across every single row … and keep in mind, there could be thousands of orders here!

In the two table option, we only have to find the misspelling once.  We will look in a single column, the column called item_ name.

And there we know that that item will occur only once: notice again in this display we have the PK indicating that item ID is a primary key which means that this item ID will not repeat. 
I’d like to pause here to look at chat and see if there are any questions so far.

To sum up where we are at this point, the theory of how to organize data for speed and efficiency is complex. However, it’s enough for now to understand that data in relational databases are fragmented into various tables using a process, called normalization.

Normalization helps reduce needless repetition, it simplifies data, and it improves system speed and performance.

## Slide 21: Quiz: Normalization

Time for another quiz. I’ll open up the poll on Teams, and I’d like to invite you to participate.  Again, there is more than one possible correct answer here.

Please read the question and respond!

[React accordingly, e.g.: Great! I feel like people are really understanding what we’re trying to teach here today.]

The reason for normalization is **not** that relational database software lacks the capacity for very wide tables with lots of columns. Rather, the kind of rich data that is stored in relational databases simply isn’t right for storage in a single table. There are many one-to-many relationships in data, and this means that using multiple tables, one for each kind of concept like address, or order, or encounter, makes sense.  

After all, there’s a lot of repetition in data. For example multiple patients might live at the same address, and multiple patients are prescribed the same medication. These complex one-to-many relationships mean that it’s much harder to correct or change data if we try to put as much data as possible into a single table. 

However, when a normalized model is used, and data is fragmented into concepts, things actually get easier.  Instead of correcting a product name thousands of times, once for each order that that product appears in, we only have to correct it once in the product table.

## Slide 22: Key Vocabulary

OK, let's add a bit more vocabulary here by adding the term "join keys".  I don't often simply read slides aloud, but that's what we'll do here.

Fields that appear in two or more tables within a database are also sometimes called **join keys**, because they can be used to join data from the two tables into one set of interrelated data.  

Two categories of join keys are **primary keys** (unique within a table) and **foreign keys** (not unique, but come from -- and can be traced back to -- tables in which they **are** a primary key).

It can be useful to know that the phrases "primary key" and "foreign key" originated in SQL, and if you use SQL, you need to learn them.  However, the concepts are useful in other situations and you might hear these terms used (less strictly and precisely) outside of relational databases.  "Let's use the student ID as the primary key," might be suggested, for example, even when the data is stored in .csv files, not in a SQL database. 

## Slide 23: Quiz: Keys

OK, so here's another quiz question.  I'll bring up the poll in Teams, and when you're ready, let me know what you think the correct answer or answers are.

[Respond appropriately, e.g. "great job"]

Which of the fields in this table is likely to be a primary key?  That's right, it's procedure\_id!

Because this table is about procedures, and there's an identifier that looks like it uniquely identifies each of these interactions, we can guess that "procedure\_id" is probably a primary key.  On the other hand, we know for sure that "date" and "provider\_id" can't be primary keys, because they have repeating values.  That makes sense -- the same provider can conduct many different procedure, and on any given **date**, there are likely to be many procedures.  By that same logic, we also know that "patient\_id" can't be a primary key... it needs to be possible for a patient to have more than one procedure!

## Slide 24: Quiz: Keys

OK, so here's a second quiz question about the same data.  I'll bring up the poll in Teams, and when you're ready, let me know what you think the correct answer or answers are.

[Respond appropriately, e.g. "great job"]

The correct answers here are patient\_id and provider\_id.  A foreign key is an identifier that originates in another table.  It certainly seems likely that there is a "patient" table and a "provider" table that the "patient\_id" and "provider\_id", respectively, originated in.  These are the two foreign keys.  The "procedure\_id" seems to originate here, in the "procedure" table, so it's not a foreign key, and the "date" just seems like, well, a date, not an identifier at all!

## Slide 25: Review

Again, I'm just going to read this slide aloud as a review.
**Normalization** breaks up data into tables that represent **entities** and tables that represent **interactions** between entities.  Data is organized in a way such that the number of columns is predictable and data repetition is avoided (well, except for IDs themselves, which end up getting repeated a lot!)

**Entities** are logical concepts like "patient" or "medication", each of which has specific aspects that adhere closely to that entity, like patient date of birth or medication class.

A **primary key** is an identifier that contains a unique value for each row in your table.  For example, the "item\_id" is a primary key for the "items" table in our supermarket example.  There will be no repeats of the "item\_id" in the "items" table.

A **foreign key** is an identifier in a table that makes reference to an identifier that originated in some other table and is a primary key there.  For example, in our "order\_items" table earlier, we had a column called "item\_id", which contained numbers that corresponded to the "item\_id" column in the "items" table. 

Together, **primary keys** and **foreign keys** are called **join keys**.

Finally, an **entity relationship diagram** is an illustration of how different tables in a relational database are related.  These diagrams often include details about join keys (primary and foreign keys).

## Slide 26: Additional Resources

And here are a couple of additional resources, and I'll add those links to chat, in case you're interested!

## Slide 27: Upcoming sessions

If you liked these talks, we have more coming!  I'll add the link to where you can sign up for all of these talks to the chat now.

## Slide 28: About these slides

These slides were created with LiaScript, an open source markdown parser for writing educational content.

All of the speaker notes from today's talk are saved in the slides themselves -- try changing the view to Textbook and it will integrate the text from the notes into the slides themselves, or turn on the sound at the bottom to hear the notes read out loud as you go through.

The content from this talk is also available as an online self-paced tutorial.

For all of the files and information from this talk, go to our GitHub repository for these materials.

I'll add the link to these slides in the chat!

I'll also now turn off recording and we can start a Q&A Session.  Thanks everyone!