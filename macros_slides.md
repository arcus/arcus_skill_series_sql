<!--

author:   DART Team
email:    dart@chop.edu
version:  0.0.0
current_version_description: Initial version.
language: en
narrator: UK English Female
title: Macros for slides
comment:  This is placeholder module to save macros used in when creating slide decks.

@version_history 
No previous versions.
@end

@onload: window.LIA.settings.sound = false

big: <b style="font-size: 1.25em;">@0</b>
center: <div style="text-align: center;">@0</div>
colorhighlight: <b style="font-size: 1.15em; background-color: rgba(var(--color-highlight), .2);">@0</b>

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

@onramp_slide

**Do you have an Arcus Lab, or are you thinking about starting one?**

Get hands-on practice working with real patient data in an Arcus On-Ramp workshop!


<div style = "align-items: center; display: flex;">
<div style = "margin: 1rem; max-width: 25%; float:left; padding-right:4em;">![""](../media/onramp-Logo.png)
</div>
<div style = "margin: 1rem auto; max-width: 70%; float:left;">


<ul>
  <li>Arcus On-Ramp: Build your SQL Query</li>
  <li>Arcus On-Ramp: Analysis in R</li>
  <li>Arcus On-Ramp: Analysis in Python </li>
</ul>

</div>
</div>

[See available dates and sign up for an Arcus On-Ramp workshop](https://arcus.chop.edu/education/webinar-signup). The next SQL On-Ramp is **Nov 20th**.

@end

@todays_talk
@big(@title)

@learning_objectives
@end

@about_these_slides

These slides were created with [LiaScript](https://liascript.github.io/), an open source markdown parser for writing educational content.

All of the speaker notes from today's talk are saved in [the slides themselves](https://liascript.github.io/course/?https://raw.githubusercontent.com/arcus/arcus_skill_series_sql/main/database_normalization/database_normalization.md#1) -- try changing the view to Textbook and it will integrate the text from the notes into the slides themselves, or turn on the sound at the bottom to hear the notes read out loud as you go through. 

<div style = "align-items: center; display: flex;">
<div style = "margin-left: 10%; max-width: 25%; float:left; border-style: solid; border-color: rgba(var(--color-highlight));">
![Screenshot showing the upper right menus on a liascript page with the mode menu open and Textbook highlighted.](../media/liascript_mode.png)
</div>
<div style = "margin-right: 10%; max-width: 25%; float:right; border-style: solid; border-color: rgba(var(--color-highlight));">
![Screenshot showing the sound buttons at the bottom of a liascript page with the speaker button highlighted.](../media/liascript_sound.png)
</div>
</div>

The content from this talk is also available as a self-paced interactive tutorial: @module_link 

For all of the files and information from this talk, go to our @repo_link 

@end

@teams_polls 

@big(Today's presentation will include interactive content!)

The best way to learn is to practice!

When we reach 💫 **Your Turn** sections, test your knowledge and respond in the Teams poll or the chat section.
Then we'll discuss the answer together.

@end
-->
# Macros for slides

