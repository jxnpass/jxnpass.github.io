---
title: Exploring Isaiah's Legacy in the Book of Mormon - EDA and Dashboard
description: The words of the biblical prophet Isaiah influenced over 35% of the Book of Mormon! This post utilizes generated data and illustrates the impact of Isaiah on the Book of Mormon using cross refeerences, textual similarities, and Bible language. 
layout: post

github:
    is_project_page: true
    repository_name: Isaiah-to-BOM
    repository_url: https://github.com/jxnpass/Isaiah-to-BoM

date: 2023-12-5 17:50:00
---

## Table of Contents

- [Synopsis](#synopsis)
- [EDA](#eda)
- [Graphical Evaluation](#graphical-evaluation)
- [Networks](#cross-reference-networks)
- [Dashboard](#dashboard)
- [Acknowledgements](#acknowledgements-and-ethical-considerations)

## Synopsis

The Holy Bible is one of the most revered and consistently read texts in the entire world. The complexities of biblical histories, from religious themes and worship, languages, and to major societal events, fascinate scholars today. However, what is commonly overlooked is the connections between the Bible and the Book of Mormon. In the narrative beginning of the Book of Mormon, the record opens with a family commanded by God to leave their home in Jerusalem, escape the impending doom of the Babylonian Exile, and start a new civilization in the modern-day Americas. One of the belongings of this family was a record written on brass plates, which contains the biblical prophets and narratives from the five books of Moses and the words of the Old Testament prophets up to Jeremiah. One of the most commonly referenced prophets made by Book of Mormon characters is Isaiah, in which his words, themes, and doctrines [consist about 35% of the Book of Mormon](https://www.churchofjesuschrist.org/study/manual/old-testament-student-manual-kings-malachi/enrichment-e?lang=eng).

The prophet Isaiah is heavily revered for Book of Mormon peoples, and their writers and preachers regularly recite from the 66 chapters we have today. However, modern scholars have stated that the authorship of the book of Isaiah is not solely written by the prophet: numerous arguments cirulated stating that Isaiah's disciples had written chapters 40-66, and Isaiah himself had only contributed chapters 1-39. This claim has validity since the second half is written after the Babylonian Exile (597 to 538 BCE), which was over a hundred years after Isaiah had passed on. The Book of Mormon family left Jerusalem around 600 BCE. This leads to the following question: how could Book of Mormon civilizations have the entire account of Isaiah in the brass plates if the latter half of the Book of Isaiah wasn't written until after 597 BCE? 

Multiple scholarly interpretations have debated these concerns. One assertion is that the book of Isaiah was written wholly by the prophet himself, and disciples later edited it to be in its current format. Others speculate the possibility of divine intervention as the writings of Isaiah and the Book of Mormon went through translations. 

The aim of this post and the [data collection post](/_posts/2023-12-5-IsaiahToBOM-DC.md) is not directed to discuss this concern in great detail, but to illuminate the breadth of Isaiah's writing using visualization and statistics, accounting for these common scholarly perspectives. We will also look into cross reference levels of similarities, subdivisions of Isaiah using [Bernhard Duhm's classifications](https://en.wikipedia.org/wiki/Book_of_Isaiah), presence of biblical terms, and summaries of words, verses, and chapters between authors. This project intends to promote a detailed understanding of the scriptures by visualizing complexities that are otherwise incomprehensible. 

## EDA

There are three areas whereby we can scope our exploration:
1. Where in Isaiah does the Book of Mormon most refer to?
2. Where in the Book of Mormon is Isaiah heavily referenced?
3. How much is biblical language utilized in Isaiah and the Book of Mormon?
4. Where do textual differences occur between Duhm's Classifications and the Book of Mormon?

### Summary Description of the Dataset

More info about the data can be found on [data collection post](/_posts/2023-12-5-IsaiahToBOM-DC.md), but here is a brief description to get started:

Duhms Category: [Bernhard Duhm](https://en.wikipedia.org/wiki/Book_of_Isaiah) uses varying structures and models to break up and explain the chronological and thematic differences in Isaiah. In this project, we used the threefold structure to identify them:
- Proto-Isaiah lists chapters 1-39 (742-687 BCE). It encompasses the stories and words of Isaiah in 8th-century BCE, where he narrates certain events like his call to prophethood, the Syro-Ephramite war, and the rise of the rightoeus king Hezekiah.
- Deutero-Isaiah lists chapters 40-55 (597-538 BCE). This is believed to originate from the work of an anonymous 6th-century acolyte of Isaiah, written during the time of the Babylonian exile. 
- Proto-Isaiah lists chapters 56-66 (after 538 BCE). This was mainly composed after the Exile and the Jews' return to Jerusalem.

Reference Type: I used a language processing library from python to calculate text similarities between the determined references. The scores calculated ranged from 0 to 1. I categorized it based on the score:
- Direct Quote: .75 to 1
- Shared Language: .25 to .75
- Similar Theme: 0 to .25




### Locations in Isaiah

A viable method to chart cross references throughout Isaiah is by utilizing a bar chart. The following graph counts the number of times a verse from the chapter is used in the Book of Mormon, whether that be a verses that directly quotes, shares language, or has a similar theme to Isaiah.  

![Isaiah-References](/assets/Isaiah-to-BOM/graphics/ref_count_ISH.png)

And a simplified version looking at the Duhm's category. 

![Duhms-References](/assets/Isaiah-to-BOM/graphics/ref_count_DUHMS.png)

Ultimately, we see that Isaiah 2-14 and 48-55 are heavily quoted, but Isaiannic language and themes are pulled from throughout the text. It is important to note, however, that based on the [linguistic data](http://www.creationismonline.com/Mormons/KJV_Verses.pdf) I scraped, a reference does not mean that the Book of Mormon author meant to directly pull doctrine or words from Isaiah, rather, modern-day scholars found a thematic or language connection between them. 

### Locations in the Book of Mormon





### Biblical Language



### Textual Differences

Recall that the Book of Mormon narrative begins in 600 BCE, when Lehi's family left Jerusalem. This brings up an interesting concern: how could Book of Mormon civilizations have the entire account of Isaiah in the brass plates if the latter half of the Book of Isaiah wasn't written until after 597 BCE? This means that only Proto-Isaiah could have been written before then. Deutero-Isaiah, however, is often quoted, as we'll see later.

Certain theories provide solutions to justify this chronological discrepancy. The most convincing inference about the Isaiah problem is arguing for the sole authorship of the book of Isaiah. Meaning, Isaiah wrote Proto, Deutero, and Trito Isaiah in one writing, and the latter two sections were written as lengthy prophecies. This viewpoint would require, however, that the writing is similar across the three sections. 

Performing the linguistic analyses of the textual differences between the three sections are beyond the scope of this project, as this post aims to illustrate how Isaiah is referenced in the Book of Mormon in general. However, we can look at a glance how the words change. 

Since we've seen so many bar charts, I figured I'd switch it up and use some wordclouds!

![ISH-WordCloud](/assets/Isaiah-to-BOM/graphics/wordcloud_DUHMS.png)

<p align="center">
    <img src="/assets/Isaiah-to-BOM/graphics/wordcloud_BOM.png" alt="image" width="50%" height="auto">
</p>





<!-- ![BOM-WordCloud](/assets/Isaiah-to-BOM/graphics/wordcloud_BOM.png) -->


<!-- Isaiah Summary  -->



![Duhms-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_DUHMS.png)

<!-- Book of Mormon Summary  -->

![BoM-References](/assets/Isaiah-to-BOM/graphics/ref_count_BOM.png)
![BoM-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_BOM.png)

<!-- Comparison -->

![BoM-ISH-BibleDictionary](/assets/Isaiah-to-BOM/graphics/bd_comp.png)


### Cross Reference Networks

[By Chapter](/assets/Isaiah-to-BOM/network-visuals/by_chapter.html)

[By Verse](/assets/Isaiah-to-BOM/network-visuals/by_verse.html)

### Dashboard

[Streamlit](https://isaiah-to-bom.streamlit.app/)

## Acknowledgements and Ethical Considerations

All data used was made publicly available. The inspiration for this project came from the [OpenBible.info](http://www.openbible.info/labs/cross-references/) and [Medium](https://medium.com/swlh/analyzing-references-in-bibles-verses-using-complex-networks-with-pandas-and-gephi-8a4edc52e7ab). Part of the data was downloaded from the [LDS Documentation Project](https://scriptures.nephi.org/), a research organization providing public domain data files on LDS scriptures. Rest of the raw data was scraped from [Linguistics Study in the Book of Mormon](http://www.creationismonline.com/Mormons/Mormons.html) and [The Church of Jesus Christ of Latter-day Saints](https://www.churchofjesuschrist.org/).